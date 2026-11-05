<!-- skeleton: optional/reports/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# reports/ — discoveries, status & final report

Committed, human-readable summaries of **what this project produced** — findings,
result write-ups, the curated status of the work, and the final report. The
shareable record for the team (vs `docs/` = how the repo works, vs `results/` =
regenerable outputs, vs the private working notes kept outside this repo).

Two front-doors:

- [`project-status.md`](project-status.md) — the **living board**: single source of
  truth for progress (shipped / active / on hold / exploratory / superseded).
  `/branch-done` drafts candidate entries on each branch before merge, so they ride
  the PR; you pick what lands, so it stays curated and publishable instead of drifting.
- [`project-report.md`](project-report.md) — the **final narrative report**:
  publication-grade writeup (abstract, methods, results, discussion). Grows as the
  project matures; the natural draft substrate for a paper or a handoff document.

Individual findings live alongside these as their own files and are linked from
the status report.

| Folder | Holds | Git |
|---|---|---|
| **`reports/`** | curated discoveries/findings + status + final report | committed |
| `docs/` | how the repo works — architecture, ADRs, specs | committed |
| `data/` | inputs the code reads | gitignored |
| `results/` | regenerable pipeline outputs (figures, data) | gitignored |

Keep reports small — embed key numbers/tables inline so they render without the
gitignored data; link to provenance + a reproduce command rather than pasting
large outputs. Both front-doors render to HTML/PDF/LaTeX via the pandoc block in
each file's Publishing section.
