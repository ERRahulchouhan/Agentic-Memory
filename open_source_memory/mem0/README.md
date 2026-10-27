# Mem0: beginner-to-production guide

This guide accompanies [experiment.ipynb](./experiment.ipynb). The notebook's Mem0 examples use a configured Mem0 memory backend and an LLM to answer from retrieved memories; they are provider-backed and may incur charges.

## 1. Beginner: what Mem0 does

Mem0 extracts useful facts from conversations, stores them as user-scoped memories, and retrieves relevant facts later. This is different from sending the entire chat history to every model call: the memory layer decides what to retain and fetch.

Basic flow:

1. Receive a conversation or event.
2. Call `memory.add(...)` with an explicit user identity.
3. Mem0's configured LLM extracts or updates facts; the configured embedder and vector store support retrieval.
4. Call `memory.search(query, user_id=...)`.
5. Add retrieved facts to the answer model's context and generate a grounded response.

Run the notebook setup cells first. Configure `OPENAI_API_KEY` in the environment, not in notebook source. The local Qdrant path is for experimentation, not a production persistence plan.

## 2. Intermediate: memory design

- **Identity and scope:** Decide whether memory belongs to a user, conversation, organization, or agent. Treat identifiers and namespace filters as authorization boundaries.
- **Extraction:** Store stable preferences, goals, and useful facts; avoid retaining every utterance.
- **Retrieval:** Tune query construction, result count, relevance threshold, and metadata filters. Inspect the returned memories before prompting the answer model.
- **Updates and contradictions:** Test whether new facts replace, qualify, or coexist with older facts. Keep timestamps and provenance where the application needs history.
- **RAG grounding:** Include retrieved memory as evidence, instruct the model to acknowledge missing evidence, and retain source metadata for citations.
- **Agent use:** Retrieve context before planning; let tools write memories only after validating their content and scope.

## 3. Advanced and production architecture

Use a controlled memory service between application/agent code and the store. A typical flow is authenticated request → tenant/user authorization → retrieval → relevance and policy checks → bounded prompt context → model response → optional validated memory write.

Production considerations:

- Use a persistent, backed-up vector store and explicitly configure the LLM, embedding model, dimensions, and provider limits.
- Enforce tenant filtering on the server side; never rely on the model prompt to isolate users.
- Minimize personal data, define consent, retention, export, correction, and deletion procedures, and ensure vector records and derived memories are included.
- Protect provider credentials with a secret manager; use TLS, least-privilege service identities, network restrictions, and audit logs.
- Bound memory count and prompt tokens; apply timeouts, retries with backoff, rate limits, and graceful behavior when memory retrieval is unavailable.
- Version extraction prompts and schemas. Re-embed or migrate records deliberately when changing embedding models.
- Monitor extraction quality, retrieval relevance, stale/conflicting facts, latency, error rates, token use, and cost without logging sensitive memory text.
- Evaluate with a versioned test set: correct retrieval, user isolation, update behavior, unsupported-answer refusal, and deletion verification.

## 4. Evaluation checklist

Test exact and paraphrased questions, conflicting updates, two isolated users, missing facts, long conversations, provider errors, and restart/recovery. Compare answers with memory disabled. Do not treat a successful API response as proof that extraction or retrieval is correct.

## 5. Common pitfalls

Do not pass unfiltered search results into a prompt, store secrets or unnecessary sensitive facts, assume local notebook storage is durable, or allow an agent to write arbitrary tool output as trusted memory. Confirm current Mem0 configuration/API options for the installed version.
