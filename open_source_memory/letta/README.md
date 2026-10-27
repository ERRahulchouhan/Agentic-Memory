# Letta: beginner-to-production guide

Use [experiment.ipynb](./experiment.ipynb) alongside a Letta server and a disposable test agent. The notebook only performs a connection/list check; it does not create or delete agents.

## 1. Beginner: persistent agent memory

Letta is a stateful-agent platform. Unlike a stateless chat completion, a Letta agent can retain and manage memory across interactions. Learn the server/client boundary, agent identity, conversation/message lifecycle, and memory blocks before adding tools.

Start a local/test server using the current official setup, configure its model provider there, create a test agent, and connect with `LETTA_BASE_URL`. Set authentication tokens through environment variables.

## 2. Intermediate: memory and tools

- Inspect the agent's memory blocks before and after conversations.
- Separate concise, always-relevant profile information from archival or searchable history.
- Give tools narrow permissions and clear input/output schemas.
- Test how the agent edits a memory when a user corrects a fact.
- Determine which conversations or agents share state; use distinct test identities.
- Use synthetic data and verify whether memory persists across server restarts.

## 3. Advanced and production

- Deploy the server with durable storage, tested backups, migrations, health checks, and capacity limits.
- Use authenticated service-to-service connections, TLS, least privilege, secret rotation, and network isolation.
- Define agent ownership and authorization independently of user-provided IDs. Isolate tenants and audit memory reads/writes.
- Set explicit retention, consent, deletion, export, and correction workflows for agent messages and memory blocks.
- Restrict tools, validate arguments and outputs, and require confirmation for consequential external actions.
- Control prompt/context growth and tool loops; apply timeouts, budgets, rate limits, and safe interruption.
- Monitor server health, model/tool failures, memory edits, latency, and cost. Redact personal memory from logs.
- Test model upgrades and memory-schema changes against a staged agent before rollout.

## 4. Evaluation

Test persistent recall in a new conversation, fact correction, contradictory facts, tool misuse attempts, multi-tenant isolation, server restart, provider outage, and user deletion. Review both the agent's answer and the actual memory state.

## 5. Common pitfalls

Do not assume that a memory block is automatically correct, private, or bounded. Avoid exposing broad tools to an agent with persistent state. Confirm client and server API compatibility for the deployed version.
