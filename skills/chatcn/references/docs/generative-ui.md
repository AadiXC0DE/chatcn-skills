# Generative UI and MCP Apps

Let the model draw charts, forms and confirmations from a Zod-checked spec, stream specs from tools and data parts, and host MCP Apps in the thread.

There are two ways for an agent to put an interface in a reply. With **generative UI** the model writes a JSON spec and chatcn renders it with its own widgets, validated against Zod schemas. With **MCP Apps** a tool on an MCP server ships its own HTML View, and chatcn hosts it in a sandboxed frame. The first keeps every pixel in your design system; the second lets a third party bring a full app.

Example: render_ui in the chatbot. A streamed generative UI spec rendered with GenUI, and a confirmation that answers through actions.send. Preview: https://chatcn.dev/preview/guide-genui

## 1. Install

```bash
npx shadcn@latest add https://chatcn.dev/r/chatcn-genui.json
```

`chatcn-genui` brings the renderer, the widget components and `use-chatcn-genui-spec`. It depends on zod 4.

## 2. Give the model a render_ui tool

`genuiSpecSchema` is the Zod schema the renderer validates against: one widget (`chart`, `stat`, `stats`, `comparison`, `form`, `calculator`, `carousel`, `map`, `weather`, `timeline`, `confirmation`, `text`, `button`) or a `stack` of them. Use it as the tool's input schema and the model is told exactly what may render.

`app/api/chat/route.ts`

```ts
import { convertToModelMessages, isStepCount, streamText, tool, type UIMessage } from "ai"
import { genuiSpecSchema } from "@/lib/chatcn-genui"

export const renderUi = tool({
  description:
    "Show a chart, stat, comparison, form, calculator, timeline or confirmation inside the answer. Use it when a picture or a control says more than a paragraph.",
  inputSchema: genuiSpecSchema,
  // The UI is the result. Telling the model it rendered lets the loop continue with prose.
  execute: async () => ({ rendered: true }),
})

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json()
  const result = streamText({
    model: "anthropic/claude-sonnet-5-5",
    messages: await convertToModelMessages(messages),
    tools: { render_ui: renderUi },
    stopWhen: isStepCount(4),
  })
  return result.toUIMessageStreamResponse()
}
```

A tool for one widget keeps the schema small, which helps smaller models. `genuiSchemas` holds the props schema per widget type:

```ts
import { tool } from "ai"
import { z } from "zod"
import { genuiSchemas } from "@/lib/chatcn-genui"

export const showChart = tool({
  description: "Draw a bar, line, area or proportion chart.",
  inputSchema: z.object({ type: z.literal("chart"), props: genuiSchemas.chart }),
  execute: async () => ({ rendered: true }),
})
```

For runtimes that want JSON Schema instead of Zod, `genuiJsonSchema()` returns it for the whole spec, and `genuiJsonSchema("chart")` for one widget.

## 3. Render the tool part

`genuiFromPart` reads the spec from a tool part (the partial input while it streams, then the final input) or from a `data-genui` part. `GenUI` renders it. Interactive widgets report back through one `onAction` callback; here a confirmation becomes the user's next message.

```tsx
import { useMemo } from "react"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import type { ToolRendererMap, ToolRendererProps } from "@/components/ui/chatcn/tool-fallback"
import { genuiFromPart } from "@/hooks/use-chatcn-genui-spec"
import { GenUI, type GenUIActionHandler } from "@/lib/chatcn-genui"
import type { ChatcnActions } from "@/lib/chatcn-types"

function useGenUIRenderers(actions: ChatcnActions): ToolRendererMap {
  return useMemo(() => {
    const onAction: GenUIActionHandler = (action) => {
      if (action.type === "confirm") return actions.send?.("Open the pull request.")
      if (action.type === "form.submit") return actions.send?.(JSON.stringify(action.values))
      return undefined
    }
    function RenderUi({ part }: ToolRendererProps) {
      const ui = genuiFromPart(part)
      return ui ? <GenUI spec={ui.spec} streaming={ui.streaming} onAction={onAction} /> : null
    }
    return { render_ui: RenderUi }
  }, [actions])
}

// In your page:
const renderers = useGenUIRenderers(chat.actions)
<Chatbot chat={chat} toolRenderers={renderers} />
```

- While the spec streams, every field that already parses renders, and the newest item of each array waits until the next one starts, so a half-written number never draws a wrong bar.
- Once complete, the spec is validated strictly. An invalid widget renders what validated plus a note naming the first failing path; an unknown type lists the supported ones. Each widget has its own error boundary.
- Return a promise from `confirm` or `form.submit` to show progress on the button. Reject it to show the error and keep the widget editable.
- `resolveGenUI(input, { streaming })` is the same resolver without React, for server checks and tests.

## 4. Stream a spec from your own code

Not every spec comes from a tool call. When your server builds the UI (a report, a dashboard summary), write it into a `data-genui` part. Writes with the same `id` replace the part, so the client sees one widget filling in.

`app/api/report/route.ts`

```ts
import {
  convertToModelMessages,
  createUIMessageStream,
  createUIMessageStreamResponse,
  Output,
  streamText,
  type UIMessage,
} from "ai"
import { genuiSpecSchema } from "@/lib/chatcn-genui"

export async function POST(req: Request) {
  const { messages }: { messages: UIMessage[] } = await req.json()
  const stream = createUIMessageStream({
    execute: async ({ writer }) => {
      const spec = streamText({
        model: "anthropic/claude-sonnet-5-5",
        system: "Summarize the CI build times as one chatcn chart spec.",
        messages: await convertToModelMessages(messages),
        output: Output.object({ schema: genuiSpecSchema }),
      })
      // Same id on every write: the client replaces the part instead of adding new ones.
      for await (const partial of spec.partialOutputStream) {
        writer.write({ type: "data-genui", id: "ci-chart", data: { spec: partial, streaming: true } })
      }
      writer.write({
        type: "data-genui",
        id: "ci-chart",
        data: { spec: await spec.output, streaming: false },
      })
    },
  })
  return createUIMessageStreamResponse({ stream })
}
```

On the client, render the data part through `MessageParts` with `components={{ "data-genui": GenUIPart }}`, where `GenUIPart` calls `genuiFromPart(part)` exactly as the tool renderer does.

### Adding a widget type

The renderer only draws types it has a schema for, so a model cannot invent widgets. To add one, add its Zod schema to `genuiSchemas` in your copy of `lib/chatcn-genui.ts` (the file is yours after install) and pass a renderer for it through the `renderers` prop of `GenUI`. The new schema flows into `genuiSpecSchema` and the tool definition automatically.

## MCP Apps

An MCP App is a tool whose `_meta.ui.resourceUri` points at a `ui://` resource of type `text/html;profile=mcp-app`. The host reads that resource and renders it next to the tool call, and the View talks to the host over the official app bridge. `McpAppFrame` is that host: a sandboxed iframe with loading and error states, resize to content, full screen and picture in picture, and chatcn tokens passed as host styles so the View matches your theme.

Example: MCP app in a tool part. A tool renderer that hosts an MCP App View with McpAppFrame and sends its messages to the chat. Preview: https://chatcn.dev/preview/guide-mcp-app

```bash
npx shadcn@latest add https://chatcn.dev/r/mcp-app-frame.json
```

### Server: return the View with the result

Connect to the MCP server, find the tool's UI resource with `getToolUiResourceUri`, and read it when the tool runs. The tool output carries the HTML for the frame; `toModelOutput` keeps it away from the model, which only sees the tool's text.

`lib/mcp-app-tool.ts`

```ts
import { Client, StreamableHTTPClientTransport } from "@modelcontextprotocol/client"
import { getToolUiResourceUri } from "@modelcontextprotocol/ext-apps/app-bridge"
import { tool } from "ai"
import { z } from "zod"
import type { McpAppResource } from "@/components/ui/chatcn/mcp-app-frame"

/** The tool's output: what the MCP tool returned, plus its View for `McpAppFrame`. */
export interface McpAppOutput {
  /** Text for the model, structured content for the View. */
  result: Awaited<ReturnType<Client["callTool"]>>
  ui?: McpAppResource
}

export async function mcpAppTool(serverUrl: string, toolName: string) {
  const mcp = new Client({ name: "chatcn-host", version: "1.0.0" })
  await mcp.connect(new StreamableHTTPClientTransport(new URL(serverUrl)))
  const { tools } = await mcp.listTools()
  const def = tools.find((t) => t.name === toolName)
  if (!def) throw new Error(`${toolName} is not on ${serverUrl}.`)
  const uri = getToolUiResourceUri(def)

  return tool({
    description: def.description ?? toolName,
    inputSchema: z.record(z.string(), z.unknown()),
    execute: async (args): Promise<McpAppOutput> => {
      const result = await mcp.callTool({ name: toolName, arguments: args })
      if (!uri) return { result }
      const resource = await mcp.readResource({ uri })
      const content = resource.contents[0]
      const html = content && "text" in content ? content.text : ""
      const meta = (content?._meta as { ui?: McpAppResource["meta"] } | undefined)?.ui
      return { result, ui: { uri, html, meta } }
    },
    // The model reads the tool's text, never the View's HTML.
    toModelOutput: ({ output }) => ({
      type: "content",
      value: (output.result.content ?? []).flatMap((c) =>
        c.type === "text" ? [{ type: "text" as const, text: c.text }] : [],
      ),
    }),
  })
}
```

### Client: a renderer that hosts the View

```tsx
import { McpAppFrame } from "@/components/ui/chatcn/mcp-app-frame"
import type { ToolRendererMap, ToolRendererProps } from "@/components/ui/chatcn/tool-fallback"
import { getToolName, type ChatcnActions } from "@/lib/chatcn-types"
import type { McpAppOutput } from "@/lib/mcp-app-tool"

export function mcpAppRenderers(toolNames: string[], actions: ChatcnActions): ToolRendererMap {
  function McpAppPart({ part }: ToolRendererProps) {
    const output =
      part.state === "output-available" ? (part.output as McpAppOutput | undefined) : undefined
    const input = (part.input ?? undefined) as Record<string, unknown> | undefined
    return (
      <McpAppFrame
        resource={output?.ui}
        toolName={getToolName(part)}
        toolInputPartial={part.state === "input-streaming" ? input : undefined}
        toolInput={part.state === "input-streaming" ? undefined : input}
        toolResult={output?.result}
        toolCancelled={part.state === "output-error" ? (part.errorText ?? true) : undefined}
        onMessage={(text) => actions.send?.(text)}
      />
    )
  }
  return Object.fromEntries(toolNames.map((name) => [name, McpAppPart]))
}
```

- The frame mounts as soon as the call starts and shows its skeleton until the resource arrives, then sends input and result to the View in protocol order.
- The iframe never gets `allow-same-origin`, so the View cannot read your page, cookies or storage. A Content-Security-Policy is injected from the resource's `_meta.ui.csp`.
- Wire `onCallTool` to `mcp.callTool` through your server if the View calls tools itself, and `onOpenLink` if you want to confirm links before opening them.
- The frame only depends on `@modelcontextprotocol/ext-apps` and `@modelcontextprotocol/client`. Nothing else in chatcn needs them.

Source: https://chatcn.dev/docs/guides/generative-ui