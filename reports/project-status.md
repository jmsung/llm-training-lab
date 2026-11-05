# llm-training-lab — project status

**Single source of truth** for what this project has shipped, what is in progress,
and what is parked. Curated for the team; the public-facing projection of the
maintainer's private working board — every entry carries a status and links
to its evidence (PR / branch / report / issue).

- **Last updated:** 2026-11-05
- **Maintainer:** Jongmin Sung

> **Keeping this current — updated in every PR.** Before review, `/branch-done`
> drafts candidate entries from the branch's outcome and asks **which to fold in** —
> you pick what lands (this report is publishable, so it stays curated). Selected
> entries go under the right status section, cite the branch (the next `/report` swaps
> in the PR number), and ride the PR. *Last updated* moves only when `/report` gathers everything since
> it, so no merge drops out of the next gather. When work is parked, name *what it is gated on*. When abandoned, move it
> to **Superseded** with one line of why. To share externally, render a snapshot
> (see [Publishing](#publishing)).

## Status legend

| Mark | Status | Means |
|---|---|---|
| ✅ | **Shipped & validated** | merged to `main`, has a committed result or report |
| 🔬 | **Active** | in-flight worktree; next step + blocker noted |
| ⏸ | **On hold** | gated — the gate is named (data, dependency, upstream decision) |
| 🧪 | **Exploratory** | RFC / spec; direction proposed, not yet committed |
| 🗑 | **Superseded** | retired or obsolete — one line on why |

---

## Overview

<!-- One paragraph: what this project is and the current focus. -->

## ✅ Shipped & validated

<!-- - **Headline outcome.** One line + key result. → report link · (PR #…), or (`<branch>`) until /report swaps it -->

## 🔬 Active

<!-- | Workstream | What | Next step / blocker | -->

## ⏸ On hold — and what unblocks each

<!-- - **name** — gated on <what>. → issue/doc link -->

## 🧪 Exploratory — proposed, not committed

<!-- - **name** (RFC/spec) — one line. → docs/specs or docs/rfc link -->

## 🗑 Superseded / obsolete

<!-- - **name** — retired because <why>. -->

---

## Roadmap

<!-- Optional: milestone table or ordered list of the next phases. -->

---

## Publishing

This file is the canonical Markdown. To produce a shareable snapshot:

```bash
# Self-contained HTML — no extra tooling beyond pandoc
pandoc reports/project-status.md -o project-status.html --toc --standalone

# LaTeX (for inclusion in a paper)
pandoc reports/project-status.md -o project-status.tex

# PDF — needs a PDF engine installed first (one-time):
#   brew install typst          # lightest; then:
pandoc reports/project-status.md -o project-status.pdf --toc --pdf-engine=typst
#   (or a full LaTeX install for the default pdflatex engine)
```

Don't hand-maintain a `.tex`/PDF copy — render it from this file when you need one.
