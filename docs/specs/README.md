<!-- skeleton: cb/docs/specs/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# docs/specs/ — feature roadmaps

Dated records of feature plans: long-term milestones spanning dev → test →
production. A spec is to a *feature* what an ADR is to a *decision* —
status-tracked (`draft → approved → in-progress → done → superseded`),
frozen after the fact.

Planning hierarchy (cite, don't copy):

    docs/specs/<spec>.md      the roadmap — milestones, official, reviewable
    (workstream note)         one milestone = one branch = one workstream; the
                              note is private, kept outside this repo
    knowledge/wiki/           validated lessons after execution (/wiki-learn)

Optional by design — solo single-branch work needs no spec, just a private
workstream note. Create a spec when someone other than you must review or
rediscover the plan.
**No spec when an ADR already carries the plan** — specs are for roadmaps with
no other durable home; duplicating an ADR's milestones just rots. Cite, don't copy.
`/branch-done` flips milestone checkboxes on merge.

Structure: `Status:` header (`draft → approved → in-progress → done →
superseded`) → milestone checklist → one section per milestone (scope,
acceptance, linked branch).
