# Safety

Trust and safety: why card, stop all, undo window, access scope, PII chip, refusal message, risk badge, report dialog. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `why-card` (Pro): **Why card.** Why the agent did that: the instruction, the evidence and the rule, a click from the action.
- `stop-all` (Pro): **Stop all.** Emergency stop for every running agent, with a confirm and a receipt of what stopped and what was rolled back.
- `undo-window` (Pro): **Undo window.** Undo an agent action within a short window, with a visible countdown that pauses on hover.
- `access-scope` (Pro): **Access scope.** What the agent can reach right now in one line, expandable to a list with revoke.
- `pii-chip` (Pro): **PII chip.** Detected personal data inline with redact and keep, and a summary with Redact all.
- `refusal-message` (Pro): **Refusal message.** A refusal that says what it cannot do, why in one line, and offers the closest safe alternative.
- `ai-label` (Pro): **AI label.** AI generated and AI assisted labels with a details popover, and a who wrote what view that marks the model's sentences in the text.
- `content-gate` (Pro): **Content gate.** Sensitive content gate with the reason and a choice to view, blurred until chosen.
- `report-dialog` (Pro): **Report dialog.** Report a response with categories, the excerpt selected and an optional note.
- `risk-badge` (Pro): **Risk badge.** Low, medium and high risk for agent actions: a badge with a shape per level, a meter with the factors, and an approval gate where high risk takes a press and hold.
