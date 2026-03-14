# Milestones

This directory contains one page per KDAT milestone.

---

## KDAT naming

KDAT stands for Keystone Deliverable Acceptance Test. Each number represents
a discrete capability that has been defined, built, and verified (or, in some
cases, described or referenced without full verification).

Sub-milestones (e.g., 011A, 011B, 011C) represent phases or aspects of a
single numbered milestone.

---

## Status values

| Status | Meaning |
|--------|---------|
| Proven | Branch delivery commits exist; tests cited; smoke locks in place |
| Historical baseline | Pre-branch established work; referenced as prior foundation |
| In validation | Curated summary exists; awaiting branch commit verification |
| Planned | Not yet started |
| Doc-only | Appears in documentation; no dedicated delivery commit |
| Curated summary | Described in human narrative; not verified from commit evidence |
| Underdocumented | Some evidence exists; insufficient to fully characterize |

---

## Evidence classes (brief)

| Class | Meaning |
|-------|---------|
| Proven on current branch | Delivery commits on lrfd-backend-bootstrap; test scripts cited |
| Historical baseline | Pre-dates the branch; referenced as prior established work |
| Curated summary | Human narrative only; no branch commits verified |
| Doc-only reference | Appears in docs; no dedicated delivery commit |
| Underdocumented | Some evidence exists; insufficient to characterize fully |
| Unknown | No evidence available |

Full definitions: [docs/evidence-classes.md](../docs/evidence-classes.md)

---

## Milestone index

### Historical baseline — Ready to publish (2)
- [KDAT-001A](KDAT-001A.md) — Single-machine governed retrieval proof
- [KDAT-002](KDAT-002.md) — Console operator workflow UX

### Branch-proven — Ready to publish (11)
- [KDAT-003](KDAT-003.md) — Document governance UI + APIs
- [KDAT-008](KDAT-008.md) — Case pack offline verifier
- [KDAT-012](KDAT-012.md) — Structured requirements extraction
- [KDAT-013](KDAT-013.md) — Requirements hygiene + content_kind rerank
- [KDAT-014](KDAT-014.md) — Operator trust polish
- [KDAT-015](KDAT-015.md) — Spec-retrieval generalization
- [KDAT-016](KDAT-016.md) — Metadata sidecar always applies
- [KDAT-017](KDAT-017.md) — Operator trust defaults
- [KDAT-018](KDAT-018.md) — Tighter operator trust defaults
- [KDAT-019](KDAT-019.md) — Domain + content_kind governance
- [KDAT-021](KDAT-021.md) — Orphan sidecar CI gate

### Branch-proven — Needs review (no smoke lock)
- [KDAT-020](KDAT-020.md) — Suggested queries panel (delivery commit exists; no regression lock)

### Doc-only
- [KDAT-007](KDAT-007.md) — Supervisor workflow (doc-only reference)

### In validation (curated summary)
- [KDAT-004](KDAT-004.md) — Signed deterministic evidence bundles
- [KDAT-005](KDAT-005.md) — Approvals workflow
- [KDAT-006](KDAT-006.md) — Operator decision receipt + incident pack
- [KDAT-009](KDAT-009.md) — Case timeline UI
- [KDAT-010](KDAT-010.md) — Run it like a product
- [KDAT-011A](KDAT-011A.md) — Demo mode toggle + safe failure UX
- [KDAT-011B](KDAT-011B.md) — ProcedureCard UX upgrade
- [KDAT-011C](KDAT-011C.md) — One-command demo run

---

Note: Some milestones (KDAT-007) are doc-only references. Some (KDAT-001A,
KDAT-002) are historical baselines. Some (KDAT-004 through KDAT-006,
KDAT-009 through KDAT-010) have curated summaries but no branch delivery
commits in the current log. Evidence class is the definitive signal.
