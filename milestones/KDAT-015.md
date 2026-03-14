# KDAT-015 — Spec-Retrieval Generalization

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Requirements-intent pattern matching is generalized beyond electrical specs
to hydraulic/flow specs, with a spec-table reranker that avoids penalizing
dense spec tables, and a requirements_evidence dict attached to all
requirements-intent guidance responses.

---

## What this milestone proves

- Requirements-intent patterns expanded: `psi`, `gpm`, `flow_rate`, `water_pressure`
- Heading signals expanded: WATER, HYDRAULIC, PLUMBING, SERVICE
- Explicit requires-spec patterns expanded: `minimum/psi/gpm/kPa`
- `_rerank_score_spec_table()`: skips front-matter and digit-density penalties
  for spec-table chunks (≥ 3 spec-data lines), preventing vendor address
  content from suppressing actual spec values on the same page
- `requirements_evidence` dict: `{heading_hit, explicit_spec_lines, pointer_only, spec_table_like}`
  attached to guidance for all requirements-intent queries
- `_is_spec_answer` bypasses LOW_CONFIDENCE gate for `spec_table_like` chunks

---

## What this milestone does NOT prove

- Exhaustive hydraulic or pneumatic spec coverage
- Accuracy across arbitrary third-party document formats
- Generalization beyond the equipment categories in the demonstration corpus

---

## Public-safe claims

"Spec retrieval covers both electrical and hydraulic/flow specifications.
A spec-table reranker prevents front-matter from suppressing dense spec
tables. All requirements-intent responses include retrieval evidence signals.
Verified by 25 test assertions across four queries against two documents
(FoamPro 2000-series, BAM compressor manual), plus a smoke regression lock."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `168c4f4` | feat(kdat-015) |
| Smoke lock commit | keystone-deploy `3c25aab` | test(kdat-015) |

---

## Verification and tests

- `api/tests/test_requirements_general.sh` — 25 assertions
  (4 queries × 2 documents: FoamPro 2000-series + BAM compressor manual)
- Smoke T23: BAM spec query returns approved guidance with psi token in
  excerpt and page ≥ 5 (non-front-matter section confirmed)

---

## Known limitations and caveats

- Spec-table detection uses a line-density heuristic (≥ 3 spec-data lines);
  may not detect sparse tables or non-standard formats
- Tested against two documents in the demonstration corpus

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
