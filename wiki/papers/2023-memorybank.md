# MemoryBank: Enhancing Large Language Models with Long-Term Memory

Wanjun Zhong et al. (Sun Yat-Sen University, Harbin Institute of Technology, KTH Royal Institute of Technology) · arXiv, May 2023 · [arXiv 2305.10250](https://arxiv.org/abs/2305.10250) · Read: full paper

**Topics:** [How memory is organized](../topics/memory-structures.md) · [Updating and forgetting](../topics/updating-and-forgetting.md) · [Evaluating memory](../topics/evaluating-memory.md)

A long-term memory for companion chatbots. It stores conversations, daily and overall summaries, and a running picture of the user's personality, and forgets memories along an Ebbinghaus forgetting curve unless they're recalled.

## Problem

Companion and counseling chatbots talk to the same user over many days, and LLMs have no long-term memory to carry what they learned from one day to the next.

## Method

* **Storage:** conversation records with timestamps; daily event summaries, rolled up into a global summary; daily personality insights, rolled up into a global user portrait.
* **Retrieval:** dense retrieval in the style of DPR, indexed with FAISS (MiniLM embeddings for English, Text2vec for Chinese).
* **Forgetting:** retention R = e^(−t/S), where t is the time elapsed and S is memory strength. S starts at 1 when a memory is first mentioned. Each time the memory is recalled, S goes up by 1 and t resets to 0, so it becomes less likely to be forgotten.
* **SiliconFriend:** a companion app built on MemoryBank, run with ChatGPT and with two open models (ChatGLM, BELLE) LoRA-tuned on 38k psychological conversations.

## Results

* Evaluated with simulated users: 15 virtual users with distinct personalities, 10 days of conversation, and 194 probing questions (97 English, 97 Chinese).
* In English, memory retrieval accuracy ranges from 0.763 (ChatGPT) to 0.814 (BELLE), while response correctness is 0.716 for ChatGPT against 0.438 (ChatGLM) and 0.479 (BELLE).
* The results compare backbone models running MemoryBank, not MemoryBank against other memory designs.

## Limits

* The authors call the forgetting model "exploratory and highly simplified": real forgetting differs by person and by type of information.
* Forgetting depends on time and recall, not on content. My inference: a fact that has been replaced fades only if nobody asks about it, and asking about the old fact makes it stronger.

## Ideas worth reusing

* **Forgetting curve that recall resets:** Each memory fades as e^(−t/S), and every recall raises its strength S and resets t.
* **Rolling summaries and user portrait:** Roll daily event summaries and personality insights up into one global summary and one user portrait.

## For my work

The first design here to treat forgetting as a feature, but its only form of updating is decay. A useful time-based baseline next to the content-based updates in [Mem0](2025-mem0.md) and [Zep](2025-zep.md).

## Connections

* **Compared with** [A-MEM](2025-a-mem.md): A-MEM runs MemoryBank as a LoCoMo baseline. With GPT-4o-mini it scores lowest in four of five categories, and uses the fewest tokens (432).
* **Compared with** [Mem0](2025-mem0.md): Mem0 reprints A-MEM's MemoryBank numbers in its LoCoMo table.
* **Critiqued by** [LongMemEval](2024-longmemeval.md): LongMemEval says MemoryBank's 194 probing questions don't test synthesizing information across many sessions, and its benchmark has no knowledge-update or abstention questions.
* **Alternative to** [Generative Agents](2023-generative-agents.md): both let old memories fade with time, there through a recency score, here through a forgetting curve.
