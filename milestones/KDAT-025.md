# KDAT-025 — Cloudflare Access Smoke Proof

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

An 8-test smoke suite (`smoke-cf.sh`) verifies that the Cloudflare Access
integration correctly gates the public URL, redirects unauthenticated requests,
allows origin health checks, and blocks login bypass attempts in CF mode.

---

## What this milestone proves

- `scripts/smoke-cf.sh`: 8-test CF smoke suite covering:
  - **T1**: Public URL routing — `200` on open paths, `302` on CF-gated paths
  - **T2**: CF Access redirect targets the expected team domain
  - **T3**: Origin `/api/health` → `status=ok db=true` (bypasses CF gate; internal)
  - **T4**: Origin `/` → `200` HTML (Caddy serves HTML without CF)
  - **T5**: JS asset from parsed HTML → `200` (asset serving verified)
  - **T6**: Authenticated public probe via CF service token (optional; skipped if token absent)
  - **T7**: `/api/auth/login` blocked (`403`) in CF mode at origin (prevents bypass)
  - **T8**: Public demo mode admin block (conditional; skipped if PDM off)
- `docs/public-access.md`: "Cloudflare smoke" section with test table, example
  outputs for gated and open cases, and service-token setup instructions
- Verified run: **PASS 6 / FAIL 0 / SKIP 2** (T6 skipped — no service token in test env;
  T8 skipped — PDM off; SKIPs are environment-conditional, not failures)

---

## What this milestone does NOT prove

- Full CF Access policy enforcement beyond what can be tested via HTTP probes
- That CF Access cannot be bypassed via undiscovered paths (this is a smoke test,
  not a penetration test)
- Authenticated CF Access behavior when a valid user JWT is present (T6 is
  optional; tested separately with a service token)
- Coverage of CF Access custom domains beyond the single team domain

---

## Public-safe claims

"A Cloudflare Access smoke suite verifies that the public URL is correctly
gated, unauthenticated requests are redirected to the CF team domain,
origin health checks remain accessible for ops, and login bypass via direct
`/api/auth/login` is blocked in CF mode. Verified: 6 PASS, 2 SKIP
(environment-conditional — no failures)."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit | keystone-deploy `25c5a5e` | test(kdat-025) — 2 files, 394 insertions |
| Smoke suite | `scripts/smoke-cf.sh` | 8 tests; 289 lines |
| Public access docs | `docs/public-access.md` | "Cloudflare smoke" section |

---

## Verification and tests

`scripts/smoke-cf.sh` — 8 tests:

| Test | Assertion | Condition |
|------|-----------|-----------|
| T1 | Public URL: 200 open / 302 gated | Always |
| T2 | CF redirect targets expected team domain | Always |
| T3 | Origin /api/health → status=ok db=true | Always |
| T4 | Origin / → 200 HTML | Always |
| T5 | JS asset from HTML → 200 | Always |
| T6 | Auth probe via service token → expected response | Skipped if no token |
| T7 | /api/auth/login → 403 in CF mode at origin | Always |
| T8 | PDM admin block | Skipped if PDM off |

Run result (2026-03-14): PASS 6 / FAIL 0 / SKIP 2

---

## Known limitations and caveats

- T6 (service token probe) requires `CF_SERVICE_TOKEN` to be set in the test
  environment; skipped in CI without the token. This is expected behavior,
  not a test failure.
- T8 (PDM block) requires `PUBLIC_DEMO_MODE=1`; skipped when PDM is off.
- This is a smoke test suite, not a security audit. CF Access policy
  configuration correctness is asserted at the HTTP response level only.
- Requires the stack to be running with CF Access configured; does not run
  in a pure local/offline environment.

---

## Source basis

Branch delivery commit on lrfd-backend-bootstrap. Date: 2026-03-14.
Commit SHA: `25c5a5e4c6bbee3a7f31ff554aa69284e0997921`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
bash scripts/smoke-cf.sh
# Expected: PASS 6 / FAIL 0 / SKIP 2 (or PASS 8 if CF_SERVICE_TOKEN set and PDM on)
```
