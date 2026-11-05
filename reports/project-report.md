# llm-training-lab — project report

The **final, narrative report** for this project — the publication-grade writeup
of what was done, what was found, and what it means. Where `project-status.md` is
the living board (what's shipped / active / parked), this is the *result*: methods,
findings, figures, and conclusions, written to be read start-to-finish by someone
outside the project (a collaborator, reviewer, or your future self).

- **Last updated:** 2026-11-05
- **Author:** Jongmin Sung
- **Status:** draft <!-- draft | under review | published -->

> Grows as the project matures — often empty or skeletal early, filled in as
> results firm up. Pull numbers/figures from `results/` (embed key values inline so
> the doc renders without the gitignored data) and cite provenance + a reproduce
> command. When it's ready to share, render a snapshot (see [Publishing](#publishing)).
> For a paper, this is the natural draft substrate; for an internal project, it's
> the handoff document.

## Abstract / TL;DR

<!-- 3-5 sentences: the problem, what you did, the headline result, why it matters. -->

## Background & motivation

<!-- Why this project exists; prior art; the gap it addresses. -->

## Methods / approach

<!-- What you built and how. Enough detail to reproduce or critique. Link docs/specs for depth. -->

## Results

<!-- The findings. Embed key numbers/tables inline; link figures in results/ with a reproduce command. -->

## Discussion

<!-- What the results mean, limitations, threats to validity, surprises. -->

## Conclusion & next steps

<!-- The takeaway and what a follow-on would do. -->

## References

<!-- Citations, linked artifacts, related reports/wiki pages. -->

---

## Publishing

This file is the canonical Markdown. To produce a shareable snapshot:

```bash
# Self-contained HTML
pandoc reports/project-report.md -o project-report.html --toc --standalone

# LaTeX (for inclusion in a paper)
pandoc reports/project-report.md -o project-report.tex

# PDF — needs a PDF engine (one-time: brew install typst)
pandoc reports/project-report.md -o project-report.pdf --toc --pdf-engine=typst
```

Don't hand-maintain a `.tex`/PDF copy — render it from this file when you need one.
