# Workspace

Artifacts and their panel and versions, web and JSX previews, resizable panes, and the AI SDK adapter hook. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `resizable`: **Resizable.** Split panes with pointer and keyboard resizing, pixel or percent limits, collapsible panels and a hairline handle. No third-party dependency.
- `artifact`: **Artifact.** The inline card that stands for an artifact in a message. It shows what is being written while it streams and opens the artifact panel.
- `artifact-panel`: **Artifact panel.** The side panel for artifacts: versions, Code and Preview, copy, download and full screen. Resizable on desktop, a bottom sheet on phones.
- `artifact-versions`: **Artifact versions.** Step through artifact versions or pick one from a list, with edit times and line diff counts to the previous version.
- `web-preview`: **Web preview.** An iframe preview for apps an agent builds: URL bar with history, device sizes, a browser style loading bar, a crash view and a console drawer.
- `jsx-preview`: **JSX preview.** Renders JSX written by a model without running it. Streaming tolerant, allowlisted and calm when it cannot render.
- `use-chatcn-chat`, `chatcn-mock-transport`: **AI SDK adapter.** Bind useChat from AI SDK 7 to chatcn actions, and run it with a scripted transport when there is no server. Docs: https://chatcn.dev/docs/components/ai-sdk.md.
