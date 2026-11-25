# Migrate from assistant-ui

Keep the assistant-ui runtime and swap only the rendering, or move to plain props. A concept map, both paths in code, and every component and primitive with its chatcn counterpart.

assistant-ui is built around a runtime: a provider owns the thread, and primitives read from it. chatcn has no runtime. Components take plain props, and a small adapter turns whatever owns your state into those props. That difference decides how you migrate: keep the runtime and change what renders, or drop the runtime and let `useChat` (or your own store) own the thread.

## Two models

|  | assistant-ui | chatcn |
| --- | --- | --- |
| Thread state | The runtime, behind `AssistantRuntimeProvider` | Your hook or store: `useChatcnChat`, `useChatcnAgUi`, `useChatcnLangGraph` or your own |
| Rendering | Primitives that read context (`ThreadPrimitive`, `MessagePrimitive`) | Components with props (`Conversation`, `Message`, `MessageParts`) |
| Message shape | `ThreadMessage` with `content` parts | `ChatcnMessage`, a structural mirror of AI SDK `UIMessage` |
| Tool UI | `makeAssistantToolUI` registered by tool name | A `ToolRendererMap` passed as a prop |
| Controls | Primitives call the runtime (`ComposerPrimitive.Send`, `ActionBarPrimitive.Reload`) | `ChatcnActions` callbacks. A missing action hides its control |
| Tests and stories | A runtime with a mock adapter | Static `ChatcnMessage[]` or a scripted stream, no provider |

## Path 1: keep the runtime

If your app depends on runtime features (thread lists from Assistant Cloud, branching, an external store adapter), keep them. `chatcn-assistant-ui` renders assistant-ui messages with chatcn text, reasoning and tool components and answers approvals through the runtime.

```bash
npx shadcn@latest add https://chatcn.dev/r/chatcn-assistant-ui.json
```

`components/assistant-message.tsx`

```tsx
"use client"

import { MessagePrimitive } from "@assistant-ui/react"
import { toolBashRenderers } from "@/components/ui/chatcn/tool-bash"
import { toolFileEditRenderers } from "@/components/ui/chatcn/tool-file-edit"
import { createChatcnPartComponents } from "@/lib/chatcn-assistant-ui"

// Module scope: new component identities would remount every part.
const components = createChatcnPartComponents({
  renderers: { ...toolBashRenderers, ...toolFileEditRenderers },
})

export function AssistantMessage() {
  return (
    <MessagePrimitive.Root className="flex flex-col gap-3">
      <MessagePrimitive.Parts components={components} />
    </MessagePrimitive.Root>
  )
}
```

Tools that already have a `makeAssistantToolUI` keep it; every other tool renders through chatcn. To use a whole block on the runtime, read the thread with `useAuiState`, convert it with `toChatcnMessages` and bind the controls with `useChatcnAssistantUiActions`.

```tsx
"use client"

import { useAuiState } from "@assistant-ui/react"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import { toChatcnMessages, useChatcnAssistantUiActions } from "@/lib/chatcn-assistant-ui"

// Render inside your existing AssistantRuntimeProvider.
export function RuntimeChat() {
  const thread = useAuiState((s) => s.thread.messages)
  const running = useAuiState((s) => s.thread.isRunning)
  const actions = useChatcnAssistantUiActions()

  return (
    <Chatbot
      messages={toChatcnMessages(thread)}
      status={running ? "streaming" : "ready"}
      actions={actions}
    />
  )
}
```

## Path 2: drop the runtime

If you used assistant-ui with AI SDK, the runtime was wrapping `useChat`. Call it directly through `useChatcnChat` and pass the result to a block or your own thread. Your route handler stays exactly as it is.

```bash
npx shadcn@latest add https://chatcn.dev/r/chatbot.json
```

`app/page.tsx`

```tsx
"use client"

import { DefaultChatTransport } from "ai"
import { Chatbot } from "@/components/chatcn/chatbot/chatbot"
import { useChatcnChat } from "@/hooks/use-chatcn-chat"

export default function Page() {
  const chat = useChatcnChat({ transport: new DefaultChatTransport({ api: "/api/chat" }) })
  return <Chatbot chat={chat} fullHeight />
}
```

Thread lists, persistence and branching become your code: `ThreadList` and `ChatSidebar` render whatever threads you load, and `BranchNavigator` shows the branch you pass it. On LangGraph or AG-UI, use [their adapters](https://chatcn.dev/docs/components/adapters) instead of `useChatcnChat`.

## Component map

Names on the left are the assistant-ui registry components; files on the right install under `components/ui/chatcn/` and `components/chatcn/`, so both kits can live side by side while you move screen by screen.

| assistant-ui | chatcn | Notes |
| --- | --- | --- |
| `Thread` | [Chatbot](/docs/components/chatbot), or `conversation`, `message`, `message-parts` | The block has the empty state, composer, actions and errors built in |
| `MarkdownText` | [Markdown](/docs/components/markdown) | Streams without layout shift; math and Mermaid load on first use |
| `ToolFallback` | [Tool fallback](/docs/components/tool-fallback), [Tool call](/docs/components/tool-call) | Plus a renderer per tool kind: bash, file edit, web search, MCP and more |
| `Reasoning` | [Reasoning](/docs/components/reasoning) |  |
| `ComposerAttachments`, `UserMessageAttachments` | `attachment`, `drop-zone` | `PromptInput` takes files from paste, drop and the attach button |
| `ThreadList` | `thread-list`, `chat-sidebar` | Grouped by date, with search |
| `TooltipIconButton` | `button` with `tooltip` |  |
| `AssistantModal`, `AssistantSidebar` | `chatbot` inside `dialog`, `popover` or `chat-layout` | The block fills its parent, so any container works |

## Primitive map

| assistant-ui primitive | chatcn |
| --- | --- |
| `ThreadPrimitive.Root`, `Viewport` | `Conversation`, `ConversationContent` |
| `ThreadPrimitive.Messages` | Map your messages to `Message` and `MessageParts` |
| `ThreadPrimitive.Empty` | `EmptyState` |
| `ThreadPrimitive.ScrollToBottom` | `ScrollToBottom` |
| `ThreadPrimitive.Suggestions`, `Suggestion` | `Suggestions`, `Suggestion` |
| `ComposerPrimitive.Root`, `Input`, `Send`, `Cancel` | `PromptInput`, `PromptInputTextarea`, `PromptInputSubmit` (Send becomes Stop) |
| `ComposerPrimitive.AddAttachment`, `Attachments`, `AttachmentDropzone` | `PromptInputAttachButton`, `PromptInputAttachments`, `DropZone` |
| `ComposerPrimitive.Dictate` | `DictationButton` |
| `ComposerPrimitive.Queue` | `QueuedMessages` |
| `ComposerPrimitive.TriggerPopover` | `RichPromptInput` with `MentionMenu` and `SlashMenu` |
| `MessagePrimitive.Parts` | `MessageParts`, or keep it with `createChatcnPartComponents` |
| `MessagePrimitive.Error` | `MessageError` |
| `ActionBarPrimitive.Copy`, `Reload`, `Edit` | `MessageActions`, `MessageActionCopy`, `MessageAction`, `MessageEdit` |
| `ActionBarPrimitive.FeedbackPositive`, `FeedbackNegative` | `MessageFeedback` |
| `BranchPickerPrimitive` | `BranchNavigator` |
| `ThreadListPrimitive`, `ThreadListItemPrimitive` | `ThreadList`, `ThreadListItem` |
| `ChainOfThoughtPrimitive` | `Trace`, `TraceGroup` |
| `makeAssistantToolUI` | An entry in a `ToolRendererMap` |

## What changes in your code

- **Tool UIs.** A `makeAssistantToolUI({ toolName, render })` becomes `{ [toolName]: Renderer }`, where the renderer receives the part and spreads `toolBasePropsFromPart(props)` into `ToolCall`.
- **Approvals.** `respondToToolApproval` becomes `actions.approve(id)` and `actions.deny(id, reason)`. The adapter keeps calling the runtime for you on path 1.
- **Status.** `thread.isRunning` maps to a `status` of `streaming` or `ready` on blocks.
- **Styling.** chatcn tokens are namespaced `--chatcn-*`, so they never touch your shadcn variables. See [Theming in depth](https://chatcn.dev/docs/guides/theming-in-depth) to map one onto the other.

Source: https://chatcn.dev/docs/guides/migrate-from-assistant-ui