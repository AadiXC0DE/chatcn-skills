# Adapters

Connect a runtime other than AI SDK: AG-UI, LangGraph and assistant-ui adapters. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `adapters`: **Adapters.** chatcn components take plain props. Adapters turn AI SDK, AG-UI, LangGraph and assistant-ui runtimes into those props, so you keep your backend and swap only the UI.
- `use-chatcn-ag-ui`: **AG-UI adapter.** Render any AG-UI agent with chatcn: a pure reducer from protocol events to messages, and a hook around HttpAgent with interrupts as approvals. Docs: https://chatcn.dev/docs/components/ag-ui.md.
- `use-chatcn-langgraph`: **LangGraph adapter.** Render LangGraph agents with chatcn: SDK messages and run streams mapped to parts, with human-in-the-loop interrupts as approvals. Docs: https://chatcn.dev/docs/components/langgraph.md.
- `chatcn-assistant-ui`: **assistant-ui adapter.** Keep your assistant-ui runtime and render its messages with chatcn text, reasoning and tool components, approvals included. Docs: https://chatcn.dev/docs/components/assistant-ui.md.
