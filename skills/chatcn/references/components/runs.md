# Runs

Running agents: approval modes and inbox, permission mode, background runs, run inbox, notifications, takeover, computer view. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `computer-view`: **Computer view.** A live view of the agent's screen: a cursor that glides to each action, a label for what it is doing, take over and hand back, and a replay scrubber with a timeline and step thumbnails.
- `approval-mode`: **Approval mode.** Manual, Auto or Skip, each with one sentence that says what the agent will do without you, a list of saved grants per site and per tool, and calm notices for actions that stay blocked in every mode. Also called: auto approve.
- `approval-inbox`: **Approval inbox.** Every pending approval across runs in one list. Approve or deny in a batch, filter by run or tool, and expand any row to read the reason and the exact tool input. Also called: human in the loop, approvals.
- `questionnaire`: **Questionnaire.** Clarifying questions from the agent, one at a time: single choice, multiple choice with Other, and free text, with Skip, a stepper and a summary before sending.
- `permission-mode`: **Permission mode.** A compact selector for the composer: Ask before edits, Edit automatically or Plan only, shown as an icon and a short label.
- `background-run`: **Background run.** A card for a detached agent task: what it is, where it runs, the latest step, elapsed time, a 2 px progress line and Open or Cancel.
- `run-inbox`: **Run inbox.** Background runs in one list, with a Needs input filter and static unread dots. Arrow keys move through the rows.
- `agent-notification`: **Agent notification.** Toasts for needs your input, done and failed that stack, fan out on hover and swipe away, plus a hook for desktop notifications while the tab is hidden.
- `takeover-banner`: **Takeover banner.** The agent is controlling the browser, with Take over, Pause and Stop, and the reverse: You are in control, with Hand back.
- `agent-lanes`: **Agent lanes.** Parallel agents side by side, each with its status, current step and streaming output. Compare lines up their results; Use this one picks the winner.
