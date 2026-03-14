# KDAT-005 — Approvals Workflow for Changes and Evidence Exports

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Not publishable yet

---

## Summary

A two-person approvals workflow governs document change requests and evidence
export gating, with TTL controls and role enforcement.

---

## What this milestone claims (curated summary)

- DB: `corpus_doc_change_requests` and `evidence_export_requests` tables; TTL and two-person control flags
- Backend: full change request lifecycle (submit, list, approve/reject/apply)
- Evidence export approvals gate ZIP downloads when `REQUIRE_EVIDENCE_APPROVAL` is set
- Console: admin approvals queue, custodian "propose change" form, evidence export request panel
- Tests: approval flows with and without `REQUIRE_EVIDENCE_APPROVAL`, regression coverage

---

## What this milestone does NOT prove

- Branch delivery commits for KDAT-005 do not appear in the lrfd-backend-bootstrap log
- "Two-person control" here means a workflow pattern, not a cryptographic enforcement scheme
- No formal compliance certification

---

## Public-safe claims

**Not available yet.** Validate branch evidence first.

If validated: "Document change requests require explicit approval before
applying. Evidence exports can be gated by a configurable approval workflow.
The system supports separation of custodian proposal from admin application."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md curated summaries section | Not independently verified |

---

## Verification and tests

Curated summary mentions: approval flow tests with and without `REQUIRE_EVIDENCE_APPROVAL`.
Not verified from branch evidence.

---

## Known limitations and caveats

- Curated summary only. Do not cite externally until evidence class is upgraded.

---

## Source basis

Curated summary from kdat-log.md. Not verified from branch commit evidence.

---

## Next action

Locate delivery commits. Validate test scripts. Upgrade evidence class.
