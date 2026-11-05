# llm-training-lab

Hands-on pretraining and post-training (SFT, DPO, GRPO) of small LLMs, published with costs and before/after numbers.

## Layout

Python: `src/llm_training_lab/` (shared helpers), `scripts/` (training and eval runs), `tests/`, `results/` (gitignored outputs), `reports/` (written-up findings).
<!-- /project-start fills code dirs per language: Python → src/<pkg>/, scripts/, tests/; Node → src/, test/. -->

### `cb/` — the artifact you ship (code + docs + knowledge)

| Dir | Scope / definition | Git |
|---|---|---|
| `src/<pkg>/` | importable **library code** — the package you'd `import` | committed |
| `scripts/` | **entry points** & one-off orchestration (hardcoded paths OK) | committed |
| `tests/` | test suite | committed |
| `notebooks/` | exploratory analysis (optional) | committed |
| `docs/` | **how THIS artifact works** — architecture, `adr/` (decisions), `specs/` (roadmaps) | committed |
| `knowledge/` | **reusable domain knowledge**, independent of the code (see leaves below) | committed (skill-managed) |
| `data/` | **inputs the code consumes** — datasets, deposited structure files (`data/structures/*.cif`) | gitignored (READMEs tracked) |
| `results/` | **generated outputs** — figures, tables, checkpoints, model-designed structures | gitignored (READMEs tracked) |
| `reports/` | **curated, committed writeups** of what the project produced — status board + final report | committed |

### `cb/knowledge/` — the corpus (ADR 0010; **distilled `.md` cards only, no binaries**)

| Leaf | Scope / definition |
|---|---|
| `source/` | **reading** distill cards — paper/repo/web/blog **and** shareable datasets/models (`kind:` distinguishes); routed by the `domains:` frontmatter list |
| `entities/<kind>/` | **repo-local entities** — structures/compounds/datasets, kind-subfoldered. Cards only; the raw file lives in `data/` (deposited) or `results/` (generated). Never synced to central. |
| `wiki/` | **synthesis** — curated pages (findings, concepts). qmd-indexed. |

**The distinctions that trip people up:** `data/` = **inputs**, `results/` = **generated outputs** (both gitignored); `reports/` = **curated, committed** writeups. `docs/` explains *the code*; `knowledge/` is *reusable knowledge* independent of the code. **Binaries never live in `knowledge/`** (cards only) — a structure's `.cif` goes to `data/structures/` (deposited) or `results/` (generated).

Every directory carries a `README.md` describing its role.

## Setup

```bash
uv sync   # e.g. uv sync · npm install
```
