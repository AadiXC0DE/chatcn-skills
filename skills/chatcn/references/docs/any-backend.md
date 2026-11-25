# Use with any backend

The data contract every component reads, the AG-UI and LangGraph adapters, your own event stream folded into messages, and the mock transport for tests.

chatcn components never import a runtime. They read one message shape and call back through one set of actions. Anything that can produce that shape works: AI SDK, an AG-UI agent, a LangGraph deployment, or a WebSocket you wrote last week.

## The contract

`chatcn-types` mirrors AI SDK 7 `UIMessage` parts without importing it, and a type test fails the build if the two drift. A message is an id, a role and a list of parts.

| Part | Shape | Rendered by |
| --- | --- | --- |
| `text` | `{ text, state?: "streaming" | "done" }` | `Markdown` or plain text |
| `reasoning` | `{ text, state? }` | `Reasoning` |
| `tool-${name}`, `dynamic-tool` | `{ toolCallId, state, input?, output?, errorText?, approval? }` | `ToolCall` and the tool renderers |
| `source-url`, `source-document` | `{ sourceId, url | title }` | `Sources`, `Citation` |
| `file` | `{ mediaType, url, filename? }` | `FileCard`, `Image` |
| `data-${name}` | `{ id?, data }`, reconciled by `id` | Your component, or `data-genui` |
| Anything else | `{ type, ... }` | A quiet fallback. Unknown parts never throw |

Tool parts move through seven states: `input-streaming`, `input-available`, `approval-requested`, `approval-responded`, `output-available`, `output-error` and `output-denied`. The UI adds `cancelled` for calls left unfinished when a run stops. The other half of the contract is `ChatcnActions`:

```ts
interface ChatcnActions {
  send?: (text: string, options?: { files?: ChatcnFilePart[] }) => void | Promise<void>
  stop?: () => void
  regenerate?: (messageId?: string) => void | Promise<void>
  approve?: (approvalId: string, options?: { scope?: ChatcnApprovalScope }) => void | Promise<void>
  deny?: (approvalId: string, reason?: string) => void | Promise<void>
  submitToolOutput?: (toolCallId: string, output: unknown) => void | Promise<void>
  editMessage?: (messageId: string, text: string) => void | Promise<void>
}
```

Every member is optional. Blocks hide the control whose action is missing: no `regenerate`, no Retry button; no `editMessage`, no Edit.

## AG-UI

AG-UI is the event protocol behind LangGraph Platform, CrewAI, Mastra, Pydantic AI, Google ADK and others. `useChatcnAgUi` wraps any AG-UI agent, reduces its events into messages and answers interrupts as approvals.

```bash
npx shadcn@latest add https://chatcn.dev/r/use-chatcn-ag-ui.json
```

```tsx
"use client"

import { HttpAgent } from "@ag-ui/client"
import { useMemo } from "react"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import { useChatcnAgUi } from "@/hooks/use-chatcn-ag-ui"

export function AgentChat() {
  // Keep the agent stable: a new instance starts a new conversation.
  const agent = useMemo(() => new HttpAgent({ url: "/api/agent" }), [])
  const { messages, status, error, actions } = useChatcnAgUi({ agent })

  return (
    <Chatbot
      messages={messages}
      actions={actions}
      status={status === "running" ? "streaming" : status === "error" ? "error" : "ready"}
      error={error ? new Error(error.message) : null}
    />
  )
}
```

The reducer underneath, `agUiReducer`, is pure. Fold a recorded event list with `reduceAgUiEvents(events)` in a test or on the server. See [AG-UI adapter](https://chatcn.dev/docs/components/ag-ui) for the event mapping.

## LangGraph

```bash
npx shadcn@latest add https://chatcn.dev/r/use-chatcn-langgraph.json
```

```tsx
"use client"

import { Client } from "@langchain/langgraph-sdk"
import { useMemo } from "react"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import { useChatcnLangGraph } from "@/hooks/use-chatcn-langgraph"

export function GraphChat() {
  const client = useMemo(() => new Client({ apiUrl: process.env.NEXT_PUBLIC_LANGGRAPH_URL }), [])
  const { messages, status, error, actions } = useChatcnLangGraph({ client, assistantId: "agent" })

  return (
    <Chatbot
      messages={messages}
      actions={actions}
      status={status === "running" ? "streaming" : status === "error" ? "error" : "ready"}
      error={error ? new Error(error.message) : null}
    />
  )
}
```

Human-in-the-loop interrupts (LangChain's `humanInTheLoopMiddleware`, Agent Inbox, or your own) land on the tool call they review, and the hook resumes with the shape each one expects. See [LangGraph adapter](https://chatcn.dev/docs/components/langgraph).

## Your own stream

For a backend with its own wire format, write a reducer from your events to `ChatcnMessage[]` and a hook that exposes `messages`, `status` and `actions`. The demo below does exactly that with no AI SDK and no adapter: a stand-in server streams text, a tool call with partial JSON arguments and an approval. Its source has the whole reducer.

Example: Your own event stream. A pure reducer from a custom wire format to chatcn messages, rendered by the chatbot block with an approval. Preview: https://chatcn.dev/preview/guide-custom-backend

The parts that matter, from that source:

```ts
// One case per event. Keep every tool call of a turn in one assistant message.
case "tool_args_delta": {
  const raw = (state.args[event.id] ?? "") + event.delta
  const { value, complete } = parsePartialJson(raw)
  return {
    ...state,
    args: { ...state.args, [event.id]: raw },
    messages: withReply(state, (parts) =>
      patchTool(parts, event.id, {
        input: value,
        rawInput: raw,
        state: complete ? "input-available" : "input-streaming",
      }),
    ),
  }
}
case "tool_needs_approval":
  return {
    ...state,
    status: "ready",
    messages: withReply(state, (parts) =>
      patchTool(parts, event.id, {
        state: "approval-requested",
        approval: { id: approvalId(event.id), requestReason: event.reason },
      }),
    ),
  }
```

- Keep everything between two user messages in one assistant message, so a multi-step run reads as one reply with its trace.
- Parse streaming tool arguments with `parsePartialJson` from `chatcn-partial-json`; renderers draw partial input as it arrives.
- Update the tool part locally when the user answers an approval, before the server confirms, so the buttons settle at once.
- Leave text parts in `streaming` until the run ends, then mark them `done`. That is what triggers the one screen reader announcement.

## The mock transport for tests

`createChatcnMockTransport` plays chatcn scripts as a real AI SDK UI message stream. `useChat`, the adapters, approvals and resubmission behave exactly as against a server, with no network and no API key. Every demo on this site runs on it.

```bash
npx shadcn@latest add https://chatcn.dev/r/chatcn-mock-transport.json
```

`tests/chat.browser.test.tsx`

```tsx
import { expect, test } from "vitest"
import { userEvent } from "vitest/browser"
import { render } from "vitest-browser-react"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import { useChatcnChat } from "@/hooks/use-chatcn-chat"
import { createChatcnMockTransport } from "@/lib/chatcn-mock-transport"
import { script } from "@/lib/chatcn-stream"

const turn = script()
  .assistant()
  .text("I'll run the tests first.", { chunkMs: 5 })
  .toolCall({ name: "run_command", toolCallId: "call_tests" })
  .streamInput({ command: "pnpm test" }, { chunkMs: 5 })
  .awaitApproval({ approvalId: "ap_tests", requestReason: "Runs the test suite." })
  .output({ stdout: "Tests  8 passed (8)\n", exitCode: 0 }, { delayMs: 20 })
  .text("All **8 tests** pass.", { chunkMs: 5 })
  .build()

function TestChat() {
  const chat = useChatcnChat({ transport: createChatcnMockTransport(turn, { speed: 4 }) })
  return (
    <div style={{ height: 640, width: 720, display: "flex" }}>
      <Chatbot chat={chat} />
    </div>
  )
}

test("asks before running the tests", async () => {
  const screen = await render(<TestChat />)
  await screen.getByRole("textbox", { name: "Message" }).click()
  await userEvent.keyboard("Run the tests{Enter}")
  await expect.element(screen.getByText("Runs the test suite.")).toBeVisible()
  await screen.getByRole("button", { name: "Allow", exact: true }).click()
  await expect.element(screen.getByText("8 tests")).toBeVisible()
})
```

- Pass one script, a list with one per user turn (the last one repeats), or a function of `{ turn, messages, trigger }`.
- An approval step ends the response with `tool-approval-request`. When the test answers, `useChat` resubmits and the same script resumes where it waited.
- Keep scripts at module scope. Sessions are keyed by the script, so a transport created on every render still resumes approvals.
- `speed` plays faster. `clock: createManualClock()` from `chatcn-stream` drives it without real timers when you need exact control.
- Not on AI SDK? Build `ChatcnMessage[]` fixtures by hand, or play a script with `useChatcnStream`, and pass them straight to any component.

Source: https://chatcn.dev/docs/guides/any-backend