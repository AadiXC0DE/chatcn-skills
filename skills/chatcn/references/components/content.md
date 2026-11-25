# Content

What answers contain: markdown, streaming text, code blocks, tables, math, mermaid, images, file cards, link previews, JSON. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `markdown`: **Markdown.** Streaming Markdown for assistant answers. Unfinished syntax heals as it arrives, finished blocks never re-render, and code, tables, math and diagrams hold their space from the first character. Also called: markdown renderer, rich text, formatted text.
- `streaming-text`: **Streaming text.** Plain text that streams in with the signature caret, an optional cadence buffer and one announcement on completion. Also called: typewriter, text streaming, token stream.
- `code-block`: **Code block.** Restrained syntax highlighting that keeps up with streaming, with copy, wrap, line numbers, highlighted lines, long-block collapse and multi-file tabs. Also called: syntax highlighting, code snippet, code viewer.
- `inline-code`: **Inline code.** Mono at 0.9em on a quiet fill. Commands and ids can copy on click.
- `table`: **Table.** Tables that stay readable at any width: two-way scroll under a sticky header, copy as Markdown, CSV or TSV, and an expanded view.
- `math`: **Math.** KaTeX math, inline and display, loaded on first use. The source holds the space while it loads or streams. Also called: latex, katex, equations.
- `mermaid`: **Mermaid.** Mermaid diagrams in the chatcn palette, with source view, zoom, pan and fullscreen. Mermaid loads on first use. Also called: diagram, flowchart.
- `image`: **Image.** An image inside a message: holds its final size from the first paint, blurs up from a placeholder, fails gracefully and opens a full-screen lightbox.
- `image-grid`: **Image grid.** One to four images in a fixed-shape grid, with a +N tile for the rest and a shared lightbox you can page through.
- `file-card`: **File card.** A file the agent made: type icon, a name that never hides its extension, size, preview and download, with generating and error states.
- `link-preview`: **Link preview.** An unfurled link: a compact row or an expanded card with image, title and description, with a skeleton in the final layout and a plain-link fallback.
- `json-viewer`: **JSON viewer.** A collapsible, searchable tree for tool inputs and outputs, with copy path and copy value on every row and full keyboard navigation. Also called: json tree, object viewer.
- `ansi-output`: **ANSI output.** Terminal output with ANSI colors mapped onto the kit palette for both themes, carriage-return progress bars collapsed and incremental parsing for streams.
- `snippet`: **Snippet.** A command or one line of code to copy, with package manager tabs that every snippet on the page follows.
