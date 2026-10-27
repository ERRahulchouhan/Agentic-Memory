# LlamaIndex: beginner-to-production memory and RAG guide

The [experiment notebook](./experiment.ipynb) indexes memory documents and retrieves nodes. Its mock embedder is only for API exploration; it does not produce meaningful semantic embeddings.

## 1. Beginner: core concepts

LlamaIndex represents source content as documents/nodes, transforms and indexes them, then retrieves relevant nodes at query time. For memory, treat each memory as a small, scoped document with useful metadata such as owner, type, creation time, and source.

Basic RAG loop: ingest → normalize/split → embed → index → retrieve → construct grounded context → answer. Retrieval and answer generation are separate steps and should be inspected independently.

## 2. Intermediate: build useful memory retrieval

- Replace `MockEmbedding` with a supported embedding model and ensure configured dimensions match the vector index.
- Add source IDs and metadata; apply owner/tenant filters before results reach the prompt.
- Choose chunk boundaries and top-k based on the content and context budget.
- Compare vector, keyword, and hybrid retrieval; add reranking only when evaluation shows a benefit.
- Keep updates/deletes synchronized between source records, index nodes, and derived summaries.
- For agentic workflows, retrieve before planning and validate any proposed memory writes before indexing.

## 3. Advanced and production

- Use a persistent vector/document store and durable source of truth; configure backups, schema/index migration, and disaster recovery.
- Separate ingestion and query workloads. Make ingestion repeatable, idempotent, observable, and safe to resume.
- Version parsers, chunking, prompts, embedding models, and index configuration. Plan backfills when these change.
- Enforce authorization filters in retrieval code, not in natural-language instructions.
- Apply retention, deletion, and correction to both source data and every derived index or cache.
- Use timeouts, bounded retries, rate limits, batching, and provider error handling. Avoid returning stale cached results after authorization changes.
- Protect credentials and data; redact sensitive text from traces and analytics.
- Track recall/precision, answer faithfulness, citation coverage, latency, index freshness, failure rate, and cost.

## 4. Evaluation

Create a query set with expected source documents. Measure retrieval recall at k and answer grounding separately. Include paraphrases, ambiguous queries, irrelevant documents, cross-user access attempts, updates, and deletion checks.

## 5. Common pitfalls

Mock embeddings can make output appear plausible without semantic retrieval. A vector index alone does not provide authorization or memory lifecycle management. Validate APIs and storage integration against the installed LlamaIndex version.
