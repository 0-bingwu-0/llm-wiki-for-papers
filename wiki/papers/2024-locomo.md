# Evaluating Very Long-Term Conversational Memory of LLM Agents

Adyasha Maharana et al. (University of North Carolina Chapel Hill, University of Southern California, Snap Inc) · arXiv, Feb 2024 · [arXiv 2402.17753](https://arxiv.org/abs/2402.17753) · Read: full paper

**Topics:** [Evaluating memory](../topics/evaluating-memory.md) · [Memory vs. long context](../topics/memory-vs-long-context.md)

Introduces LoCoMo, a benchmark of 50 very long conversations, about 300 turns and 19 sessions each, grounded in each speaker's life events over months. Long-context LLMs and RAG fall far behind humans, most of all on temporal and adversarial questions.

## Problem

Long-term memory should be tested on conversations that run for months, where facts depend on events in each speaker's life. The paper builds such conversations and measures how far current models are from humans on them.

## Method

* **Generation:** two LLM agents talk. Each has a persona, expanded from Multi-Session Chat personas with gpt-3.5-turbo, and a temporal event graph of up to 25 causally linked events over 6–12 months. They use [Generative Agents](2023-generative-agents.md)' memory and reflection to stay consistent, and can share and react to images.
* **Human editing:** annotators edited about 15% of the turns and removed or replaced about 19% of the images.
* **Size:** 50 conversations, averaging 304.9 turns, 19.3 sessions, and 9,209 tokens.
* **Tasks:** question answering, scored by F1, with 7,512 questions: single-hop 2,705, multi-hop 1,104, temporal 1,547, open-domain 285, and adversarial (unanswerable) 1,871. Also event summarization against the event graphs, and multimodal dialogue generation.

## Results

* Question answering with gpt-3.5-turbo-16k given 16K of context: F1 37.8 overall (single-hop 56.4, multi-hop 42.0, temporal 20.3, open-domain 37.2, adversarial 2.1). Humans: 87.9 overall.
* RAG with gpt-3.5-turbo-16k and top-5 retrieval: retrieving observations (assertions about each speaker extracted from the dialogue) scores 41.4, raw dialogue turns 31.7, and session summaries 29.9.
* Temporal and adversarial questions have the biggest gaps to humans: 72.3 and 87.3 points.

## Limits

* The authors note the conversations are machine-generated with human edits, so they may miss real-world nuance; the shared web images lack the consistency of personal photos; and the data is English only, built with closed models.
* There are no questions about facts that change; see the critique from [LongMemEval](2024-longmemeval.md) below.

## Ideas worth reusing

* **Conversations grounded in an event graph:** Generate months-long conversations from personas and a causal graph of life events, so every question has ground truth.
* **Retrieve observations, not turns:** Index assertions extracted about each speaker; on LoCoMo they retrieve better than raw turns or session summaries.

## For my work

Results on LoCoMo say little about updates, because no question type targets a changed fact; temporal questions are the closest. Worth keeping in mind whenever a paper reports LoCoMo as evidence that its memory "stays current".

## Connections

* **Builds on** [Generative Agents](2023-generative-agents.md): uses its memory and reflection architecture to generate the conversations.
* **Benchmark for** [A-MEM](2025-a-mem.md): A-MEM's main evaluation, scored with F1 and BLEU-1.
* **Benchmark for** [Mem0](2025-mem0.md): Mem0's only evaluation, without the adversarial category and with an added LLM judge.
* **Critiqued by** [LongMemEval](2024-longmemeval.md): LongMemEval says LoCoMo doesn't test recall of what the assistant said or reasoning with updated user information.
