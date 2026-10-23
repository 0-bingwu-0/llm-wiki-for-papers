# Memory vs. long context

Whether a memory system beats putting the whole history in the model's context, and at what history length.

## Where it stands

It depends on how long the history is. When the history fits comfortably, full context wins or ties: on DMR (up to 60 messages), full conversation matches [MemGPT](../papers/2023-memgpt.md) and [Zep](../papers/2025-zep.md), and on LoCoMo (about 9K tokens per conversation), [Mem0](../papers/2025-mem0.md) reports full context at 72.90 J against 68.44 for its best variant. At about 115K tokens, [LongMemEval](../papers/2024-longmemeval.md) finds long-context models lose 30.3% (GPT-4o) to 55.1% (Llama 3.1 70B) of their accuracy, and Zep beats full context, 71.2% against 60.2% with gpt-4o.

Memory wins on cost wherever it's measured: Mem0 reports 91% lower p95 latency than full context, and Zep about 90% lower latency with 1.6K tokens of context instead of 115K. My inference: the point where memory starts to beat full context lies somewhere between about 10K and 100K tokens, but no paper here maps it.

## Evidence

Numbers within a row come from the same paper; rows can't be compared with each other.

| Benchmark | History | Full context | Memory or retrieval | Reported in |
| --- | --- | --- | --- | --- |
| DMR | Up to 60 messages | 94.4% (gpt-4-turbo), 98.0% (gpt-4o-mini) | Zep 94.8% and 98.2%; MemGPT 93.4% (gpt-4-turbo, as reported by MemGPT) | [Zep](../papers/2025-zep.md) |
| LoCoMo | About 9K tokens | 72.90 J (GPT-4o-mini) | Mem0 66.88, Mem0^g 68.44 | [Mem0](../papers/2025-mem0.md) |
| LoCoMo | About 9K tokens | 37.8 F1 (gpt-3.5-turbo-16k, 16K context) | RAG over observations 41.4 F1 | [LoCoMo](../papers/2024-locomo.md) |
| LongMemEval_S | About 115K tokens | 60.2% (gpt-4o), 55.4% (gpt-4o-mini) | Zep 71.2% and 63.8% | [Zep](../papers/2025-zep.md) |

## How the papers connect

* MemGPT framed memory as the answer to fixed context windows, but compared it with a recursive summary of past sessions (35.3% with GPT-4 Turbo on DMR), not with full context.
* On LoCoMo, retrieving observations beat long context with gpt-3.5-turbo-16k. On the same benchmark in 2025, Mem0 found full context beat every memory system with GPT-4o-mini. The models, metrics, and question sets differ. My inference: stronger models use a short history in context better, which shrinks the case for memory on short histories.
* LongMemEval measured the long-context drop directly: GPT-4o goes from 0.870 with only the evidence sessions to 0.606 with the full ~115K-token history.
* Zep, on LongMemEval_S, beats full context overall but still loses on single-session-assistant questions (94.6% against 80.4% with gpt-4o).
* Zep's critique of DMR follows from the same pattern: when full conversation already scores 94.4–98.0%, the benchmark can't separate memory from long context.

## Open questions

* Where's the crossover, by history length and by model? No paper varies history length for the same system.
* Do stronger models keep pushing the crossover out? The LoCoMo and Mem0 results point in opposite directions, but too much differs between them to say.
