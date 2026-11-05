# Ask

A question can be about one paper ("How does Zep decide a fact is outdated?"), several ("Who decides what gets stored in MemGPT and in A-MEM?"), a topic ("Where do the benchmarks disagree?"), or my own work ("Has anyone tested memory updates the way I plan to?"). It can also be what to read next, or writing: a related work section, a survey outline.

## Answer

1. Start from the wiki: the index, then the topic and paper pages that cover the question. Search the wiki for specific terms. When the question touches my own work, read my notes on it too.
2. When the wiki isn't detailed enough, go back to the paper in `library/`. If what you find belongs on its paper page, add it there too.
3. Answer in a few sentences, linking the paper pages behind each point. Separate what papers show from what you infer.
4. If the wiki doesn't cover the question well, say so plainly, and suggest the papers that would fill the gap, searching arXiv if needed. Don't stretch thin evidence.

## What to read next

When I ask what to read next, look for the papers that several papers in the wiki build on, compare with, or evaluate on, but that aren't in the wiki yet. Rank them by how many wiki papers point to them, and by how much they bear on what I'm working on. Give me two or three, each with its authors and year, its arXiv link, and one line on why.

## Keep what we settle

A good discussion shouldn't disappear into the chat. When one produces something lasting, keep it in the right place:

* **About the papers,** such as a new comparison, a connection the pages missed, or a sharper "Where it stands": fold it into the right topic or paper page. When it's a new question that several papers speak to, make it a topic. Then update the dashboard's data, as in [maintain.md](maintain.md).
* **My own ideas,** such as what I make of a paper, an experiment I want to run, how my work differs from the others, or a direction I've taken up or dropped: write it in `notes/`. One idea per note, named after it, like `notes/retire-delete-or-decay.md`, with the idea itself as the title. Start with the idea in a few sentences, then what it rests on, linking the paper and topic pages, then what's still open. Keep my reasoning, not our back-and-forth. When an idea comes up again and changes, rewrite its note instead of adding to the end. If it changes what I'm working on, offer to update profile.md.

Tell me in one line what you kept and where.

Passing questions need none of this. While we're still going back and forth, wait until the discussion settles before writing anything.

## Writing

When I ask for writing of my own, like a related work section or a survey outline, save it as a note, `notes/<short-name>.md`, and link it in your reply. Short things, like a reading list for a new labmate, stay in Chat unless I ask you to save them.

* Write from the wiki, organized by idea, not paper by paper. The topic pages already have the structure.
* Cite papers as (First author et al., year) and list them at the end with their arXiv links.
* When it's for my own paper, place my work against the others: what it shares with them and where it differs, from my notes on it.
* Before saving, check every claim against the paper page it comes from, and every number against the paper.
