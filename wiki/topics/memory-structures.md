# How memory is organized

What a memory system stores, at what granularity, and how it finds it again.

## Where it stands

Designs have moved from one flat list of records ranked at read time ([Generative Agents](../papers/2023-generative-agents.md), [MemoryBank](../papers/2023-memorybank.md)) toward structure built at write time: tiers the LLM manages itself ([MemGPT](../papers/2023-memgpt.md)), notes linked to each other ([A-MEM](../papers/2025-a-mem.md)), and facts or graphs extracted from conversations ([Mem0](../papers/2025-mem0.md), [Zep](../papers/2025-zep.md)). Building structure at write time costs LLM calls on every message but keeps reads small: A-MEM and Zep read about 1–3K tokens per question.

What's not settled is whether the structure matters, or mostly the extraction of facts. The only same-condition comparison is Mem0's two variants on LoCoMo, where the graph helped temporal and open-domain questions and hurt single-hop and multi-hop.

## Approaches

| Approach | Papers | What one memory is | Who organizes it | Trade-off |
| --- | --- | --- | --- | --- |
| Flat stream, ranked at read time | [Generative Agents](../papers/2023-generative-agents.md) | An observation, reflection, or plan with timestamps and an importance score | A fixed scoring formula; the LLM writes reflections | Simple, but nothing is ever dropped, so retrieval does all the work |
| Logs plus rolling summaries | [MemoryBank](../papers/2023-memorybank.md) | Conversation turns, daily and global summaries, a user portrait | A fixed pipeline | Summaries compress the history; forgetting is by time only |
| Tiered context, like OS paging | [MemGPT](../papers/2023-memgpt.md) | Whatever the LLM writes to working context or archival storage | The LLM, through function calls | Flexible, but only as good as the model's function calling |
| Linked notes | [A-MEM](../papers/2025-a-mem.md) | A note with keywords, tags, context, and links | The LLM links new notes and rewrites their neighbors | Small reads (token length 1,216–2,520); quality depends on the LLM |
| Extracted facts | [Mem0](../papers/2025-mem0.md) | A short fact | The LLM chooses ADD, UPDATE, DELETE, or NOOP | Small store, about 7K tokens per LoCoMo conversation |
| Temporal knowledge graph | [Zep](../papers/2025-zep.md), Mem0^g | An entity, or a fact between entities with validity times | LLM extraction and resolution, plus graph algorithms | Keeps time and relations; Mem0 measured Zep's graph at over 600K tokens per conversation |

## How the papers connect

* [Generative Agents](../papers/2023-generative-agents.md) (April 2023) set the template: a memory stream scored by recency, importance, and relevance, plus reflection. [LoCoMo](../papers/2024-locomo.md) later used this architecture to generate its benchmark conversations.
* [MemoryBank](../papers/2023-memorybank.md) (May 2023) added summaries at two levels, a user portrait, and a forgetting curve.
* [MemGPT](../papers/2023-memgpt.md) (October 2023) handed the decisions to the LLM: what to keep in context, what to archive, and what to search.
* [LongMemEval](../papers/2024-longmemeval.md) (October 2024) gave a common vocabulary for comparing designs: the value stored, the key it's indexed by, how the query is formed, and whether time is used. Its experiments favor rounds as values with extracted facts added to the keys (Recall@5 from 0.582 to 0.644).
* In 2025, three designs build structure at write time: [Zep](../papers/2025-zep.md) (January) a bi-temporal graph, [A-MEM](../papers/2025-a-mem.md) (February) linked notes, and [Mem0](../papers/2025-mem0.md) (April) facts with explicit update operations plus a graph variant. A-MEM argues that graph memories with predefined schemas, like Mem0's, limit adaptability; Mem0 reports that Zep's graph is far larger than its own stores.
* These systems are rarely tested against each other under the same conditions; see [Evaluating memory](evaluating-memory.md).

## Open questions

* Does structure help beyond fact extraction? No paper compares flat facts, linked notes, and a graph with the same model and benchmark; Mem0's two variants are the only same-condition pair.
* How much does write-time structure cost per message at scale, against what it saves at read time? A-MEM puts one memory operation at about 1,200 tokens.
* Only Zep is tested on LongMemEval, so it's unknown how A-MEM, Mem0, or MemGPT do on its harder questions.
