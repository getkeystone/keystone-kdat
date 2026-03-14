# KDAT-013 — Requirements Hygiene + content_kind Rerank + Migration

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Requirements output is filtered for relevance (hygiene pass), retrieval
reranks documents by content_kind, and a database migration introduces the
content_kind column.

---

## What this milestone proves

- `filter_requirements_notes()`: retains notes only when relevance keywords
  (vdc, volt, amp, battery, disconnect, contactor, pto, ground, strap, rfi,
  emi) are present; drops pointer-only phrases without spec keywords
- Wiring notes capped at 4; grounding notes capped at 2
- content_kind rerank: ×1.15 on procedure-kind docs in initial FTS sort;
  ×1.35 on requirements-kind docs inside `_req_intent_score`
- `initdb/10-content-kind.sql`: `ADD COLUMN content_kind TEXT NOT NULL DEFAULT 'procedure'`; index; GRANT UPDATE to `keystone_app`
- `lint-corpus-metadata.sh` validates content_kind against `procedure|requirements|reference` enum

---

## What this milestone does NOT prove

- Exhaustive noise filtering for all possible corpus documents
- Production-scale database migration behavior
- Content_kind correctness beyond the validated enum values

---

## Public-safe claims

"Requirements note extraction filters out pointer-only noise and caps wiring
and grounding note counts for relevance. Document retrieval reranks by
content type, improving spec query accuracy. Verified by 7 test assertions
and a smoke regression lock."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `5ac7338` | feat(kdat-013) |
| Deploy delivery commit | keystone-deploy `d9e2653` | feat(kdat-013) |

---

## Verification and tests

- `api/tests/test_requirements_hygiene.sh` — 7 assertions
  (items ≥ 5, wiring ≤ 4, grounding ≤ 2, no pointer-only notes)
- Smoke T21: hygiene lock on foampro electrical requirements query

---

## Known limitations and caveats

- Relevance keyword list is fixed; may not generalize to all equipment domains
- Rerank multipliers (1.15, 1.35) tuned for demonstration corpus; may need
  adjustment for different document sets

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
