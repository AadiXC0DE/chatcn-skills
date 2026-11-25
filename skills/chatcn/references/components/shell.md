# Shell

App chrome: chat layout, sidebar, thread list, header, command palette, search, shortcuts, onboarding, and Pro mobile shells. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `chat-layout`: **Chat layout.** The app shell: sidebar, thread and an optional side panel on the shared Resizable. Below 768 px the sidebar becomes a drawer and the panel a full-screen sheet. Also called: chat app layout, app shell, chat shell.
- `chat-sidebar`: **Chat sidebar.** The thread sidebar: New chat, a filter, threads grouped by date with Pinned on top, inline rename, delete with undo, live status per thread, a 52 px rail and a resizable edge. Also called: sidebar, conversation list, history sidebar.
- `thread-list`: **Thread list.** The rows and groups the sidebar is built from: a roving-focus list, date grouping, inline rename, a row menu and a status mark for running, waiting, failed and unread threads. Also called: chat history, conversation history.
- `project-switcher`: **Project switcher.** Switches the project a sidebar shows. Each project lists its knowledge files, instructions, sharing and indexing, so picking one says what context the next chat starts with.
- `app-mode-switcher`: **App mode switcher.** A segmented control for product modes like Chat, Work and Code. One clipped pill slides between segments, locked modes say why, and the whole control freezes during a run.
- `chat-header`: **Chat header.** The bar above a thread: a title you rename in place, the model, a Temporary badge, Share and a More menu, plus the sidebar toggle on mobile. Also called: header, top bar.
- `command-palette`: **Command palette.** Cmd/Ctrl+K: one field that finds chats, runs actions and switches models, with fuzzy matching, groups, shortcut hints and no open animation from the keyboard. Also called: cmd k, command menu, spotlight, search palette.
- `chat-search`: **Chat search.** Full-text search across chats with the matched words marked in titles and snippets, role filters, recent chats and full keyboard control.
- `keyboard-shortcuts`: **Keyboard shortcuts.** A dialog with every shortcut grouped by area, a filter and platform-aware keys, plus a ShortcutKeys renderer for tooltips and menus.
- `composer-mobile`: **Composer mobile.** A bottom-anchored phone composer that rides the on-screen keyboard, with attach sources and tools in a bottom sheet. Also called: mobile chat input, mobile composer.
- `onboarding`: **Onboarding.** First-run UI that stays calm: a skippable step flow with live vignettes, a setup checklist, and a capability tour anchored to real controls.

## chatcn Pro

- `sheet-model-picker` (Pro): **Sheet model picker.** The model and mode picker for phones: a bottom sheet with half and full heights, drag, flick and native feeling physics.
- `artifact-sheet` (Pro): **Artifact sheet.** An artifact opens as a near full height sheet and the chat steps back behind it, scaled down with rounded corners.
- `swipe-actions` (Pro): **Swipe actions.** Swipe a message or a thread for retry, copy, pin or delete, with a commit line for a long swipe and a small bump when you cross it.
- `long-press-menu` (Pro): **Long press menu.** Press and hold a message for its actions: it sinks, pops, lifts above a blurred screen, and the menu opens beside it.
- `voice-sheet` (Pro): **Voice sheet.** Voice mode as a sheet over the chat: compact with the chat readable above it, or full with the big orb, live captions and controls.
- `mobile-shell` (Pro): **Mobile shell.** The phone shell for a chat app: swipe the chat aside for the sidebar, on a spring that carries the flick, with safe areas handled.
- `camera-capture` (Pro): **Camera capture.** Point the camera at something and ask about it: the subject is outlined, the shot freezes into a crop, and the question goes with the picture.
- `mobile-tab-bar` (Pro): **Mobile tab bar.** The bottom tab bar for an AI app, with a pill that slides between tabs on a spring and badges that say what is waiting.
