# Add Papers

Adding a paper is more than summarizing it. One paper usually touches several pages: its own, the pages of the papers it connects to, one to three topics, and the index. Do all of it in one go, so the wiki never has a paper that isn't connected.

## Get the paper

* **A PDF in library/:** use it. When I say "add the new papers", look for PDFs in `library/` that don't have a page yet.
* **An arXiv link or ID:** save the PDF to `library/` first, with `curl -L -o library/<name>.pdf https://arxiv.org/pdf/<ID>`. For other links, find the PDF; if there's none, read the page.
* **A title only:** find the paper on arXiv or the publisher's site, check that the title and authors match, then save it as above.

Name the PDF and the page the same way, `<year>-<short-name>`. The short name is the method or benchmark name if the paper has one, otherwise two or three words from the title: `2023-memgpt`, `2024-locomo`.

If the paper already has a page, tell me and stop. The exception is a new version with changed results: then update its page.

## Read it

Read the full paper, not just the abstract: the method and experiments in full, and the related work to see how it places itself. If you can only get the abstract, write the page from it and say so on the page.

While reading, note what it cites, compares against, or evaluates on that's already in the wiki, and the papers it builds on most that aren't.

## Write the paper page

Save it to `wiki/papers/<year>-<short-name>.md`:

```markdown
# <Full title>

**Authors:** <First author> et al. (<affiliations as listed>) · **Published:** <venue and year, or "arXiv, Mon YYYY"> · [arXiv <ID>](https://arxiv.org/abs/<ID>) · [PDF](../../library/<year>-<short-name>.pdf)
**Read:** full paper | abstract only
**Topics:** [<Topic>](../topics/<topic>.md), ...

<One or two sentences: what it does and what it finds.>

## Problem
## Method
## Results
## Limits
## For my work
## Connections
```

* **Problem:** the gap it addresses and where earlier work falls short, by its own account. A few sentences.
* **Method:** the mechanism, specific enough that I could explain it to a labmate without opening the paper. Use the paper's own names for its parts.
* **Results:** the main findings, each with the paper's own numbers and the setting they belong to. Include an ablation when it shows what actually matters.
* **Limits:** the limits the authors state, then any you see, labeled "My inference".
* **For my work:** one to three lines on what it means for what I'm working on, as described in profile.md. This part is inference by nature, so it needs no label. If the paper doesn't bear on my work, say so in one line.
* **Connections:** typed links to other paper pages, one line each. The types are in [AGENTS.md](../AGENTS.md#connections).

## Connect it

1. Find related papers in the wiki. Search for the paper's method, benchmark, and problem, and check the papers it cites against the index.
2. Add the connections to the new page, and the reverse connection to each of the other pages.
3. Check whether the new paper changes anything on those pages. For example, it may report new results for an older method, or show a limit the older page doesn't mention. If so, update them.

## Update topics

1. Decide which topics the paper belongs to, usually one to three.
2. For each topic, fold the paper in where it belongs: its row in the table, its place in how the papers connect, and any open question it answers or raises. If it changes the picture, rewrite "Where it stands"; don't add a note at the end.
3. When a theme has at least two papers and no topic yet, create one. When a topic grows past about a dozen papers or splits into two questions, split it. Name a topic after its question or theme, not after a paper: `memory-structures.md`, not `memgpt-and-friends.md`.

A topic page looks like this:

```markdown
# <Topic>

<One or two sentences: the question or theme this topic covers.>

## Where it stands
## <A table that lays out the topic>
## How the papers connect
## Open questions
```

* **Where it stands:** a few sentences on the picture across the papers: what's settled, what's contested, and where the evidence is thin.
* **The table:** the topic at a glance, one row per approach, benchmark, or whatever splits the topic best, with the papers in each row. Pick the columns that fit the topic, such as key idea and trade-off for a method topic.
* **How the papers connect:** the story in order: what came first, who built on whom, who compared with whom and how it came out, where they disagree. Link the papers on every claim.
* **Open questions:** what the papers leave unanswered, especially what bears on my work, and where the library is thin.

## Update the index

Add the paper to the papers table, and update a topic's line if its picture changed. Update the reading list: add the papers this one builds on most that aren't in the wiki, and take this paper off the list if it was there.

## Many papers at once

For setup or a batch of papers, first read them all and write every paper page without connections. Then go over them together: work out the connections, settle the topics (three to six to start), write the topic pages, and write the index last. Seeing all the papers at once gives better topics than adding them one by one. For more than about ten papers, tell me how many there are before you start.

## Tell me

In a few sentences: what the paper does, which topics it landed in, and its most interesting connection, especially when it disagrees with something in the wiki or bears on my work. Link the paper page. Don't list every file you changed.
