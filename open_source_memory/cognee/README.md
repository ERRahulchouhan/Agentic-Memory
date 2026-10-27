# Cognee: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) demonstrates the high-level add → cognify → search flow with synthetic facts. It requires a configured provider and may incur API charges.

## 1. Beginner: from data to knowledge

Cognee helps transform source data into structured knowledge and retrieve it later. The basic pattern is: add source material to a dataset → process/cognify it into a knowledge representation → search with a question. Think of the graph/index as a derived representation; retain control of the original sources and their permissions.

## 2. Intermediate: ingestion and retrieval

- Start with a small synthetic dataset and a dedicated dataset name.
- Inspect extracted entities and relationships, not just the final answer.
- Compare direct fact retrieval with multi-hop questions.
- Track source identifiers and ingestion time so retrieved claims can be checked.
- Test repeat ingestion, changed source facts, and dataset boundaries.
- Add an answer-generation step only after retrieval is relevant; require evidence for claims.

## 3. Advanced and production

- Choose persistent stores deliberately and configure backups, migrations, recovery, and dataset retention.
- Enforce tenant/dataset authorization for add, process, and search operations.
- Separate ingestion credentials and workloads from online query services where possible.
- Make ingestion repeatable and idempotent; record source versions and processing status.
- Validate extracted knowledge and provide a correction/retraction path for bad facts.
- Limit data sent to providers, protect credentials, use TLS and least privilege, and redact sensitive logs.
- Bound graph expansion, retrieved evidence, prompt tokens, concurrency, retries, and spend.
- Monitor ingestion freshness, extraction failures, retrieval quality, query latency, index growth, and cost.
- Test model/pipeline upgrades on a representative corpus before rebuilding production knowledge.

## 4. Evaluation

Maintain a labeled set of source questions and expected evidence. Measure extraction accuracy, retrieval recall, multi-hop answer faithfulness, freshness after updates, isolation, and deletion completeness.

## 5. Common pitfalls

Successful processing does not prove that the knowledge graph is complete or accurate. Avoid sharing datasets across tenants and avoid treating generated relationships as verified facts. Confirm exact APIs and provider settings for your installed Cognee version.
