# KDAT-024 — Operational Scope Guard + CLARIFY_MODEL Clarifier

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Gate A2 enforces content_kind alignment in operational mode — refusing
requirements queries against non-requirements documents and vice versa —
while a CLARIFY_MODEL notice enables the console to offer one-click
model-selection chips when multiple apparatus models are found.

---

## What this milestone proves

**Backend (keystone-gov `b4b34c8`):**
- Gate A2 enforcement after Gate A (fail-closed gate for doc domain):
  - requirements-intent query + procedure doc (no spec data) → refuse with
    `NO_REQUIREMENTS_FOUND`
  - non-requirements intent + requirements doc (no spec data) → refuse
    `LOW_CONFIDENCE` with rephrase hint
- `CLARIFY_MODEL` notice: when parsed requirements items contain multiple
  distinct apparatus model names and the question names none of them, a
  `CLARIFY_MODEL` notice segment is appended to the guidance response
- 64 lines added to `api/main.py`

**Console (keystone-console `b254491`):**
- `parseClarifyModels()` helper decodes the `CLARIFY_MODEL` notice segment
- `ClarifyModelHint` component: hint box + per-model chips; each chip
  pre-fills the question textarea with the model name and navigates to
  the query page
- `ClarifyModelHint` rendered below `RequirementsCard` in `GuidancePage.tsx`
- `ConfidenceStrip` updated to match `LOW_CONFIDENCE` by substring contains
  (handles compound notices like `LOW_CONFIDENCE|CLARIFY_MODEL:…`)
- Generic notice block suppressed for `CLARIFY_MODEL` notices (prevents raw
  text display)
- 68 insertions in `src/routes/GuidancePage.tsx`

**Deploy smoke locks (keystone-deploy `4455f89`):**
- T30: requirements-intent query → `NO_REQUIREMENTS_FOUND` refusal OR
  content_kind=requirements doc (corpus-dependent)
- T31: procedure-intent query → must NOT return type=approved when top doc
  is content_kind=requirements with no spec data
- T32: operational medical_emr query → Gate B regression: type=approved
  never returned for medical_emr domain
- 127 lines added to `scripts/smoke-web.sh`

---

## What this milestone does NOT prove

- Exhaustive content_kind × intent combinations for all possible corpus compositions
- CLARIFY_MODEL chips trigger an accurate backend response (the chips pre-fill
  and submit; answer quality depends on corpus)
- Gate A2 coverage for all possible malformed queries; this covers the two
  primary misalignment patterns

---

## Public-safe claims

"Keystone enforces content type alignment in operational mode: a requirements
query against a procedure document is refused rather than returning a
misleading answer. When multiple apparatus models are found, the console
surfaces one-click clarification chips so operators can refine their query
without re-typing. Verified by three smoke regression locks (T30–T32)."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `b4b34c8` | feat(api): KDAT-024 — 64 insertions |
| Console delivery commit | keystone-console `b254491` | feat(ui): KDAT-024 — 68 insertions |
| Smoke lock commit | keystone-deploy `4455f89` | T30, T31, T32 in smoke-web.sh |
| Console component | `src/routes/GuidancePage.tsx` | ClarifyModelHint, parseClarifyModels |

---

## Verification and tests

- Smoke T30: requirements-intent refusal or correct content_kind=requirements doc
- Smoke T31: procedure-intent does NOT return approved when top doc is requirements type
- Smoke T32: operational medical_emr query never returns type=approved (Gate B regression)

---

## Known limitations and caveats

- T30 outcome is corpus-dependent: if the corpus contains a requirements-kind
  document that matches the query, it returns approved rather than refusing.
  The test accepts both outcomes because both are correct.
- CLARIFY_MODEL chips are a console-side convenience; they do not guarantee a
  more accurate backend response — they only narrow the query.
- Gate A2 runs after Gate A (domain gate); queries that fail Gate A never
  reach Gate A2.

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Date: 2026-03-14.
Commit SHAs:
- keystone-gov: `b4b34c8c445aa2520d9250e0feeecd4d90297f73`
- keystone-console: `b254491d666a83b58d440e7bf8a0d5118cd79764`
- keystone-deploy: `4455f89b946e1ef8d115f8d1b41a77cbce02522c`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
bash scripts/smoke-web.sh
# Check T30, T31, T32 results — expect PASS for all three
```
