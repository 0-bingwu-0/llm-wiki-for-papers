# Agent memory

How LLM agents keep, use, and lose information over long interactions. The papers here run from the first memory designs (2023), through benchmarks for long conversations (2024), to systems that extract facts and graphs as conversations come in (2025). The open question that matters most for my work: whether explicit update mechanisms handle changed facts better, which no paper here tests head to head.

## Where I could dig in

Open questions and limits in the wiki that bear on what I'm working on:

* **Retire, delete, or decay: never compared** (open question). Does retiring a fact beat deleting it or letting it decay on knowledge-update questions, with the same model and judge? No paper compares them. See [Updating and forgetting](topics/updating-and-forgetting.md).
* **No one measures misjudged contradictions** (open question). How often does the LLM misjudge a contradiction, deleting a fact that still holds or missing a real change? No paper measures the update step on its own. See [Updating and forgetting](topics/updating-and-forgetting.md).
* **Facts that change repeatedly go untested** (limit). Each knowledge-update question in [LongMemEval](papers/2024-longmemeval.md) plants one change. A fact that changes again and again isn't tested by any benchmark here.
* **Zep's update gains rest on thin evidence** (limit). [Zep](papers/2025-zep.md), the only system tested on update questions, is compared only with full context, and its gains are mixed across models.

## Topics

| Topic | Where it stands |
| --- | --- |
| [How memory is organized](topics/memory-structures.md) | Designs moved from flat lists ranked at read time to structure built at write time: tiers, linked notes, facts, graphs. No same-condition test of which structure matters. |
| [Updating and forgetting](topics/updating-and-forgetting.md) | Mem0 and Zep make updates explicit, but only Zep is tested on knowledge-update questions, with mixed results. |
| [Evaluating memory](topics/evaluating-memory.md) | Each system uses a different benchmark, and even on shared ones the papers disagree on labels and re-run scores. |
| [Memory vs. long context](topics/memory-vs-long-context.md) | Full context wins or ties on short histories; memory wins at about 115K tokens, and on latency everywhere. |

## Papers

| Paper | Published | In one line | Topics |
| --- | --- | --- | --- |
| [Generative Agents](papers/2023-generative-agents.md) | UIST 2023 | A memory stream ranked by recency, importance, and relevance, plus reflection | Organized, Updating |
| [MemoryBank](papers/2023-memorybank.md) | arXiv, May 2023 | Summaries, a user portrait, and an Ebbinghaus forgetting curve for companion chat | Organized, Updating, Evaluating |
| [MemGPT](papers/2023-memgpt.md) | arXiv, Oct 2023 | The LLM pages memory between its context and external storage, like an OS; introduces DMR | Organized, Updating, Evaluating, Long context |
| [LoCoMo](papers/2024-locomo.md) | arXiv, Feb 2024 | Benchmark of 50 months-long conversations; models fall far behind humans on temporal questions | Evaluating, Long context |
| [LongMemEval](papers/2024-longmemeval.md) | ICLR 2025 | Benchmark of 500 questions over ~115K-token histories, including knowledge updates | Evaluating, Updating, Organized, Long context |
| [Zep](papers/2025-zep.md) | arXiv, Jan 2025 | A temporal knowledge graph that retires old facts with a valid-time; beats full context on LongMemEval | Organized, Updating, Evaluating, Long context |
| [A-MEM](papers/2025-a-mem.md) | NeurIPS 2025 | Zettelkasten-style linked notes that the LLM keeps rewriting | Organized, Updating, Evaluating |
| [Mem0](papers/2025-mem0.md) | arXiv, Apr 2025 | Extracted facts with ADD, UPDATE, DELETE, and NOOP decided by the LLM; full context still scores higher on LoCoMo | Organized, Updating, Evaluating, Long context |
