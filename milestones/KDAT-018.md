# KDAT-018 — Tighter Operator Trust Defaults

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

AboutExpander restricts metadata to operator-safe fields only. A compact
requirements key strip appears above excerpts. Reference cards always display
a "Not a protocol" reminder.

---

## What this milestone proves

- AboutExpander: operators see only Title, Status, Effective date, Review date, Type;
  Domain and Kind (raw) are admin-only
- Field label changes: "Document"→"Title", "Kind"→"Type"
- `KeyRequirementsStrip`: compact one-liner above excerpt on approved results
  when `requirements.items` present (Models/Voltages/Max amps)
- Reference and medical_reference cards: always-visible "Not a protocol" reminder
  above excerpt
- `RequirementsEvidence` type carried forward from KDAT-017

---

## What this milestone does NOT prove

- Domain and Kind fields cannot be extracted through console developer tools
  (client-side restriction, not server-enforced by this milestone alone)
- Formal security review of field exposure

---

## Public-safe claims

"Operator-facing document metadata is restricted to Title, Status, and dates.
Domain and document kind are admin-only. Equipment spec summaries appear
compactly above excerpts. Reference results always display a protocol reminder.
Admin-gating of retrieval signals is verified by smoke T24."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Console delivery commit | keystone-console `60b6b47` | feat(kdat-018) |
| Smoke lock commit | keystone-deploy `8d646dd` | test(kdat-018): T24 |

---

## Verification and tests

- Smoke T24: JS bundle contains `rerank_reason` and `requirements_evidence`;
  `rerank_reason` appears only within 800 chars of an admin role guard;
  no operator-visible exposure confirmed

---

## Known limitations and caveats

- Bundle proximity heuristic. If admin UI is restructured, re-run T24.

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
