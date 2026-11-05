# Retire, delete, or decay: test them head to head

My first experiment. Systems handle a changed fact in three ways, and no paper compares them with the same backbone model, judge, and questions ([Updating and forgetting](../wiki/topics/updating-and-forgetting.md)):

* **Retire:** keep the old fact and mark when it stopped being true, as in [Zep](../wiki/papers/2025-zep.md) and Mem0's graph variant.
* **Delete:** remove the contradicted fact, as in base [Mem0](../wiki/papers/2025-mem0.md).
* **Decay:** never resolve the change, and let the old fact rank lower over time, as in [Generative Agents](../wiki/papers/2023-generative-agents.md) and [MemoryBank](../wiki/papers/2023-memorybank.md).

I'll start from [LongMemEval](../wiki/papers/2024-longmemeval.md)'s knowledge-update questions, the only ones in the wiki that target a changed fact. Each plants a single change, so I'll add histories where the same fact changes several times. That's where I expect delete and decay to fall behind: delete loses what used to be true, and decay keeps an old fact strong as long as it keeps coming up.

## Still open

* Whether to give all three the same extraction step, which isolates the update rule but means reimplementing each system, or to run each system as published.
* Which judge to use, so my scores can sit next to Zep's LongMemEval results.
