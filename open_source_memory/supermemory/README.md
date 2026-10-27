# Supermemory: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) defines a synthetic retrieval/update experiment. Confirm the current Supermemory API, SDK, and deployment options before connecting a service.

## 1. Beginner: persistent context

Persistent memory stores useful information between interactions so an application can personalize or contextualize responses. Identify who owns each memory, what it means, where it came from, and when it should expire.

## 2. Intermediate: retrieve and update

- Add a few synthetic memories under a dedicated test identity.
- Search using exact terms and paraphrases.
- Inspect metadata and sources; avoid injecting every result.
- Update a preference and check for stale/conflicting values.
- Test access boundaries and lifecycle controls.
- Ground generated answers in retrieved evidence and acknowledge gaps.

## 3. Advanced and production

- Choose a persistence model, backup and recovery plan, and index migration process.
- Enforce authorization before retrieval; isolate tenants and test cross-scope access.
- Define consent, data minimization, expiry, export, correction, and deletion workflows.
- Protect credentials and stored data; use TLS, least privilege, and privacy-aware audit logs.
- Bound retrieval count, context size, retries, rate limits, and spend.
- Track provider/model/index versions and re-evaluate after changes.
- Monitor retrieval relevance, stale memory, isolation failures, latency, availability, and cost.

## 4. Evaluation

Test direct and paraphrased recall, corrections, missing facts, cross-user queries, expiry, and deletion. Measure whether the answer is supported by retrieved memories, not just whether it sounds plausible.

## 5. Common pitfalls

Do not assume persistent storage includes application authorization or a complete deletion guarantee. The notebook is a scenario guide; verify exact product semantics and API behavior with the current project documentation.
