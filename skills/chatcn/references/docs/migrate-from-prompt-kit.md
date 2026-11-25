# Migrate from prompt-kit

Every prompt-kit component and block with its chatcn counterpart, and what behaves differently.

prompt-kit and chatcn are both shadcn registries, so the move is mostly a rename. chatcn files install under `components/ui/chatcn/`, which means both kits can share a project while you replace one screen at a time. The larger differences are behavioral: chatcn components handle tool states and approvals, read AI SDK message parts directly, and keep motion to a short, written list.

## How they differ

- **Base UI and Radix.** chatcn serves both from the same URL through the `{style}` placeholder in `components.json`, so a Base UI project does not ship a second primitive layer.
- **Message parts in, components out.** Pass AI SDK `UIMessage` parts to `MessageParts`, or map one tool part with `toolCallPropsFromPart`. Approvals, denials, errors and cancelled calls each have a designed state.
- **No typewriter or bouncing dots.** Streaming text appears as it arrives. `Markdown` has an optional `cadence` that evens out bursts without per word effects, and pending states use a delayed Thinking label instead of a dots loader.
- **Composer details built in.** `PromptInput` never sends while an IME is composing, turns Send into Stop in the same footprint, and takes files from paste, drop and the attach button.

## Component map

| prompt-kit | chatcn | Notes |
| --- | --- | --- |
| `PromptInput`, `PromptInputTextarea`, `PromptInputActions`, `PromptInputAction` | [Prompt input](/docs/components/prompt-input): `PromptInput`, `PromptInputTextarea`, `PromptInputToolbar`, `PromptInputActions`, `PromptInputButton`, `PromptInputSubmit` | `onSubmit` receives `{ text }`. Pass `status="streaming"` and `onStop` instead of a loading flag |
| `PromptSuggestion` | [Suggestions](/docs/components/suggestions) |  |
| `Message`, `MessageAvatar`, `MessageContent`, `MessageActions`, `MessageAction` | [Message](/docs/components/message) and `message-actions`, same names | `Message` takes `from`, and `layout` for bubble, flat or compact |
| `Markdown` | [Markdown](/docs/components/markdown) | Pass `streaming` while text arrives |
| `CodeBlock`, `CodeBlockCode`, `CodeBlockGroup` | [Code block](/docs/components/code-block): `CodeBlock`, `CodeBlockTabs` | Shiki with a restrained palette (or gray with `chatcn-code-mono`), loaded on first use, highlighted while it streams |
| `ChatContainerRoot`, `ChatContainerContent`, `ChatContainerScrollAnchor` | [Conversation](/docs/components/conversation): `Conversation`, `ConversationContent` | Stick to bottom and the reply anchor are built in; no anchor element needed |
| `ScrollButton` | `scroll-to-bottom` | Shows a count of messages that arrived below |
| `Loader` | `spinner`, `shimmer-text`, `thinking-indicator` | Fewer variants on purpose: a spinner for work, a shimmer label for thinking |
| `ResponseStream` | `Markdown` with `cadence`, or `streaming-text` | No typewriter or per word fade |
| `FileUpload`, `FileUploadTrigger`, `FileUploadContent` | `drop-zone`, `attachment`, `PromptInputAttachButton` |  |
| `JSXPreview` | [JSX preview](/docs/components/jsx-preview) | Nothing is evaluated |
| `Tool` | [Tool call](/docs/components/tool-call) and the tool renderers | Spread `toolCallPropsFromPart(part)`; approvals included |
| `Source`, `SourceTrigger`, `SourceContent` | `citation`, `sources` |  |
| `Image` | `image` | Holds its size before it loads |
| `Steps`, `ChainOfThought` and their parts | `trace`, `trace-group` |  |
| `SystemMessage` | `system-notice` |  |
| `TextShimmer` | `shimmer-text` | The only shimmer in chatcn |
| `ThinkingBar` | `thinking-indicator`, with Stop in `PromptInputSubmit` |  |
| `FeedbackBar` | `message-feedback` | Thumbs up or down with reasons |
| `Reasoning`, `ReasoningTrigger`, `ReasoningContent` | [Reasoning](/docs/components/reasoning) |  |

## Blocks

| prompt-kit block | chatcn |
| --- | --- |
| Full chat app, full conversation | [Chatbot](/docs/components/chatbot) |
| Sidebar chat history | `chat-sidebar`, `thread-list` |
| Prompt input with actions or suggestions | `prompt-input`, `suggestions` |
| Conversation with scroll to bottom | `conversation`, `scroll-to-bottom` |
| Conversation actions and avatars | `message`, `message-actions` |

## A message, rewritten

A typical prompt-kit message maps text parts to `Markdown` and tool parts to `Tool`. In chatcn, `MessageParts` walks the parts for you, in order, with reasoning, sources, files and the thinking gap between steps.

```tsx
import type { UIMessage } from "ai"
import { Markdown } from "@/components/ui/chatcn/markdown"
import { Message, MessageContent } from "@/components/ui/chatcn/message"
import { MessageActionCopy, MessageActions } from "@/components/ui/chatcn/message-actions"
import { MessageParts } from "@/components/ui/chatcn/message-parts"
import { toChatcnMessages } from "@/lib/chatcn-ai-sdk"
import type { ChatcnActions, ChatcnMessage, ChatcnTextPart } from "@/lib/chatcn-types"

const textOf = (m: ChatcnMessage) =>
  m.parts.map((p) => (p.type === "text" ? (p as ChatcnTextPart).text : "")).join("")

export function ChatMessage({
  message,
  streaming,
  actions,
}: {
  message: UIMessage
  streaming: boolean
  actions: ChatcnActions
}) {
  const [chatcn] = toChatcnMessages([message])
  if (!chatcn) return null
  return (
    <Message from={chatcn.role} state={streaming ? "streaming" : "done"}>
      <MessageContent>
        <MessageParts
          message={chatcn}
          streaming={streaming}
          renderText={(text, ctx) => <Markdown streaming={ctx.streaming}>{text}</Markdown>}
          toolProps={() => ({
            onApprove: (id, scope) => actions.approve?.(id, { scope }),
            onDeny: (id, reason) => actions.deny?.(id, reason),
          })}
        />
      </MessageContent>
      <MessageActions>
        <MessageActionCopy value={() => textOf(chatcn)} />
      </MessageActions>
    </Message>
  )
}
```

Then remove the prompt-kit files you no longer import. The chatcn tokens are namespaced, so removing prompt-kit never changes chatcn's colors.

Source: https://chatcn.dev/docs/guides/migrate-from-prompt-kit