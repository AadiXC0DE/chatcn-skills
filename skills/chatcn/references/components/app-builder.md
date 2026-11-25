# App builder

Prompt to app builders: element picker, visual style panel, layers, pending edits, version timeline, device switcher. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `element-picker` (Pro): **Element picker.** Pick elements on a live preview the way a design tool does: tag, name, size and padding on hover, a breadcrumb of the element tree, arrow keys to walk it, and Cmd L to attach the element to the next message.
- `visual-style-panel` (Pro): **Visual style panel.** An inspector for the selected element that applies live and writes back to code, no tokens spent: layout with an alignment matrix, a box model you scrub, size, type, the app's palette, border and opacity, with a dot on every property that differs from the code.
- `annotation-pins` (Pro): **Annotation pins.** Numbered notes pinned on a live preview. Drop them, drag them into place, resolve them, and send every open note to the agent as one message that says where each one is.
- `pending-edits` (Pro): **Pending edits.** Visual edits made in the preview, collected as numbered markers on the page and one batch above the composer: review each before and after, undo one, discard all, or save them to code without spending credits.
- `layers-panel` (Pro): **Layers panel.** The generated app's element tree, synced with the preview selection: hide, lock, rename and drag to reorder or nest, with indent guides, a drop line and the full tree keyboard model.
- `version-timeline` (Pro): **Version timeline.** Every version of a generated app on one rail: a live thumbnail, the prompt that made it, what changed and whether it built. Preview any version, restore it, or compare two with a wipe and the prompts in between.
- `theme-token-editor` (Pro): **Theme token editor.** Edit a generated app's tokens and watch the preview follow as you drag: OKLCH sliders with tracks drawn in the color, radius and font, presets, a WCAG contrast check that updates live, and Copy CSS.
- `db-schema-diagram` (Pro): **Database schema diagram.** Tables and relations from the generated schema with crow's foot ends. Pan and zoom, hover a table to trace its relations, open one for sample rows, and see what the last prompt added.
- `device-switcher` (Pro): **Device switcher.** Responsive sizes for a live preview: device presets, rotate, typed width and height, and handles that resize from the center over a breakpoint ruler that shows which breakpoint is active. A Pro variant of the free preview toolbar.
