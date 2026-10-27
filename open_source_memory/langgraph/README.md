# LangGraph: beginner-to-production memory guide

See [experiment.ipynb](./experiment.ipynb) for a local example of conversation checkpoints and a cross-thread store.

## 1. Beginner: distinguish state from memory

- **Thread state/checkpoint:** The evolving state of one conversation, addressed by a thread ID. A checkpointer saves graph state so the conversation can resume.
- **Long-term store:** Data that should be available beyond one thread, usually addressed with a namespace and key.

A checkpoint is not automatically a user profile, and a store is not automatically safe to share. Start with an in-memory implementation to learn the APIs; it is temporary and disappears with the process.

## 2. Intermediate: wire memory into a graph

1. Define a typed graph state and decide which fields are conversation-local.
2. Compile with a checkpointer and pass a stable, authorized `thread_id` at invocation.
3. Use a store for cross-thread records with explicit user/tenant namespaces.
4. Add graph nodes that read relevant store entries before model reasoning.
5. Add a validated write node after the conversation turn; keep extraction and persistence separate from answer generation.
6. Test resume, concurrent threads, missing records, and conflicts.

For semantic memory, index store records and retrieve a small, relevant subset. Add source, timestamp, and memory type as metadata where useful.

## 3. Advanced and production

- Select a durable checkpointer and store supported by the deployment; configure connection pooling, backups, migrations, and retention.
- Authorize thread IDs and store namespaces server-side. Never accept a client-supplied namespace as proof of ownership.
- Make writes idempotent where graph retries are possible. Use versioning or timestamps to handle duplicate, concurrent, and conflicting updates.
- Keep checkpoints and long-term memory policies distinct: checkpoint retention may be short while user preferences persist longer.
- Bound state size and retrieved context; define node timeouts, retry policies, interrupt/resume behavior, and fallbacks if storage is unavailable.
- Protect secrets, encrypt network/storage, redact logs, and support user access, correction, and deletion across checkpoints, stores, and indexes.
- Trace graph execution without exposing full private memory content. Monitor node latency, checkpoint failures, retrieval quality, and model cost.

## 4. Evaluation

Test same-thread continuity, cross-thread recall for the same user, strict separation across users, resume after process restart, store outages, repeated writes, stale facts, and deletion. Check that the graph does not claim information when the store returns no relevant result.

## 5. Common pitfalls

An in-memory saver is not durable production persistence. Do not use globally shared namespaces, put all user facts in thread state, or assume a checkpoint automatically provides semantic search. Consult documentation for the installed LangGraph version and backend.
