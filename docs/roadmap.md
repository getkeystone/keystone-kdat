# Capability Roadmap

This roadmap reflects the state of the KDAT milestone ledger as of
2026-03-14, derived from branch lrfd-backend-bootstrap evidence.

It is organized by evidence quality, not by timeline. Do not treat
"In validation" items as delivered. Do not treat "Unknown / underdocumented"
items as planned unless separately confirmed.

---

## Historical baseline

These milestones predate the current tracked branch. They established the
foundation for all subsequent work.

| Milestone | Capability |
|-----------|-----------|
| KDAT-001A | Single-machine governed retrieval proof (fail-closed, citations, audit receipts) |
| KDAT-002 | Console operator workflow layer over governed retrieval |

---

## Branch-proven current work

These milestones are directly evidenced by commits on lrfd-backend-bootstrap.
Test scripts and smoke locks are cited on each milestone page.

| Milestone | Capability |
|-----------|-----------|
| KDAT-003 | Document governance UI + APIs |
| KDAT-008 | Case pack offline verifier + nested verification |
| KDAT-012 | Structured requirements extraction |
| KDAT-013 | Requirements hygiene + content_kind rerank + migration |
| KDAT-014 | Operator trust polish |
| KDAT-015 | Expanded spec-retrieval coverage + requirements evidence |
| KDAT-016 | Metadata sidecar always applies on SHA-match |
| KDAT-017 | Operator trust defaults with admin-only debug signals |
| KDAT-018 | Tighter operator trust defaults |
| KDAT-019 | Domain + content_kind governance |
| KDAT-020 | Suggested queries panel |
| KDAT-021 | Orphan sidecar CI gate |

KDAT-011 appears as a grouped milestone in the delivery table (console demo
mode + stack scripts). Its sub-milestones 011A, 011B, 011C are described in
the curated summary; 011C has partial branch evidence (admin-only label gate
verified by check-dist-leaks.sh).

KDAT-007 is listed in the delivery table but has no dedicated delivery commit;
it is doc-only.

---

## In validation (curated summary)

These milestones are described in curated summaries. No delivery commits for
these milestones appear in the current branch log. Status is "In validation"
pending direct verification.

| Milestone | Capability | Validation gap |
|-----------|-----------|---------------|
| KDAT-004 | Signed deterministic evidence bundles (Ed25519) | Branch commits not found in log |
| KDAT-005 | Approvals workflow for changes + evidence exports | Branch commits not found in log |
| KDAT-006 | Operator decision receipt + incident pack | Branch commits not found in log |
| KDAT-009 | Case timeline UI | Branch commits not found in log |
| KDAT-010 | Run it like a product (healthchecks, stack scripts) | Branch commits not found in log |
| KDAT-011A | Demo mode toggle + safe failure UX | Branch commits not definitively tagged |
| KDAT-011B | ProcedureCard UX upgrade | Branch commits not definitively tagged |
| KDAT-011C | One-command demo run | Partial branch evidence (check-dist-leaks) |

---

## Unknown / underdocumented

Numbers in the KDAT sequence with no evidence in this log.

- KDAT-001B through KDAT-001Z variants: not referenced in this log
- KDAT-011 variants beyond 011C: not referenced

---

## Likely next capability areas

Based on the arc from KDAT-003 through KDAT-021, areas not yet addressed
by any milestone:

- External identity integration (not proven by any current milestone)
- Multi-tenant isolation (not proven by any current milestone)
- Audit export for external compliance tooling (not proven)
- Deployment at scale beyond single-machine demo (not proven)
- Automated corpus ingestion pipeline beyond manual ops (partially addressed
  by corpus-ops scripts; no dedicated KDAT milestone)

These are observations from the evidence gap, not forward commitments.
