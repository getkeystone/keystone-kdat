# KDAT-023 — Evidence Signing Key Custody + Rotation + Verifier Trust Store

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Offline evidence verification now requires a trust store match by default;
key rotation generates dated keypairs and updates the trust store without
interrupting verification of existing bundles.

---

## What this milestone proves

- `tools/verify_lib.py`: adds `DEFAULT_TRUST_DIR` (`~/.config/keystone/trust/evidence_pubkeys/`),
  `pubkey_fingerprint()` (sha256 of raw Ed25519 bytes), `load_trusted_pubkeys()`
  (sorted deterministic dict), and `check_pubkey_trusted()` (fingerprint-based check)
- `tools/verify_evidence.py`: now requires embedded public key to match the trust
  store by default (exit 2 if not found); `--accept-embedded` bypasses with a
  `[WARN]` line (demo use only); `--trust-dir` overrides the default path;
  `--pubkey` skips trust check (backwards-compatible)
- `tools/verify_case_pack.py`: same trust flags as `verify_evidence.py`
- `scripts/install-evidence-trust.sh`: idempotent installer — copies active public
  key into trust dir as `evidence_pubkey_<fp16>.pem`; lists trust store contents
- `scripts/rotate-evidence-keys.sh`: generates dated keypair, updates active
  symlinks, installs new public key in trust store (old key retained for
  existing bundle verification); restarts API and waits for healthy
- `tools/tests/test_trust_store.sh`: 6 assertions (see Verification below)
- `docs/keys-and-trust.md`: custody runbook + minimum safe checklist

---

## What this milestone does NOT prove

- Hardware security module (HSM) key storage
- Multi-party key approval workflows
- Automatic rotation scheduling (manual `rotate-evidence-keys.sh` invocation)
- Cross-organization trust store federation

---

## Public-safe claims

"Evidence bundle verification now requires the signing key to be present in a
local trust store before accepting a bundle as valid. Key rotation generates
dated keypairs and preserves the old key for existing bundles. The trust store
is fingerprint-based (sha256 of raw Ed25519 bytes). Verified by 6 test
assertions covering trust-present, trust-absent, bypass flag, bypass warning,
determinism, and explicit-key override."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit | keystone-deploy `a2db809` | feat(kdat-023) — 7 files, 795 insertions |
| Trust store library | `tools/verify_lib.py` | fingerprint, load, check functions |
| Verifier (evidence) | `tools/verify_evidence.py` | --trust-dir, --accept-embedded, --pubkey |
| Verifier (case pack) | `tools/verify_case_pack.py` | same trust flags |
| Trust installer | `scripts/install-evidence-trust.sh` | idempotent; lists contents |
| Key rotation | `scripts/rotate-evidence-keys.sh` | dated keypair + old key retained |
| Test suite | `tools/tests/test_trust_store.sh` | 6 assertions |
| Runbook | `docs/keys-and-trust.md` | custody runbook + minimum safe checklist |

---

## Verification and tests

`tools/tests/test_trust_store.sh` — 6 assertions:

| Test | Assertion |
|------|-----------|
| T1 | Trusted key present → exit 0 (pass) |
| T2 | Empty trust dir → exit 2, trust store message |
| T3 | `--accept-embedded` → bypass, exit 0 |
| T4 | `--accept-embedded` → `[WARN]` printed |
| T5 | Deterministic output across runs |
| T6 | Explicit `--pubkey` → trust store skipped |

Verified run (2026-03-14): PASS 6 / FAIL 0

Additional manual verification:
- `install-evidence-trust.sh` → `evidence_pubkey_3ad3871c0eaaf332.pem` installed
- `verify_evidence.py` → `[PASS] All checks passed (trust store match confirmed)`

---

## Known limitations and caveats

- Default trust dir is user-local (`~/.config/keystone/trust/`); system-wide
  or shared trust stores require `--trust-dir` override
- `--accept-embedded` bypass is retained for demo use; operators should confirm
  this flag is never used in production verification workflows
- `export-evidence.sh` is blocked in CF Access mode (expected; requires CF JWT
  assertion); trust store verification was demonstrated with a bundle signed by
  the actual private key

---

## Source basis

Branch delivery commit on lrfd-backend-bootstrap. Date: 2026-03-14.
Commit SHA: `a2db809f5e8ebe32e297a2c70dc2e8bfc9ca0061`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
bash scripts/install-evidence-trust.sh
bash tools/tests/test_trust_store.sh
# Expected: PASS 6 / FAIL 0
```
