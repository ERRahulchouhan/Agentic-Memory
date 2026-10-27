# Memary: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) outlines entity, relation, and multi-hop tests. Review current project maintenance, dependencies, and API support before using Memary.

## 1. Beginner: graph memory

A knowledge graph represents entities and their relationships explicitly. It can support multi-hop questions that require connecting several facts. Store where a relationship came from and when it is valid; generated relationships may be incorrect.

## 2. Intermediate: graph quality

- Extract entities and relations from a small, synthetic dataset.
- Normalize entity names and inspect duplicate/ambiguous entities.
- Test direct and multi-hop queries against source evidence.
- Add corrections and verify outdated edges are handled.
- Keep facts separate from generated explanations.

## 3. Advanced and production

- Use a secured, durable graph backend with backups, migrations, monitoring, and recovery.
- Partition and authorize graph reads/writes by tenant and user.
- Preserve provenance, timestamps, confidence, and correction history.
- Define entity-resolution and edge-retraction policies.
- Limit graph traversal, result size, prompt context, retries, and model spend.
- Review dependency health and pin compatible versions; isolate the service if maintenance status is uncertain.
- Protect credentials and sensitive source data, and support deletion across graph/index/cache layers.
- Monitor graph growth, extraction accuracy, multi-hop evidence coverage, latency, and errors.

## 4. Evaluation

Use labeled entity/relation facts and multi-hop questions. Measure extraction precision/recall, entity resolution, answer grounding, correction behavior, and cross-user isolation.

## 5. Common pitfalls

An incorrect edge can create a convincing but false multi-hop answer. Do not treat graph structure as proof. Verify current project activity and supported runtime before production adoption; notebook cells are scenarios, not a live Memary integration.
