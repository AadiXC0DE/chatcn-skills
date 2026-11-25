# Installation

Add chatcn components to a React project that uses Tailwind CSS v4 and the shadcn CLI.

## Requirements

- React 19 and Tailwind CSS v4.
- A project initialized with the shadcn CLI. If you have not done that yet, run `npx shadcn@latest init`.

## Add a component

Every component installs from its own URL. The CLI copies the source into `components/ui/chatcn/`, adds the theme tokens to your CSS and installs the few dependencies it needs.

```bash
npx shadcn@latest add https://chatcn.dev/r/tool-call.json
```

## Use the namespace

Register chatcn once and install by name. One command adds it to `components.json`; the `{style}` placeholder lets the registry serve the Base UI or Radix version that matches your project.

```bash
npx shadcn@latest registry add "@chatcn=https://chatcn.dev/r/{style}/{name}.json"
```

```bash
npx shadcn@latest add @chatcn/tool-call
```

Or add the entry by hand. Either way, `npx shadcn@latest search @chatcn -q voice` finds components by name, and the shadcn MCP server can browse them too.

`components.json`

```json
{
  "registries": {
    "@chatcn": "https://chatcn.dev/r/{style}/{name}.json"
  }
}
```

[chatcn Pro](https://chatcn.dev/pro) items install the same way from a second registry, `@chatcn-pro`, with a license token. [Pro setup](https://chatcn.dev/docs/chatcn-pro) covers the token and the `components.json` entry.

Building with a coding agent? Install the [chatcn skill](https://chatcn.dev/docs/agents) and it picks, installs and wires components for you.

## Theme

Components depend on the `chatcn-theme` item, which the CLI installs automatically. Its variables are namespaced `--chatcn-*`, so they never overwrite your shadcn theme. Dark mode follows the `.dark` class, the same as shadcn. See [Theming](https://chatcn.dev/docs/theming) to change the accent or map chatcn onto your own palette.

## Fonts

Components inherit your `font-sans` and `font-mono`. These docs are set in Familjen Grotesk and Reddit Mono; any grotesk with a tall x-height suits the type scale, Geist included (`npm i geist`).

Source: https://chatcn.dev/docs/installation