# KDAT-009 — Case Timeline UI

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Not publishable yet

---

## Summary

The case timeline endpoint was normalized to a stable `items[]` response
shape, and the console CaseDetail page renders the timeline as a navigable
table.

---

## What this milestone claims (curated summary)

- Backend timeline endpoint normalized to `items[]` with stable sort and simplified type vocabulary
- Console CaseDetail timeline rendered as a table with links and correct error states
- Tests and smoke updated to assert items shape and access controls

---

## What this milestone does NOT prove

- Branch delivery commits for KDAT-009 do not appear in the lrfd-backend-bootstrap log
- The curated summary has not been verified against commit evidence

---

## Public-safe claims

**Not available yet.** Validate branch evidence first.

If validated: "Case timelines are returned as a normalized, stably sorted
items array. The console renders timeline items as a navigable table."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md curated summaries section | Not independently verified |

---

## Verification and tests

Curated summary mentions: tests and smoke covering items shape and access controls.
Not verified from branch evidence.

---

## Known limitations and caveats

- Curated summary only. Do not cite externally until evidence class is upgraded.

---

## Source basis

Curated summary from kdat-log.md. Not verified from branch commit evidence.

---

## Next action

Locate delivery commits. Validate test scripts. Upgrade evidence class.
