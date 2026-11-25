# Observability

LLM observability: trace waterfall, span detail, run replay and diff, cost explorer, token and latency charts, log tail, error groups. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `trigger-builder` (Pro): **Trigger builder.** A when this happens, run this agent builder: the event, filters on its payload, the agent and its input, with a test event that shows what would run.
- `cost-explorer` (Pro): **Cost explorer.** Spend by model, user or feature over days, with its change and a breakdown table.
- `token-breakdown-chart` (Pro): **Token breakdown chart.** Input, cached, output and reasoning tokens per day or request, or one context window.
- `latency-histogram` (Pro): **Latency histogram.** The latency distribution with p50, p90 and p99, a target zone and slow request drill down.
- `model-routing-flow` (Pro): **Model routing flow.** Requests from features to models to outcomes, as ribbons that blend from step to step, with failures in red and every path traceable.
- `uptime-strip` (Pro): **Uptime strip.** A 90 day status strip with day cards, incidents and a compact row.
- `budget-guard` (Pro): **Budget guard.** A spend cap with a projected run out date and pause behavior.
- `graph-state-viewer` (Pro): **Graph state viewer.** A state graph with the run drawn on it, and the state object.
- `checkpoint-travel` (Pro): **Checkpoint travel.** Time travel over saved graph checkpoints, fork from any checkpoint.
- `traces-to-dataset` (Pro): **Traces to dataset.** Select traces and add them to an eval dataset with field mapping.
- `trace-waterfall` (Pro): **Trace waterfall.** Spans of an agent run on one time axis, with nesting, duration, token and cost columns, collapse by depth and keyboard tree navigation.
- `span-detail` (Pro): **Span detail.** One span in full: input, output, metadata, events and scores in tabs, readable and JSON views, and copy as cURL.
- `trace-graph` (Pro): **Trace graph.** An agent run as a graph: aggregated mode merges same named steps with a count, expanded mode shows every step, and the current step is marked.
- `run-scrubber` (Pro): **Run scrubber.** A timeline over an agent run with ticks for tool calls, approvals and errors, a playhead that snaps to them, and keyboard seeking.
- `run-replay` (Pro): **Run replay.** Replay a finished agent run step by step with a scrubber, play at 1x to 8x and jump to tool calls.
- `run-diff` (Pro): **Run diff.** Two runs of the same task side by side, with step alignment, changed outputs and time, token and cost deltas.
- `log-tail` (Pro): **Log tail.** A live log stream with level filters, search, pause on scroll and jump to live.
- `error-groups` (Pro): **Error groups.** Agent errors grouped by signature, with counts, a 24 hour trend, first and last seen, sample traces and the stack.
- `guardrail-log` (Pro): **Guardrail log.** Blocked, modified or flagged text with the rule, the excerpt with the catch marked, and an override that needs a reason and leaves an audit line.
