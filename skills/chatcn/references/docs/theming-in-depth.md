# Theming in depth

How the tokens reach your CSS, the accent and where it may appear, matching a shadcn theme, dark mode, density, a brand that stays monochrome, and pairing with NeonKit.

[Theming](https://chatcn.dev/docs/theming) lists the tokens. This guide is about changing them without losing what makes the kit read well: a neutral ramp, one accent, and elevation that comes from surfaces rather than shadows.

## How tokens reach your CSS

Every component depends on the `chatcn-theme` item. When the shadcn CLI installs it, three things land in your global stylesheet:

1. An `@theme inline` block that maps Tailwind names to variables: `--color-chatcn-card: var(--chatcn-card)`, plus the radii, shadows and easings. This is what makes `bg-chatcn-card` and `shadow-chatcn-sm` exist.
2. `--chatcn-*` values on `:root` for light and on `.dark` for dark.
3. The utilities: the type scale (`chatcn-text-12` to `chatcn-text-72`), `chatcn-focus`, `chatcn-press`, `chatcn-shimmer`, `chatcn-spin`, and the keyframes.

Colors, shadows and radii resolve through variables at runtime, so overriding a `--chatcn-*` variable changes every component at once, in any scope. The quickest way to a full set is a [preset or the theme builder](https://chatcn.dev/themes).

## Semantic tokens

| Token | Use |
| --- | --- |
| `--chatcn-bg`, `--chatcn-bg-subtle` | Page canvas, and the slightly offset canvas behind panels |
| `--chatcn-surface`, `--chatcn-card` | Raised surfaces. In dark mode they are lighter than the canvas |
| `--chatcn-inset` | Code, terminal and output wells inside a card |
| `--chatcn-fg` | Primary text and solid buttons |
| `--chatcn-fg-muted` | Secondary text and icons |
| `--chatcn-fg-subtle` | Tertiary text and placeholders |
| `--chatcn-fg-faint` | Disabled text and decorative marks. Not for text people need to read |
| `--chatcn-border`, `-hover`, `-strong` | Hairlines, their hover, and the few borders that must hold in a dense layout |
| `--chatcn-fill`, `-hover`, `-active` | Quiet backgrounds for controls, rows and chips |
| `--chatcn-accent`, `--chatcn-accent-fg` | The one accent and the text that sits on it |
| `--chatcn-primary`, `-fg`, `-hover` | Solid buttons and the send button. Ink until you point it at a brand color |
| `--chatcn-radius-xs` to `-2xl` | The radius scale: 4, 6, 8, 12, 16 and 24 px by default |
| `--chatcn-red`, `-amber`, `-green`, `-blue` | Status as small icons, dots or short text, always with a label |
| `--chatcn-scrim`, `--chatcn-on-media` | Behind dialogs, and text drawn over images |

## The accent

The accent is ink until you set it. Components use it in five places only: focus rings, text selection, links, active toggles and progress fills. It never fills a large surface, so a saturated brand color stays safe.

`app/globals.css`

```css
:root {
  --chatcn-accent: oklch(0.55 0.2 260);
  --chatcn-accent-fg: oklch(1 0 0);
}

.dark {
  --chatcn-accent: oklch(0.72 0.15 260);
  --chatcn-accent-fg: oklch(0.145 0 0);
}
```

- Set both values in both themes. `--chatcn-accent-fg` is the text and icon color on accent fills such as an active toggle.
- Check the focus ring against `--chatcn-bg` and `--chatcn-card`. It needs 3:1 against both to pass WCAG 2.2 non-text contrast.
- Leave status colors alone. A blue accent and the blue status dot can coexist because the status dot always has a label.

## Match a shadcn theme

If your app already has a shadcn palette, point the chatcn roles at it after the theme import. Map roles, not gray steps: the components only read the semantic tokens below.

`app/globals.css`

```css
:root,
.dark {
  --chatcn-bg: var(--background);
  --chatcn-surface: var(--popover);
  --chatcn-card: var(--card);
  --chatcn-inset: var(--muted);
  --chatcn-fg: var(--foreground);
  --chatcn-fg-muted: var(--muted-foreground);
  --chatcn-fg-subtle: var(--muted-foreground);
  --chatcn-border: var(--border);
  --chatcn-border-strong: var(--input);
  --chatcn-fill: var(--muted);
  --chatcn-fill-hover: var(--accent);
  --chatcn-accent: var(--ring);
  --chatcn-accent-fg: var(--primary-foreground);
}
```

shadcn has fewer text steps than chatcn, so `fg-subtle` and `fg-muted` collapse into one. That is fine for most screens; dense ones such as the coding agent read better if you keep chatcn's own `--chatcn-fg-subtle`.

## Dark mode

Dark values live on the `.dark` class, the same convention as shadcn, so a theme toggle that sets `class="dark"` on `<html>` (next-themes with `attribute="class"`, for example) switches chatcn with the rest of your app. Components almost never use `dark:` variants: the tokens flip, and elevation comes from lighter surfaces plus a hairline instead of heavier shadows.

Because the values are plain variables, the class also works on a subtree. A dark terminal panel inside a light page is one class:

```tsx
<section className="dark bg-chatcn-bg text-chatcn-fg rounded-chatcn-lg">
  <Terminal text={output} />
</section>
```

## Density

There is no global density switch, because density is a decision per surface: a chat for customers and an agent trace for engineers want different things. The levers are props.

| Prop | On | Effect |
| --- | --- | --- |
| `density="comfortable"` | `Markdown`, `ResearchReport` | 16/26 prose instead of 15/24 |
| `layout="compact"` | `Message` | The dense log style for traces and side panels |
| `variant="inline"` or `"card"` | `ToolCall`, and `toolVariant` on `Chatbot` and `createChatcnPartComponents` | Quiet rows for long traces, or a card per call |
| `density="compact"` | `Trace` | Shorter rows and smaller icons |
| `variant="compact"` | `TodoList` | A plan that fits inside a message |
| `variant="minimal"` | `PromptInput` | One row: text and actions inline |

Touch density is automatic: interactive parts of components grow to 44 px on coarse pointers through `pointer-coarse:` classes, while desktop keeps the 28, 32 and 36 px control scale.

## A brand that stays monochrome

- **Put the brand in the accent.** Focus, selection, links and progress are the moments people look at; they carry the color well.
- **Put the mark in a slot.** Provider and server marks are user supplied: `renderProviderMark` on the chatbot's model picker, `icon` on `McpAppFrame`, `header` and `headerActions` on the blocks.
- **Keep the type.** Components inherit your `font-sans` and `font-mono`, so a brand typeface applies everywhere with no extra work. Keep weights at 400, 500 and 600.
- **Tint the ramp lightly, if at all.** Chrome, borders and secondary text come from the gray steps. The presets keep the tint under 0.015 chroma so the steps still read against the status, diff and chart hues.
- **Want no hue at all?** Point the status, diff, chart and syntax variables at gray steps, and add `chatcn-code-mono` for code. Diffs also take `tone="mono"`.
- **Brand buttons are opt in.** `--chatcn-primary` follows ink until you point it at your color, which the Cobalt, Lagoon, Forest, Clay and Plum presets do.

## With NeonKit

[NeonKit](https://neonkit.heyaadi.com) is the expressive sibling and shares the icon drawings. Both namespace their variables, so they install into one project without collisions. Point the chatcn accent at the NeonKit color and the two read as one product: NeonKit for the moments that should glow, chatcn for the working surfaces around them.

```css
:root {
  --chatcn-accent: var(--neon);
}
```

Source: https://chatcn.dev/docs/guides/theming-in-depth