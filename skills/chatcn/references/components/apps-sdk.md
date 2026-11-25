# Apps SDK

ChatGPT apps and MCP Apps widgets: display modes, PiP and fullscreen, a host simulator, and widgets for checkout, seats, maps, polls, email drafts. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `slides-widget` (Pro): **Slides widget.** A generated deck in the chat: slides arrive as they are written, then Present fills the screen and Export hands over an editable file.
- `media-widget` (Pro): **Media widget.** A talk, recording or podcast in the chat with chapters an assistant wrote, cut into the scrubber and listed below.
- `translation-card` (Pro): **Translation card.** A translation that shows its work: the source above, the result below, phrase by phrase, so pointing at any phrase lights the words it came from.
- `location-picker` (Pro): **Location picker.** Set a pickup or delivery point the way a ride app does: the pin stays still and the map moves under it, snapping to the spots a car can actually stop.
- `sheet-widget` (Pro): **Sheet widget.** A small table the assistant hands over to be corrected: edit a cell, watch totals follow, and send exactly what changed back.
- `checklist-widget` (Pro): **Checklist widget.** Steps an assistant laid out, to tick off in the chat, with a progress bar of one segment per step and drag to reorder.
- `rating-widget` (Pro): **Rating widget.** Feedback in one tap that invites a little more: stars that name what they mean, or a 0 to 10 scale, then quick reasons and a comment.
- `file-picker-widget` (Pro): **File picker widget.** Pick files from a connected drive without leaving the chat: folders, a path, search, and files the assistant can't read shown with the reason.
- `definition-card` (Pro): **Definition card.** A dictionary entry that sounds the word out: syllables that light as it is spoken, parts of speech as tabs, examples, similar words and where it came from.
- `currency-widget` (Pro): **Currency widget.** A conversion you can work with: both amounts are fields, swap turns the pair, and the rate says how fresh it is.
- `business-profile` (Pro): **Business profile.** A place or a person, ready to act on: actions up front, open status worked out from the hours, local time for people, details to copy.
- `message-draft` (Pro): **Message draft.** A text or team chat message the assistant drafted, drawn as the thing it will become. Edit it in place, see how a text will split, and send with a few seconds to take it back.
- `doc-card` (Pro): **Doc card.** A document the assistant found or made: a first page drawn from its own outline, who owns it and who can see it, the passage that answers the question, and the outline as jump links.
- `news-stack` (Pro): **News stack.** Headlines as a stack with one story open at a time: its summary, picture and every outlet that ran it. The rest stay a line or two with their source and age.
- `widget-skeletons` (Pro): **Widget skeletons.** Loading skeletons for chat app widgets at their exact final size, and a loading boundary that hands over to the widget strip by strip with nothing moving.
- `availability-picker` (Pro): **Availability picker.** Open times from someone's calendar, picked and booked without leaving the thread, in your time zone or theirs.
- `rsvp-card` (Pro): **RSVP card.** An invite answered in the thread, drawn against your own calendar so a clash is seen before it is read, with a counter proposal from times you are free.
- `poll-widget` (Pro): **Poll widget.** A poll that lives in the thread, with results that grow from each row as votes arrive and an owner close that names the winner.
- `stock-quote` (Pro): **Stock quote.** A quote that answers how it is doing in one look, with a drag across the chart to measure any move and a price alert drawn on the line.
- `email-draft` (Pro): **Email draft.** A draft email the assistant writes and you finish in the thread, sent with a few seconds to undo.
- `oauth-connect` (Pro): **OAuth connect.** The card an assistant shows when a tool needs an account: who runs the server, what it may do in one plain sentence, and one button to connect.
- `kanban-widget` (Pro): **Kanban widget.** A small board for tasks made in the conversation, moved by drag, by one press, or entirely from the keyboard.
- `score-card` (Pro): **Score card.** A live score with the period, the clock and the moments that mattered, drawn on a strip that tells the story of the match.
- `recipe-card` (Pro): **Recipe card.** A recipe you can cook from in the thread: change the servings and every amount rescales, in the list and inside the method.
- `countdown-widget` (Pro): **Countdown widget.** A timer on a minute tape you drag to set, or a countdown to a moment in steady tabular digits.
- `chess-board` (Pro): **Chess board.** A calm board for a game played in the thread, with the assistant's suggestion drawn as an arrow and one button to play it.
- `seat-map` (Pro): **Seat map.** A flight or venue seat map the assistant renders in the thread: price tiers, taken seats, exit rows, keyboard navigation that skips aisles, a live readout of the focused seat and a selection summary with a rolling total.
- `instant-checkout` (Pro): **Instant checkout.** A checkout sheet in the thread: order, ship to, delivery, payment and totals with tax, confirmed with one button that names the amount. Processing, declined and paid all happen in place.
- `delegated-payment` (Pro): **Delegated payment.** Grant an agent a spend limit, a merchant scope and an expiry, then watch it spend: a token summary, a usage meter with a segment per charge, and revoke one confirm away.
- `list-map-widget` (Pro): **List map widget.** Places as a list and a drawn map side by side, with selection and hover synced between them. Built for full screen; on a phone the list stands alone.
- `simulation-widget` (Pro): **Simulation widget.** A small simulation the assistant sets up and hands over: a projectile or compound interest with parameters as sliders, play, pause and reset, a sentence that explains the result and the last run kept as a ghost.
- `explorable-lesson` (Pro): **Explorable lesson.** An interactive explainer in the thread: steps, sliders and a drawing that redraws as they move, with prose rewritten from the live values so the words always describe the picture.
- `widget-display-modes` (Pro): **Widget display modes.** One shell that moves a widget between inline, inline carousel, full screen and picture in picture without remounting it, with spatially honest transitions, host safe areas, max height and the current mode in context.
- `pip-widget` (Pro): **PiP widget.** A floating picture in picture window that stays on top while the conversation continues: drag and throw it to any corner, move it with the arrow keys, minimize it to a bar with a live summary.
- `fullscreen-widget` (Pro): **Fullscreen widget.** A full screen widget frame that keeps the composer docked, grows out of its inline card, clears notches through safe areas so close never clips, traps focus and closes on Escape.
- `widget-host-simulator` (Pro): **Widget host simulator.** A host on your desk for building ChatGPT Apps and MCP Apps widgets: theme, locale, display mode, max height, screen width, tool input and output editors, widget state, and a log of every call the widget makes.
