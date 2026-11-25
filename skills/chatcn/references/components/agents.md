# Agents

Tool calls with approvals and a renderer per tool (web search, files, shell, code, MCP, browser), reasoning, traces, run status, sources and citations. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `tool-call`: **Tool call.** Shows an agent tool call through its whole life: streaming input, approval, running, output, failure, denial and cancellation. Also called: function call, function calling, tool use, tool invocation.
- `trace`: **Trace.** One line primitive for every agent step on a vertical rail: status glyph, label, mono detail and duration, with ten states and expandable details.
- `trace-group`: **Trace group.** Folds consecutive steps into one line, Read 6 files, with a live line that shows what the agent is doing right now.
- `reasoning`: **Reasoning.** Model reasoning behind one quiet line: Thinking with a live timer while it streams, then Thought for 12 s. Collapsed by default, never closed on a timer. Also called: chain of thought, thinking, thoughts, reasoning trace.
- `step-timer`: **Step timer.** Elapsed and final duration for an agent step, in tabular figures that tick once per second.
- `run-status`: **Run status.** The state of a whole agent run for a header or thread row: idle, running, waiting for input, done, failed or stopped, with elapsed time.
- `sources`: **Sources.** The sources behind an answer: a stack of letter tiles and a count, expanding to a numbered list that matches the citations. Also called: citations, references, search sources.
- `citation`: **Citation.** An inline numbered source with a hover card: title, site, the supporting passage highlighted, open and copy link. Also called: footnote, inline citation, source link.
- `tool-web-search`: **Web search tool.** A web search tool call: the query and result count in the header, results as a quiet list with letter tiles, titles, domains and snippets.
- `tool-web-fetch`: **Web fetch tool.** A page fetch: the address, the page title and an excerpt of what the agent read.
- `tool-file-read`: **File read tool.** A file read: path and line range in the header, a numbered preview of what the agent saw.
- `tool-file-edit`: **File edit tool.** A file edit: path and +12 -3 in the header, a unified mini diff that reads without color. During approval, the diff is what the user approves.
- `tool-file-write`: **File write tool.** A new file: the path in the header, then a file card with its name, size and first lines.
- `tool-search-code`: **Code search tool.** A grep or glob: the pattern and match count in the header, matches grouped by file with file:line and the match highlighted.
- `tool-bash`: **Shell tool.** A shell command: a monochrome terminal that streams output and stays pinned to the bottom, the exit code, and Stop while it runs.
- `tool-code-exec`: **Code execution tool.** Code run in a sandbox: the code with line numbers, then output, errors and the result.
- `tool-mcp`: **MCP tool.** A call to a tool on an MCP server or connector: the server with its mark, the tool name, input and output, with approval.
- `tool-fallback`: **Tool fallback.** The renderer for tools nobody wrote a renderer for: summary first, JSON one click away. Also home to the renderer map that ties tool names to renderers.
- `tool-browser`: **Browser tool.** A browser agent at work: the steps it takes (open, click, type, scroll) with the running one live, and a screenshot thumbnail with the cursor where it last acted.

## chatcn Pro

- `session-state-badge` (Pro): **Session state badge.** The six agent session states as a badge, a ring around an avatar, a fleet summary and a session history.
- `agent-heartbeat` (Pro): **Agent heartbeat.** Last activity that ticks once a second, and a live trace of every event, so a slow agent never looks stuck and a stuck one never looks busy.
- `reasoning-budget-bar` (Pro): **Reasoning budget bar.** Reasoning tokens against the effort budget as a bar or a ring, with an effort picker that sets the budget.
- `tool-registry` (Pro): **Tool registry.** Every tool an agent can call, with its schema, call count, error rate and latency, and a switch per tool.
- `mcp-server-manager` (Pro): **MCP server manager.** Connected MCP servers with transport, sign in and connection state in words, tool lists, latency and the one action each state needs.
- `memory-inspector` (Pro): **Memory inspector.** The developer view of agent memory: source, author, last use and use count per entry, with undoable deletes.
- `agent-schedule` (Pro): **Agent schedule.** When an agent runs on its own: plain words or cron, a time zone, and the next five runs in that zone.
- `agent-hierarchy` (Pro): **Agent hierarchy.** An orchestrator and its subagents as a live tree, with the reason for each handoff on its edge.
- `agent-kanban` (Pro): **Agent kanban.** Issues delegated to agents, by state. People stay the owner; agents show as contributors with live state.
- `agent-config-editor` (Pro): **Agent config editor.** System prompt, model, tools and parameters with versions, a word diff against production, and publish.
- `agent-fleet` (Pro): **Agent fleet.** Every running agent across local, worktree, cloud and remote machines as live cards. Waiting agents first.
- `multi-model-race` (Pro): **Multi model race.** Parallel lanes for models answering the same prompt: tokens, time and first token per lane, and a finish marker with the place.
