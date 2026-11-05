# LLM Wiki for Papers

When you work in a research area, you read a lot of papers. Notes on each one pile up, but how they fit together stays in your head: who built on whom, which results disagree, what's still open. And it fades.

This project has AI build and keep a wiki of the papers you add. It follows Andrej Karpathy's [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) idea: instead of searching the PDFs every time you ask something, the AI works the papers into linked pages once and keeps them current. The wiki has two layers:

* **A page for each paper.** What it asks, how it works, what it finds, its limits, the ideas worth reusing, and what it means for your own work.
* **Topic pages on how the papers relate.** For each question several papers speak to: how settled it is, how the papers line up, who builds on whom, which results can and can't be compared, where they disagree, and what's still open.

Each new paper updates both layers: its own page, the pages of papers it connects to, and the topics it lands in. When you ask a question, the answer comes from a wiki that's already worked out, with sources. What you settle as you talk is kept: findings about the papers go back into the wiki, so it gets sharper the more you use it, and your own ideas, like an experiment you want to run, go into your notes.

## Getting started

You'll mostly do two things. Open this project in StashBase and tell the Agent:

1. **"Set me up."** It asks you a few questions, one at a time: your research area, what you're working on, how you want papers explained, and which papers you have. Then it replaces the example with a wiki of your papers.
2. **"Add the new papers."** Drop PDFs into `library/` first, or paste a link instead: "Add arxiv.org/abs/2310.08560". Each paper gets its page, its connections, and a place in the topics. Not sure what to add? Ask "What should I read next?"

Open the dashboard, `index.html`, to see the whole area at a glance. It shows what to say in Chat, too.

You can also:

* **Ask anything.** For example, "How do Zep and Mem0 handle a fact that changes?", "Which of these results on LoCoMo can I actually compare?", or "Draft a related work paragraph on memory structures for my paper." Drafts go into your notes.
* **Say "Check the wiki."** every so often. It fixes conflicts and missing connections, and tells you which papers your library keeps citing but doesn't have yet.

The template comes with an example: a wiki of eight papers on agent memory, from Generative Agents and MemGPT to Zep and Mem0, kept for a PhD student working on memory that stays correct when facts change, with a few of the student's notes: an experiment idea, what sets the work apart, and a related work draft. Browse it and ask it questions before running setup. Setup replaces it with yours. The example's PDFs aren't included; its pages link to arXiv.

## The dashboard

The wiki is all text, and you never have to open anything else. The dashboard is an index on top of it, kept current by the Agent each time the wiki changes. Every topic and paper name opens its page.

* **Topics:** each topic, how settled it is, and the papers that speak to it.
* **Papers:** each paper's main point, and the topics it speaks to. Click a row to see which papers it connects to, and how.
* **What you're working on, and your progress:** your current focus, and how the wiki has grown.

## Requirements

An Agent that can run local commands, to download papers from links. No API key is needed.

## Make it yours

Setup covers most of it. You can also change things anytime:

* **Your area, what you're working on, and how you want papers explained** are in `context/profile.md`.
* **What goes on paper and topic pages** is in `workflows/add.md`.
* **How your notes are kept** is in `workflows/ask.md`.
* **What the dashboard shows,** and how the Agent keeps it current, is in `workflows/maintain.md`.
* **The Agent's persona and rules,** including the types of connections between papers, are in `AGENTS.md`.

## Files

* `AGENTS.md`: the Agent's persona, how the wiki is organized, how to keep it trustworthy, and the task index.
* `CLAUDE.md`: points Claude Code to `AGENTS.md`.
* `context/profile.md`: your area, what you're working on, and how to explain papers to you.
* `workflows/setup.md`: the setup Q&A.
* `workflows/add.md`: how to add papers, with the page formats for paper and topic pages.
* `workflows/ask.md`: how to answer questions, suggest what to read next, keep what you settle in the wiki or your notes, and write from it.
* `workflows/checkup.md`: what to look for in a check-up.
* `workflows/maintain.md`: how the Agent keeps the dashboard in line with the wiki, and the format of its data.
* `library/`: the papers themselves.
* `wiki/index.md`: the map: where you could dig in, and every topic and paper in one line each.
* `wiki/papers/`: one page per paper.
* `wiki/topics/`: one page per question or theme that several papers speak to.
* `notes/`: your own ideas, settled as you talk with the Agent, and drafts of your writing, like a related work section.
* `index.html`: the dashboard.
* `assets/wiki.json`: everything the dashboard shows, a short version of the wiki.
* `assets/banner.svg`: the dashboard's banner.
