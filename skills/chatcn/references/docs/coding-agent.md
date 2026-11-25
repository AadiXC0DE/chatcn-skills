# Build a coding agent UI in 10 minutes

An AI SDK route with tools that wait for approval, useChatcnChat on the client, and the coding agent block rendering every tool call, diff and command.

By the end of this guide you have a route handler that streams a coding agent with four tools, a page that renders it with the [Coding agent](https://chatcn.dev/docs/components/coding-agent) block, and approvals that pause the run until someone clicks Allow. The demo below is the finished page. It plays the stream the route would send, so it runs without an API key. Approve the edit to watch the tests run, or deny it.

Example: Coding agent on useChatcnChat. The coding agent block on AI SDK useChat with a mock transport: a plan, a read, an edit that waits for approval and a test run. Preview: https://chatcn.dev/preview/guide-coding-agent

## 1. Install

You need a Next.js app with Tailwind CSS v4, the shadcn CLI (see [Installation](https://chatcn.dev/docs/installation)), AI SDK 7 and zod. Add the block and the AI SDK hook. The block brings every component it composes; the hook brings the adapter.

```bash
npx shadcn@latest add https://chatcn.dev/r/coding-agent.json
```

```bash
npx shadcn@latest add https://chatcn.dev/r/use-chatcn-chat.json
```

```bash
npm i ai @ai-sdk/react zod
```

## 2. Write the route

The route is plain AI SDK. The block reads tool calls by name and shape, so use names it knows: `read_file`, `edit_file` with `old` and `new` text (or a unified `diff`), `run_command` with `stdout`, `stderr` and `exitCode`, and `todo_write` with Claude Code style todos. Spellings such as `str_replace`, `apply_patch`, `bash` and `TodoWrite` work too.

`app/api/agent/route.ts`

```ts
import { spawn } from "node:child_process"
import { readFile, writeFile } from "node:fs/promises"
import path from "node:path"
import { convertToModelMessages, isStepCount, streamText, tool, type UIMessage } from "ai"
import { z } from "zod"

/** The checkout the agent works in. Run the route inside a sandbox or container, never on a laptop. */
const ROOT = process.env.AGENT_WORKSPACE ?? "/workspace"

function resolveInRoot(file: string) {
  const full = path.resolve(ROOT, file)
  if (!full.startsWith(`${ROOT}${path.sep}`)) throw new Error(`${file} is outside the workspace.`)
  return full
}

const tools = {
  read_file: tool({
    description: "Read a file from the repository.",
    inputSchema: z.object({ path: z.string().describe("Path relative to the repository root") }),
    execute: async ({ path: file }) => readFile(resolveInRoot(file), "utf8"),
  }),

  edit_file: tool({
    description: "Replace one exact snippet in a file. Read the file first.",
    inputSchema: z.object({ path: z.string(), old: z.string(), new: z.string() }),
    execute: async (input) => {
      const full = resolveInRoot(input.path)
      const source = await readFile(full, "utf8")
      if (!source.includes(input.old)) throw new Error(`The snippet is not in ${input.path}.`)
      await writeFile(full, source.replace(input.old, input.new))
      return { path: input.path, applied: true }
    },
  }),

  run_command: tool({
    description: "Run a shell command in the repository root.",
    inputSchema: z.object({ command: z.string() }),
    // An async generator streams preliminary output, so the terminal fills while it runs.
    async *execute({ command }, { abortSignal }) {
      const child = spawn(command, { cwd: ROOT, shell: true, signal: abortSignal })
      const run = { stdout: "", stderr: "", exitCode: null as number | null }
      child.stdout.on("data", (chunk) => {
        run.stdout += chunk
      })
      child.stderr.on("data", (chunk) => {
        run.stderr += chunk
      })
      const closed = new Promise<void>((resolve) =>
        child.on("close", (code) => {
          run.exitCode = code ?? 1
          resolve()
        }),
      )
      while (run.exitCode === null) {
        yield { stdout: run.stdout, stderr: run.stderr }
        await Promise.race([closed, new Promise((resolve) => setTimeout(resolve, 250))])
      }
      yield { ...run }
    },
  }),

  todo_write: tool({
    description: "Write the current plan. Send the whole list every time.",
    inputSchema: z.object({
      todos: z.array(
        z.object({
          content: z.string(),
          activeForm: z.string(),
          status: z.enum(["pending", "in_progress", "completed"]),
        }),
      ),
    }),
    execute: async ({ todos }) => ({ count: todos.length }),
  }),
}

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json()

  const result = streamText({
    model: "anthropic/claude-sonnet-5-5",
    system:
      "You are a coding agent working in a git checkout. Plan with todo_write, read before you edit, and run the tests after a change.",
    messages: await convertToModelMessages(messages),
    tools,
    // Edits wait for Allow or Deny in the UI. Test runs go through, other commands ask first.
    toolApproval: {
      edit_file: { type: "user-approval", reason: "Changes a file in your checkout." },
      run_command: ({ command }) =>
        /^pnpm (test|lint|typecheck)\b/.test(command) ? "approved" : "user-approval",
    },
    stopWhen: isStepCount(20),
  })

  return result.toUIMessageStreamResponse({ sendReasoning: true })
}
```

- `toolApproval` decides per call. A string applies to every call of that tool; a function reads the input and returns `user-approval`, `approved` or `denied`. The `reason` shows above Allow and Deny.
- `needsApproval: true` on the tool itself still works, but AI SDK 7 marks it deprecated in favor of `toolApproval`.
- The model string goes through the AI Gateway. Pass a provider model instead, for example `anthropic("claude-sonnet-5-5")` from `@ai-sdk/anthropic`, if you call the provider directly.
- `run_command` is an async generator: every `yield` before the last one is a preliminary result, which the block streams into its terminal while the command runs.

> This route edits files and runs commands on the machine it runs on. Point `AGENT_WORKSPACE` at a disposable checkout inside a container or a sandbox, and keep approvals on for anything that writes.

## 3. Render the block

`app/agent/page.tsx`

```tsx
"use client"

import { DefaultChatTransport } from "ai"
import { CodingAgent } from "@/components/chatcn/coding-agent/coding-agent"
import { useChatcnChat } from "@/hooks/use-chatcn-chat"

export default function AgentPage() {
  const chat = useChatcnChat({
    transport: new DefaultChatTransport({ api: "/api/agent" }),
  })

  return (
    <CodingAgent
      fullHeight
      messages={chat.chatcnMessages}
      status={chat.status}
      actions={chat.actions}
      branch="fix/runs-list-query"
      model="claude-sonnet-5-5"
      emptyTitle="What should the agent work on?"
    />
  )
}
```

`useChatcnChat` is `useChat` with three additions: `chatcnMessages` (the same array, typed for chatcn), `actions` (send, stop, regenerate, approve, deny, tool output and edit) and `isStreaming`. The block builds its workspace from the tool calls in the thread: edits become changed files and diffs, commands become the terminal session, and the latest `todo_write` becomes the pinned todo list.

## 4. How an approval travels

1. The model calls `edit_file`. `toolApproval` returns `user-approval`, so the server streams a `tool-approval-request` instead of running the tool, and the response ends.
2. The tool part arrives in state `approval-requested`. The block renders the diff with Allow, Always allow and Deny, and the header says Needs approval.
3. Allow calls `actions.approve(id)`, which calls `addToolApprovalResponse({ id, approved: true })`. Deny can carry a note and calls it with `approved: false` and the note as `reason`.
4. `useChatcnChat` sets `sendAutomaticallyWhen` to `lastAssistantMessageIsCompleteWithApprovalResponses`, so the answer goes back to the route on its own. The server runs the tool, or tells the model it was denied, and the run continues.

Always allow is a promise your app keeps. AI SDK has no approval scope, so `onApprovalScope` hands it to you before the approval is sent. Store it, send it with each request and read it in `toolApproval`.

```tsx
const allowed = useRef(new Set<string>())

const chat = useChatcnChat({
  transport: new DefaultChatTransport({
    api: "/api/agent",
    body: () => ({ allowedTools: [...allowed.current] }),
  }),
  onApprovalScope: (approvalId, scope) => {
    if (scope !== "always") return
    const part = chat.chatcnMessages
      .flatMap((m) => m.parts)
      .filter(isToolPart)
      .find((p) => p.approval?.id === approvalId)
    if (part) allowed.current.add(getToolName(part))
  },
})
```

## 5. Render tool parts yourself

The block is a composition, not a black box. When you need your own layout, render the same messages with `MessageParts` and send tool parts through `renderToolPart`, which picks a renderer by tool name and falls back to the generic tool call.

Example: Your own thread. MessageParts with Markdown text and tool parts sent through renderToolPart, approvals included. Preview: https://chatcn.dev/preview/guide-tool-parts

`components/thread.tsx`

```tsx
import { Conversation, ConversationContent } from "@/components/ui/chatcn/conversation"
import { Markdown } from "@/components/ui/chatcn/markdown"
import { Message, MessageContent } from "@/components/ui/chatcn/message"
import { MessageParts } from "@/components/ui/chatcn/message-parts"
import { toolBashRenderers } from "@/components/ui/chatcn/tool-bash"
import { renderToolPart, type ToolRendererMap } from "@/components/ui/chatcn/tool-fallback"
import { toolFileEditRenderers } from "@/components/ui/chatcn/tool-file-edit"
import { toolFileReadRenderers } from "@/components/ui/chatcn/tool-file-read"
import type { ChatcnActions, ChatcnMessage } from "@/lib/chatcn-types"

// Module scope: a stable map, so renderers keep their identity between renders.
const renderers: ToolRendererMap = {
  ...toolFileReadRenderers,
  ...toolFileEditRenderers,
  ...toolBashRenderers,
}

export function Thread({
  messages,
  streaming,
  actions,
}: {
  messages: ChatcnMessage[]
  streaming: boolean
  actions: ChatcnActions
}) {
  return (
    <Conversation className="h-full" aria-label="Agent thread">
      <ConversationContent className="mx-auto max-w-2xl p-5">
        {messages.map((message, i) => {
          const live = streaming && i === messages.length - 1 && message.role === "assistant"
          return (
            <Message key={message.id} from={message.role} state={live ? "streaming" : "done"}>
              <MessageContent>
                <MessageParts
                  message={message}
                  streaming={live}
                  renderText={(text, { streaming }) => (
                    <Markdown streaming={streaming}>{text}</Markdown>
                  )}
                  components={{
                    tool: ({ part, stopped }) =>
                      renderToolPart(part, renderers, {
                        stopped,
                        onApprove: (id, scope) => actions.approve?.(id, { scope }),
                        onDeny: (id, reason) => actions.deny?.(id, reason),
                      }),
                  }}
                />
              </MessageContent>
            </Message>
          )
        })}
      </ConversationContent>
    </Conversation>
  )
}
```

### A renderer for your own tool

A renderer is a component that takes a tool part. `toolBasePropsFromPart` maps the part's state, approval, error and timing to `ToolCall` props, so yours only adds the title and detail. Passing `toolRenderers` replaces the block's defaults, so spread the maps you still want.

```tsx
import { CodingAgent, ToolTodoWritePart } from "@/components/chatcn/coding-agent/coding-agent"
import { toolBashRenderers } from "@/components/ui/chatcn/tool-bash"
import { ToolCall } from "@/components/ui/chatcn/tool-call"
import { type ToolRendererProps, toolBasePropsFromPart } from "@/components/ui/chatcn/tool-fallback"
import { toolFileEditRenderers } from "@/components/ui/chatcn/tool-file-edit"
import { toolFileReadRenderers } from "@/components/ui/chatcn/tool-file-read"

function DeployPart(props: ToolRendererProps) {
  const input = props.part.input as { service?: string; env?: string } | undefined
  return (
    <ToolCall
      {...toolBasePropsFromPart(props)}
      name="deploy"
      title="Deploy"
      detail={input?.service ? `${input.service} to ${input.env ?? "staging"}` : undefined}
    />
  )
}

const toolRenderers = {
  ...toolFileReadRenderers,
  ...toolFileEditRenderers,
  ...toolBashRenderers,
  todo_write: ToolTodoWritePart,
  deploy: DeployPart,
}

<CodingAgent messages={messages} actions={actions} toolRenderers={toolRenderers} />
```

## Next

- Prefer a general chat surface? The [Chatbot](https://chatcn.dev/docs/components/chatbot) block takes the same `chat` object.
- Model picker, permission modes, a queue and a context meter are props on the block. See [Coding agent](https://chatcn.dev/docs/components/coding-agent).
- Not on AI SDK? [Use with any backend](https://chatcn.dev/docs/guides/any-backend) covers AG-UI, LangGraph and your own stream.

Source: https://chatcn.dev/docs/guides/coding-agent