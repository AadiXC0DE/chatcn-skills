# Performance

Streaming without layout shift, keeping long threads fast, lazy Shiki, KaTeX and Mermaid, measured bundle sizes per item, and notes on the React Compiler.

A chat interface re-renders dozens of times a second while a reply streams, and the page keeps every earlier reply on screen. chatcn is built so that work stays proportional to what changed. This guide covers what the components do and what your app should do around them.

## Streaming without layout shift

- **Markdown.** Finished blocks keep their props and never render again. Code block chrome appears with the opening fence and highlighting swaps in on the same text, so lines never move. Unfinished bold, links and code heal instead of flashing raw syntax. The Markdown demo streams with a cumulative layout shift under 0.001.
- **Math and diagrams.** Display math reserves the height of a one-line formula while it streams, and KaTeX fonts load before the first render. A Mermaid fence shows its source in place until the diagram is ready.
- **Images.** Pass `width` and `height` (or `aspectRatio`) to `Image` and the frame holds its size before the file arrives.
- **Charts and widgets.** Pass `expectedCount` and `domain` to `Chart` while points stream, so the axis never rescales. Generative UI widgets receive `streaming` and reserve their final size.
- **Pending state.** `ThinkingIndicator` shows nothing for 300 ms and then stays at least 400 ms, so fast replies never flash a loader.
- **Scrolling.** `Conversation` scrolls a new user turn near the top and puts a spacer below it, so the reply streams into empty space instead of pushing the turn away. Content added above the viewport keeps your reading position.
- **Composer.** Send becomes Stop in the same footprint, so nothing around it moves.

## Long threads

AI SDK replaces only the message being streamed; every earlier message keeps its object identity between updates. Render each message in a memoized component and earlier turns skip rendering entirely while the newest one streams.

```tsx
import { memo } from "react"
import { Markdown } from "@/components/ui/chatcn/markdown"
import { Message, MessageContent } from "@/components/ui/chatcn/message"
import { MessageParts } from "@/components/ui/chatcn/message-parts"
import type { ChatcnMessage } from "@/lib/chatcn-types"

// Earlier messages keep their identity, so memo skips them while the last one streams.
export const ThreadMessage = memo(function ThreadMessage({
  message,
  streaming,
}: {
  message: ChatcnMessage
  streaming: boolean
}) {
  return (
    <Message from={message.role} state={streaming ? "streaming" : "done"}>
      <MessageContent>
        <MessageParts
          message={message}
          streaming={streaming}
          renderText={(text, ctx) => <Markdown streaming={ctx.streaming}>{text}</Markdown>}
        />
      </MessageContent>
    </Message>
  )
})
```

- Keep renderer maps and part component maps at module scope. A new map on every render gives every part a new component identity and remounts it.
- Throttle updates when tokens arrive faster than the screen can use them: `useChatcnChat({ transport, throttle: 50 })` passes `throttle` to `useChat`.
- For threads with hundreds of turns, load older history on demand and prepend it. `Conversation` keeps the reading position when content is inserted above.
- The blocks derive their side panels from the messages on each render (`codingWorkspaceFromMessages` is pure and linear in the number of parts). That is cheap for real sessions; if you run thousands of tool calls in one thread, memoize it on the messages array.

## Heavy dependencies load on first use

| Library | Loads when | How |
| --- | --- | --- |
| Shiki | The first code block on the page asks for a language | One shared instance. Core, the JavaScript regex engine (no WebAssembly) and each grammar are separate chunks, fetched once per page. After that, highlighting is synchronous, so streaming code highlights on the frame it arrives |
| KaTeX | An answer contains math | Imported once, fonts loaded before the first formula renders |
| Mermaid | An answer contains a `mermaid` fence | Imported once and rendered when the fence closes |

None of the three is in the initial bundle of any component. A page whose answers never contain code, math or diagrams never downloads them.

## Bundle size per item

Measured with `node packages/registry-tools/src/size.mjs`: each item is bundled from its own entry, minified and gzipped, with React external. **Own** is the item's files alone. **+npm** adds the npm packages it imports. **Total** is everything an install loads up front, including other chatcn items it depends on. **Lazy** is code behind dynamic imports, the most that could load on demand.

| Item | Own | +npm | Total | Lazy |
| --- | --- | --- | --- | --- |
| `button` | 0.7 kB | 0.7 kB | 10.9 kB |  |
| `conversation` | 0.9 kB | 0.9 kB | 13.0 kB |  |
| `streaming-text` | 0.5 kB | 0.5 kB | 11.6 kB |  |
| `message` | 2.6 kB | 2.6 kB | 51.0 kB |  |
| `message-parts` | 2.3 kB | 8.5 kB | 34.5 kB |  |
| `tool-call` | 4.3 kB | 10.3 kB | 32.5 kB |  |
| `reasoning` | 2.1 kB | 8.3 kB | 28.8 kB |  |
| `prompt-input` | 2.8 kB | 2.8 kB | 54.3 kB |  |
| `code-block` | 2.6 kB | 12.1 kB | 60.4 kB | 1,297.1 kB |
| `math` | 1.6 kB | 1.6 kB | 50.3 kB | 74.8 kB |
| `mermaid` | 3.8 kB | 3.8 kB | 61.6 kB | 1,400.0 kB |
| `markdown` | 4.0 kB | 152.4 kB | 238.0 kB | 2,792.3 kB |
| `diff-viewer` | 5.5 kB | 5.5 kB | 58.0 kB |  |
| `terminal` | 3.9 kB | 3.9 kB | 54.3 kB |  |
| `chart` | 8.1 kB | 8.1 kB | 56.6 kB |  |
| `rich-prompt-input` | 5.5 kB | 99.2 kB | 128.1 kB |  |
| `chatcn-genui` | 5.0 kB | 31.5 kB | 104.1 kB |  |
| `coding-agent` | 7.0 kB | 7.0 kB | 299.6 kB | 2,792.3 kB |
| `use-chatcn-chat` | 0.4 kB | 45.8 kB | 46.1 kB |  |
| `chatcn-mock-transport` | 1.7 kB | 1.7 kB | 3.5 kB |  |
| `use-chatcn-ag-ui` | 1.8 kB | 1.8 kB | 6.0 kB |  |
| `use-chatcn-langgraph` | 1.3 kB | 1.3 kB | 5.0 kB |  |
| `chatcn-icons` | 11.1 kB | 11.1 kB | 11.1 kB |  |

- Leaf components stay under 5 kB of their own code. The few above it (`chart`, `diff-viewer`, `rich-prompt-input`) draw without a chart library, parse diffs and run Tiptap respectively.
- Lazy sizes count every Shiki grammar. A page loads only the grammars its code blocks use, typically a few kB each.
- Totals overlap. `markdown` brings `code-block`, `math` and `mermaid`; installing all four costs the `markdown` total once, not four times.
- `chatcn-icons` is one module with named exports. Bundlers keep only the icons your components import.

## React Compiler

- chatcn does not require the compiler and its tests run without it. Components work the same with it on.
- Components avoid mutating values during render and keep hooks unconditional, so most of them compile.
- A few hooks, `useChatcnChat` among them, write the latest value into a ref during render so their callbacks stay stable. The compiler skips optimizing a function that does this and leaves it as written, which keeps behavior the same.
- The handful of explicit `React.memo` wrappers (code block, diff viewer, terminal, ANSI output, file tree) are harmless under the compiler. Leave them in.

Source: https://chatcn.dev/docs/guides/performance