# Memobase: beginner-to-production guide

Use [experiment.ipynb](./experiment.ipynb) to explore synthetic profile and timeline questions. Follow the current Memobase documentation for setup and SDK calls.

## 1. Beginner: profile versus timeline

A profile summarizes relatively stable user information; a timeline preserves dated events and changes. Keeping these concepts distinct helps answer both “what is true now?” and “what was true then?”

## 2. Intermediate: profile lifecycle

- Ingest consented user interactions with timestamps and source IDs.
- Inspect profile fields and timeline entries after extraction.
- Ask current-state and historical questions separately.
- Apply corrections and verify both representations update consistently.
- Set confidence/expiry policies for facts that can become stale.

## 3. Advanced and production

- Partition data by authorized user/tenant and enforce filters server-side.
- Store source-of-truth events separately from derived profiles; make reconstruction possible.
- Define retention, consent, correction, export, and deletion across profile, timeline, caches, and indexes.
- Protect credentials and personal information with encryption, least privilege, and redacted logs.
- Version profile schema and extraction prompts; migrate/backfill deliberately.
- Handle concurrent updates, duplicate events, ordering, time zones, and retries.
- Monitor profile freshness, timeline accuracy, retrieval quality, latency, failures, and cost.

## 4. Evaluation

Test changing preferences with dated facts, current and historical queries, duplicate events, out-of-order events, two users, and deletion. Verify the profile does not erase useful history and the timeline does not misstate the current preference.

## 5. Common pitfalls

Do not infer that a profile snapshot is a complete audit history. Check how the deployed version represents time, confidence, corrections, and data deletion. Notebook examples are scenarios, not a live service integration.
