# KDAT-017 — Operator Trust Defaults

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Debug retrieval signals are hidden from non-admin users. Officers see an
evidence-backed hint when substantive retrieval signals are present. Admins
have a collapsible debug panel.

---

## What this milestone proves

- `RequirementsEvidence` type: `{heading_hit, explicit_spec_lines, pointer_only, spec_table_like}`
- Officer hint: "Evidence-backed excerpt. Open document to verify." displayed
  when `pointer_only=false` AND at least one of `heading_hit`, `explicit_spec_lines > 0`,
  `spec_table_like` is true
- Admin-only: collapsible "Debug: retrieval signals" panel (rerank_reason +
  full requirements_evidence)
- Non-admin roles never see raw rerank or evidence debug fields

---

## What this milestone does NOT prove

- Formal information flow security guarantees
- All possible admin/non-admin UI surface exposure scenarios

---

## Public-safe claims

"Retrieval debug signals are not exposed to operator roles. Officers see a
brief evidence-backed verification hint when substantive retrieval evidence
is present. Admins can access a collapsible debug panel. Separation is
protected by a regression smoke lock (KDAT-018 T24)."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Console delivery commit | keystone-console `1ed2f5c` | feat(kdat-017) |
| Regression protection | keystone-deploy `8d646dd` | test(kdat-018): T24 covers kdat-017 regression |

---

## Verification and tests

- Regression protected by KDAT-018 smoke T24: `rerank_reason` present in
  JS bundle only within 800 chars of an admin role guard

---

## Known limitations and caveats

- Verified by bundle proximity heuristic (800-char window), not by formal
  access control analysis
- Any admin UI refactoring must re-verify the 800-char constraint or add
  a more robust guard

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
