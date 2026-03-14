# KDAT-011A — Demo Mode Toggle + Safe Failure UX

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Not publishable yet

---

## Summary

A demo mode toggle and safe failure UX (offline banner, retry screens,
demo bypass) allow the console to degrade gracefully when the backend
is unavailable.

---

## What this milestone claims (curated summary)

- Demo Mode toggle: enables offline/bypass mode in the console
- Offline banner displayed when backend is unreachable
- Retry screen with user feedback
- Demo bypass screens allow demonstration without live backend

---

## What this milestone does NOT prove

- Sub-milestone commits (tagged specifically to 011A) do not appear distinctly
  in the lrfd-backend-bootstrap log
- The grouped KDAT-011 delivery commit (`3112590` in keystone-console,
  `1f22624` in keystone-deploy) covers demo mode broadly; which aspects
  correspond to 011A vs. 011B vs. 011C is not determinable from commit
  evidence alone

---

## Public-safe claims

**Not available yet.** The 011A sub-milestone requires separate validation.

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md | 011A described as demo mode toggle + offline UX |
| Grouped delivery | keystone-console `3112590` | feat(kdat-011): demo mode + offline UX polish |
| Grouped delivery | keystone-deploy `1f22624` | feat(kdat-011): stack scripts and demo-run helpers |

The grouped KDAT-011 commits exist on the branch but are not tagged
specifically to 011A.

---

## Verification and tests

None cited for 011A specifically. Grouped KDAT-011 milestone had admin-only
label verified by `check-dist-leaks.sh`.

---

## Known limitations and caveats

- The curated summary splits KDAT-011 into 011A/011B/011C, but the branch
  delivery table treats it as a single KDAT-011. Sub-milestone assignment
  is curated narrative, not commit evidence.
- Do not cite externally until 011A scope is confirmed from tagged commits.

---

## Source basis

Curated summary from kdat-log.md. Grouped commits exist but are not tagged
to 011A specifically.

---

## Notes

See [index/timeline.md](../index/timeline.md) for explanation of the 011
grouping vs. sub-milestone relationship.
