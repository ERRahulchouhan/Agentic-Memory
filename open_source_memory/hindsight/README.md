# Hindsight: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) provides synthetic, dated facts for testing recall, corrections, and evidence. Use the current Hindsight documentation for the supported API and deployment model.

## 1. Beginner: evidence-aware memory

Memory with retrieval, reasoning, and reflection should make it easier to answer questions from prior experience while keeping the evidence visible. Separate stored observations from generated conclusions, and preserve time and provenance.

## 2. Intermediate: build an evaluation loop

- Ingest dated, source-linked events.
- Retrieve evidence for a new question.
- Generate an answer constrained to retrieved evidence.
- Compare the answer with sources and record errors.
- Add corrections and verify obsolete claims are handled appropriately.
- Use reflection to identify failures, not to silently rewrite evidence.

## 3. Advanced and production

- Persist source records and derived memories separately; support restore and reprocessing.
- Apply server-side tenant isolation, authorization, retention, and deletion to all derived data.
- Track provenance and distinguish observed facts, inferred claims, and user corrections.
- Constrain reflection to evidence; require validation before memory writes.
- Version extraction/reasoning prompts and schemas; evaluate changes on a fixed corpus.
- Use bounded context, traversal, retries, timeouts, and provider budgets.
- Protect sensitive data and credentials; redact logs while retaining operational traces.
- Monitor evidence coverage, unsupported claims, correction latency, retrieval quality, and cost.

## 4. Evaluation

Use temporal questions, contradictory facts, missing evidence, source citations, user separation, and correction tests. Score answer correctness and evidence support independently.

## 5. Common pitfalls

Reflection is not a substitute for verified data. Do not treat a confident answer as evidence, and do not allow ungrounded self-critique to overwrite trusted memory. The notebook is an experiment plan rather than a live Hindsight client.
