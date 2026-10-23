# Updating and forgetting

What happens to a memory when time passes or a newer fact contradicts it. This is the question my own work is on.

## Where it stands

The papers fall into three groups. [Generative Agents](../papers/2023-generative-agents.md) and [MemoryBank](../papers/2023-memorybank.md) never resolve a changed fact; old memories only fade, by a recency score or a forgetting curve. [MemGPT](../papers/2023-memgpt.md) and [A-MEM](../papers/2025-a-mem.md) let the LLM rewrite memory, but neither tests whether it gets a changed fact right. [Mem0](../papers/2025-mem0.md) and [Zep](../papers/2025-zep.md) make updates explicit: Mem0's LLM chooses UPDATE or DELETE, while Zep and Mem0^g mark the old fact invalid instead of deleting it.

The evidence lags the designs. Of the benchmarks here, only [LongMemEval](../papers/2024-longmemeval.md) has knowledge-update questions, and only Zep reports on them, against full context alone and with mixed results: 78.2% to 83.3% with gpt-4o, but 76.9% to 74.4% with gpt-4o-mini. Mem0 and A-MEM are tested on LoCoMo, which has no update questions. So no paper here shows that an explicit update mechanism beats the alternatives on changed facts.

## Approaches

| Approach | Papers | When an old fact goes away | Who decides | Tested on changed facts? |
| --- | --- | --- | --- | --- |
| Decay at read time | [Generative Agents](../papers/2023-generative-agents.md) | Never; it ranks lower as recency decays (factor 0.99 per game hour since last retrieval) | A fixed formula | No |
| Forgetting curve | [MemoryBank](../papers/2023-memorybank.md) | When retention e^(−t/S) falls; each recall resets t and raises S | A fixed formula | No |
| LLM edits its own memory | [MemGPT](../papers/2023-memgpt.md) | When the LLM rewrites working context or archival storage | The LLM | No |
| Evolve related notes | [A-MEM](../papers/2025-a-mem.md) | Never removed; neighbors' context, keywords, and tags get rewritten | The LLM | No |
| Explicit operations | [Mem0](../papers/2025-mem0.md) | DELETE when contradicted; UPDATE to merge | The LLM, per candidate fact against the 10 most similar memories | No; LoCoMo has no update questions |
| Retire with a valid-time | [Zep](../papers/2025-zep.md), Mem0^g | Never deleted; the old fact's t_invalid is set to the new fact's t_valid | The LLM detects the contradiction | Zep only, on LongMemEval's knowledge-update questions |

## How the papers connect

* Generative Agents and MemoryBank both reward memories that get used: Generative Agents measures recency from the last retrieval, and MemoryBank strengthens a memory each time it's recalled. My inference: in both, an outdated fact that keeps coming up stays strong, the opposite of what an update should do.
* MemGPT gives the LLM tools to overwrite memory but no rule for when to. A-MEM's memory evolution changes how old notes are described, not whether they still hold.
* Mem0 and Zep both have an LLM compare each new fact with similar stored ones, but differ on what happens next. Base Mem0 deletes the contradicted fact; Zep and Mem0^g keep it with an end time. My inference: keeping it lets the system answer what used to be true, at the cost of a larger store (Mem0 reports Zep's graph at over 600K tokens per conversation).
* LongMemEval criticized [LoCoMo](../papers/2024-locomo.md) for not testing updated user information, added knowledge-update questions, and showed that time-aware query expansion raises Recall@5 on temporal questions by 6.8% to 11.3% with GPT-4o.
* Zep is the only system here tested on those questions: a gain with gpt-4o, a small drop with gpt-4o-mini.

## Open questions

* Does retiring a fact (Zep, Mem0^g) beat deleting it (Mem0) or letting it decay, on knowledge-update questions with the same model and judge? No paper compares them.
* How often does the LLM misjudge a contradiction, deleting a fact that still holds or missing a real change? None of the papers measures the update step on its own.
* LongMemEval's filler sessions are chosen not to conflict with the evidence. My inference: a fact that changes several times over a history isn't tested by any benchmark here.
