# Playground

Model playground parts: parameters, system prompt, prompt templates, API key input, response compare, eval results, generation stats. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `eval-results`: **Eval results.** The results of an eval run: pass rate, average score, cost and duration against a baseline, and every case with its score, latency and pass or fail. Filter, sort, and expand a case for the full input, output and the grader's reasoning. Rows fill in while the run is going.
- `retrieved-chunks`: **Retrieved chunks.** What the retriever handed the model, for RAG debugging: each passage with its source and page, similarity as a bar and a figure, the query terms it matched, its token count and whether the answer used it. A cutoff grays out weak matches.
- `generation-stats`: **Generation stats.** How a response was generated: model, time to first token, tokens per second, input and output tokens, cost and finish reason. A quiet line under a message, an info popover, or a breakdown for dev panels, with a live mode that never shifts.
- `response-compare`: **Response compare.** Two to four model responses to the same prompt, side by side, like an arena or an A/B test. Columns stream in parallel with their own carets and stats, blind mode hides model names until the vote, scrolling can move together, and narrow screens stack into tabs.
- `api-key-input`: **API key input.** A bring-your-own-key field: masked as prefix and last four, a reveal toggle, paste cleanup, a format check per provider, an optional live check, a saved state and a confirmed remove. The key never reaches an attribute.
- `model-parameters`: **Model parameters.** Sampling controls for prompt playgrounds: temperature, top P, max output tokens, frequency and presence penalty and stop sequences, with presets, reset, help tooltips, typed values and a modified dot.
- `system-prompt-editor`: **System prompt editor.** A textarea editor for system prompts with `{{variable}}` highlighting, a live token count against a budget, optional line numbers, version history with restore, unsaved changes and Cmd/Ctrl+S to save.
- `prompt-template`: **Prompt template.** Fill a prompt template's variables: `{{name}}` and `{{name:default}}` become text, multiline and select fields, with a live preview, required validation, copy and Run.
