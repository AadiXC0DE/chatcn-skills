# Frames

Where the AI shows up: chat inside phones, laptops, watches, car displays, keyboards, inboxes and meeting grids, plus device frames. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `plain-screen`: **Plain screen.** A flat phone sized screen for demos: children lay out at a true 393 by 852 viewport, scale to fit, and read the status bar and home bar insets as CSS variables.
- `site-widget`: **Site widget.** A website with a support assistant in the corner: launcher, nudge, a panel that grows out of the launcher into a chat with sources, and a handoff to a person. A full screen sheet on phone viewports.
- `phone-keyboard`: **Phone keyboard.** The on screen phone keyboard with a strip above the keys: word suggestions, rewrite tones with a preview that underlines what changed, and dictation. Letter keys pop into a callout as a script types.
- `search-page`: **Search page.** A search results page with an answer above the links. Numbered citations light up their result and source card, and a highlight option rings your own site and marks it cited.
- `text-thread`: **Text thread.** A phone text conversation where the other side is an assistant: runs of bubbles with tails, a typing bubble that grows into the reply, reactions, link cards, receipts and a script that plays the thread.
- `issue-thread`: **Issue thread.** An issue tracker page where the assignee is an agent: it picks up the ticket, posts progress, links a pull request whose checks run and pass, and moves the status.
- `control-glow`: **Control glow.** The edge a browser draws around a page while an agent drives it, with a badge and a Stop button. It holds still while the agent waits for you and drains away when you take over.
- `touch-playback`: **Touch playback.** A scripted finger for phone and tablet screens that glides, taps with a ring, holds and swipes. The touch twin of the agent cursor: the same props, so one script drives either.
- `inbox-frame`: **Inbox frame.** A mail client with an agent in it: it sorts the inbox into labels, writes a summary over the open thread and drafts the reply.
- `home-widgets`: **Home widgets.** Phone widgets in the standard home and lock screen sizes that show an agent's progress while its app is closed: research running, flights being compared, a task finishing.
- `meeting-grid`: **Meeting grid.** A video call with a note taking assistant: initials tiles with a speaking ring, the assistant's tile with the voice orb, captions that roll up, and notes that fill in with decisions and action items.
- `car-display`: **Car display.** A car's wide centre screen in a flat dash: a dock on the driver's side, tiles for the route, media and answers, and a voice bar that rises with the orb and one line of transcript.
- `keyboard`: **Keyboard.** A laptop keyboard drawn from above with every legend. Keys travel down as a line types along, shift held for capitals, or light from real key presses; a shortcut can be ringed in the accent.

## chatcn Pro

- `spatial-window` (Pro): **Spatial window.** A floating spatial computing window: frosted glass hanging in a room, leaning toward the pointer, with a grabber, a close control and tab and toolbar ornaments.
- `team-chat-frame` (Pro): **Team chat frame.** A generic team chat window showing an agent replying in a channel: channels, grouped messages, an app label, reactions, threads, a streaming reply and a composer.
- `menubar-popover` (Pro): **Menu bar popover.** A desktop menu bar app framed: the menu bar slice with menus, status items and the clock, the app glyph pressed, and a translucent popover hanging from it.
- `paper-frame` (Pro): **Paper frame.** A printed page for documents and reports: true A4, Letter or A5 proportions, margins in millimetres, running header and footer, page numbers and a stack of sheets.
- `device-stack` (Pro): **Device stack.** A phone standing in front of a laptop, the classic product composition, with shadows that hold up in light and dark.
- `annotated-screenshot` (Pro): **Annotated screenshot.** A screenshot with numbered callouts and notes that point at each other, with a dimmed spotlight on the part being described.
- `zoom-inset` (Pro): **Zoom inset.** A magnified inset of one region of an image or live UI, joined to it by connector lines. Drag the region to move the zoom.
- `og-templates`, `og-template-preview` (Pro): **OG templates.** Open graph image templates for docs pages, models and changelogs, rendered with Satori, in light and dark.
- `lock-screen-notification` (Pro): **Lock screen notification.** A phone lock screen with stacked agent notifications that fan out into a list with their actions.
- `editor-window` (Pro): **Editor window.** A code editor frame with a file tree slot, file tabs, breadcrumbs, change bars, an inline suggestion and a status bar.
- `device-preview` (Pro): **Device preview.** Render any component inside a phone, tablet, laptop, display, browser or watch, for docs and marketing.
- `phone-island` (Pro): **Phone island.** Agent status in the phone's cutout. A pill with a spinner and the step while an agent works, a card when it is done or needs a yes, and the assistant dropping out of it to answer. One black shape that grows out of the cutout on a spring.
- `exploded-screen` (Pro): **Exploded screen.** A screen of live UI pulled apart into floating layers, each labelled on a leader line, so one image explains how an AI product is built: the app, the agent panel over it, the tool calls and the agent's cursor. It is flat at progress 0 and apart at 1.
- `fold-frame` (Pro): **Fold frame.** A book style foldable with two live displays. Shut, the small cover display; open, one wide display with two apps side by side; standing like a book; and the back with its camera plateau. It folds between them in real 3D on a spring.
- `phone-frame` (Pro): **Phone frame.** A current flagship phone mockup with a pill cutout, status bar, home indicator and safe area insets, in portrait and landscape.
- `tablet-frame` (Pro): **Tablet frame.** A generic tablet mockup in portrait and landscape, with an optional keyboard case and safe area insets for the content.
- `laptop-frame` (Pro): **Laptop frame.** A generic laptop mockup with lid, camera notch and base, front on or from five CSS 3D cameras, with a real app on the screen.
- `monitor-frame` (Pro): **Monitor frame.** Studio monitor and all-in-one desktop mockups with a stand, rendering a full app at a real desktop viewport.
- `watch-frame` (Pro): **Watch frame.** A smartwatch mockup with rectangular and round faces for glanceable agent status: approvals, progress and results.
- `browser-frame` (Pro): **Browser frame.** Browser chrome for product shots: real tab shapes with concave corners, back, forward and reload, an address field with the lock, and a loading bar, in light and dark chrome.
- `app-window` (Pro): **App window.** A generic desktop app window with a unified title bar, refined gray controls, an inset sidebar panel and an inactive state.
- `terminal-window` (Pro): **Terminal window.** A terminal window with one chrome surface for the title bar and process tabs, a true mono character grid and a cursor. Pairs with the free Terminal.
- `device-tilt` (Pro): **Device tilt.** A CSS 3D perspective wrapper that settles a frame flat as it scrolls into view. Flat under reduced motion.
- `screen-recording` (Pro): **Screen recording.** A stage for product demos: a scripted cursor that moves, clicks and types over the real UI, with click rings, key press overlays and play, pause and loop.
- `chat-share-card` (Pro): **Chat share card.** A social image of an answer or a conversation sized for X and LinkedIn, with a PNG export painted on a canvas and no library.
