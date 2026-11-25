# Voice

Voice agents: voice session, orbs, waveform, transcript, voice controls and picker, mic selector, and Pro live captions, call screen, push to talk. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `voice-session`: **Voice session.** One surface for voice and text: the orb carries the call state, a shared transcript holds spoken and typed turns, and the user can barge in or switch to text mid-conversation.
- `voice-orb`: **Voice orb.** A monochrome sphere of fine contour lines that carries the whole voice state machine through form and motion: idle, connecting, listening, thinking, speaking, interrupted, muted and error. Also called: voice agent, voice assistant, siri orb, voice visualizer.
- `waveform`: **Waveform.** Live input and output levels as a scrolling history, in bars or one continuous line, or a recorded waveform with its played portion. Also called: audio waveform.
- `audio-visualizer`: **Audio visualizer.** Agent audio in five monochrome forms: bars, radial, grid, line and dots, with connecting and thinking motion when there is no sound. Also called: audio bars, sound visualizer.
- `voice-controls`: **Voice controls.** The call bar: mute with a live input level and a microphone menu, speaker, captions, your own controls and End.
- `transcript`: **Transcript.** Live voice transcript with speaker labels, unsettled words in a lighter gray, timestamps that seek, typed turns and a clean cut where the user interrupted. Also called: captions, subtitles, speech transcript.
- `audio-player`: **Audio player.** Read-aloud and audio output player: play and pause, a seek bar you can drag or step with keys, time in tabular figures, speed, and a compact mini player for message actions.
- `voice-picker`: **Voice picker.** Choose a voice after hearing it. Each voice has its own preview button, which becomes stop with a progress ring while the sample plays.
- `use-chatcn-audio-level`: **Audio level.** A Web Audio level meter for a microphone stream or a media element: a perceptual level and log-spaced frequency bands for orbs, waveforms and visualizers.
- `voice-type`: **Voice type.** A live transcript whose letter weight follows how loudly each word was said, so a spoken sentence keeps its emphasis on the page.
- `mic-selector`: **Mic selector.** Pick the microphone and see that it hears you, with clear words when access is not granted, blocked, or there is none.

## chatcn Pro

- `voice-memo` (Pro): **Voice memo.** Record a memo, then get the transcript, a summary and action items to check off.
- `call-log-table` (Pro): **Call log table.** Every call a voice agent took, with outcome, length, sentiment, latency and cost, filters and CSV export.
- `voice-agent-config` (Pro): **Voice agent config.** Everything a phone agent needs in one form: prompt, greeting, voice, tools, interruptions and silence.
- `human-transfer` (Pro): **Human transfer.** Handing a call to a person: queue, ringing, who picked up, and the summary they get.
- `sentiment-track` (Pro): **Sentiment track.** Caller sentiment along a call as one quiet line, with the dips labeled by what happened.
- `call-simulator` (Pro): **Call simulator.** A test call against a voice agent with a persona, a live transcript and pass or fail checks.
- `presence-pill` (Pro): **Presence pill.** The voice presence as a floating capsule. A dot at rest, a pill with the orb, the state word and a live meter while you talk, a card with the transcript and tool chips when there is something to show. One shape that springs between the three.
- `engraved-orb` (Pro): **Engraved orb.** A voice orb drawn like a banknote engraving: a sphere made only of parallel lines that swell where the form is dark, thin out where it is lit, and swell again with the voice. A drop-in swap for the free voice orb.
- `stipple-orb` (Pro): **Stipple orb.** A voice orb drawn as pen and ink stippling: a sphere of evenly spaced dots of one size, where only how close the dots sit makes the form. The dots travel to a new form for every voice state. A drop-in swap for the free voice orb.
- `live-captions` (Pro): **Live captions.** Rolling captions for voice: the recognizer's interim words in gray, settled words in ink, a fixed number of lines that roll up by exactly one line as speech wraps, and an overlay style for video.
- `voice-widget` (Pro): **Voice widget.** A floating call widget for websites. The launcher opens a small panel that asks for consent once, then runs the call with the orb, rolling captions, mute and End, and the full transcript a tap away. Minimize mid call and the launcher carries it.
- `camera-voice-view` (Pro): **Camera voice view.** A voice call with the camera on. The agent marks what it sees with viewfinder brackets and labels, a pointer glides to whatever it is talking about, and its captions roll over the feed.
- `turn-latency-bar` (Pro): **Turn latency bar.** Where a voice agent's response time goes. Each turn splits into transcriber, endpointing, LLM, voice and transport, with the call's p50 and p90 marked and the budget dashed, so the slow turn and the stage to fix are obvious.
- `call-detail` (Pro): **Call detail.** One voice agent call, reviewed. The recording, who spoke when, and the transcript on one clock, with response latency on every agent turn, tool calls where they ran, and a summary of p50 and p90, interruptions and talk time.
- `mic-permission-gate` (Pro): **Mic permission gate.** Asks for the microphone before the browser does, points at the prompt while it is up, and when the answer is no shows the exact steps for the user's browser or system. It opens by itself once the site setting flips to Allow.
- `audio-device-test` (Pro): **Audio device test.** The audio check before a call: pick a microphone and watch it pass on your voice, pick a speaker and hear a chime through it. Too quiet, no sound and too loud each say what to change. The setup flow version of the free voice controls.
- `particle-orb` (Pro): **Particle orb.** A voice orb as a point cloud sphere. It breathes in with the user's voice and ripples out with the agent's, with its own motion for every voice state. A drop-in swap for the free voice orb.
- `pixel-orb` (Pro): **Pixel orb.** A voice orb on a coarse grid of rounded square cells, like an LED panel, for pixel themed products. Four lit steps per cell, rings that say who is talking, and every voice state. A drop-in swap for the free voice orb.
- `wireframe-orb` (Pro): **Wireframe orb.** A voice orb as a globe of latitude lines and meridians whose mesh deforms with the level: lobes push out for the agent and press in for the user. Every voice state. A drop-in swap for the free voice orb.
- `voice-fullscreen` (Pro): **Voice full screen.** Full screen voice mode: the orb on the stage with rolling captions, a self view, screen sharing that moves the screen to the stage, and mute, camera, share, captions and End in one bar. Connecting, reconnecting, a dropped call and the ended summary each have their own stage.
- `call-screen` (Pro): **Call screen.** A phone call surface for voice agents and people: name, state or timer, a ring that follows the other side's voice, mute, keypad with key tones and speaker, and hang up. Incoming, calling, on hold, reconnecting, ended and failed calls are all designed.
- `push-to-talk` (Pro): **Push to talk.** Hold the button or Space to talk, with a ring that follows your voice, and let go to send. Slide away or press Escape to cancel, too short holds cancel with a hint, and keyboard users can latch it with Enter.
- `turn-indicator` (Pro): **Turn indicator.** Who has the floor in a voice call, with live level bars, and a barge-in mark when the user talks over the agent. The turn timeline shows the whole call as two lanes with every barge-in as a mark you can jump to.
- `dither-orb` (Pro): **Dither orb.** A voice orb drawn as a lit sphere in 1 bit ordered dither. Threshold, grain and silhouette react to the input and output levels, and every voice state has its own motion. A drop-in swap for the free voice orb.
- `halftone-orb` (Pro): **Halftone orb.** A voice orb as a sphere of halftone dots. Dot size follows the light and the voice level, and the sphere turns slowly while thinking. A drop-in swap for the free voice orb.
- `ascii-orb` (Pro): **ASCII orb.** A voice orb drawn in Geist Mono cells. Glyph density follows the light and the voice, in short ticks that read as motion. A drop-in swap for the free voice orb.
