<!-- skeleton: cb/knowledge/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# knowledge/

Domain knowledge that accretes independently of the code. Hybrid-authored via
human-gated skills (`/kb-ingest`, `/wiki-learn`, `/kb-sync`); indexed by qmd.

- `source/<stem>.md` — the **readings corpus** (flat, ADR 0010). Distilled cards for
  papers/blogs/repos/sites/talks **and datasets/models** — pulled from knowledge-base
  *and* native. `kind:` frontmatter distinguishes card types; routed by the `domains:`
  frontmatter list. See [`source/README.md`](source/README.md). (Per the ADR 0010 D1
  amendment the `data/` leaf is retired: datasets/models are `source/` cards; entities
  with an exotic schema — structures/compounds — are project-local, never central.)
- `entities/<kind>/` — **project-local** specific-shape entities (structures /
  compounds / datasets), kind-subfoldered. Distilled `.md` **cards only** — the raw
  file lives *outside* `knowledge/` (`data/structures/` for deposited/reference,
  `results/` for generated). Never synced to central. See [`entities/README.md`](entities/README.md).
- `wiki/` — synthesized, curated pages (findings, concepts, per-topic synthesis).
  In git, qmd-indexed. This is where cross-source synthesis lives.
- `pins.yaml` — the **adoption record** (ADR 0011). A project is born `mode: pull` with
  `pins: []`: it searches the whole central corpus but holds only the cards it has proven it
  needs. `/kb-answer` pins a card when a page here cites it (the citation is the receipt);
  `/kb-ingest` pins a newly-ingested card provisionally until a page does. `/kb-sync pull
  <proj>` then materializes exactly the pinned cards into flat `source/`. The sync is
  **source-only** — `raw/` full text stays in knowledge-base and on Drive; a synced card's
  `source_url` + `drive_file_id` are how you get back to it.

**No binaries in `knowledge/` — only distilled `.md` cards.** Raw files (`.cif`/`.pdb`/
`.sdf`/PDF) live in `data/` (inputs the project consumes) or `results/` (outputs it
produces); the card points to them via `source_local:`/manifest (ADR 0010, extends D4).

The permitted leaves here are exactly `{source, entities, wiki}` — there is **no `raw/`
leaf** in a project (it is central-only; the fan-out is source-only since 2026-08-03).
The set is declared as `KS_REPO_LEAVES` in harness `scripts/lib/knowledge_sync.sh` and
enforced by `knowledge-shape-lint`.

There are **no `domains/<domain>/` folders** — routing is by `domains:` frontmatter
(ADR 0010, superseding the domain-nested shape of ADR 0009 D1). No `primary:`/`tags:`
on corpus cards; `kind:` is frontmatter, never a folder.

Boundary test: "reusable knowledge I'd retrieve regardless of this code" → here.
Decision rule for placement (`knowledge: cb | mb` in the manifest): "if a
teammate cloned cb, should they get this knowledge?" Yes → this is a real dir.
No → this path is a symlink to a private location outside the repo, excluded
via the clone's `info/exclude` (skill-written).
