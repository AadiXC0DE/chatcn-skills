# Conversation

The thread: conversation scroller, messages and their parts, actions, feedback, editing, branches, errors, empty state, suggestions, follow-ups. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `conversation`: **Conversation.** The thread scroller. Sticks to the bottom only while you are there, lets go the moment you scroll up, and scrolls each new question to the top so the reply has room. Also called: chat, chat window, chat view, chat ui.
- `message`: **Message.** One turn in the thread. Users get a subtle bubble, the assistant writes like a document, and every lifecycle state has a designed look. Also called: chat message, chat bubble, message bubble, assistant message.
- `message-parts`: **Message parts.** Renders a message's parts in order: text, reasoning, tool calls, sources, files and app data, with a quiet fallback for anything unknown.
- `message-actions`: **Message actions.** The toolbar under a message: copy, retry, edit, feedback, share and more. Visible on the latest reply and on touch, revealed instantly on hover everywhere else. Also called: copy message, message toolbar, regenerate.
- `message-feedback`: **Message feedback.** Thumbs up and down. The icon fills when chosen, thumbs down asks what went wrong, and both end with a quiet thank-you. Also called: thumbs up, thumbs down, rating, like and dislike.
- `message-edit`: **Message edit.** Inline editing of a user message. It grows with the text, warns how many replies saving will replace, and never saves in the middle of IME composition. Also called: edit message.
- `branch-navigator`: **Branch navigator.** Moves between the versions of an edited message or a regenerated reply: previous, 2 / 3, next. Also called: message versions, response branches, regenerated versions.
- `message-error`: **Message error.** A failed reply with the fix right next to it. Network, rate limit with a live countdown, context too long, content filter and a generic failure.
- `scroll-to-bottom`: **Scroll to bottom.** The jump-to-latest pill. Appears once you are a viewport away or when something new lands below, counts what you missed, and sticks to the bottom again when pressed. Also called: jump to latest, scroll button.
- `thinking-indicator`: **Thinking indicator.** The pending state before the first token. Nothing for 300 ms, then a shimmering Thinking that stays at least 400 ms, so it never flashes. Also called: typing indicator, loading dots, thinking dots, chat loader.
- `streaming-caret`: **Streaming caret.** The kit's signature mark: a small rounded square at the end of text the model is writing. Solid while tokens flow, a slow blink while waiting, gone when done. Also called: typing cursor, blinking cursor.
- `system-notice`: **System notice.** Divider-style events inside the thread: model switched, context compacted, memory updated, agent joined.
- `checkpoint`: **Checkpoint.** A restore point in the thread. Rewind to here asks first and lists exactly what will be lost: the messages after it and every file change.
- `empty-state`: **Empty state.** The first screen of a chat: a greeting, one line, the composer and up to four suggestions. No illustration. Also called: welcome screen, zero state, new chat screen.
- `suggestions`: **Suggestions.** Starter prompts and follow-ups as chips, rows or cards, with a scrolling chip row that fades only the edges hiding more. Also called: suggested prompts, prompt suggestions, starter prompts.
- `open-in-chat`: **Open in chat.** Hand the current prompt, page or answer to another assistant, with the prompt shown before it leaves.
- `quote-reply`: **Quote reply.** Reply to part of a message. Select text in an answer and a small Reply and Copy toolbar appears; Reply puts the excerpt above the composer as a chip, and the sent message carries it as a quiet block above the text.
- `message-skeleton`: **Message skeleton.** Placeholder for thread history while past messages load: alternating user bubbles and assistant paragraphs with varied line lengths. It renders through the real Message layout, so swapping in content causes no layout shift. Also called: loading skeleton, message placeholder.
- `conversation-divider`: **Conversation divider.** Dividers inside a thread: day boundaries (Today, Yesterday, Mon 12 Oct), where unread messages start, context events such as a model change or a compaction, and the point where the user left off. A hairline with a short label, centered or start aligned, with sticky dates.
- `follow-ups`: **Follow-ups.** Related questions after an answer: hairline rows that send on click, a compact chip layout, one tab stop with arrow key navigation, and a streaming state where rows append in place. Also called: follow up questions, suggested questions.
- `read-aloud`: **Read aloud.** Read a message aloud. An icon button in the message actions turns into a compact player with play and pause, progress, speed and stop, through idle, preparing, playing, paused and failed states. Plays a URL, your own text to speech, or the browser's Web Speech API.
- `export-menu`: **Export menu.** Export or share a conversation: copy as Markdown, download Markdown or JSON, print or save as PDF, and copy a share link with an async success state. Comes with chatcn-export, the helpers that turn ChatcnMessage[] into Markdown, JSON and print HTML.
- `thread-summary`: **Thread summary.** A catch-up card for long threads and returning users: summary points, key decisions, open questions and files touched, each with a Jump to link. Collapsed and expanded, with regenerate, a stale note and a streaming state while the summary is written.
- `receipt-chat`: **Receipt chat.** Chat as a receipt printer. Each answer prints out of a slot above the composer, the paper feeding up as the text streams, then it is cut with a torn edge and settles into the thread.

## chatcn Pro

- `long-message-collapse` (Pro): **Long message collapse.** Long messages fold at a paragraph break with one faded line of the next, say how much is hidden, and keep your place when they fold back.
- `sources-first-answer` (Pro): **Sources first answer.** An answer that shows where it comes from before it says anything: a row of source cards above the text, tied both ways to the citations.
- `retry-with-model` (Pro): **Retry with model.** The retry action with a choice: a new seed from the same model, or another model. Every version is kept and labelled with the model that wrote it.
- `compaction-marker` (Pro): **Compaction marker.** Where a thread was compacted: one quiet line that says how many messages became a summary and how much room it made, with the summary one click away.
- `low-confidence` (Pro): **Low confidence.** Marks the parts of an answer the model is unsure about, calmly, with the reason on hover or focus and a line that steps through them.
- `structured-answer` (Pro): **Structured answer.** An answer laid out like a good magazine page: the one line answer, the key facts in a row of figures, the prose, then where to go next.
- `artifact-card-inline` (Pro): **Artifact card inline.** A compact artifact card for inside a message that keeps every version: step back and the minimap marks the lines that version added.
- `translate-toggle` (Pro): **Translate toggle.** A message in two languages that never jumps: switching crossfades in place, and the block is always as tall as the longer version.
- `message-reactions` (Pro): **Message reactions.** A reactions row under a message: chips with counts, your own in the accent, an add picker, and counts that roll digit by digit.
- `pinned-message` (Pro): **Pinned message.** The strip at the top of a thread that holds its pinned messages. Press it to jump to the pin and step to the next one.
- `voice-message` (Pro): **Voice message.** A voice note bubble whose waveform is the seek bar, with speed, an unplayed dot and a transcript that opens underneath.
- `read-along` (Pro): **Read along.** A message read aloud with each word lit as it is spoken. The highlight follows the playhead through pauses, seeks and speed changes.
- `answer-tabs` (Pro): **Answer tabs.** One response with Answer, Sources, Images and Steps tabs, counts that fill in while it streams, and citations that open their source.
- `paste-chip` (Pro): **Paste chip.** A long paste becomes an attachment chip with its line count, a language guess and a preview, in the composer and in the sent message.
- `compare-responses` (Pro): **Compare responses.** Two candidate answers stream side by side; pick one, call a tie or skip, and the kept answer settles into the thread.
