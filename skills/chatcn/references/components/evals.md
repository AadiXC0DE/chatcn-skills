# Evals

Evals and prompt work: results tables, leaderboards, judge rubrics, datasets, review queues, pairwise votes, prompt playground, versions and diffs. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `confusion-matrix` (Pro): **Confusion matrix.** A classification eval matrix with counts on one sequential tint, row and column totals, recall and precision, and a click to drill into the cases behind any cell.
- `calibration-chart` (Pro): **Calibration chart.** A reliability diagram: predicted confidence against accuracy in bins, the diagonal, cases per bin and an expected calibration error readout.
- `injection-warning` (Pro): **Injection warning.** Marks content from a page, file, email or tool result that tried to instruct the agent, shows the injected text in place and what the agent ignored.
- `leaderboard` (Pro): **Leaderboard.** Ranked models with confidence intervals drawn as whiskers on one axis, honest shared ranks, a task filter and rank changes since the last run.
- `tool-schema-builder` (Pro): **Tool schema builder.** A function or tool definition builder: a parameter table with name, type, required, description and allowed values, and the generated JSON schema live beside it.
- `red-team-panel` (Pro): **Red team panel.** Attack categories with pass and fail counts and severity, the failures behind each, and the transcript behind each failure with the turn that gave way marked.
- `prompt-lint` (Pro): **Prompt lint.** A prompt editor with inline warnings: conflicting rules, vague words, a missing output format and shouting, with squiggles, a gutter, hover explanations and one click fixes.
- `eval-results-table` (Pro): **Eval results table.** A full experiment: a column per scorer, baseline deltas, regressions first, rows that open in place.
- `score-delta` (Pro): **Score delta.** A score and its change against a baseline: inline, as a stat tile with run history, or as two runs compared metric by metric.
- `judge-rubric-editor` (Pro): **Judge rubric editor.** An LLM judge rubric with weighted criteria, a scale, and a test on a sample.
- `dataset-table` (Pro): **Dataset table.** An eval dataset edited in place, with tags, splits and import.
- `review-queue` (Pro): **Review queue.** A human labeling queue with keyboard shortcuts, skip, flag and progress.
- `pairwise-vote` (Pro): **Pairwise vote.** A versus B with tie and both bad, keys 1 to 4, blind by default.
- `experiment-summary` (Pro): **Experiment summary.** Aggregate scores, improvements, regressions and cost for one experiment.
- `expected-vs-actual` (Pro): **Expected vs actual.** Expected and actual output compared field by field.
- `eval-run-progress` (Pro): **Eval run progress.** A live pass and fail tally while an eval runs, as a square per case, one stacked bar, or a ring per suite.
- `span-annotator` (Pro): **Span annotator.** Select spans in an output and tag them.
- `prompt-playground` (Pro): **Prompt playground.** System prompt, messages, variables, tools and sampling on one screen, with Run streaming the reply, Stop, and Save as version.
- `prompt-variables` (Pro): **Prompt variables.** `{{variable}}` highlighting in a prompt template, a test value per variable, warnings for missing values and a preview of the filled prompt.
- `model-compare` (Pro): **Model compare.** One prompt across any number of models: latency, time to first token, output tokens and cost per column, measured against a baseline, with answers that scroll together.
- `prompt-versions` (Pro): **Prompt versions.** Every saved version of a prompt with author, note and environment labels, a word diff against the version before or against production, and promotion with undo.
- `prompt-diff` (Pro): **Prompt diff.** A word level diff of two prompts that keeps `{{variables}}` whole, lists variables added and removed, and folds long unchanged stretches.
- `schema-builder` (Pro): **Schema builder.** A JSON Schema builder for structured output: named fields, lists, nested objects and allowed values, with a live example, the schema, and a check for real responses.
- `tokenizer-view` (Pro): **Tokenizer view.** Text split into tokens with every boundary drawn, ids on demand, and counts per tokenizer side by side.
- `logprob-view` (Pro): **Logprob view.** A reply with every token shaded by its probability, and the alternatives the model nearly chose on hover or focus.
- `sampling-explainer` (Pro): **Sampling explainer.** Live probability bars for the next token that reshape as temperature and top P change, with the top P cut marked and real samples drawn from the shape.
- `context-window-map` (Pro): **Context window map.** What fills a model's context window as one stacked bar and a table: system prompt, tools, history, files, the reply's reserve and what is free, with drill in.
