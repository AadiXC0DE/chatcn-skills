# Composer

The input: prompt input, send button, attachments and drop zone, model picker, reasoning effort, dictation, mentions and slash menus. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `prompt-input`: **Prompt input.** The composer: a growing textarea with slots for context, attachments and tools, IME-safe Enter to send, Escape to stop, and paste and drop that turn into files. Also called: chat input, chatbox, chat box, message input.
- `send-button`: **Send button.** Send that becomes Stop in the same footprint: the arrow lifts and blurs out while the kit's square mark settles in. Also called: submit button, send message button.
- `attachment`: **Attachment.** Files in the composer as chips or cards: image thumbnails with a hairline, type icons, sizes, a determinate upload ring, errors with retry, and a 140 ms removal. Also called: file attachment, attach file, image upload.
- `drop-zone`: **Drop zone.** Composer-sized and full-page drop targets that say before the drop whether files will be accepted, and why not. Also called: file upload, drag and drop, dropzone, upload area.
- `model-picker`: **Model picker.** Model menu for the composer footer, grouped by provider, with search, capability glyphs, a New tag and your own provider marks. Also called: model selector, model switcher, model dropdown, choose model.
- `reasoning-effort`: **Reasoning effort.** How hard the model thinks: a segmented Low, Medium, High control with a spring-driven indicator, or a compact Think toggle. Also called: thinking level, reasoning level, effort selector.
- `mode-switcher`: **Mode switcher.** The tools menu: web search, deep research, canvas and image. Active modes become chips in the composer and can change its placeholder.
- `dictation-button`: **Dictation button.** Microphone button with permission, listening with live level bars, transcribing and a blocked state that says how to fix it. Backed by useChatcnDictation. Also called: voice input, speech to text, microphone button, dictate.
- `context-chips`: **Context chips.** The context the agent will read with the next message: files, a selection, a link, the current page. Removable, with overflow folded into +3.
- `character-counter`: **Character counter.** Character or token budget for the composer, with soft and hard limits, a ring variant and announcements only at thresholds.
- `rich-prompt-input`: **Rich prompt input.** The composer with a rich editor: inline chips for @ mentions and / commands, prompt variables filled with Tab, long pastes as attachments, and a value serialized to text, mentions and commands. Also called: rich text input, rich composer, mentions input.
- `mention-menu`: **Mention menu.** The @ popup for files, folders, symbols, people, agents and connectors: grouped, fuzzy filtered with the matched characters emphasized, recent first, anchored to the caret. Also called: at mention, mentions, mention autocomplete.
- `slash-menu`: **Slash menu.** The / popup for commands and skills, with categories, descriptions, shortcuts, the active command's arguments, and a ghost argument hint after insertion. Also called: slash commands.
- `inline-chip`: **Inline chip.** A token inside text for a mention, file, URL, command or prompt variable. Shares the prose baseline, inverts when selected and removes as one unit.
- `upload-queue`: **Upload queue.** Several uploads at once: per-file progress, speed and time left, processing, failures with retry and cancel, an overall header with Cancel all, and a fold into attachment chips when every file is done.

## chatcn Pro

- `template-composer` (Pro): **Template composer.** Prompt templates with fillable slots inline in the sentence. Tab between them, watch filled ones settle into the text, and never send half a prompt.
- `voice-first-composer` (Pro): **Voice first composer.** A composer where talking comes first: a large mic that becomes the live waveform, the words appearing as you speak, and one tap to switch to typing without losing any of them.
- `search-composer` (Pro): **Search composer.** A search field with its focus scope inside it: web, academic, social or files, switchable from the keyboard, with recency at the end.
- `token-estimate` (Pro): **Token estimate.** A live token and cost estimate under the composer that never jitters, knows the model's context window, and says how much room is left before it runs out.
- `multimodal-tray` (Pro): **Multimodal tray.** Camera, screen, file, voice and a sketch pad in one tray that opens from the composer, with everything attached shown as previews above the text.
- `cli-composer` (Pro): **CLI composer.** A terminal style composer for coding agents: a prompt glyph, history on Up and Down, Ctrl R reverse search, and slash commands that Tab completes.
- `persona-picker` (Pro): **Persona picker.** Choose which agent answers, right from the composer: @ mentions, a searchable picker, and each agent's model and tools before you send.
- `schedule-send` (Pro): **Schedule send.** Run a prompt later or on a schedule: presets with the real time they mean, a custom time, repeat, the time zone written out, and Undo right after.
- `region-capture` (Pro): **Region capture.** Pick part of a screen and attach it: drag a selection with its size in real pixels, capture it at full resolution, and watch it land in the message.
- `pill-composer` (Pro): **Pill composer.** A compact pill that opens into the full composer when it gets focus, growing out of the pill's own shape, and folds back with the draft kept.
- `prompt-enhancer` (Pro): **Prompt enhancer.** A composer that rewrites your prompt in place and shows the rewrite as an inline word diff: keep or drop each change, then use the result.
- `steer-input` (Pro): **Steer input.** The composer for an agent that works in steps. While a run is live it stays open, and every message goes in one of two named ways: Steer, at the next step without stopping, or Queue, after the run.
- `prompt-autocomplete` (Pro): **Prompt autocomplete.** The composer with ghost completions after the caret. Tab takes the suggestion, one keystroke takes the next word, and accepted words ink in where they land.
- `inline-edit-box` (Pro): **Inline edit box.** A document you select in and press Cmd K to edit with an instruction. The edit streams into the page where it will land, so you read it in context before you accept.
