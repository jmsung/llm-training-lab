# knowledge/wiki/

Synthesized, curated pages — the usable output of the knowledge layer.
qmd-indexed; queried via `/wiki-query`, grown via `/wiki-learn` and manual
curation. Universal primitives (shipped with this skeleton — fill the `{{...}}`
placeholders):

- `home.md`  — narrative front door (start here)
- `index.md` — catalog of every page
- `log.md`   — append-only event trail (ingests, promotions, lints)

Categories (`findings/`, `concepts/`, `reference/`, …) emerge per project —
see `../.claude/CLAUDE.md` for structure, frontmatter schema, and conflict rules
(the self-contained, authoritative copy). Only validated knowledge lands here —
plans live in `docs/specs/`; private scratch and drafts stay out of the wiki.
