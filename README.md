# chatcn skills

An agent skill for [chatcn](https://chatcn.dev), the shadcn registry of 750+ components for AI products: chat, agents, tool calls and approvals, voice, generative UI, evals and observability.

With the skill installed, Claude Code, Cursor, Codex, GitHub Copilot and other coding agents know which chatcn component fits a job, how to install it with the shadcn CLI and how to wire it to AI SDK or any other backend.

```bash
npx skills add AadiXC0DE/chatcn-skills
```

Then ask your agent for the UI, for example "build a support chat with tool approvals" or "add a voice agent screen".

## What is inside

- `skills/chatcn/SKILL.md`: the workflow, starting points, design rules and how chatcn Pro works.
- `skills/chatcn/references/components/`: every component by group, with its install name.
- `skills/chatcn/references/docs/`: installation, theming, the data contract and the main guides.

The skill holds names, descriptions and setup only, no component source. It is generated from the chatcn docs, so it changes when they do. Update it with `npx skills update`.

## License

You may install, copy and share this skill. chatcn itself is free to use but not open source; see the [chatcn license](https://chatcn.dev/docs/license).
