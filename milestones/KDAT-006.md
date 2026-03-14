# KDAT-006 — Operator Decision Receipt + Incident Pack

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Not publishable yet

---

## Summary

Operators record decisions against guidance queries. Officers can export
deterministic signed incident packs gated by role and optionally approvals.

---

## What this milestone claims (curated summary)

- DB: `operator_decisions` table (unique by query_id)
- Backend: create decision, get decision, supervisor review patch
- Incident manifest + deterministic signed incident pack ZIP, role-gated (officer/admin)
- Console: Operator Decision panel on Guidance page, decision card on Audit page, incident pack export button
- Tests: decision creation/validation, incident pack gating, determinism, tamper verification

---

## What this milestone does NOT prove

- Branch delivery commits for KDAT-006 do not appear in the lrfd-backend-bootstrap log
- "Signed" refers to Ed25519 manifest signing (from KDAT-004); this milestone extends that capability

---

## Public-safe claims

**Not available yet.** Validate branch evidence first.

If validated: "Operators record decisions against AI guidance. Officers export
signed, deterministic incident packs. Role gating enforces who can create
and export incident records."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md curated summaries section | Not independently verified |

---

## Verification and tests

Curated summary mentions: decision creation/validation, incident pack gating,
determinism, tamper verification. Not verified from branch evidence.

---

## Known limitations and caveats

- Curated summary only. Do not cite externally until evidence class is upgraded.

---

## Source basis

Curated summary from kdat-log.md. Not verified from branch commit evidence.

---

## Next action

Locate delivery commits. Validate test scripts. Upgrade evidence class.
