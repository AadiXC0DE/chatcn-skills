# Planning

Plans, todo lists, tasks, subagents, handoffs, queued messages, context meter, workflows. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `plan`: **Plan.** The agent's proposed plan, from the first streamed step to the last one done: approve, edit or reject it before anything runs.
- `todo-list`: **Todo list.** The agent's checklist with a live 3 of 7 count, a hairline progress rail and a check that draws itself when a todo finishes. Also called: checklist, task list.
- `task`: **Task.** A single task row: status, title, mono detail, a live timer that becomes a duration, and details on demand.
- `subagent`: **Subagent.** A subagent folded to one line that says what it is doing right now. Expand it for its own trace on a rail and its result.
- `handoff`: **Handoff.** The marker between two agents in a transcript, with the reason in plain words so nobody wonders why the voice changed.
- `queued-messages`: **Queued messages.** Messages typed while the agent works, in a visible queue: send after this run or steer now, edit in place, reorder, remove with undo.
- `context-meter`: **Context meter.** How full the context window is, as a ring or a bar, with a breakdown on click and a warning before compaction. Also called: context window, token usage, token counter.
- `agent-card`: **Agent card.** Who an agent is: name, what it does, the model behind it, the tools it may call and what it is doing now.
- `workflow`: **Workflow.** A node graph of an agent workflow with live status, rounded SVG edges and keyboard-focusable nodes. No dependencies.
