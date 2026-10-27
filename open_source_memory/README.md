# Open-source memory experiments

This collection contains individual `experiment.ipynb` notebooks for the
15 memory projects listed in the workspace-root `readme.md`, plus examples for
LangGraph, LlamaIndex, and Haystack:

| Folder | Focus | Runtime requirements |
|---|---|---|
| [`mem0`](./mem0/README.md) | User-scoped semantic memory | LLM and embedding provider credentials |
| [`letta`](./letta/README.md) | Stateful agents with editable memory blocks | A running Letta server |
| [`cognee`](./cognee/README.md) | Knowledge-graph extraction and retrieval | LLM provider credentials |
| [`zep_graphiti`](./zep_graphiti/README.md) | Temporal knowledge-graph memory | Neo4j and LLM/embedding providers |
| [`langmem`](./langmem/README.md) | Memory extraction and management for LangGraph | Follow project setup; compatible store |
| [`memori`](./memori/README.md) | Structured memory for AI applications | Follow project setup and provider requirements |
| [`memu`](./memu/README.md) | Proactive-agent memory | Follow project setup and provider requirements |
| [`hindsight`](./hindsight/README.md) | Retrieval, reasoning, and reflection memory | Follow project setup and provider requirements |
| [`supermemory`](./supermemory/README.md) | Persistent context retrieval | Follow project setup and provider requirements |
| [`memobase`](./memobase/README.md) | Structured user profiles and timelines | Follow project setup and provider requirements |
| [`memoryos`](./memoryos/README.md) | Hierarchical long-term memory | Follow project setup and provider requirements |
| [`memos`](./memos/README.md) | Managed agent memory | Follow project setup and provider requirements |
| [`reme`](./reme/README.md) | Reusable agent memory and experience | Follow project setup and provider requirements |
| [`memary`](./memary/README.md) | Knowledge-graph-based agent memory | Follow project setup and provider requirements |
| [`openmemory`](./openmemory/README.md) | Persistent structured memory | Follow project setup and provider requirements |
| [`langgraph`](./langgraph/README.md) | Thread checkpoints and cross-thread stores | Local, in-memory demo |
| [`llamaindex`](./llamaindex/README.md) | Indexed knowledge retrieval | Local mock embeddings |
| [`haystack`](./haystack/README.md) | Local BM25 RAG pipeline | Local, in-memory demo |

Open a notebook from its folder and follow its setup and experiment guidance.
Provider-backed projects can change their APIs and deployment requirements;
use the linked project's current official documentation before connecting a
service. Do not put API keys directly in notebook cells. The LangGraph,
LlamaIndex, and Haystack examples include local demonstrations that avoid
external API calls.

Each project folder has a `README.md` covering beginner concepts, intermediate
design, advanced topics, production guidance, and evaluation. Every notebook
contains ten individual examples covering profile and preference
recall, goals, episodic and temporal facts, updates, user isolation, procedures,
related facts, and grounded RAG. The Mem0 notebook uses Mem0's configured LLM
and vector search, then asks an LLM to answer from retrieved memories; these
provider-backed calls may incur charges. The other notebooks' offline examples
use a small token-overlap retriever as a deterministic baseline, not the named
framework's SDK or a semantic model. Use each project's specific example and
current documentation to test its actual framework.

These are starter experiments rather than an exhaustive catalog or benchmark:
compare each tool's
memory scope, persistence, retrieval, update behavior, and operational
requirements before choosing one for an application.
