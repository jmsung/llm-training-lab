<!-- skeleton: optional/results/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# results/ — generated outputs

Pipeline **outputs**: figures, tables, metrics, model checkpoints. **Gitignored**
(appended to `cb/.gitignore` by `/project-start`) — regenerable by re-running the
code. Keep this README tracked so the empty dir survives clone.

The trio, kept distinct:
- **`data/`** — *inputs* (gitignored)
- **`results/`** — *generated outputs*: figures, tables, model artifacts (gitignored)
- **`reports/`** — *curated, committed* human-readable summaries of what the project produced

When a result is worth sharing, summarize it (with the key numbers inline) in a
`reports/` page and link back to the reproduce command — don't commit the raw output.

When you add a run here, record it in this README's contents list — the bytes stay
out of git, so nothing else does: `readme-contents.sh --describe <path>
'<what · how to reproduce>' <repo-root>`.

**Generated structures (`.cif`/`.pdb` from modeling/design)** are outputs → they live
here (recorded in the contents list), *not* in `knowledge/`. If one becomes reference-worthy
it earns a distilled **card** in `knowledge/entities/structures/`; routine run outputs
just stay here. Deposited/reference structures (public, re-fetchable) are *inputs* →
`data/structures/` instead (ADR 0010).
