# llm-training-lab — Knowledge Conventions

This file governs the project knowledge base: `knowledge/wiki/` (resolves to
`cb/knowledge/wiki/`, or — when the manifest sets `knowledge: mb`, meaning the
knowledge is kept private rather than shipped with cb — to a private location
outside this repo, via a symlink).
For code conventions, see the repo CLAUDE.md.

> **This file is the authoritative, self-contained instantiation of the knowledge
> conventions** — it ships into the repo and governs an agent working here even
> with no access to harness. Rationale and canonical schema live in
> `harness/docs/knowledge-harness.md`; the conflict cascade, frontmatter schema,
> nav-link rule, and agent instructions are mirrored there — edit both together.
> Trim freely: delete the rows, rules, and sections this project doesn't use.

## Knowledge structure

Hierarchical levels + source quality. Use only what the project needs — a small
wiki stays flat (home/index/log plus a few pages); adopt levels as content
accretes. Delete the rows you don't use.

| Level | Name | Example |
|---|---|---|
| L0 | Axiom | axioms.md — foundational rules; changes require human approval |
| L1 | Finding | findings/ — validated cross-cutting patterns (one file per theme) |
| L2 | Strategy | per-topic strategy.md — operational heuristics, recipes |
| L3 | Observation | experiment logs, session notes |
| L4 | Source | ingested papers, external docs, datasets/models (see `../source/`) |

Source-quality axis: at the same level, `published_paper` > `agent_analysis` > `experiment_note`.

## Conflict resolution

This cascade is an **editable default — reorder or delete rules to fit this wiki;
the trimmed list below IS this project's conflict policy.** (Source-quality wikis
lead with provenance; hierarchical with level; temporal/product with recency.)

0. **`supersedes:`** — if page B lists A in `supersedes:`, A is historical-only.
   An explicit author decision; it wins outright. Don't edit superseded pages.
1. **Lex superior** — higher `level` wins (L0 > L1 > … > L4).
2. **Source-quality** — *at the same level*, `published_paper` > `agent_analysis` > `experiment_note`.
3. **Lex specialis** — all else equal, the more specific page wins.
4. **Lex posterior** — last resort, newer wins, by **`git log`** (commit recency);
   never by `created:`/`updated:` frontmatter (banned).

Multiple L3 observations contradicting an L1 finding → surface in log.md and
escalate to human. The cascade decides which page is authoritative; the human
decides the actual edit. Do NOT auto-override or silently resolve.

## Common directories

Create as needed — not all directories are required from the start:

```
knowledge/
├── source/               ← flat readings corpus, in git — papers/blogs/repos + datasets/models
│                            (kind: distinguishes; pulled + native; ADR 0010, data/ leaf retired)
├── entities/<kind>/      ← project-local entities (structures/compounds/datasets); cards
│                            only — raw files live at the cb root, in data/ (deposited)
│                            or results/ (generated), never under knowledge/
│                            (no raw/ leaf here: it is central-only, ADR 0010 D6)
├── pins.yaml             ← adoption record (ADR 0011): mode: pull|push + the pinned
│                            cards /kb-sync pull materializes; new repos ship mode: pull
└── wiki/
    ├── home.md           ← entry point (project overview, where to start)
    ├── index.md          ← catalog of all pages (always present)
    ├── log.md            ← append-only event trail (always present)
    ├── sources.md        ← optional: external sources (Drive, web)
    ├── axioms.md         ← optional: L0 rules (hierarchical wikis)
    ├── reference/        ← curated per-source entity pages
    ├── findings/         ← L1 validated patterns (one file per theme)
    ├── concepts/         ← optional: conceptual pages
    └── {{topic-slug}}/   ← optional: per-topic pages or subdirectories
                            (flat wikis use plain pages; research-style uses
                             subdirs with strategy.md + experiment logs)
```

Every harness dir ships a placeholder README describing its role; the wiki
seeds (home/index/log) ship filled-in with `{{...}}` placeholders.

## Frontmatter

```yaml
---
level: {{0-4}}        # hierarchical wikis — validation status; omit on flat wikis
cites:                # ONLY when the body links another directory; root-relative from wiki/
  - findings/foo.md
source_type: {{type}} # optional — published_paper | agent_analysis | experiment_note
supersedes:           # temporal wikis — root-relative pages this replaces (historical-only)
  - reference/old-page.md
# Provenance (added by /kb-ingest on source/ pages):
# type, source_url, source_local, source_drive, author
---
```

`level` (validation status) and `source_type` (provenance) are independent axes.

Conventions:
- `cites:` is **conditional, cross-directory only** — add it only when the body
  links a page in a different directory. Siblings don't need cites.
- Paths in `cites:`/`supersedes:` are **wiki-root-relative** from `wiki/` (e.g.,
  `findings/foo.md`, not `../findings/foo.md`) — file-relative paths trip lint.
- Every `[[cross-directory]]` link in the page **body** needs a matching `cites:`
  entry — the `[[home]] | [[index]]` nav line is exempt.
- No `created:` or `updated:` fields — use `git log`.
- YAML files use `# cites: ...` comments instead of frontmatter.

## Nav links

Every page gets a nav line right after the frontmatter closing `---`:
- Root pages: `[[home]] | [[index]]`
- Subdirectory pages: `[[../home]] | [[../index]]`

**`[[wikilinks]]` are wiki-internal only.** They resolve relative to this `wiki/` dir and are
checked only here. Anything outside it — `cb/docs/`, README, or any file kept outside the
artifact — cites a wiki page **by path** (`knowledge/wiki/<page>.md` from cb root), never `[[…]]`.

## Agent instructions

1. **Search first for lookups; orient via home/index for curation.** Use
   `/wiki-query` to *find* things; read home.md then index.md to *orient*.
2. **Follow `cites:` links** to navigate related pages.
3. **When creating or modifying a page**, update index.md and append to log.md in
   the same action. For a manually created page, add the nav line and re-embed qmd
   (`qmd embed -c ${PROJECT}-knowledge`) so search sees it.
4. **When ingesting a source**, use `/kb-ingest` — it files a flat card with a
   `domains:` list + `kind:` (no `primary:`/`tags:`). Where the card lands follows
   `../pins.yaml`: in a `mode: pull` repo (the default for a new project) it is
   written **upstream** to knowledge-base, pinned here provisionally, and pulled
   back into `../source/`; in a `mode: push` repo (or with no `pins.yaml`) it is
   written straight to `../source/` (ADR 0011 D8). Don't inline summaries into
   wiki pages; cross-source synthesis goes in `wiki/`.
5. **Never write `../source/` without explicit per-artifact human
   approval.** Ingest is human-gated; `source/` cards are regen-able (and synced
   copies are read-only) — don't hand-edit.
6. **When you find a contradiction**, append to log.md and apply the conflict
   cascade above. The cascade decides which page is authoritative; you don't
   silently resolve, and the human decides the actual edit.
7. **Respect level and source weighting where used.** An L0 axiom outweighs any
   number of L3 observations; cite the source type when making claims. (Skip on
   flat wikis.)
8. **Promote good answers to pages — via `/wiki-answer`.** Reusable synthesis →
   findings/ or the appropriate location. `/wiki-query` never writes; re-run the
   question as `/wiki-answer` (or `/kb-answer` for corpus questions) so the page
   lands with its nav line, index entry, and log entry.
9. **Keep axioms.md small** (hierarchical wikis only). If unsure whether something
   is L0, it's L1 at most.
