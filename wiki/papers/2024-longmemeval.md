# LongMemEval: Benchmarking Chat Assistants on Long-Term Interactive Memory

Di Wu et al. (UCLA, Tencent AI Lab Seattle, UC San Diego) · ICLR 2025 · [arXiv 2410.10813](https://arxiv.org/abs/2410.10813) · Read: full paper

**Topics:** [Evaluating memory](../topics/evaluating-memory.md) · [Updating and forgetting](../topics/updating-and-forgetting.md) · [How memory is organized](../topics/memory-structures.md) · [Memory vs. long context](../topics/memory-vs-long-context.md)

A benchmark of 500 questions that tests five memory abilities, including knowledge updates and abstention, over chat histories of about 115K tokens, or 1.5M in the larger setting. Commercial assistants and long-context LLMs lose much of their accuracy on it. The paper also lays out the design choices of memory systems and tests which ones help.

## Problem

Earlier benchmarks are short or leave out key abilities. By the paper's comparison, MemoryBank's evaluation has 194 questions over about 5K tokens and no multi-session reasoning, knowledge updates, or abstention; LoCoMo has no knowledge updates and doesn't test whether the assistant remembers what it said itself.

## Method

* **Questions:** 500, curated by hand, covering five abilities: information extraction, multi-session reasoning, knowledge updates, temporal reasoning, and abstention. Seven question types: single-session-user, single-session-assistant, single-session-preference, multi-session, knowledge-update, temporal-reasoning, and false-premise questions for abstention.
* **Histories:** needle-in-a-haystack. Evidence sessions are hidden among filler sessions drawn from ShareGPT, UltraChat, and simulated sessions that don't conflict with the evidence. LongMemEval_S is about 115K tokens per question; LongMemEval_M has 500 sessions, about 1.5M tokens.
* **Scoring:** GPT-4o as judge, with over 97% agreement with human experts.
* **A framework for memory designs:** three stages (indexing, retrieval, reading) and four choices: what's stored as the value (round, session, summary, fact), what it's indexed by (the key), how the query is formed, and whether time is used. The paper places existing designs, including [MemoryBank](2023-memorybank.md), on these choices.

## Results

* **Commercial assistants:** ChatGPT (GPT-4o) reaches 57.73% accuracy, a 37% drop from reading the same history offline (91.84%); Coze (GPT-4o) reaches 32.99%, a 64% drop.
* **Long-context LLMs** on LongMemEval_S, against reading only the evidence sessions: GPT-4o goes from 0.870 to 0.606, a 30.3% drop. The drops for open models are 36.1% (Llama 3.1 8B) to 55.1% (Llama 3.1 70B).
* **Design choices that help:**
  * Fact-augmented key expansion, indexing each round together with the facts extracted from it: Recall@5 from 0.582 to 0.644, and 5.4% higher accuracy on average across models.
  * Time-aware query expansion, narrowing retrieval to the time range a question implies: Recall@5 on temporal questions up 6.8% (rounds) to 11.3% (sessions) with GPT-4o.
  * Splitting sessions into rounds helps with GPT-4o. Reading with Chain-of-Note and JSON-formatted history adds up to 10 points with oracle retrieval.

## Limits

* The paper has no limitations section. Its ethics statement flags the privacy risk of storing and recalling user information.
* Filler sessions are chosen not to conflict with the evidence. My inference: each knowledge-update question tests one planted change, not a fact that changes again and again.

## Ideas worth reusing

* **Fact-augmented keys:** Index each round together with the facts extracted from it, so retrieval can match on facts, not just wording.
* **Time-aware query expansion:** Narrow retrieval to the time range a question implies before searching.
* **Evidence hidden among filler sessions:** Scale a test history by hiding the evidence sessions among filler sessions that don't conflict with them.

## For my work

The only benchmark in the wiki with knowledge-update questions, so it's where any claim about handling changed facts should be tested. Time-aware query expansion is a direct lead for answering "when was this true".

## Connections

* **Critiques** [LoCoMo](2024-locomo.md): says LoCoMo doesn't test recall of what the assistant said or reasoning with updated user information.
* **Critiques** [MemoryBank](2023-memorybank.md): says MemoryBank's evaluation doesn't test synthesizing information across many sessions; also places MemoryBank's design in its framework (summaries and rounds as values, time-aware).
* **Benchmark for** [Zep](2025-zep.md): Zep's main evaluation, on LongMemEval_S.
