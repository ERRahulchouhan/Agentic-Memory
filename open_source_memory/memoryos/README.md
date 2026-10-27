# MemoryOS: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) gives stable preference, long-term goal, and episodic examples. Use the current MemoryOS documentation for implementation details.

## 1. Beginner: hierarchical memory

Hierarchical memory organizes information by role or timescale—for example, stable profile facts, ongoing goals, and individual episodes. The goal is to retrieve the right level of detail for a question without putting an entire history into every prompt.

## 2. Intermediate: organize and retrieve

- Define categories and criteria for moving information between them.
- Preserve source and timestamp for each extracted item.
- Retrieve category-appropriate context; distinguish current profile from historical events.
- Allow correction, expiry, and consolidation; inspect what is removed or summarized.
- Keep a bounded prompt context and test whether summaries preserve important facts.

## 3. Advanced and production

- Persist category data and source events with backups and tested recovery.
- Enforce tenant isolation across every hierarchy, index, cache, and retrieval path.
- Define lifecycle and deletion policies for original records and derived summaries.
- Version schemas and consolidation logic; support reprocessing after a change.
- Make updates idempotent and handle event ordering and conflicting facts.
- Protect secrets and sensitive data; audit reads/writes without logging unnecessary content.
- Monitor retrieval by category, stale facts, summary fidelity, latency, storage growth, and cost.

## 4. Evaluation

Test category placement, cross-category queries, current versus historical facts, summary retention, corrections, multiple users, and data deletion. Measure both retrieval relevance and whether hierarchy reduces prompt size without losing accuracy.

## 5. Common pitfalls

More levels do not automatically improve recall. Avoid rigid categories that hide relevant facts and summaries that discard provenance. The notebook is a study design, not an executable MemoryOS integration.
