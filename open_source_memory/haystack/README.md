# Haystack: beginner-to-production RAG guide

The [experiment notebook](./experiment.ipynb) uses an in-memory document store and BM25 retrieval. It runs locally but is a lexical baseline, not a semantic embedding retriever.

## 1. Beginner: pipeline and retrieval

Haystack pipelines connect components such as converters, document stores, retrievers, rankers, and generators. This example writes synthetic memories to an in-memory store and retrieves matching documents using BM25. BM25 is useful for keyword overlap; it will not understand every paraphrase.

Basic RAG: ingest documents → retrieve evidence → optionally rerank → build bounded context → generate a grounded answer.

## 2. Intermediate: build a memory pipeline

- Attach metadata such as tenant, owner, source, type, and timestamp.
- Add a semantic or hybrid retriever when queries need semantic matching.
- Apply metadata filters before returning documents to an answer model.
- Use a generator that is instructed to cite retrieved evidence and say when evidence is missing.
- Keep document updates and deletion synchronized with the store.
- Inspect each pipeline component's input/output during development.

## 3. Advanced and production

- Replace the in-memory store with a durable backend; plan backups, indexing, schema changes, and recovery.
- Isolate ingestion, retrieval, and generation workloads; configure connection pools and concurrency limits.
- Enforce access filters in the pipeline/service layer and test bypass attempts.
- Version converters, chunking, embeddings, retriever settings, prompts, and rankers.
- Use timeouts, bounded retries, circuit breakers, and graceful degradation when a component/provider fails.
- Protect source documents and credentials; redact traces and logs; define deletion for indexes and caches.
- Monitor retrieval recall, answer faithfulness, citation correctness, freshness, latency per component, failure rates, and cost.

## 4. Evaluation

Build a retrieval dataset with expected relevant documents. Measure recall@k and ranking metrics separately from answer correctness. Include lexical matches, paraphrases, irrelevant context, access-control tests, source updates, and deleted documents.

## 5. Common pitfalls

BM25 is not a vector search model. A pipeline does not automatically provide tenant isolation, source governance, or memory update semantics. Confirm component names and backend integration for the installed Haystack version.
