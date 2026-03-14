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

- A dedicated smoke lock exists for the suggested queries panel
- Exhaustive coverage of query domains or scenarios
- The six queries are representative of all deployment scenarios

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

- Needs a smoke regression lock before this milestone is considered fully
  locked (hence "Needs review" publication status)
- Query content is static; not driven by corpus content or user role

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.

---

## Next action

Add smoke T25 (or similar) asserting the suggested queries panel renders
and at least one suggestion produces an approved guidance response.
