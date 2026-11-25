# Data contract

One message shape for every component, structurally compatible with AI SDK, with scripted streams for demos and tests.

Components take plain props, so they work with any backend. When you render whole messages, chatcn uses a small set of types that mirror AI SDK `UIMessage` parts without importing it. A type test fails the build if AI SDK drifts.

`lib/chatcn-types.ts`

```ts
type ToolState =
  | "input-streaming" | "input-available"
  | "approval-requested" | "approval-responded"
  | "output-available" | "output-error" | "output-denied"

// UI only: a call that will not finish because the response stopped.
type ToolDisplayState = ToolState | "cancelled"

interface ChatcnMessage {
  id: string
  role: "system" | "user" | "assistant"
  parts: ChatcnPart[]
}
```

## With AI SDK

```tsx
import { useChat } from "@ai-sdk/react"
import { ToolCall, toolCallPropsFromPart } from "@/components/ui/chatcn/tool-call"
import { isToolPart } from "@/lib/chatcn-types"

const { messages, addToolApprovalResponse } = useChat()

message.parts.filter(isToolPart).map((part) => (
  <ToolCall
    key={part.toolCallId}
    {...toolCallPropsFromPart(part)}
    onApprove={(id) => addToolApprovalResponse({ id, approved: true })}
    onDeny={(id, reason) => addToolApprovalResponse({ id, approved: false, reason })}
  />
))
```

## Scripted streams

`chatcn-stream` plays deterministic scripts: text deltas, tool input streamed as partial JSON, approvals that wait for the user. Every demo on this site runs on it, with no API key.

```tsx
import { script } from "@/lib/chatcn-stream"
import { useChatcnStream } from "@/hooks/use-chatcn-stream"

const run = script()
  .assistant()
  .toolCall({ name: "edit_file" })
  .streamInput({ path: "src/app/page.tsx" })
  .awaitApproval({ approvalId: "edit" })
  .output({ ok: true })
  .build()

const { parts, resolve } = useChatcnStream(run)
// resolve("edit", { approved: true }) continues the run
```

Source: https://chatcn.dev/docs/data-contract