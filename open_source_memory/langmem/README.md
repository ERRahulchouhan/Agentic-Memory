# LangMem: beginner-to-production guide

See [experiment.ipynb](./experiment.ipynb) for a scenario-based evaluation worksheet. Use the current LangMem documentation for installation and version-specific API calls.

## 1. Beginner: memory as a managed workflow

LangMem provides memory-management capabilities intended for agent applications, especially LangGraph workflows. Distinguish extraction (turning conversation into candidate facts), storage (where facts live), retrieval (which facts matter now), and update (how changed facts supersede old ones).

## 2. Intermediate: extraction, storage, retrieval

- Identify which facts are durable and useful; avoid storing every turn.
- Define a structured memory schema and include provenance/time where needed.
- Connect memory to an authorized store and use namespaces to scope user or tenant data.
- Retrieve relevant memories before generation and bound the prompt context.
- Validate candidate writes, then test correction and conflict behavior.
- Keep memory-management nodes separate from agent actions with external side effects.

## 3. Advanced and production

- Use a durable store and a documented migration/backup strategy.
- Enforce ownership and tenant isolation in the application, not only in prompts or generated filters.
- Make writes idempotent and handle concurrent updates with versions or timestamps.
- Apply consent, retention, deletion, export, and correction policies to source conversations and derived memories.
- Version schemas, extraction prompts, and model settings; evaluate migrations before rollout.
- Limit retries, token budgets, retrieval count, and provider spend; design a safe no-memory fallback.
- Audit memory reads/writes while minimizing sensitive logs; monitor extraction precision, retrieval quality, staleness, latency, and errors.

## 4. Evaluation

Use the notebook's profile, preference, update, and isolation scenarios. Add tests for paraphrase recall, incorrect extraction, duplicate writes, unsupported questions, store outages, and end-to-end deletion.

## 5. Common pitfalls

Do not confuse an example worksheet with an integrated LangMem runtime. The notebook scenario is a test plan, not a live LangMem call. Verify package APIs and compatible LangGraph/store versions before implementation.
