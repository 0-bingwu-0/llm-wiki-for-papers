# Score the update step, not only the final answer

This is what sets my work apart from [Zep](../wiki/papers/2025-zep.md) and [Mem0](../wiki/papers/2025-mem0.md). Both make the update decision explicit, but both judge it only by end-to-end answers: Zep on DMR and LongMemEval, Mem0 on LoCoMo, which has no questions about changed facts at all ([Evaluating memory](../wiki/topics/evaluating-memory.md)). A right answer can hide a wrong update, and a wrong answer can come from retrieval instead.

So for each new fact, I'll check the decision itself: did the system keep, update, retire, or delete the right memory? That measures how often the LLM misjudges a contradiction, which no paper in the wiki reports ([Where I could dig in](../wiki/index.md#where-i-could-dig-in)).

In related work, this is the line to draw: the same problem as Zep and Mem0, evaluated step by step instead of only by answer accuracy.

## Still open

* Where the right decision for each change comes from. LongMemEval's planted changes give it for one change per question; facts that change several times will need my own labels.
