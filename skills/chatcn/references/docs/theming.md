# Theming

Pick a preset or build your own theme, install it with one command or paste a few variables. OKLCH tokens, one accent, light and dark.

chatcn ships in ink, but every component reads the same set of `--chatcn-*` variables. Change them once and the whole kit follows: accent, solid buttons, the gray ramp, radii, font and density. Nothing in a component needs editing.

## Pick a theme

10 presets: Ink, Slate, Cobalt, Lagoon, Forest, Olive, Sand, Clay, Plum, Contrast. Try them, or build your own, at [chatcn themes](https://chatcn.dev/themes).

Want something else? The [theme builder](https://chatcn.dev/themes) tunes accent, gray tint, radius, font, density and contrast on a live agent run, checks the focus ring contrast in both modes and gives you a link to share.

## Install a preset

Each preset is a registry item. It installs on top of the base `chatcn-theme` and writes light and dark values into your global CSS, so dark mode keeps working with the `.dark` class.

```bash
pnpm dlx shadcn@latest add https://chatcn.dev/r/theme-forest.json
```

| Preset | Item | Character |
| --- | --- | --- |
| Slate | `theme-slate` | Cool blue grays with an ink accent. Quiet and technical. |
| Cobalt | `theme-cobalt` | A clear blue for buttons and focus on a neutral ramp. |
| Lagoon | `theme-lagoon` | Teal accents on cool grays, with softer corners. |
| Forest | `theme-forest` | Sage grays and a deep green for primary actions. |
| Olive | `theme-olive` | Warm green grays with an ink accent. Editorial. |
| Sand | `theme-sand` | Paper warm grays and an amber accent on focus and progress. |
| Clay | `theme-clay` | Terracotta buttons on warm grays, round corners. |
| Plum | `theme-plum` | Mauve grays and a muted plum for the accent. |
| Contrast | `theme-contrast` | Darker secondary text, stronger hairlines and square corners. |

## Or paste variables

A theme is plain CSS. Two lines give the kit a brand color: the accent for focus, selection, links, switches and progress, and `--chatcn-primary` for solid buttons and the send button.

`globals.css`

```css
:root {
  --chatcn-accent: oklch(0.55 0.2 262);
  --chatcn-primary: var(--chatcn-accent);
}

.dark {
  --chatcn-accent: oklch(0.72 0.18 262);
}
```

The builder writes the full set for you, including a tinted gray ramp and dark values, and can also print shadcn variables so the rest of your shadcn components match.

## What a theme changes

| Variables | What follows them |
| --- | --- |
| `--chatcn-accent`, `--chatcn-accent-fg` | Focus rings, selection, links, active switches, progress fills |
| `--chatcn-primary`, `-fg`, `-hover` | Solid buttons and the send button. Ink by default |
| `--chatcn-gray-100` to `-1000` | Text, borders, fills and surfaces. A small tint gives slate, sage or sand grays |
| `--chatcn-bg`, `-surface`, `-card`, `-inset` | Canvas and raised surfaces |
| `--chatcn-radius-xs` to `-2xl` | Every corner, kept concentric |
| `--font-sans`, `--font-mono` | Components inherit your fonts |
| `--spacing` on a wrapper | Density: padding and control heights scale together |

## The neutral ramp

Ten steps from `--chatcn-gray-100` (subtle fill) to `--chatcn-gray-1000` (primary text), zero chroma in both themes. Readable text never goes lighter than `gray-800`. Light canvas is `oklch(1 0 0)`, dark canvas is `oklch(0.145 0 0)`, never pure black.

## Semantic tokens

| Token | Use |
| --- | --- |
| `--chatcn-fg` | Primary text |
| `--chatcn-fg-muted` | Secondary text and icons |
| `--chatcn-fg-subtle` | Tertiary text, placeholders, idle icons |
| `--chatcn-border` | Hairlines and dividers |
| `--chatcn-card` | Raised surfaces: white in light, a lighter gray in dark |
| `--chatcn-inset` | Code and output wells inside a card |
| `--chatcn-primary` | Solid buttons and the send button. Ink by default |
| `--chatcn-accent` | Focus rings, selection, links, active toggles, progress. Ink by default |

## Status colors

Red marks failures. It appears as a small icon or a short label, never as a fill, and always next to a word that says the same thing. Every other state is told apart by shape and weight. Themes leave status colors alone.

## Match your shadcn theme

Prefer your existing palette? Map the chatcn tokens onto shadcn variables after the theme import. To go the other way, copy the shadcn variables from the [theme builder](https://chatcn.dev/themes).

```css
:root {
  --chatcn-fg: var(--foreground);
  --chatcn-fg-muted: var(--muted-foreground);
  --chatcn-border: var(--border);
  --chatcn-card: var(--card);
  --chatcn-primary: var(--primary);
  --chatcn-primary-fg: var(--primary-foreground);
  --chatcn-accent: var(--ring);
}
```

More on accents, dark mode, density and pairing with NeonKit in [Theming in depth](https://chatcn.dev/docs/guides/theming-in-depth).

Source: https://chatcn.dev/docs/theming