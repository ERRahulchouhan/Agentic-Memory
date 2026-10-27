# OpenMemory: beginner-to-production guide

Use [experiment.ipynb](./experiment.ipynb) as a synthetic memory lifecycle checklist. Consult current OpenMemory documentation for supported deployment and APIs.

## 1. Beginner: persistent structured memory

Persistent memory lets an application retain selected facts across sessions. Start with a few non-sensitive records, identify their owner and source, and test add, search, update, and delete behavior.

## 2. Intermediate: retrieval and lifecycle

- Define memory types and metadata that support filtering.
- Retrieve by relevance within an authorized scope.
- Update changed facts while preserving unrelated memories.
- Set expiry and retention rules.
- Inspect how the system handles duplicate records, corrections, and no-result queries.

## 3. Advanced and production

- Configure durable storage, backups, encryption, monitoring, and recovery.
- Enforce tenant isolation and access control in the service, including search and administrative APIs.
- Implement consent, export, correction, retention, and verifiable deletion across derived indexes and caches.
- Protect credentials, redact sensitive logs, and maintain audit trails for access and changes.
- Bound query results, prompt context, retries, rate limits, and resource usage.
- Pin versions, apply security updates, and test migrations before rollout.
- Monitor retrieval relevance, stale/conflicting records, deletion completion, latency, and availability.

## 4. Evaluation

Test paraphrase retrieval, updates, duplicates, separate users, deletion, backup restore, and service outages. Verify that deleted records cannot be retrieved from any path.

## 5. Common pitfalls

Persistence is not the same as authorization or compliance. Confirm actual deletion semantics and backups/retention interaction for the deployed version. The notebook is a test guide, not a live OpenMemory SDK integration.
