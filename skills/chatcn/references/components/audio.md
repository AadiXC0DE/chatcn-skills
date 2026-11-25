# Audio

Audio and speech: TTS studio, voice design and cloning, music composer, stem mixer, multitrack timeline, spectrogram, dubbing, lyrics. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `pronunciation-dictionary` (Pro): **Pronunciation dictionary.** Word to phoneme or alias rules with a test play per row.
- `lyrics-editor` (Pro): **Lyrics editor.** Structured verse, chorus and bridge sections with syllable hints and a rewrite per section.
- `chapter-waveform` (Pro): **Chapter waveform.** A waveform with chapter markers, titles and a jump list.
- `speaker-lanes` (Pro): **Speaker lanes.** Diarized speakers as lanes on a timeline, with rename and merge.
- `lyrics-sync` (Pro): **Lyrics sync.** Lyrics highlighted line and word in time with playback.
- `dubbing-panel` (Pro): **Dubbing panel.** Source and target language with speaker tracks, per line review and re-voice.
- `music-composer` (Pro): **Music composer.** One composer for a song: a description with genre, mood, tempo with tap tempo, key and length chips, an instrumental switch, and lyrics with section tags that autocomplete.
- `song-card` (Pro): **Song card.** A generated song as a row or a tile: cover with play, title and style, waveform with the position, A and B takes, and extend, remix and download for the take you hear.
- `stem-mixer` (Pro): **Stem mixer.** Stems in sync with mute, solo, a fader and a live meter each, export per stem with its state, and the mix meter.
- `multitrack-timeline` (Pro): **Multitrack timeline.** A DAW lite timeline: clips you drag, trim and move between tracks, a bar and beat ruler, snap, a loop region, zoom around the pointer and synced playback.
- `waveform-region-editor` (Pro): **Waveform region editor.** Select a stretch of a song and regenerate only that part from a prompt, then compare the new take in place and keep or discard it.
- `spectrogram` (Pro): **Spectrogram.** A spectrogram on canvas in the gray ramp with a log frequency axis: a whole recording with a playhead and seek, or live from an analyser or a stream, with a hover readout.
- `level-meter` (Pro): **Level meter.** A segmented level meter, vertical or horizontal, mono or stereo, with peak hold and a clip light, read every frame without re-rendering.
- `audio-ab-switch` (Pro): **A/B switch.** Two takes playing in sync with one key to switch, a 30 ms crossfade, the waveform of the take you hear and keep A or B.
- `record-button` (Pro): **Record button.** Record with a count in, the input level as a ring around the button, pause and resume, and a take to play back, keep or discard.
- `tts-studio` (Pro): **TTS studio.** A long form script editor for speech: a voice per paragraph, expressive tags inside the text, stale marks after edits, regenerate one sentence at the caret, and a timeline of takes with play all and take switching.
- `audio-tags` (Pro): **Audio tags.** Expressive tags such as [whispers] and [laughs] drawn as chips inside the script text, with a menu that opens on [ and filters as you type. Tags the model does not know are marked.
- `voice-design` (Pro): **Voice design.** Describe a voice in words, hear three previews, pick the closest, nudge it or refine from it, then name and save it.
- `voice-clone-flow` (Pro): **Voice clone flow.** Record or upload samples, each checked for background noise, clipping and level, with a meter of speech against what a close match needs, then a consent step and creation.
- `voice-library` (Pro): **Voice library.** A voice grid with search and filters by accent, use case and register, each card with its sample and waveform in place. The library scale variant of the free voice-picker.
- `speech-settings` (Pro): **Speech settings.** Stability, similarity, style and speed, each slider saying what its ends do, with presets to start from, Custom once anything moves, and a reset.
- `sfx-generator` (Pro): **Sound effect generator.** Prompt, length and four variations as a playable grid: play in place, pick one, download, with a pending state that holds the grid and failures per tile.
- `audio-overview` (Pro): **Audio overview.** A two host audio overview of a set of sources: captions that follow the speaker, a scrubber drawn from the turns, speeds, a transcript, and Ask a question to cut in and hear an answer before it resumes.
