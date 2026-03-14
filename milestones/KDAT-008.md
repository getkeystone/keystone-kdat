# KDAT-008 — Case Pack Offline Verifier + Nested Verification

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

An offline case pack verifier validates signed case manifests, file hashes,
and nested incident packs. Determinism fixes ensure reproducible exports.

---

## What this milestone proves

- `verify_case_pack.py`: validates signed case manifest, file hashes, embedded incident packs
- `verify_evidence.py` and `verify_lib.py`: shared verifier library
- Determinism fixes in API for consistent export behavior
- Console case pages: `CasesListPage`, `CaseDetailPage` with offline verify note
- Deploy: case-pack verify wrapper scripts, smoke-web coverage
- Database migrations: initdb 06 (approvals), 07 (operator-decisions), 08 (incident-cases)
- `export-evidence.sh`, `gen-evidence-keys.sh` added

---

## What this milestone does NOT prove

- Production-scale case volume
- In-browser verification (explicitly out of scope; offline tool only)
- Full chain-of-custody from external system import

---

## Public-safe claims

"Keystone AI provides an offline case pack verifier that validates Ed25519-signed
manifests, file integrity, and embedded incident pack authenticity. Case exports
are deterministic. Verified by six test scripts covering determinism, tamper
detection, role gating, and nested incident pack verification."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API/tools delivery commit | keystone-gov `d7f85af` | feat(kdat-008) |
| Console delivery commit | keystone-console `9ae70ea` | feat(kdat-008) |
| Deploy delivery commit | keystone-deploy `39a6bb3` | chore(kdat-008) |

---

## Verification and tests

- `api/tests/test_case_pack_signature.sh`
- `api/tests/test_case_workflow.sh`
- `api/tests/test_incident_pack.sh`
- `api/tests/test_operator_decision.sh`
- `api/tests/test_evidence_approval.sh`
- `api/tests/test_evidence_signature.sh`

Tests cover: determinism, tamper signature, tamper content, tamper embedded
incident zip (exit code 5), role gating.

---

## Known limitations and caveats

- Offline verification only; no in-browser verification is provided or claimed
- Tested at demonstration scale

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
