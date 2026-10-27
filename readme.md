# AI memory guide: types, use cases, and tool selection

## What “memory” means in an AI application

An AI model does not automatically retain facts between independent requests.
An application supplies relevant state or retrieves stored information and
places it in the model's context. “Memory” is therefore a system made up of
storage, retrieval, update/forgetting rules, authorization, and the prompt or
agent workflow that uses it.

Do not confuse these related concepts:

- **Context window:** Information included in the current model request. It is
  temporary and consumes tokens.
- **Conversation history:** Earlier messages, often persisted so a conversation
  can resume. A transcript is not automatically a useful or safe memory.
- **Memory:** Selected, structured or searchable information retained for
  future tasks.
- **Knowledge base / RAG corpus:** Documents or reference material the
  application retrieves to answer questions. It is usually not personal
  conversational memory.
- **Cache:** A speed/cost optimization for repeated work. Cached output can be
  stale and is not a source of truth.

## Types of memory and when to use them

These are logical memory types. A system can combine several in one product;
they are not mutually exclusive and do not require one tool per type.

| Memory type | What it stores | Use it when… | Example |
|---|---|---|---|
| **Working / in-context** | Facts needed for the current request or plan | The agent is solving a multi-step task right now | Current task constraints and tool results |
| **Conversation / thread state** | Messages and workflow state for one conversation | A user must resume the same chat or an agent graph must continue after interruption | Recent messages, pending approval, current step |
| **Semantic / profile** | Durable facts, preferences, identity, and goals | Personalization should carry across conversations | “Prefers concise explanations” |
| **Episodic / event** | Specific experiences with time and provenance | The user asks what happened, when, or what was decided | “On Tuesday, we selected option B” |
| **Procedural / skill** | How to perform a recurring task or follow a preference | The agent should repeat a validated workflow | “Check required fields before summarizing a CSV” |
| **Entity / relationship** | Entities and links between them | Questions require relationships or multi-hop reasoning | “Mira works at X; X builds product Y” |
| **Temporal** | Facts with effective time, history, and changes | Answers depend on what was true at a particular time | “The project moved from SQLite to PostgreSQL in June” |
| **Document / knowledge (RAG)** | External or organizational source material | Answers need current, attributable reference documents | Product manuals, policies, internal knowledge |
| **Experience / reflection** | Prior task outcomes, successes, failures, and lessons | An agent can improve or reuse experience across similar tasks | A successful troubleshooting sequence |
| **Hierarchical / consolidated** | Summaries or layers of short-, medium-, and long-term memory | The full history is too large and different details have different lifetimes | Profile summary + recent episodes + archive |

### A practical retention rule

Before storing a fact, ask: **Will this help a future task, is it appropriate to
retain, and can it be corrected or deleted?** Prefer small, explicit memories
with a source, owner, timestamp, and expiry/retention policy over an unfiltered
transcript. Do not retain secrets or sensitive personal data unless there is a
clear, consented, lawful need and suitable safeguards.

## Memory storage and retrieval approaches

Memory *type* describes the information. Storage/retrieval describes how the
system finds it. Select the approach based on the question:

| Approach | Strong at | Limitations / when not enough |
|---|---|---|
| **Recent-message window** | Exact continuity over the latest turns | Old facts fall out; context cost grows with window |
| **Structured database / key-value** | Exact fields, filters, updates, permissions | Requires a schema; weak for fuzzy natural-language lookup by itself |
| **Keyword / BM25 search** | Exact names and terms; simple and explainable RAG | Misses many paraphrases and semantic relationships |
| **Vector search** | Semantic similarity across varied wording | Similarity is not truth; needs good embeddings, filters, and evaluation |
| **Hybrid search / reranking** | Combining lexical matches and semantic recall | More components, cost, tuning, and operational complexity |
| **Knowledge graph** | Explicit entities, relationships, and multi-hop queries | Extraction/entity resolution can be wrong; graph operations add complexity |
| **Temporal graph / event store** | Relationships and facts that change over time | Requires careful timestamps, provenance, and correction semantics |
| **Summary / hierarchical store** | Compressing long histories and separating time horizons | Summaries can omit details and provenance; retain original records when needed |

For private user memory, retrieval must be **authorized before relevance is
considered**. A highly relevant memory belonging to another user must never be
returned.

## How memory fits into RAG and an agent

### Basic RAG flow

1. Ingest and normalize trusted source documents.
2. Split/index them with metadata and access-control labels.
3. Retrieve a small set of relevant, authorized sources for the question.
4. Optionally rerank or apply policy/freshness checks.
5. Ask the model to answer from that evidence and cite it.
6. Return “not found” or ask a question when evidence is insufficient.

### Agentic memory flow

1. **Identify scope:** Resolve the authenticated user, tenant, agent, and
   conversation on the server.
2. **Load working state:** Restore the thread/checkpoint if this is a continuing
   task.
3. **Retrieve:** Query only authorized memories and knowledge relevant to the
   current goal.
4. **Reason and act:** Give the agent bounded evidence and only the tools it
   needs; require confirmation for consequential external actions.
5. **Validate writes:** Treat proposed memories as untrusted candidates. Check
   sensitivity, usefulness, provenance, conflicts, and retention before saving.
6. **Update or forget:** Supersede stale facts, preserve history when needed,
   and propagate corrections/deletion to indexes, summaries, caches, and
   backups according to policy.
7. **Evaluate:** Measure retrieval and answer quality separately.

## Which tools are best?

There is no universal winner. The project names below describe their general
focus; APIs, licensing, maintenance, self-hosting, and production readiness
change. Verify those points against the current official project documentation
before choosing. This workspace is a learning collection, **not a benchmark**.

| If your main need is… | Start by evaluating… | Why / caveat |
|---|---|---|
| User-specific semantic memories with a simple add/search workflow | **Mem0** | Good starting point for personalization. The notebook has a provider-backed Mem0 + LLM example; evaluate update quality, isolation, cost, and persistence for your needs. |
| A stateful agent with explicit editable memory and ongoing conversations | **Letta** | Evaluate its agent/server lifecycle and memory controls; requires a running service and operational setup. |
| Durable conversation workflow state and cross-thread application memory | **LangGraph** | Checkpointing and stores are useful primitives; you still design memory extraction, policy, and retrieval. |
| Memory management integrated with LangGraph workflows | **LangMem** | Consider when building around LangGraph; verify compatible versions and storage integration. |
| Temporal facts and relationship-aware retrieval | **Graphiti** | Evaluate when “what was true when?” and graph relationships matter; it needs graph infrastructure and model configuration. |
| Turning source data into a knowledge graph and querying it | **Cognee** | Evaluate for graph-oriented knowledge ingestion; inspect extracted facts and provenance. |
| General document indexing and RAG pipelines | **LlamaIndex** or **Haystack** | These are broader data/RAG frameworks rather than turnkey personal-memory systems. Choose based on integrations, pipeline model, and team familiarity. |
| Structured user profiles and timelines | **Memobase** | Evaluate current schema, timeline, update, and lifecycle behavior for profile-heavy applications. |
| Proactive reminders or event-driven context | **memU** | Test timing, user controls, and false-positive interruptions carefully. |
| Reusing task procedures and prior agent experience | **ReMe** | Evaluate applicability and whether the agent adapts lessons instead of blindly repeating them. |
| Memory with reflection/reasoning or hierarchical concepts | **Hindsight**, **MemoryOS**, or **MemOS** | Treat as candidates for targeted evaluation; verify project maturity, APIs, and operational requirements. |
| Structured memory experiments or alternate memory services | **Memori**, **Supermemory**, or **OpenMemory** | Compare supported deployment, lifecycle, access controls, and actual retrieval behavior in a proof of concept. |
| Knowledge-graph-oriented agent memory | **Memary** | Check maintenance and dependency health, then evaluate extraction and multi-hop accuracy. |

### Short recommendations

- **Learning the concepts:** Start with the local LangGraph, LlamaIndex, and
  Haystack examples, then try the provider-backed Mem0 notebook if you can
  configure credentials.
- **Building a personalized assistant:** Prototype with Mem0 or a structured
  profile store; add explicit user scoping, correction, and deletion tests from
  day one.
- **Building a durable multi-step agent:** Use your agent framework's
  checkpoint/state mechanism (for example, LangGraph or Letta) and add a
  separate long-term memory store only for information that must outlive a
  thread.
- **Answering from company documents:** Start with a RAG framework (LlamaIndex
  or Haystack) and a permission-aware document store. Do not put all reference
  documents into personal memory.
- **Reasoning over changing relationships:** Evaluate a temporal graph such as
  Graphiti; use a simpler database/vector RAG system if temporal relations are
  not a real requirement.
- **Production choice:** Select the smallest design that meets measured
  retrieval, latency, privacy, durability, and cost targets. A single database
  plus good metadata may be better than adding graph, vector, and agent-memory
  services at once.

## Production checklist

- **Authorization:** Derive user/tenant scope from authenticated identity;
  enforce it in every read, write, search, tool, and admin path.
- **Privacy and lifecycle:** Minimize collection; provide consent, retention,
  correction, export, and deletion. Include derived embeddings, summaries,
  graph edges, caches, and backups in the policy.
- **Evidence and freshness:** Store provenance and timestamps; distinguish
  observed facts from inferred facts; expire or supersede stale data.
- **Reliability:** Use durable storage, backups, restore drills, migrations,
  idempotent writes, timeouts, bounded retries, and a safe no-memory fallback.
- **Agent safety:** Retrieved content is untrusted data, not instructions.
  Protect against prompt injection in memories/documents and restrict tools
  independently of what memory says.
- **Evaluation:** Build a representative test set. Measure retrieval recall,
  precision, answer faithfulness, citations, update behavior, isolation,
  deletion, latency, and cost.
- **Operations:** Monitor errors and quality trends without logging sensitive
  content. Set budgets for tokens, retrieval count, graph traversal, and
  notifications.
- **Change management:** Version schemas, prompts, embedding models, indexes,
  and extraction logic; test migrations and re-indexing before rollout.

## Project guides and experiments

## Experiments

Each project listed above has a dedicated folder containing an `experiment.ipynb`
under [`open_source_memory/`](./open_source_memory/). Open the notebook for the
project you want to explore. Some experiments need provider credentials or a
running service; those requirements are described in the notebook. Never put
secrets directly in notebook cells. Every notebook includes at least ten
separately runnable examples. The Mem0 notebook uses Mem0 with an LLM and
provider-backed calls; other notebooks provide offline scenario cells where
noted, which are learning baselines and not replacements for each project's
own integration.

| Project | Guide | Notebook |
|---|---|---|
| Mem0 | [README.md](./open_source_memory/mem0/README.md) | [experiment.ipynb](./open_source_memory/mem0/experiment.ipynb) |
| Letta (MemGPT) | [README.md](./open_source_memory/letta/README.md) | [experiment.ipynb](./open_source_memory/letta/experiment.ipynb) |
| Cognee | [README.md](./open_source_memory/cognee/README.md) | [experiment.ipynb](./open_source_memory/cognee/experiment.ipynb) |
| Graphiti | [README.md](./open_source_memory/zep_graphiti/README.md) | [experiment.ipynb](./open_source_memory/zep_graphiti/experiment.ipynb) |
| LangMem | [README.md](./open_source_memory/langmem/README.md) | [experiment.ipynb](./open_source_memory/langmem/experiment.ipynb) |
| Memori | [README.md](./open_source_memory/memori/README.md) | [experiment.ipynb](./open_source_memory/memori/experiment.ipynb) |
| memU | [README.md](./open_source_memory/memu/README.md) | [experiment.ipynb](./open_source_memory/memu/experiment.ipynb) |
| Hindsight | [README.md](./open_source_memory/hindsight/README.md) | [experiment.ipynb](./open_source_memory/hindsight/experiment.ipynb) |
| Supermemory | [README.md](./open_source_memory/supermemory/README.md) | [experiment.ipynb](./open_source_memory/supermemory/experiment.ipynb) |
| Memobase | [README.md](./open_source_memory/memobase/README.md) | [experiment.ipynb](./open_source_memory/memobase/experiment.ipynb) |
| MemoryOS | [README.md](./open_source_memory/memoryos/README.md) | [experiment.ipynb](./open_source_memory/memoryos/experiment.ipynb) |
| MemOS | [README.md](./open_source_memory/memos/README.md) | [experiment.ipynb](./open_source_memory/memos/experiment.ipynb) |
| ReMe | [README.md](./open_source_memory/reme/README.md) | [experiment.ipynb](./open_source_memory/reme/experiment.ipynb) |
| Memary | [README.md](./open_source_memory/memary/README.md) | [experiment.ipynb](./open_source_memory/memary/experiment.ipynb) |
| OpenMemory | [README.md](./open_source_memory/openmemory/README.md) | [experiment.ipynb](./open_source_memory/openmemory/experiment.ipynb) |

Additional retrieval-framework guides and notebooks: [LlamaIndex](./open_source_memory/llamaindex/README.md) and [Haystack](./open_source_memory/haystack/README.md); [LangGraph](./open_source_memory/langgraph/README.md) covers checkpoint and store primitives."# Agentic-Memory" 
