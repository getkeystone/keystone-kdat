# Timeline

This timeline is derived from commit dates on lrfd-backend-bootstrap
(2026-03-13 through 2026-03-14) and from the position of historical
baseline milestones.

Dates shown are approximate commit dates from the evidence log.
Earlier milestones predate the branch and do not have recorded dates
in this log.

---

## Historical baselines (pre-branch)

These milestones have no commit dates in the current evidence log.
They establish the foundation all subsequent work builds on.

- **KDAT-001A** — Single-machine governed retrieval proof
- **KDAT-002** — Console operator workflow UX

---

## Curated-summary milestones (ordering approximate)

These appear in the curated summary in this order, suggesting approximate
delivery sequence. Branch commits are not directly available for these.

- **KDAT-003** — Document governance UI + APIs *(later confirmed as branch-proven)*
- **KDAT-004** — Signed deterministic evidence bundles
- **KDAT-005** — Approvals workflow
- **KDAT-006** — Operator decision receipt + incident pack
- **KDAT-007** — Supervisor workflow *(doc-only on this branch)*
- **KDAT-008** — Case pack offline verifier *(branch-proven: 2026-03-13)*
- **KDAT-009** — Case timeline UI
- **KDAT-010** — Run it like a product
- **KDAT-011A/B/C** — Demo mode, ProcedureCard, one-command demo run

---

## KDAT-011 grouping note

The delivery table in the evidence log treats KDAT-011 as a single grouped
milestone with commits in keystone-console (`3112590`) and keystone-deploy
(`1f22624`), both dated 2026-03-13. The curated summary subdivides this into:

- **KDAT-011A**: Demo Mode toggle + safe failure UX
- **KDAT-011B**: ProcedureCard presentation
- **KDAT-011C**: One-command demo run (`demo-run.sh`)

This subdivision is a narrative description, not commit-level evidence. The
011A, 011B, 011C pages carry "Curated summary" evidence class. Only 011C has
partial branch evidence (admin-only label gate via check-dist-leaks.sh and
the `a377ff8` / `b026186` console commits).

Do not conflate the grouped KDAT-011 delivery table entry with the sub-milestone
pages as if they were independently proven milestones.

---

## Branch-proven milestones (lrfd-backend-bootstrap, 2026-03-13 to 2026-03-14)

| Date (approx) | Milestone | Summary |
|---------------|-----------|---------|
| 2026-03-13 | KDAT-003 | Document governance APIs + console UI |
| 2026-03-13 | KDAT-008 | Case pack offline verifier |
| 2026-03-13 | KDAT-011 | Demo mode + stack scripts (grouped) |
| 2026-03-13 | KDAT-012 | Structured requirements extraction |
| 2026-03-13 | KDAT-013 | Requirements hygiene + content_kind rerank |
| 2026-03-13 | KDAT-014 | Operator trust polish |
| 2026-03-13 | KDAT-015 | Spec-retrieval generalization |
| 2026-03-13 | KDAT-016 | Metadata sidecar always applies |
| 2026-03-13 | KDAT-017 | Operator trust defaults |
| 2026-03-13 | KDAT-018 | Tighter operator trust defaults |
| 2026-03-13 | KDAT-019 | Domain + content_kind governance |
| 2026-03-13 | KDAT-021 | Orphan sidecar CI gate |
| 2026-03-13/14 | KDAT-020 | Suggested queries panel |

---

## Evidence log metadata

- Branch: lrfd-backend-bootstrap
- Log generated: 2026-03-14T13:27:36Z
- keystone-gov HEAD: `93aa470`
- keystone-console HEAD: `8f7abd5`
- keystone-deploy HEAD: `3dbaaa0`
