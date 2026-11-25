# Knowledge

RAG and knowledge bases: hybrid search, ingestion, chunk inspector, retrieval debugger, embedding map, knowledge graph, PDF viewer with cited spans. Install a free item with `npx shadcn@latest add @chatcn/<name>` and a Pro item with `npx shadcn@latest add @chatcn-pro/<name>`. Full docs for any item: `https://chatcn.dev/docs/components/<name>.md`.

## chatcn Pro

- `hybrid-search-box` (Pro): **Hybrid search box.** Search with keyword, semantic and hybrid modes, a weight slider that reranks live and scores that explain themselves.
- `entity-card` (Pro): **Entity card.** One entity at a glance: mentions over time, the documents that cite it most and what it connects to.
- `crawl-progress` (Pro): **Crawl progress.** A website crawl as a radial tree: one ring per depth of links, live counts and a log that says why pages were skipped.
- `study-tools` (Pro): **Study tools.** Flashcards, a quiz and a study guide outline made from the sources a person selected.
- `file-library` (Pro): **File library.** The files behind a knowledge base: type, size, index state and how often chats cite them.
- `corpus-manager` (Pro): **Corpus manager.** Knowledge collections with access groups, size, document count and how fresh each index is.
- `source-sync-grid` (Pro): **Source sync grid.** Connected knowledge sources as cards: items indexed, last sync, live progress and failures with a resync.
- `knowledge-graph` (Pro): **Knowledge graph.** Entities and relations laid out once, deterministically, then still, with search and focus.
- `grounding-meter` (Pro): **Grounding meter.** How much of an answer its sources back, sentence by sentence, with the answer itself marked to match.
- `unsupported-claim` (Pro): **Unsupported claim.** A dotted underline on a claim no source backs, with a note that says why.
- `query-rewrite` (Pro): **Query rewrite.** The question as asked and the narrower searches the agent ran to answer it.
- `notebook-sources` (Pro): **Notebook sources.** The sources a notebook chat answers from, with select all and per source toggles.
- `mind-map` (Pro): **Mind map.** A mind map generated from sources, with branches that open and topics you can ask about.
- `ingestion-pipeline` (Pro): **Ingestion pipeline.** Files on their way into a vector index: upload, parse, chunk, embed and index as live steps with stage totals, per file tracks and retry from the stage that failed.
- `chunk-inspector` (Pro): **Chunk inspector.** A document as the retriever sees it: chunk boundaries overlaid, overlap shaded, token count per chunk and the nearest vectors of the chunk you select.
- `chunking-config` (Pro): **Chunking config.** Strategy, chunk size and overlap with a live preview on a sample document, the chunk sizes as bars against the target and the trade-offs in words.
- `embedding-map` (Pro): **Embedding map.** A 2D projection of chunks with clusters, the query as a point and lines to the neighbors it retrieved.
- `retrieval-debugger` (Pro): **Retrieval debugger.** Query, rewritten queries, retrieved chunks with scores and the reranked order, with a line from each chunk's first place to its new one.
- `pdf-viewer` (Pro): **PDF viewer.** Thumbnails, page jump, zoom, find in document, highlights and a toolbar on selected text to ask about a passage.
- `cited-span-pdf` (Pro): **Cited span PDF.** An answer beside the PDF it cites, with each citation jumping to its exact passage and each passage finding its sentence.
