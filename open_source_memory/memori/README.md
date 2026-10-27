# Memori: beginner-to-production guide

The [experiment notebook](./experiment.ipynb) gives a synthetic scenario for evaluating structured AI memory. Follow the current project documentation for installation, provider support, and SDK usage.

## 1. Beginner: structured memory

Structured memory stores useful facts in a more inspectable form than an unfiltered transcript. Separate identity/profile, preference, goal, and episodic facts. Decide what should persist and how users can correct it.

## 2. Intermediate: application workflow

1. Assign an authorized user/tenant scope.
2. Extract candidate facts from a conversation.
3. Validate type, source, and sensitivity before persistence.
4. Retrieve relevant facts for a query.
5. Generate an answer grounded in retrieved evidence.
6. Apply updates, expiry, or deletion consistently.

Test corrections and conflicting records; inspect structured memory rather than judging only the model's answer.

## 3. Advanced and production

- Choose a durable backend, backups, disaster recovery, and migration process.
- Apply server-side tenant isolation and least privilege to reads and writes.
- Define data minimization, consent, retention, export, correction, and deletion across all derived records.
- Validate input and extracted output; treat model-generated memories as untrusted until checked.
- Version schemas and extraction rules; make writes idempotent.
- Configure bounded retries, timeouts, context limits, rate limits, and provider budgets.
- Use encryption, TLS, secret management, audit trails, and privacy-conscious logging.
- Monitor extraction/update precision, retrieval relevance, stale/conflicting facts, latency, error rates, and cost.

## 4. Evaluation

Measure extraction accuracy, update correctness, paraphrase retrieval, user isolation, unsupported-answer behavior, and deletion verification. Include synthetic sensitive-looking values to ensure they are excluded when policy says so.

## 5. Common pitfalls

The notebook is an evaluation scenario, not an SDK integration. Confirm the current project's actual storage, update, and deletion semantics before promising persistence or privacy guarantees.
