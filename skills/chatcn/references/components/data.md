# Data

Data answers: notebook cells, SQL results, data tables, and Pro charts (sankey, heatmap, funnel, forecast, pivot, AI spreadsheet). Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## Free

- `notebook-cell`: **Notebook cell.** A Jupyter style cell a data agent runs: execution count, highlighted code, a live timer, and nbformat outputs (streams, results, DataFrames, charts and tracebacks), with code and output that collapse on their own and a Notebook layout that stacks cells.
- `sql-result`: **SQL result.** A query the agent ran and what came back: highlighted SQL, row count and run time, a result table with a sticky header, NULL badges, full values for long cells, paging, CSV export and the running, empty, error and canceled states.
- `data-table`: **Data table.** A table the model generates: typed columns that format currency, percents, dates and status, sorting, column resize, a sticky first column, rows that stream in without reflow, selection, density and virtualization for thousands of rows. Also called: data grid.

## chatcn Pro

- `sankey-chart` (Pro): **Sankey chart.** Where things flow, step by step: ribbons blend from one step's color to the next, and pointing at a step lights every flow through it with dots traveling the way things move. Also called: flow diagram, alluvial chart.
- `heatmap-chart` (Pro): **Heatmap chart.** Two categories against each other with the amount as shade: requests by weekday and hour, eval scores by model and task. Also called: activity grid, contribution graph, calendar heatmap.
- `treemap-chart` (Pro): **Treemap chart.** Sizes as area, grouped: spend by team and feature, storage by project. Rounded, gapped tiles saturate when pointed at, and a group grows to fill the chart when opened. Also called: hierarchy chart.
- `cohort-table` (Pro): **Cohort table.** Retention by cohort as a shaded triangle, a weighted average, and the curve of the cohort you point at drawn against the average.
- `funnel-chart` (Pro): **Funnel chart.** A conversion funnel that says where people stop: one smooth shape that narrows step by step, the drop on a chip at every seam, the biggest drop called out and last period as a ghost. Also called: conversion funnel.
- `candlestick-chart` (Pro): **Candlestick chart.** Prices for a finance answer: rounded candles in soft up and down tones, volume as tints, a crosshair with a tooltip card, events on their day, and line or OHLC views. Also called: stock chart, ohlc chart, trading chart.
- `histogram-chart` (Pro): **Histogram chart.** A distribution that answers how many and how bad the tail is: round bins with a width slider, percentile lines and a target with the share past it.
- `box-plot` (Pro): **Box plot.** Several distributions on one axis, a row each: the middle half, the median, whiskers and outliers, with every point a click away.
- `ai-spreadsheet` (Pro): **AI spreadsheet.** A sheet where AI columns fill row by row as results stream in, with a fill rail per column, per row progress and errors, retry for one row or every failed row, and arrow key navigation.
- `analysis-notebook` (Pro): **Analysis notebook.** Analysis as question, code, output and note cells on one spine. Cells run in order, turn stale when a source gets new data, rerun in one action and collapse their code.
- `nl-to-sql` (Pro): **Question to SQL.** A question turned into SQL you can read, edit and run, with table chips that light up where the query uses them, edit tracking with revert, errors that underline the token and offer the fix, and a result grid.
- `column-profile` (Pro): **Column profile.** Every column of a dataset at a glance: inferred type, a histogram with outlier bins or the top values, nulls, unique values and outliers, with a convert action for text that parses as a better type.
- `pivot-table` (Pro): **Pivot table.** Drag fields into rows, columns and values, with subtotals, grand totals and value tinted cells. Every drag has a keyboard twin.
- `chart-spec-editor` (Pro): **Chart spec editor.** A chart with its spec in the open (type, x, y, aggregate and color by) and an ask field: plain requests come back as a new spec and the chart morphs into it, with what changed and Undo.
- `insight-card` (Pro): **Insight card.** One finding from a data agent: the sentence, a chart of the shift with both levels named, the numbers behind it, a confidence label with its reason and the query one click away.
- `chart-annotation` (Pro): **Chart annotation.** Anomaly, event and note callouts pinned to points, with labels placed so none overlap each other or the line. A ready line chart, or a layer over any chart.
- `forecast-chart` (Pro): **Forecast chart.** History as a smooth line over a soft gradient and the forecast inside layered 80% and 95% bands that fade further out, split by a Today pill, with the horizon total as the headline and a crosshair tooltip. Also called: prediction chart, projection.
