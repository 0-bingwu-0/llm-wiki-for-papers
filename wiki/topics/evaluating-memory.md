# Evaluating memory

Which benchmarks the papers use, what each one tests, and which results can be compared.

**Status:** Contested

## Where it stands

Each system paper picks a different benchmark, so there is almost no head-to-head evidence. [MemGPT](../papers/2023-memgpt.md) introduced DMR, which [Zep](../papers/2025-zep.md) later called too weak: full conversation already scores 94.4–98.0% on it. [LoCoMo](../papers/2024-locomo.md), used by [A-MEM](../papers/2025-a-mem.md) and [Mem0](../papers/2025-mem0.md), has long conversations by turn count but only about 9K tokens each, and no knowledge-update questions. [LongMemEval](../papers/2024-longmemeval.md) is the hardest and the only one that tests updates and abstention, but only Zep reports on it.

Even on the same benchmark, results don't line up. A-MEM and Mem0 put the same LoCoMo numbers under different category names, and Mem0's re-run of A-MEM scored lower than A-MEM's own report.

## Benchmarks

| Benchmark | From | History | Questions | What it tests | Scored by | Used by |
| --- | --- | --- | --- | --- | --- | --- |
| DMR | [MemGPT](../papers/2023-memgpt.md) | 5 sessions, up to 60 messages per conversation (per Zep) | One per conversation, 500 conversations (per Zep) | Recalling a fact from earlier sessions | Accuracy (LLM judge), ROUGE-L | MemGPT, Zep |
| LoCoMo | [LoCoMo](../papers/2024-locomo.md) | 50 conversations, averaging 304.9 turns, 19.3 sessions, 9,209 tokens | 7,512 | Single-hop, multi-hop, temporal, open-domain, adversarial | F1 (LoCoMo, A-MEM); F1, BLEU-1, and an LLM judge (Mem0) | A-MEM, Mem0 |
| LongMemEval | [LongMemEval](../papers/2024-longmemeval.md) | About 115K tokens (S), or 500 sessions and 1.5M tokens (M) | 500 | Information extraction, multi-session reasoning, knowledge updates, temporal reasoning, abstention | GPT-4o judge | Zep |
| MemoryBank's probing questions | [MemoryBank](../papers/2023-memorybank.md) | 10 days of conversation with 15 simulated users | 194 | Recall in companion chat | Retrieval accuracy, correctness, coherence | MemoryBank |

## How the papers connect

* **DMR:** MemGPT built it on Multi-Session Chat and reported 93.4% with GPT-4 Turbo. Zep reported 94.8%, then argued DMR is weak: single-turn fact retrieval, ambiguous phrasing, and conversations short enough that full conversation scores 94.4% (gpt-4-turbo) and 98.0% (gpt-4o-mini). Zep moved its main evaluation to LongMemEval.
* **LoCoMo:** generated with [Generative Agents](../papers/2023-generative-agents.md)' architecture; its own baselines found temporal and adversarial questions hardest. A-MEM evaluates on it with F1 and BLEU-1. Mem0 drops the adversarial category, saying it lacks ground-truth answers, and adds an LLM judge.
* **The LoCoMo label mismatch:** Mem0's results table reprints A-MEM's GPT-4o-mini numbers for five methods, but under different category names. The column A-MEM labels Multi Hop appears in Mem0 as Single Hop, A-MEM's Open Domain as Multi-Hop, and A-MEM's Single Hop as Open Domain; only Temporal matches. Before comparing per-category claims across the two papers, check which labeling matches LoCoMo's data.
* **Re-runs:** Mem0's re-run of A-MEM at temperature 0 scored lower in every category than A-MEM's own report, for example 20.76 against 27.02 F1 in the first column.
* **Critiques of earlier benchmarks:** LongMemEval says MemoryBank's evaluation doesn't test synthesis across many sessions, and LoCoMo doesn't test recall of what the assistant said or reasoning with updated user information.
* **Who runs whose system:** Mem0 ran Zep and OpenAI's memory itself; Zep compared itself only with full context and with MemGPT's reported DMR score. Both papers come from the companies that sell the systems.

## Open questions

* No paper here tests systems on both LoCoMo and LongMemEval, so results can't be bridged between the two.
* The LLM judges differ (GPT-4o in LongMemEval, Mem0's own judge on LoCoMo), so scores both called "accuracy" aren't the same measure.
* Which LoCoMo category labeling is right, A-MEM's or Mem0's.
