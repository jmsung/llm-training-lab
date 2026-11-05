<!-- skeleton: cb/knowledge/source/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# knowledge/source/

The **readings** leaf of the flat, tag-routed corpus (ADR 0010, superseding the
domain-nested shape of ADR 0005 / 0009 D1) — one distilled `<stem>.md` card per
external artifact. Flat: **no `domains/<domain>/` subfolders, no `kind:` folders**.

```
source/<stem>.md   ← distilled reading card, in git; qmd-indexed
```

- `kind:` frontmatter distinguishes reading types (`paper | blog | repo | site |
  talk`) — a blog and a paper sit side by side here. `kind:` is never a folder.
- `domains:` frontmatter (a **list**) does all routing — one card routes to every
  subscriber whose domain appears in the list, with zero duplication. **No
  `primary:`, no `tags:`** on corpus cards (ADR 0010 D3).
- Full text does **not** live here — `raw/` is a central-corpus leaf, not a project
  one (source-only fan-out since 2026-08-03, ADR 0010 D6). Get back to the original
  through the card's `source_url` / `drive_file_id`. Entities go in `../entities/`;
  their raw files at the cb root, in `data/` (deposited) or `results/` (generated) —
  written here as `../../data/` / `../../results/` relative to a card in this leaf.

Two ways content lands here:

1. **Pulled from knowledge-base** — `/kb-sync pull` copies exactly the cards pinned in
   `../pins.yaml`, each stamped *"synced from knowledge-base — do not edit"*. Read-only
   here; fix upstream and re-pull. (A `mode: push` repo instead receives every upstream
   card whose `domains:` intersects its subscription — ADR 0011 D6.)
2. **Native distillations** — in a `mode: pull` project (the default a new repo ships
   with) `/kb-ingest` writes the card **upstream** and it comes back through (1),
   pinned provisionally (ADR 0011 D8). Only a `mode: push` repo — or one with no
   `pins.yaml` at all — has `/kb-ingest` file its readings straight into this leaf
   (set `domains:` + `kind:`). Synthesis across sources belongs in `../wiki/`, not here.

Domain values come from the knowledge-base enum. A pull-mode project searches the whole
central corpus (ADR 0011 D7); its `downstream.yaml` entry only enumerates it for the
fan-out. `base` (`ai-agents`) is implicit.
