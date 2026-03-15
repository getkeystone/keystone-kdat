# Milestones

This directory contains one page per KDAT milestone.

---

## What KDAT means

**KDAT = Keystone Delivery Acceptance Test**

A KDAT is a numbered Keystone milestone with explicit scope, verification, evidence quality, and publication status. The KDAT sequence is used to track what is historically established, what is proven on the current branch, what is still under review, and what is not yet safe to claim publicly.

## KDAT naming

KDAT stands for Keystone Delivery Acceptance Test. Each number represents
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

### Branch-proven — Ready to publish (15)
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
- [KDAT-022](KDAT-022.md) — Backup + restore with smoke verification
- [KDAT-023](KDAT-023.md) — Evidence signing key custody + rotation + trust store
- [KDAT-024](KDAT-024.md) — Operational scope guard + CLARIFY_MODEL clarifier
- [KDAT-025](KDAT-025.md) — Cloudflare Access smoke proof

### Branch-proven — Needs review (3)
- [KDAT-020](KDAT-020.md) — Suggested queries panel (delivery commit exists; no regression lock)
- [KDAT-026](KDAT-026.md) — Public demo reset timer (systemd timer; environment-dependent verification)
- [KDAT-027](KDAT-027.md) — KDAT log publisher + external CF smoke timer (timer fire confirmed on live system; not CI-verifiable)

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

Ledger currently covers KDAT-001A through KDAT-027. Publication readiness
varies by milestone; see individual pages.
