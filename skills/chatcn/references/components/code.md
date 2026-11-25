# Code

Coding agent pieces: diff viewer, changed files, file tree, terminal, test results, sandbox, stack traces, commits, pull requests, deploys. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `diff-viewer`: **Diff viewer.** Review an agent's code changes: unified or split, word-level highlights, collapsed unchanged lines, per-hunk accept and reject, streaming patches and a guard for very large files. Red and green by default, with a gray tone. Also called: code diff, git diff, compare code.
- `changed-files`: **Changed files.** The files an agent changed, with status letters, dimmed directories, +/- counts and a five-cell bar. Selecting a file opens its diff.
- `commit-card`: **Commit card.** A commit or pull request the agent made. The message streams in while drafting, then the short sha, branch, files changed, link and push land in place.
- `file-tree`: **File tree.** The files an agent touched, as a real WAI-ARIA tree: keyboard navigation with typeahead, change markers, churn counts, indentation guides and virtualization for large repositories. Also called: file explorer, directory tree.
- `terminal`: **Terminal.** Streaming command output with ANSI colors in the kit palette, a command header, exit code and duration, copy, clear, wrap and follow toggles, and an optional input line. Also called: shell, console, command line.
- `test-results`: **Test results.** A test run as the agent sees it: counts that double as filters, progress while running, failures that open to the error, diff and stack, and rerun.
- `sandbox`: **Sandbox.** The machine an agent works in: status, CPU and memory, open ports with links, a logs drawer and a files shortcut.
- `preview-toolbar`: **Preview toolbar.** A floating toolbar over a live preview for pointing at what to change: select an element, edit text, draw or comment, with single-key shortcuts and a selection outline.
- `stack-trace`: **Stack trace.** An error stack that leads with your code: app frames in front, dependency and runtime frames folded by package, and file and line links into your editor.
- `environment-variables`: **Environment variables.** Environment variables an agent needs or has set: masked values with reveal and copy, copy as .env, and a warning that says which required keys are missing and where to add them.
- `package-info`: **Package info.** A package an agent added, upgraded or removed: the version change with what kind of change it is, the dependencies it touched, and the install state.
- `schema-display`: **Schema display.** An API endpoint or a tool's input, readable: method and path, then parameters and bodies as a folding typed tree.
- `pull-request-card`: **Pull request card.** A pull request an agent opened, with its merge box: status, branches, author, change totals with the five-cell bar, checks with failures first, review state, and a Merge button gated the way the host gates it, with the reason in words when it is blocked.
- `deploy-status`: **Deploy status.** A deployment the agent started: each step with its duration, a live log tail for the running step, the URL once it is ready, and Cancel, Redeploy or a rollback confirmed in place. Includes a one-line variant for chat.

## chatcn Pro

- `findings-report` (Pro): **Findings report.** Bug and security findings with severity, file and line, a repro, and fix or dismiss actions.
- `agent-commits` (Pro): **Agent commits.** Commits an agent made in a session, with files, line counts and a revert per commit.
- `request-inspector` (Pro): **Request inspector.** An HTTP request and response with headers, bodies, a timing waterfall and copy as cURL.
- `ci-checks` (Pro): **CI checks.** The checks on a commit, failures first, each against how long it usually takes. Rows open to annotations and the live log, and a failure turns Ask agent to fix into the agent's fix attempt in place.
- `review-comment` (Pro): **Review comment.** One review comment from an agent, anchored to its lines: the code around them, a bracket in the severity's hue, the rationale and a suggested fix in place. Apply, dismiss with a reason, or discuss.
- `session-cost-footer` (Pro): **Session cost footer.** The status bar under a coding session: model, tokens in and out, cost and time, all live. A hairline on the top edge fills toward the budget; hover the numbers for the breakdown.
- `sandbox-meters` (Pro): **Sandbox meters.** CPU, memory, disk and network for the agent's sandbox as live sparklines against their limits. Near a limit a meter turns amber, then red, and a warning says what will break and offers to raise it.
- `error-fix-card` (Pro): **Error fix card.** A build or runtime error with the agent's diagnosis and a one click fix. The fix runs its steps in place with a live clock, then shows the line it replaced, the proof it worked and Undo.
- `environment-picker` (Pro): **Environment picker.** Where the agent runs: this machine, a new worktree, a cloud sandbox or an SSH host, each with its machine and what an hour costs. Cloud grows a size control in place and the session estimate rolls as you choose.
- `worktree-switcher` (Pro): **Worktree switcher.** The worktree and branch the agent works in, with uncommitted changes and drift from main. The list filters as you type, and the highlighted worktree previews what Apply to main would bring, conflicts included.
- `agents-window` (Pro): **Agents window.** Every coding agent you run, wherever it runs: a sidebar grouped by this machine, cloud sandboxes and SSH hosts, each agent on its own worktree, and the work as tabs or a grid.
- `best-of-n` (Pro): **Best of n.** Several attempts at one task side by side, from different models: tests, diff size, cost and time on aligned rows with the best of each marked, the same file's diff in every column, and one Apply.
- `pr-review` (Pro): **Pull request review.** The full review of a pull request: summary and risk, every comment by file with its severity, the lines it points at and a red and green suggestion, and Fix all to apply them in one commit.
- `inline-hunk-review` (Pro): **Inline hunk review.** Accept or reject an agent's edit hunk by hunk inside the file it changed. Y accepts, N rejects and both move on, J and K step between hunks, U undoes.
- `repo-map` (Pro): **Repo map.** The repository as a treemap by lines of code or by churn, with every file the agent changed outlined and lettered A, M, D or R, and files it only read dashed.
- `git-graph` (Pro): **Git graph.** Commit history with its graph: one lane per branch in a steady color, curved merges, the checked out commit ringed, and agent commits drawn as squares with an Agent label.
- `merge-conflict` (Pro): **Merge conflict.** Merge conflicts one decision at a time: ours and theirs side by side with the differing lines marked, the agent's merged version with its reasoning, and Keep ours, Keep theirs, Keep both, Use merge or Edit by hand.
- `task-composer` (Pro): **Task composer.** Where a coding task starts: what to do, which repository and branch, where it runs (cloud, this machine or SSH), which model and how many attempts, then Ask or Code.
- `cli-agent-replica` (Pro): **Terminal agent session.** A terminal coding agent session drawn in HTML for docs and launch videos: the prompt, tool lines with results under an elbow, inline diffs, the plan as a checklist, approval prompts and the turning star status line.
- `next-edit-ghost` (Pro): **Next edit.** The model's next edit as a ghost in the editor: a multi line completion after the cursor, or a change anywhere in the file with a jump marker. Tab jumps, Tab again accepts.
