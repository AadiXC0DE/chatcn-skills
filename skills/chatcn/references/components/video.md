# Video

Video generation and editing: video player, clip timeline, frame scrubber, storyboard, keyframes, camera motion, motion brush, generation queue. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `timecode` (Pro): **Timecode.** SMPTE timecode with drop frame, editable by scrubbing a field, stepping or typing.
- `loop-card` (Pro): **Loop card.** A gallery card that plays a muted loop on hover or focus and shows its poster otherwise.
- `audio-lanes` (Pro): **Audio lanes.** Music, sound and voice lanes under the video with levels.
- `caption-editor` (Pro): **Caption editor.** A caption track with timing handles, split and merge, and a burn in toggle.
- `reference-elements` (Pro): **Reference elements.** Character, object and scene references for consistent video, with tags.
- `lipsync-panel` (Pro): **Lipsync panel.** Pair a voice track with a face clip and preview sync quality.
- `video-player-pro` (Pro): **Video player pro.** A player for editors: frame steps, J K L shuttle, in and out points that loop, speed, a timecode that cycles to clock and frame number, and a scrub bar that previews the frame under the pointer.
- `frame-scrubber` (Pro): **Frame scrubber.** Scrub a clip frame by frame on a strip of thumbnails or a thin bar. Hover shows the frame under the pointer with its timecode; dragging and the arrow keys land on whole frames.
- `clip-timeline` (Pro): **Clip timeline.** The edit: tracks of clips with thumbnails or waveforms, trim handles, drag to move across tracks, snapping to edges, markers and the playhead, and a ruler that scrubs on whole frames.
- `render-filmstrip` (Pro): **Render filmstrip.** The frames of a render as they arrive, left to right, each resolving out of the paper through the dither reveal. Counts, time left, Stop, and Retry on a frame that failed.
- `video-compare` (Pro): **Video compare.** Two to four takes of one prompt in lockstep from one transport. Shorter takes hold their last frame, pick the winner on its tile or with 1 to 4, and two takes can share one frame in a split view.
- `shot-storyboard` (Pro): **Shot storyboard.** A storyboard of shot cards: prompt, camera move and length edited in place, reorder by drag or keyboard, and Generate all with the total cost on the button.
- `shot-sequencer` (Pro): **Shot sequencer.** Sequence shots with cuts, crossfades, dips to black or wipes, preview the real transitions, and export the edit as one file.
- `3d-asset-viewer` (Pro): **3D asset viewer.** An orbit viewer for generated 3D assets on a small WebGL 2 renderer: matcap, wireframe or both, a slow turntable, throw and zoom, and a turntable export to video.
- `video-prompt-bar` (Pro): **Video prompt bar.** The video prompt: start and end frame slots above the text, and chips for length, aspect and camera motion in the line. The cost follows the length, a short balance blocks Generate with the reason, and Generate turns into Stop while the clip renders.
- `keyframe-strip` (Pro): **Keyframe strip.** Start, middle and end frames as drop targets, with interpolation markers between them that show each gap and insert a keyframe half way. Frames a model is filling in show the denoise placeholder.
- `camera-motion-picker` (Pro): **Camera motion picker.** Pan, tilt, dolly, orbit, zoom and roll as drawn tiles whose little scene performs the move, combinable up to a limit, each with direction and intensity, and the whole move said in words for the prompt.
- `motion-brush` (Pro): **Motion brush.** Paint up to five regions over the start frame and drag a direction arrow for each, with speed. A region without an arrow holds still. Dabs and vectors come out in frame fractions, ready for a motion mask.
- `motion-path` (Pro): **Motion path.** Draw the path an object follows over the clip, shape the timing on a cubic bezier graph with draggable handles or presets, and play it along the path at the clip's length.
- `duration-picker` (Pro): **Duration picker.** The clip length as film you drag out, priced on the handle, or as 5 s, 10 s and custom options. Lengths the model cannot render are off with the model's range in words.
- `extend-clip` (Pro): **Extend clip.** Continue a clip from its last frame: a timeline with the seam and the added stretch sized to the chosen length, a composer that says the cost and turns into Stop, and the seam kept once the new frames land.
- `generation-queue` (Pro): **Generation queue.** A job queue panel: progress and time left per job, place in line with drag or Alt and arrow reorder, cancel, retry with the reason, notify me, and credits spent.
