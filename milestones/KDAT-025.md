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
- Subsequent commits hardened T6: strict env validation (space/paste checks on token
  headers), inline self-diagnosis on failure (abbreviated client_id, HTTP code,
  Location headers, cf-ray), and explicit success criterion (HTTP 200 from
  `/api/health` with CF-Access-Client-Id/Secret headers = PASS)
- `docs/public-access.md`: "Fixing T6 = 302" root cause section — service_token_status
  field, Zero Trust UI path, 5-step checklist
- Verified run: **PASS 7 / FAIL 0 / SKIP 1** (T6 passes with service token configured;
  T8 skipped — PDM off; SKIP is environment-conditional, not a failure)

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
origin health checks remain accessible for ops, login bypass via direct
`/api/auth/login` is blocked in CF mode, and authenticated service-token
probes succeed. Verified: 7 PASS, 1 SKIP (T8 is PDM-conditional —
environment-conditional, not a failure)."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit (initial) | keystone-deploy `25c5a5e` | test(kdat-025) — 8-test smoke suite, 394 insertions |
| Hardening commit 1 | keystone-deploy `8960989` | Self-diagnosing T6 probe + env validation |
| Hardening commit 2 | keystone-deploy `a5cd164` | docs: clarify service-token 302 root cause |
| Hardening commit 3 | keystone-deploy `1b343ff` | T6 explicit success criterion → PASS 7/FAIL 0/SKIP 1 |
| Smoke suite | `scripts/smoke-cf.sh` | 8 tests; all commits on lrfd-backend-bootstrap |
| Public access docs | `docs/public-access.md` | "Cloudflare smoke" section; T6 self-diagnosis; T6 fix checklist |

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
| T6 | Authenticated public probe via service token → HTTP 200 from /api/health | Passes with token; skipped if absent |
| T7 | /api/auth/login → 403 in CF mode at origin | Always |
| T8 | PDM admin block | Skipped if PDM off |

Run result (2026-03-14): PASS 7 / FAIL 0 / SKIP 1 (T6 passes with service token; T8 skipped — PDM off)

---

## Known limitations and caveats

- T6 (service token probe) requires `CLOUDFLARE_ACCESS_CLIENT_ID` and
  `CLOUDFLARE_ACCESS_CLIENT_SECRET` to be set. It now passes when those are
  configured (HTTP 200 from `/api/health`); it is skipped in CI without them.
  T6 includes inline self-diagnosis on failure: abbreviated client_id, HTTP
  code, Location headers, cf-ray, and a one-line root-cause diagnosis.
- T8 (PDM block) requires `PUBLIC_DEMO_MODE=1`; skipped when PDM is off.
- This is a smoke test suite, not a security audit. CF Access policy
  configuration correctness is asserted at the HTTP response level only.
- Requires the stack to be running with CF Access configured; does not run
  in a pure local/offline environment.

---

## Source basis

Four commits on lrfd-backend-bootstrap. Date: 2026-03-14.

| Commit | Purpose |
|--------|---------|
| `25c5a5e` | Initial smoke suite (8 tests, PASS 6/FAIL 0/SKIP 2) |
| `8960989` | T6 self-diagnosing env validation + failure debug block |
| `a5cd164` | Docs: service-token 302 root cause + Zero Trust fix checklist |
| `1b343ff` | T6 explicit pass criterion → PASS 7/FAIL 0/SKIP 1 |

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
bash scripts/smoke-cf.sh
# Expected: PASS 7 / FAIL 0 / SKIP 1 (T6 passes with service token; T8 skips if PDM off)
```
