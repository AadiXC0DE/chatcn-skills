# Media

Image and video generation in a chat: generation cards, edit region, gallery, compare, aspect ratio, style and settings pickers. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `image-generation`: **Image generation.** A generated image in a conversation: prompt and settings, one to four variations at their final shape, a blur-to-sharp scan reveal while the model works, and actions for the one you pick. Also called: text to image, image generator.
- `image-edit-region`: **Image edit region.** Mark part of an image with a rectangle or a brush, then describe the change. The mask shows as monochrome hatching that reads on any image.
- `video-generation`: **Video generation.** A video job in a conversation: queue position, progress with the time left, a poster frame revealed as it renders, then a compact player with the clip's length and resolution.
- `media-gallery`: **Media gallery.** A library of generated images and videos: filter by kind, a square grid grouped by day, a full-screen viewer and multi-select.
- `tool-image-gen`: **Image generation tool.** The renderer for image generation tool calls. The prompt sits in the header, the frames reveal while the tool runs, and refusals read calmly.
- `image-loader`: **Image loader.** The frame an image generation renders into: a live placeholder while the model works, then the reveal. Three variants on one canvas (denoise, mosaic and scan), driven by progress or running indeterminate, in token colors, from 64 px thumbnails to full width.
- `image-compare`: **Image compare.** Before and after for edits and upscales, split by a draggable hairline. Drag, click to jump or use the keyboard, horizontal or vertical, with labels that step aside near the handle.
- `aspect-ratio-picker`: **Aspect ratio picker.** Pick the shape of an image before it is generated. Every option draws its ratio, so 9:16 and 16:9 never get confused. A segmented row or a compact popover grid, with a lockable custom size.
- `style-picker`: **Style picker.** A grid of style presets with your own thumbnails. One style or several with a cap, an optional None tile, and grid keyboard movement by column and row.
- `generation-settings`: **Generation settings.** A compact settings panel for image generation: model, aspect ratio and count up top, with steps, guidance, seed and the negative prompt folded into Advanced. One typed value object in and out.
