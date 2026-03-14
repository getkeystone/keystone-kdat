# KDAT-004 — Signed Deterministic Evidence Bundles

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Not publishable yet

---

## Summary

Evidence bundles are signed with Ed25519 and produced deterministically,
enabling offline verification of document exports.

---

## What this milestone claims (curated summary)

- Ed25519 signing: public key endpoint, signed manifest
- Deterministic ZIP ordering for reproducible bundles
- Offline verifier tool for signature and integrity checking
- Deploy: key mount via `EVIDENCE_SIGNING_KEY_PATH`, keygen script
- Console: admin button to download evidence bundle
- Tests: determinism, tamper cases, offline verification exit codes

---

## What this milestone does NOT prove

- This milestone's branch delivery commits do not appear in the current
  evidence log (lrfd-backend-bootstrap)
- The curated summary has not been verified against commit evidence
- No independent test output is available in this log

---

## Public-safe claims

**Not available yet.** This milestone must be validated against branch
delivery commits before any public claim is made.

If validated, safe to claim: "Evidence bundles are signed with Ed25519 and
verified offline. Deterministic ZIP ordering ensures reproducibility."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md curated summaries section | Not independently verified |

No branch delivery commits for KDAT-004 appear in the lrfd-backend-bootstrap
commit log.

---

## Verification and tests

Curated summary mentions: determinism tests, tamper cases, offline verification
exit codes. These have not been verified from branch evidence in this log.

---

## Known limitations and caveats

- Curated summary only. Evidence class must be upgraded before external use.
- Delivery commits may exist on a different branch or in an ancestor branch
  not included in the lrfd-backend-bootstrap log.
- Do not cite this milestone externally until evidence class is verified.

---

## Source basis

Curated summary from kdat-log.md. Not verified from lrfd-backend-bootstrap
branch commit evidence.

---

## Next action

Locate delivery commits for KDAT-004. If found on this branch or an ancestor,
upgrade evidence class to Proven or Historical baseline. Add test script output.
