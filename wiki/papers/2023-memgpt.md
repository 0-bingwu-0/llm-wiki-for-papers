# MemGPT: Towards LLMs as Operating Systems

Charles Packer et al. (University of California, Berkeley) · arXiv, Oct 2023 · [arXiv 2310.08560](https://arxiv.org/abs/2310.08560) · Read: full paper

**Topics:** [How memory is organized](../topics/memory-structures.md) · [Updating and forgetting](../topics/updating-and-forgetting.md) · [Evaluating memory](../topics/evaluating-memory.md) · [Memory vs. long context](../topics/memory-vs-long-context.md)

Treats the context window the way an operating system treats RAM: the LLM moves information between a small main context and external storage itself, through function calls, so a conversation or a document collection can outgrow the window.

## Problem

Context windows have a fixed size, so long conversations and large document collections don't fit. An agent needs a way to decide what stays in view and to find the rest when it needs it.

## Method

* **Main context** (the prompt): read-only system instructions, a fixed-size read/write working context, and a FIFO queue of recent messages.
* **External context:** recall storage (the full message history, searchable) and archival storage (a read/write database for any text).
* **Self-directed memory management:** the LLM edits working context and moves information in and out of external storage by calling functions. A `request_heartbeat` flag lets it chain calls, such as paging through search results, before it replies.
* **Memory pressure:** at 70% of the context window, the queue manager warns the LLM so it can save what matters. At 100%, it evicts 50% of the window's messages and folds them into a recursive summary.

## Results

* **Deep Memory Retrieval (DMR),** a task the paper builds on Multi-Session Chat: answer a question in session 6 about sessions 1–5. Accuracy with MemGPT, against the same model reading a recursive summary of past sessions: GPT-4 Turbo 93.4% vs 35.3%, GPT-4 92.5% vs 32.1%, GPT-3.5 Turbo 66.9% vs 38.7%.
* **Document QA** (NaturalQuestions-Open, 50 questions): MemGPT's accuracy holds as more documents are retrieved, because it pages through them; fixed-context baselines degrade as documents get truncated.
* **Nested key-value retrieval** (140 UUID pairs, about 8k tokens): GPT-3.5 and GPT-4 baselines fall to 0% at two to three levels of nesting; MemGPT with GPT-4 stays steady.

## Limits

* The authors report much worse results with GPT-3.5, because of its weaker function calling, and that MemGPT often stops paging through retriever results before reaching the end.
* My inference: everything depends on the LLM's judgment about what to save, overwrite, and search; nothing checks those decisions.

## Ideas worth reusing

* **Context the LLM manages itself:** The LLM moves information between a small main context and external storage through function calls. Needs strong function calling: results were much worse with GPT-3.5.
* **Memory-pressure warning:** Warn the model at 70% of the context window so it saves what matters before old messages are evicted and summarized.

## For my work

MemGPT gives the LLM the tools to overwrite a changed fact in working context, but has no rule for when, and DMR doesn't test it: each question asks about a fact stated once.

## Connections

* **Compared with** [Zep](2025-zep.md): Zep reports MemGPT's DMR score (93.4% with GPT-4 Turbo) next to its own 94.8% and a full-conversation baseline at 94.4%.
* **Critiqued by** [Zep](2025-zep.md): Zep argues DMR is a weak test, with single-turn fact-retrieval questions, ambiguous phrasing, and conversations of only 60 messages.
* **Compared with** [A-MEM](2025-a-mem.md): MemGPT is an A-MEM baseline on LoCoMo. With GPT-4o-mini, its token length in A-MEM's table is 16,977 against A-MEM's 2,520.
* **Compared with** [Mem0](2025-mem0.md): Mem0 reprints A-MEM's MemGPT numbers in its LoCoMo table.
* **Alternative to** [Generative Agents](2023-generative-agents.md): MemGPT cites it as related work; it lets the LLM manage memory instead of scoring records with a fixed formula.
