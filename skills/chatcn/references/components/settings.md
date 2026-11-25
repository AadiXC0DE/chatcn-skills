# Settings

Settings for AI apps: memory, custom instructions, connectors, knowledge base, usage and cost, model status, sharing, and Pro billing and API keys. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `settings-panel`: **Settings panel.** The settings layout for an AI app: a sections nav and panes, with groups, rows, switches and segmented controls. The nav moves above the pane when the panel is narrow. Also called: preferences.
- `memory-chip`: **Memory chip.** The quiet line under an assistant turn that says memory changed, with View to read exactly what was saved and Undo to take it back.
- `memory-manager`: **Memory manager.** Everything the assistant remembers, searchable and editable in place. Delete hides a memory at once and offers Undo for 5 seconds before it is really gone.
- `temporary-chat`: **Temporary chat.** A header toggle for chats that stay out of history and memory, and the banner that says plainly what that means.
- `custom-instructions`: **Custom instructions.** The personalization editor: a response style with a sample answer, what the assistant should know about you, and how it should respond, with live character counts.
- `connectors`: **Connectors.** A connector directory with connect and disconnect states and per-tool permissions: Allow, Ask or Deny for every tool a connector exposes.
- `knowledge-base`: **Knowledge base.** Project files the assistant reads in every chat, each with its indexing state: queued, indexing with progress, ready with the tokens it adds, or failed with the reason and Retry.
- `usage-meter`: **Usage meter.** Plan usage with tabular numbers and live reset times: one bar per limit, a warning line, a Limit reached state and an upgrade slot. Also called: usage, quota, credits.
- `rate-limit-banner`: **Rate limit banner.** Docks above the composer when a limit is near or reached: how many are left and until when, then a live countdown and a model that still has room. Also called: rate limit, quota exceeded.
- `cost-display`: **Cost display.** What a message or an agent run cost, in tabular figures, with the breakdown one click away: input, cached input, output and tool calls, each with tokens and cost.
- `model-status`: **Model status.** Degraded, outage or maintenance notice for a model or provider, with when it started, a link to the status page and a switch to a model that works.
- `share-dialog`: **Share dialog.** Share a chat as a snapshot: who can open it, the link with Copy link, a note that later messages stay private, Update link, and export as Markdown or PDF. Also called: share link.
- `safety-notice`: **Safety notice.** Refusal and warning messaging with a calm, non-judgmental tone and a next step every time: refusals, warnings that need one decision, covered sensitive content and the disclaimer line.
- `tool-memory`: **Tool memory.** Tool renderer for memory saved, updated or forgotten, built on Tool call, with the exact text so people can see what the assistant now knows.

## chatcn Pro

- `agent-permissions-matrix` (Pro): **Agent permissions matrix.** What each agent may do with each tool, as one grid: allow, ask or deny per cell, set by row, column or brush.
- `api-keys` (Pro): **API keys.** A workspace's keys with scopes, who made them, last use and expiry; create, rotate with a grace period, and revoke.
- `key-reveal-once` (Pro): **Key reveal once.** A new secret, shown once, with copy, a .env line and a check before it is closed uncopied.
- `billing-overview` (Pro): **Billing overview.** Plan, next invoice, usage this period and the card it goes to, on one page, with nothing in the total left to guess.
- `invoice-table` (Pro): **Invoice table.** Every invoice with status, amount and a PDF, the amount owed in the header, and Pay on what is still due.
- `usage-breakdown` (Pro): **Usage breakdown.** Who and what is driving usage and what changed: ranked by member, model or feature, compared with the period before, and drillable.
- `seat-manager` (Pro): **Seat manager.** Members, roles and seats, with invites that catch typos and state the cost of extra seats before anything is sent.
- `spend-limits` (Pro): **Spend limits.** Caps per member and per agent: spend against each, the day it gets there, and what happens at the limit.
- `model-policy` (Pro): **Model policy.** Which models a workspace may use, by provider, with each provider's data terms and the defaults per task kept in step.
- `default-models` (Pro): **Default models.** The model each kind of work starts on, limited to what the task can use and the workspace allows.
- `audit-log` (Pro): **Audit log.** Who did what, in sentences, with agents and keys told apart from people, the changes behind each event, and export.
- `status-page` (Pro): **Status page.** Provider and model health for an AI product: a plain headline, 90 days of daily bars and uptime per model, and incidents as timelines.
