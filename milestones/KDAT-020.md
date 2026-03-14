# KDAT-020 — Suggested Queries Panel

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Needs review

---

## Summary

Six one-click query buttons appear above the query textarea, covering fire_ops
procedural, requirements/spec, and medical_reference scenarios, with automatic
mode switching for the medical suggestion.

---

## What this milestone proves

- Six suggested query buttons rendered above the question textarea on the
  Query page
- Queries: 3 fire_ops procedural (MAYDAY declaration, two-in/two-out,
  hydrant supply); 2 requirements/spec (FoamPro 2001 wiring, aerial fuse
  sizing); 1 medical_reference (epistaxis/nosebleed with auto mode-switch)
- Medical suggestion calls `session.setMode('medical_reference')` before
  submission
- Buttons are colour-coded by tag (fire_ops / spec / medical)
- Buttons disabled while a query is in-flight

---

## What this milestone does NOT prove

- Regression safety: no smoke lock exists for this feature; a future refactor
  could break it silently without automated detection
- Exhaustive coverage of query domains or scenarios
- That the six queries are representative of all deployment scenarios
- That mode-switching behavior is tested end-to-end against the backend

---

## Public-safe claims

"The operator console provides one-click suggested queries across procedural,
specification, and medical reference scenarios. The medical suggestion
automatically switches query mode before submission. Build-verified; no
dedicated smoke regression lock yet."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Console delivery commit | keystone-console `df1ad19` | feat(kdat-020) |

---

## Verification and tests

- UX verified by build (npm run build passes)
- No dedicated smoke lock as of the evidence log date

---

## Known limitations and caveats

- No smoke regression lock. This is the primary reason for "Needs review"
  publication status. The feature exists and the build passes, but a future
  change to the Query page could break the panel without CI catching it.
- Query content is static; not driven by corpus content or user role.
- The medical mode-switch (`session.setMode`) is verified by code inspection,
  not by an end-to-end API call test.
- Do not cite this milestone in external materials as fully validated until
  a smoke lock is added.

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.

---

## Next action

Add smoke T25 (or similar) asserting the suggested queries panel renders
and at least one suggestion produces an approved guidance response.
