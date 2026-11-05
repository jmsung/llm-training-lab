<!-- skeleton: cb/knowledge/entities/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# entities/ — project-local entities

Specific-shape entities this project owns — each with its own frontmatter schema —
that are **not** part of the shared readings corpus and are **never synced to
central**. The local counterpart to `source/` (readings). Organized by
**kind-subfolder** (the one place folder-by-kind is used, because entity kinds carry
radically different schemas and nothing here is routed):

```
entities/
  structures/   macromolecular structures — pdb-<id>.md  (kind: structure; pdb_id/resolution/method)
  compounds/    small molecules           — <name>.md    (kind: compound; chembl_id/smiles)
  datasets/     bespoke project datasets  — <name>.md    (kind: dataset)
```

**Cards only — no binaries.** Each file is a distilled `.md` provenance card. The
actual raw file lives **outside `knowledge/`** (ADR 0010, extends D4):
- **deposited / reference** (public, regenerable, e.g. an RCSB `.cif`) → **`data/structures/`**
  (gitignored cache; re-fetch by `pdb_id` with a repo script). The card's `source_local:`
  points there.
- **generated / design** (your model's output — the work product, not regenerable) →
  **`results/<pipeline>/`** (recorded in `results/README.md`'s contents list).

Placement of the *cards*: **public** entities live in the program's commons repo and are
*referenced* by others (not synced); **private/unpublished** entities stay in the specific
working repo with `confidentiality: private|lab`. Central (knowledge-base) has **no**
`entities/` leaf — entities are repo-specific.

`entities/` is often empty in a fresh repo — create a `<kind>/` subfolder only when you
have that kind of entity.
