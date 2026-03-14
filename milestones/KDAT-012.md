# KDAT-012 — Structured Requirements Extraction

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

The API extracts structured equipment requirements (model, voltage, amperage,
wiring/grounding notes) from corpus documents, exposed in guidance responses
and rendered as a requirements card in the console.

---

## What this milestone proves

- `requirements_parse.py`: inline spec regex (`requires N amps` format),
  table-row fallback, model-group expansion, wiring/grounding note extraction
- Guidance response gains `requirements` field when items or wiring_notes present
- Summary text overridden with compact requirements paragraph for spec queries
- Console RequirementsCard: Model/Voltage/Min-amps table + wiring/grounding notes
  displayed between summary and ProcedureCard for approved guidance

---

## What this milestone does NOT prove

- Exhaustive specification extraction across all possible document formats
- Correctness guarantees for arbitrary manufacturer spec sheets
- Structured output for non-spec document types

---

## Public-safe claims

"Keystone AI extracts structured equipment requirements (electrical specs,
wiring requirements, grounding requirements) from corpus documents and
presents them as a structured card in the operator console. Verified by 9
contract test assertions and a smoke regression lock."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `7f4a790` | feat(kdat-012) |
| Console delivery commit | keystone-console `2036051` | feat(kdat-012) |
| Smoke lock commit | keystone-deploy `c651ce3` | test(kdat-012) |

---

## Verification and tests

- `api/tests/test_requirements_structured.sh` — 9 assertions
  (items ≥ 5, model variants 2001/12/41 and 2024/24/60, wiring_notes ≥ 1 with battery)
- Smoke T20d: `requirements.items ≥ 5` on foampro electrical query

---

## Known limitations and caveats

- Regex-based extraction; accuracy depends on corpus document formatting
- Tested against FoamPro 2000-series documents; generalization validated in
  KDAT-015

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
