# KDAT-011C — One-Command Demo Run + Milestone Hygiene

**Status:** In validation
**Evidence class:** Curated summary
**Publication status:** Needs review

---

## Summary

`demo-run.sh` preloads query IDs and runs the canonical demo flow. Milestone
labels are gated to admin-only in the build, verified by the dist leak guard.

---

## What this milestone claims (curated summary + partial branch evidence)

- `demo-run.sh` script preloads canonical demo query IDs and runs the full
  demo flow from a single command
- KDAT-011C milestone label is admin-only: gated by `session.role==='admin'`
  in `AdminBuildInfoPage`; not exposed to operator-visible bundle paths
- `check-dist-leaks.sh` verifies that no KDAT labels appear in operator-facing
  HTML; JS bundle KDAT occurrences are admin-only

---

## What this milestone does NOT prove

- The full 011C scope (all demo-run.sh features, complete admin-only gating)
  has not been verified from distinctly tagged 011C commits
- The admin-only label gate is verified by CI (check-dist-leaks), but the
  full demo-run.sh end-to-end flow is not covered by a dedicated smoke test
  in this log

---

## Public-safe claims

**Partially safe, needs review.** The admin-only label gate is verified.
`demo-run.sh` is present in the deploy commit. Full 011C scope validation
is pending.

Verified claim: "Milestone labels are gated to admin-only in the console
build. The dist leak guard confirms zero KDAT labels in operator-visible HTML."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Curated summary | kdat-log.md | 011C: demo-run.sh + admin-only label |
| Grouped delivery | keystone-deploy `1f22624` | feat(kdat-011): includes demo-run.sh |
| Dist leak guard | keystone-deploy `80c65ce` | ci(lrfd): KDAT-* regression check |
| Console admin gate | keystone-console `a377ff8` | Admin-only build-info page; KDAT labels removed from operator UI |
| Console admin gate | keystone-console `b026186` | Confirms KDAT-011C label is admin-only |

---

## Verification and tests

- `check-dist-leaks.sh`: HTML has zero KDAT- hits; JS bundle admin-only
- `b026186` commit body: "no KDAT/admin labels in HTML; runtime-gated in JS bundle"

---

## Known limitations and caveats

- Curated sub-milestone. The branch has grouped KDAT-011 commits tagged to
  `feat(kdat-011)`, not to `kdat-011c` specifically. The 011A/B/C subdivision
  exists only in the curated narrative, not in commit evidence.
- `demo-run.sh` is present in deploy commit `1f22624` but the end-to-end
  demo flow is not covered by a dedicated smoke test. Its correct operation
  is asserted by description only.
- `check-dist-leaks.sh` verifies the KDAT label gate and exists as a local
  file (`scripts/check-dist-leaks.sh`). This is the strongest evidence on this
  page. It does NOT constitute proof of the broader 011C scope.
- Do not cite the one-command demo run as independently proven. Cite only
  the label-gate behavior, which is locally verifiable.

---

## Source basis

Curated summary. Partial branch evidence for the admin-only label gate
(keystone-deploy `check-dist-leaks.sh` + smoke T28, keystone-console
commits `a377ff8` and `b026186`). Evidence for the full 011C scope is
insufficient from the current branch log.

---

## Notes

See [index/timeline.md](../index/timeline.md) for the 011A/011B/011C
vs. grouped KDAT-011 explanation.
