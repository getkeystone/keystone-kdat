# Artifact — KDAT-008

**Milestone:** [KDAT-008](../../milestones/KDAT-008.md)
**Artifact readiness:** Needs review

---

## What artifact exists

Case pack verifier tools (`verify_case_pack.py`, `verify_evidence.py`,
`verify_lib.py`) and six test scripts covering determinism, tamper detection,
and role gating.

---

## What it proves

- Offline verification of Ed25519-signed case manifests
- File hash integrity checking
- Nested incident pack verification
- Tamper detection (exit code 5 on content tamper)

---

## What it does not prove

- In-browser verification
- Verification of case packs from external systems

---

## Public-safe artifact candidates

- Sanitized copies of the verification tools (no internal hostnames or
  credentials)
- A public-safe summary of the verification protocol

---

## Publication readiness

**Needs review.** Verification tools must be reviewed for internal paths
or identifiers before publishing.

---

## Next action

Review `tools/verify_case_pack.py`, `verify_evidence.py`, `verify_lib.py`
for publication safety. If clean, publish here.
