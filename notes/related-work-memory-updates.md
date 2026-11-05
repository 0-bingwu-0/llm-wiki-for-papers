# Related work: updating memory

Draft for my paper's related work section.

**Forgetting by decay.** Early memory designs never resolve a changed fact. Generative Agents ranks memories by recency, importance, and relevance, with recency counted from the last retrieval (Park et al., 2023). MemoryBank lets memories fade along a forgetting curve, and each recall makes a memory last longer (Zhong et al., 2023). In both, an outdated fact that keeps being recalled stays strong.

**Updates decided by the LLM.** MemGPT gives the model tools to edit its own memory, but no rule for when to (Packer et al., 2023). A-MEM rewrites the context and tags of related notes as new ones arrive, which changes how old notes are described, not whether they still hold (Xu et al., 2025). Mem0 makes the decision explicit: for each new fact, the LLM adds, updates, deletes, or leaves memories as they are (Chhikara et al., 2025). Zep keeps a contradicted fact and marks when it stopped being valid (Rasmussen et al., 2025), as does Mem0's graph variant.

**Evaluation.** LoCoMo has no questions that target a changed fact (Maharana et al., 2024). LongMemEval adds knowledge-update questions (Wu et al., 2025), but of the systems above, only Zep reports on them, against full context alone and with mixed results across backbone models.

**Our work** scores the update decision itself rather than only the final answer, and compares retiring, deleting, and decaying under the same model and judge, including facts that change more than once.

## References

* Chhikara et al., 2025. [Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory](https://arxiv.org/abs/2504.19413)
* Maharana et al., 2024. [Evaluating Very Long-Term Conversational Memory of LLM Agents](https://arxiv.org/abs/2402.17753)
* Packer et al., 2023. [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560)
* Park et al., 2023. [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442)
* Rasmussen et al., 2025. [Zep: A Temporal Knowledge Graph Architecture for Agent Memory](https://arxiv.org/abs/2501.13956)
* Wu et al., 2025. [LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory](https://arxiv.org/abs/2410.10813)
* Xu et al., 2025. [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110)
* Zhong et al., 2023. [MemoryBank: Enhancing Large Language Models with Long-Term Memory](https://arxiv.org/abs/2305.10250)
