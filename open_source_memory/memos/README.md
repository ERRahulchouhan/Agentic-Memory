# MemOS: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) provides a synthetic memory lifecycle scenario. Check the current MemOS project documentation for APIs, supported storage, and deployment requirements.

## 1. Beginner: managed memory

Think of memory as a managed resource with types, ownership, access, and lifecycle—not just prompt text. A useful design distinguishes source conversation, extracted facts, summaries, indexes, and the context selected for one model call.

## 2. Intermediate: lifecycle and policy

- Identify memory types and their purpose.
- Validate extracted records and retain provenance.
- Retrieve only authorized, relevant records.
- Update or supersede stale facts without corrupting unrelated memory.
- Apply retention and deletion across all representations.
- Track model-facing context and explain where each fact came from.

## 3. Advanced and production

- Use durable infrastructure with backups, recovery tests, and capacity controls.
- Apply policy enforcement and tenant isolation at the service boundary.
- Define data lineage from source to derived memory and ensure deletion propagates.
- Version schemas, policies, prompts, indexes, and model configurations.
- Protect data with encryption, least privilege, secret management, and audit trails.
- Bound tool permissions, context size, retries, processing queues, and provider cost.
- Monitor policy violations, stale data, retrieval quality, latency, and operational health.

## 4. Evaluation

Test authorization, correction, retention expiry, deletion propagation, repeated ingestion, provider failures, and recovery from backup. Confirm that a memory's origin and access scope remain inspectable.

## 5. Common pitfalls

Do not infer a production guarantee from the “memory OS” concept alone. Confirm the exact implementation and its security, tenancy, persistence, and lifecycle capabilities. The notebook is a scenario, not a MemOS SDK example.
