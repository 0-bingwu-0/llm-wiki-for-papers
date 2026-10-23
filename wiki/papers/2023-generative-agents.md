# Generative Agents: Interactive Simulacra of Human Behavior

Joon Sung Park et al. (Stanford University, Google Research, Google DeepMind) · UIST 2023 · [arXiv 2304.03442](https://arxiv.org/abs/2304.03442) · Read: full paper

**Topics:** [How memory is organized](../topics/memory-structures.md) · [Updating and forgetting](../topics/updating-and-forgetting.md)

Twenty-five LLM agents live in a simulated town for two days and stay believable because of a memory architecture: a stream of everything they observe, retrieval that weighs recency, importance, and relevance, and reflection that turns observations into higher-level thoughts.

## Problem

An LLM can act believably in a single moment, but an agent that lives for days has to remember what happened, draw conclusions from it, and plan ahead. The full history doesn't fit in the prompt, and earlier LLM-driven characters had no long-term memory that kept growing and changing.

## Method

* **Memory stream:** every record is a natural-language description with a creation timestamp and a last-access timestamp. Observations, reflections, and plans all go into the same stream.
* **Retrieval:** each record gets three scores, min-max normalized and summed with equal weights (all α = 1):
  * recency: exponential decay over sandbox hours since the record was last retrieved, with a decay factor of 0.99;
  * importance: the LLM rates the record 1–10 when it's written, from mundane ("brushing teeth") to poignant;
  * relevance: cosine similarity between the record's embedding and the query's.
* **Reflection:** when the summed importance of recent events passes 150 (about two or three times a game day), the agent asks itself the most salient questions about its 100 latest records, retrieves memories for each, and writes insights that cite the records they came from. Reflections can build on reflections, forming a tree.
* **Planning:** plans are broken down top-down (a day into five to eight chunks, then hours, then 5–15 minute actions), stored in the stream, and revised when the agent sees something relevant.
* Backbone: gpt-3.5-turbo.

## Results

* In interviews about self-knowledge, memory, plans, reactions, and reflections, rated by 100 human evaluators, the full architecture ranked highest (TrueSkill μ = 29.89), ahead of no reflection (26.88), no reflection or planning (25.64), crowdworkers role-playing the agents (22.95), and no memory at all (21.21). Removing reflection cost the most.
* Over two simulated days, news of one agent's candidacy spread from 1 agent to 8 (4% to 32%), news of a Valentine's Day party from 1 to 13 (4% to 52%), and the town's relationship network density rose from 0.167 to 0.74. Five of the twelve invited agents came to the party.

## Limits

* The authors list three main failure modes: agents fail to retrieve the relevant memory, embellish what they know (hallucinations in 1.3% of 453 answers about other agents), and talk too formally. As memory grows, agents also pick odd places to act.
* Nothing in the stream is ever updated or removed. My inference: an outdated fact stays forever, and only the recency score pushes it down.

## For my work

The baseline for "keep everything, rank at read time". Recency is measured from the last time a record was retrieved, not when it was written, so an old fact that keeps coming up stays "recent". For changed facts, that's the opposite of what I want.

## Connections

* **Built on by** [LoCoMo](2024-locomo.md): LoCoMo's two conversing agents use this memory and reflection architecture to keep their months-long conversations consistent.
* **Alternative to** [MemoryBank](2023-memorybank.md): both let old memories fade with time, here through a recency score at retrieval, there through a forgetting curve.
* **Alternative to** [MemGPT](2023-memgpt.md): MemGPT cites this work; it hands memory decisions to the LLM instead of a fixed scoring formula.
