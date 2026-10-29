# Keep the Dashboard Current

The dashboard is `index.html`, an index of the wiki: every topic with the papers that speak to it, every paper with its main point and topics, how the papers connect, and my progress. Every name on it opens its page. It can't read the pages, so what it shows comes from `assets/wiki.json`, and keeping that file in line with the wiki is your job. The wiki stays the source: every line in the JSON is a short version of something already on a page. StashBase shows the change within a couple of seconds, even while the dashboard is open.

## When to update it

* **After adding papers:** the papers, their topics and connections, and any topic or reading list change. This is the last step of [add.md](add.md).
* **After folding an answer back into the wiki:** a new or renamed topic, a changed status, or a new connection.
* **At setup:** replace the example with the new wiki, and leave out `example`.
* **At a check-up:** compare the JSON with the pages and the index, and fix every mismatch.

## Editing rules

* Keep it valid JSON. Change only what you need, and leave every other field as it is, including fields not listed here.
* A paper's `id` is its page name, like `2025-zep`, and a topic's `id` is its page name, like `memory-structures`. The dashboard links to `wiki/papers/<id>.md` and `wiki/topics/<id>.md`, so the ids must match the files.
* Don't change `schemaVersion` or `index.html`.

## Format

```json
{
  "example": true,
  "area": "Agent memory",
  "focus": "Memory that stays correct when facts change.",
  "topics": [{ "id": "memory-structures", "name": "How memory is organized", "status": "thin", "standing": "..." }],
  "papers": [{ "id": "2025-zep", "title": "Zep", "year": 2025, "added": "2026-10-27", "topics": ["memory-structures"], "oneLine": "..." }],
  "connections": [{ "from": "2025-zep", "to": "2024-longmemeval", "type": "evaluated-on", "note": "..." }],
  "readingList": [{ "title": "...", "authors": "Xu et al., 2021", "url": "https://arxiv.org/abs/...", "why": "..." }]
}
```

* `example` is `true` only while the template's example is in place; the dashboard then also tells people to say "Set me up." Setup removes it.
* `area` is the index's title, and `focus` is the first sentence of "What I'm working on" in profile.md.
* `topics` follow the index's topics table. `status` is `settled`, `contested`, or `thin`, from the page's Status line, and `standing` is the topic's line in the table.
* `papers` follow publication order. `year` is the year of the page name. `added` is the date the page was written, which the progress chart uses to draw the total over time. `topics` match the page's Topics line. `oneLine` is the paper's line in the index's papers table, shown as its main point, so keep it to one short sentence.
* `connections` hold each connection once, in one direction: `builds-on`, `compared-with`, `evaluated-on`, `critiques`, `disagrees-with`, or `alternative-to`. The dashboard shows the reverse side by itself, like "Benchmark for" or "Critiqued by", so "Built on by" on a page is a `builds-on` from the other paper. `note` is the connection's line on the page, shortened.
* `readingList` matches the index's reading list.
