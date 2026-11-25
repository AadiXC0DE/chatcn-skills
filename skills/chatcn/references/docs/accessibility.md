# Accessibility

What chatcn guarantees for each kind of component, how it is tested, and what your app still has to do.

AI interfaces add problems a normal form never has: text that streams for twenty seconds, controls that appear halfway through a reply, approvals that block a run. chatcn handles those in the components. Some things only your app can do, and they are listed at the end.

## How it is tested

- axe runs against every preview route in light and dark with the WCAG 2.0, 2.1 and 2.2 A and AA rules. Serious and critical violations fail the test run.
- Browser tests drive the keyboard paths that matter: Enter and Shift+Enter in composers, IME composition, approvals, menus, tabs and Escape.
- Visual tests run with reduced motion, so every animated component has to look finished without its animation.

## By kind of component

| Kind | Keyboard | Screen readers |
| --- | --- | --- |
| Threads: `Conversation`, `Message`, `Markdown`, `StreamingText` | The thread is focusable and scrolls with the arrow keys. Any upward scroll releases stick to bottom at once | A labelled `log` with `aria-live="off"`. Tokens are silent; each finished reply is read once through a polite live region |
| Composers: `PromptInput`, `RichPromptInput`, `ComposerMobile` | Enter sends, Shift+Enter adds a line, Escape stops a run. Enter never sends while an IME is composing | Labelled field. Send and Stop swap in one button with a changing label |
| Tool calls and approvals: `ToolCall` and the tool renderers | Header is a disclosure button. Allow, Always allow and Deny are buttons in reading order | State is text (Running, Needs approval, Denied), never color alone. The request reason sits above the buttons |
| Pending and progress: `ThinkingIndicator`, `RunStatus`, `StepTimer` | Not focusable | `role=status`. Thinking waits 300 ms before it shows, so quick replies announce nothing extra |
| Disclosures: `Reasoning`, `Trace`, `TraceGroup`, `Plan` | Enter and Space toggle. Collapsed by default, and nothing closes on a timer while someone reads it | `aria-expanded` on the trigger; collapsed content leaves the accessibility tree |
| Menus, popovers, dialogs: `Menu`, `Popover`, `Dialog`, `ModelPicker`, `CommandPalette` | Base UI focus management: arrow keys, typeahead, Escape, focus returns to the trigger | Correct roles from Base UI (`menu`, `listbox`, `dialog`) with labelled popups |
| Tabs and panes: the blocks, `Resizable` | Arrow keys move between tabs; the divider resizes with the arrow keys | A real `tablist`; each panel is labelled by its tab. The divider is a labelled separator with its value |
| Data: `Chart`, `Table`, `DiffViewer`, `Terminal`, `JsonViewer` | Scroll regions are focusable; chart points take focus and show their tooltip | Charts carry a table alternative. Diffs name added and removed lines in text |
| Generative UI widgets and `McpAppFrame` | Forms label every control and validate on submit. Full screen apps trap Tab and leave on Escape | Streaming widgets set `aria-busy`. The app iframe is titled with the app name |

## Across every component

- **Live regions.** Streaming content announces once on completion through `useChatcnAnnounce`, never per token. Errors use `role=alert` and say how to fix the problem.
- **IME.** Every text input that submits on Enter checks `isComposing`, so Japanese, Chinese and Korean input never sends a half-composed message.
- **RTL.** Layout uses logical properties (`ms`, `pe`, `start`, `end`), and directional icons such as chevrons and arrows mirror under `dir="rtl"`. Code, diffs and terminals stay left to right.
- **Reduced motion.** Movement is removed and short opacity fades stay. The press and enter scales become 1, the shimmer stops on a solid label, and smooth scrolling becomes instant.
- **Forced colors.** Focus rings are outlines, which Windows high contrast keeps. Components that show state with a fill (selected rows, meters, active toggles) add an outline or a system color in forced colors mode.
- **Touch targets.** Interactive parts of components are 44 px on coarse pointers and at least 32 px with a mouse. The bare `Button` primitive keeps its size; add `pointer-coarse:size-11` when you place one yourself.
- **Focus.** Every control shows the `chatcn-focus` ring on keyboard focus. Nothing removes it.

## What your app still has to do

- Set `lang` and `dir` on `<html>`, and give the page a title that names the conversation.
- Label each thread: pass `aria-label` to `Conversation` when there is more than one on screen.
- Check your accent against `--chatcn-bg` and `--chatcn-card` for 3:1 contrast if you change it.
- Give generated images real alt text. `Image` takes `alt`; ask the model for a description or use the prompt.
- Announce events that happen outside a component: a background run finishing, a file uploaded by another tab. `useChatcnAnnounce` and the conversation's `announce` are there for that.
- Keep approvals waiting until a person answers. Auto-allow timers, like the one in the demos, are for recordings, not products.
- Test with a screen reader on your real content. Model output is your content: headings, tables and links in Markdown are only as good as the model makes them.

Source: https://chatcn.dev/docs/guides/accessibility