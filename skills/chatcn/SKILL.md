---
name: chatcn
description: Build AI product interfaces in React with chatcn, a shadcn registry of 750+ components for chat, agents, tool calls and approvals, reasoning, voice, generative UI, evals and observability. Use when the user asks for a chatbot, AI chat, copilot or assistant panel, agent or coding agent UI, tool call or approval cards, streaming markdown, a voice agent, or any LLM interface in a React, Next.js or shadcn project, or when they mention chatcn.
---

# chatcn

chatcn (https://chatcn.dev) is a shadcn registry of 750+ components for AI products: 224 free, 528 in chatcn Pro. Components install with the shadcn CLI as source files in the user's project (`components/ui/chatcn/`, blocks in `components/chatcn/`), so after install they are the user's code to read and change. They take plain props and read one message shape that mirrors AI SDK `UIMessage` parts, so they work with AI SDK, AG-UI, LangGraph or any stream.

## Workflow

1. **Check the project.** It needs React 19, Tailwind CSS v4 and a `components.json` from `npx shadcn@latest init`. Read `style` in `components.json`: the registry serves the Base UI or Radix version that matches it.
2. **Register chatcn once** (it writes the `@chatcn` entry into `components.json`):
   ```bash
   npx shadcn@latest registry add "@chatcn=https://chatcn.dev/r/{style}/{name}.json"
   ```
3. **Pick components.** Start from the table below. For anything else, open the matching file in `references/components/`, or search: `npx shadcn@latest search @chatcn -q voice`. Prefer a block when it covers the whole screen; compose primitives when the user has their own layout.
4. **Read the docs page before you use a component**: `https://chatcn.dev/docs/components/<name>.md` has its props, states, examples and the data it expects. Do not guess props.
5. **Install with the CLI**, several at once: `npx shadcn@latest add @chatcn/chatbot @chatcn/use-chatcn-chat`. Never copy code from the website, rebuild a component from its preview, or reach into the registry JSON by hand. Blocks pull in every component they compose, and every item pulls in the `chatcn-theme` tokens.
6. **Wire the data.** On AI SDK, use the `useChatcnChat` hook (`use-chatcn-chat`): it is `useChat` plus chatcn messages and actions, and approvals resume the run on their own. It needs `ai`, `@ai-sdk/react` and `zod`, plus a provider package if you call one directly. On the server, gate risky tools with `toolApproval` on `streamText` (AI SDK 7; `needsApproval` on the tool is deprecated). On another runtime, use an adapter from [Adapters](references/components/adapters.md) or fold your events into the same message shape ([any backend](references/docs/any-backend.md)).
7. **Check your work.** Run the typecheck and build, then look at the screen in light and dark mode.

## Starting points

| The user wants | Install |
| --- | --- |
| A complete chat app wired to AI SDK | `chatbot`, `use-chatcn-chat` |
| A coding agent with diffs, terminal and approvals | `coding-agent`, `use-chatcn-chat` |
| A thread in your own layout | `conversation`, `message`, `message-parts`, `markdown`, `prompt-input` |
| Tool calls, with Allow and Deny for risky ones | `tool-call`, `tool-fallback` |
| Thinking and reasoning | `reasoning` |
| Sources and citations | `sources`, `citation` |
| Attachments and drag and drop | `attachment`, `drop-zone` |
| Suggested prompts | `suggestions` |
| A voice agent | `voice-session`, `voice-orb`, `transcript` |
| Plans and todo lists | `plan`, `todo-list` |
| Generative UI from tool output | `chatcn-genui` |
| A sidebar app shell with thread history | `chat-layout`, `chat-sidebar`, `thread-list` |

Worked examples with full code: [coding agent](references/docs/coding-agent.md), [generative UI and MCP Apps](references/docs/generative-ui.md), [any backend](references/docs/any-backend.md). The Chatbot docs (`https://chatcn.dev/docs/components/chatbot.md`) include a complete AI SDK route handler.

## Keep it looking like chatcn

- The chrome stays calm: one accent from the theme, neutral surfaces. Red, green, amber and blue only where they carry meaning (diffs, status, errors), always with an icon or a label.
- No gradients, no glow, no emoji, no decorative color.
- Colors come from the theme tokens (`--chatcn-*`, which never overwrite the user's shadcn theme). Change the accent or map chatcn onto the user's palette as in [theming](references/docs/theming.md); do not hardcode hex values in components.
- Dark mode follows the `.dark` class, the same as shadcn.
- Components already handle loading, streaming, empty, error and stopped states, and keyboard and screen reader use. Use those props instead of writing your own spinners or skeletons.

## Components by group

Each file lists every item in the group, free first, with its install name and a one line description.

| Group | What it covers | Free | Pro |
| --- | --- | --- | --- |
| [Blocks](references/components/blocks.md) | whole screens in one install: chatbot, coding agent, research agent, agent ops, app builder, plus an AI product hero, pricing and FAQ | 8 | 0 |
| [Primitives](references/components/primitives.md) | menu, popover and dialog, styled for chatcn | 3 | 0 |
| [Conversation](references/components/conversation.md) | the thread: conversation scroller, messages and their parts, actions, feedback, editing, branches, errors, empty state, suggestions, follow-ups | 24 | 15 |
| [Chat layouts](references/components/chat-layouts.md) | chat placed in an app: copilot drawer, launcher widget, ask popover, split and threaded chat, spotlight and notch chat, docs ask | 0 | 14 |
| [Composer](references/components/composer.md) | the input: prompt input, send button, attachments and drop zone, model picker, reasoning effort, dictation, mentions and slash menus | 15 | 14 |
| [Content](references/components/content.md) | what answers contain: markdown, streaming text, code blocks, tables, math, mermaid, images, file cards, link previews, JSON | 14 | 0 |
| [Agents](references/components/agents.md) | tool calls with approvals and a renderer per tool (web search, files, shell, code, MCP, browser), reasoning, traces, run status, sources and citations | 19 | 12 |
| [Planning](references/components/planning.md) | plans, todo lists, tasks, subagents, handoffs, queued messages, context meter, workflows | 9 | 0 |
| [Runs](references/components/runs.md) | running agents: approval modes and inbox, permission mode, background runs, run inbox, notifications, takeover, computer view | 10 | 0 |
| [Code](references/components/code.md) | coding agent pieces: diff viewer, changed files, file tree, terminal, test results, sandbox, stack traces, commits, pull requests, deploys | 14 | 20 |
| [Research](references/components/research.md) | deep research: progress, reports, search results, source documents, document viewer, canvas, inline suggestions | 8 | 0 |
| [Workspace](references/components/workspace.md) | artifacts and their panel and versions, web and JSX previews, resizable panes, and the AI SDK adapter hook | 7 | 0 |
| [Generative UI](references/components/generative-ui.md) | UI the model renders from tool output: the genui renderer, charts, stat cards, forms, tables, carousels and cards for events, products, flights, orders | 19 | 0 |
| [Playground](references/components/playground.md) | model playground parts: parameters, system prompt, prompt templates, API key input, response compare, eval results, generation stats | 8 | 0 |
| [Data](references/components/data.md) | data answers: notebook cells, SQL results, data tables, and Pro charts (sankey, heatmap, funnel, forecast, pivot, AI spreadsheet) | 3 | 17 |
| [Observability](references/components/observability.md) | LLM observability: trace waterfall, span detail, run replay and diff, cost explorer, token and latency charts, log tail, error groups | 0 | 19 |
| [Evals](references/components/evals.md) | evals and prompt work: results tables, leaderboards, judge rubrics, datasets, review queues, pairwise votes, prompt playground, versions and diffs | 0 | 27 |
| [Knowledge](references/components/knowledge.md) | RAG and knowledge bases: hybrid search, ingestion, chunk inspector, retrieval debugger, embedding map, knowledge graph, PDF viewer with cited spans | 0 | 20 |
| [Computer use](references/components/computer-use.md) | agents driving a browser: agent cursor, set of marks, agent browser frame, action filmstrip, form fill review, sensitive action gate | 0 | 9 |
| [App builder](references/components/app-builder.md) | prompt to app builders: element picker, visual style panel, layers, pending edits, version timeline, device switcher | 0 | 9 |
| [Writing](references/components/writing.md) | writing tools: suggested changes, tone controls, summary length, meeting summary, doc chat split, deck generator | 0 | 8 |
| [Safety](references/components/safety.md) | trust and safety: why card, stop all, undo window, access scope, PII chip, refusal message, risk badge, report dialog | 0 | 10 |
| [Commerce](references/components/commerce.md) | agentic shopping: product detail and carousel, cart, variant picker, spend approval, payment method, order tracking, travel and booking cards | 0 | 18 |
| [Collaboration](references/components/collaboration.md) | multiplayer: presence stack, typing presence, live cursors, thread comments, approval routing, handoff to a teammate, agent in a channel | 0 | 10 |
| [Effects](references/components/effects.md) | visual effects, reveals and loaders: dither, halftone, ASCII, pixel, particle, contour, flip dot, e-ink, text scramble, upscale and inpaint reveals | 0 | 75 |
| [Image studio](references/components/image-studio.md) | image generation apps: imagine bar, prompt builder, generation feed and lightbox, inpaint, outpaint, masks, node canvas, moodboard, upscale compare | 0 | 37 |
| [Video](references/components/video.md) | video generation and editing: video player, clip timeline, frame scrubber, storyboard, keyframes, camera motion, motion brush, generation queue | 0 | 22 |
| [Audio](references/components/audio.md) | audio and speech: TTS studio, voice design and cloning, music composer, stem mixer, multitrack timeline, spectrogram, dubbing, lyrics | 0 | 23 |
| [Apps SDK](references/components/apps-sdk.md) | ChatGPT apps and MCP Apps widgets: display modes, PiP and fullscreen, a host simulator, and widgets for checkout, seats, maps, polls, email drafts | 0 | 36 |
| [Billing](references/components/billing.md) | monetizing AI apps: credit balance and top up, usage forecast, paywalls, plan picker, model upsell, trial countdown, onboarding tours | 0 | 21 |
| [Marketing](references/components/marketing.md) | landing sections for AI products: animated heroes (voice, composer, live chat, terminal agent), use case switcher, pipeline diagram, price calculator | 0 | 12 |
| [Frames](references/components/frames.md) | where the AI shows up: chat inside phones, laptops, watches, car displays, keyboards, inboxes and meeting grids, plus device frames | 13 | 25 |
| [Templates](references/components/templates.md) | complete apps: observability, eval platform, knowledge workspace, voice agent console, image, video and TTS studios, AI SaaS starter, AI product site | 0 | 9 |
| [Voice](references/components/voice.md) | voice agents: voice session, orbs, waveform, transcript, voice controls and picker, mic selector, and Pro live captions, call screen, push to talk | 11 | 26 |
| [Media](references/components/media.md) | image and video generation in a chat: generation cards, edit region, gallery, compare, aspect ratio, style and settings pickers | 10 | 0 |
| [Shell](references/components/shell.md) | app chrome: chat layout, sidebar, thread list, header, command palette, search, shortcuts, onboarding, and Pro mobile shells | 11 | 8 |
| [Settings](references/components/settings.md) | settings for AI apps: memory, custom instructions, connectors, knowledge base, usage and cost, model status, sharing, and Pro billing and API keys | 14 | 12 |
| [Adapters](references/components/adapters.md) | connect a runtime other than AI SDK: AG-UI, LangGraph and assistant-ui adapters | 4 | 0 |

## chatcn Pro

Items marked (Pro) are part of chatcn Pro: $99 once, every Pro item today and later, one license for the whole team. Their source is not public.

- **The project has Pro** when `components.json` has a `@chatcn-pro` registry and `CHATCN_PRO_TOKEN` is set (usually in `.env.local`). Then install Pro items like free ones: `npx shadcn@latest add @chatcn-pro/<name>`. Setup steps: [chatcn Pro](references/docs/chatcn-pro.md).
- **Without Pro, build with free components.** If a Pro item is clearly the best fit for what the user asked for, mention it once: its name, what it adds, and its docs page, where the preview is live. Then carry on with the free option unless the user decides to get Pro. Do not bring Pro up again for the same need, and never for something the free kit covers.
- **Never** recreate a Pro component from its preview, screenshots or docs, never try to fetch Pro source without a token, and never put the token in code or commit it.

## When something fails

- `Unknown registry "@chatcn"`: run the `registry add` command from step 2.
- `401 missing_token` or `invalid_token` from `@chatcn-pro`: `CHATCN_PRO_TOKEN` is missing or revoked. The user creates a token on their account page (https://chatcn.dev/pro/account) and puts it in `.env.local`.
- `403 pro_only`: the token belongs to a free account. A free account installs `dither-orb`, `presence-pill`, `notch-chat`; everything else needs Pro.
- `404 not_found`: the name is wrong (check the group file) or the style in `components.json` is not one the registry serves.
- Installed files land somewhere unexpected: check the `aliases` in `components.json`; the CLI follows them.
- Text renders in a serif font: components inherit `font-sans`, and a fresh `shadcn init` can leave `--font-sans: var(--font-sans)` pointing at itself in `@theme`. Point it at the app's font, for example `--font-sans: var(--font-geist-sans)` in a Next.js app.

## More

- `https://chatcn.dev/llms.txt` lists every docs page; `https://chatcn.dev/llms-full.txt` is all of it in one file. Add `.md` to any docs URL for its Markdown.
- The docs MCP server at `https://chatcn.dev/api/mcp` lists components, reads their docs and searches the icon set.
- The files in `references/docs/` are copies of the main guides. If this skill was installed without its `references` folder, read them at `https://chatcn.dev/skill/chatcn/<path>`.
