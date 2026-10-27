# Zep / Graphiti: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) outlines a temporal knowledge-graph experiment. It requires a configured graph database and model providers; the notebook intentionally avoids writing to a service until configuration is ready.

## 1. Beginner: graph and time

Graphiti builds a knowledge graph from episodes: entities are connected by relationships, and facts can have temporal context. This is useful when questions depend on changing facts, relationships, and when information was true. It differs from ordinary vector search, which ranks text by similarity but may not represent validity intervals explicitly.

Learn the terms episode, entity, edge/fact, group or tenant scope, and temporal validity from the installed Graphiti version's documentation.

## 2. Intermediate: add and query episodes

1. Start a disposable Neo4j instance and configure supported LLM/embedding providers through environment variables.
2. Add dated synthetic episodes to a dedicated test group.
3. Query current and historical facts separately.
4. Inspect the graph and evidence used for answers.
5. Add a correction and verify how old and new facts are represented.
6. Compare graph retrieval with a vector-search baseline on the same questions.

## 3. Advanced and production

- Use durable, secured graph infrastructure with backups, monitoring, capacity planning, and tested restore procedures.
- Separate graph groups/namespaces by tenant and enforce authorization before query or write operations.
- Track provenance and temporal boundaries; define how corrections, duplicates, retractions, and entity merges are handled.
- Version extraction prompts, schemas, model/provider settings, and graph migrations.
- Bound episode size, query result count, model context, and graph traversal depth.
- Protect Neo4j and provider credentials, use TLS and least privilege, and avoid sending unnecessary personal data to external models.
- Make ingestion idempotent and recoverable. Use a disposable environment for experiments and documented deletion for cleanup.
- Monitor extraction errors, graph growth, retrieval relevance, query latency, provider cost, and stale facts.

## 4. Evaluation

Create dated questions whose answers change over time. Score current-state accuracy, historical accuracy, entity/relation extraction, evidence traceability, update handling, and tenant isolation. Include ambiguous dates and contradictory sources.

## 5. Common pitfalls

Do not treat every extracted edge as verified truth or assume graph retrieval alone grounds a generated answer. Use the actual installed version's quickstart for exact client calls, provider configuration, and cleanup operations.
