# KDAT-021 — Orphan Sidecar CI Gate

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

A CI harness and GitHub Actions workflow fail the build when orphan metadata
sidecars are detected in the corpus, preventing silent regressions.

---

## What this milestone proves

- `scripts/test_lint_corpus_orphans.sh`: deterministic test harness for
  orphan sidecar detection
- `.github/workflows/corpus-lint.yml`: GitHub Actions workflow that gates
  CI on corpus orphan lint
- Orphan sidecar regressions now fail CI rather than passing silently
- Detection is deterministic (reproducible result for any given corpus state)

---

## What this milestone does NOT prove

- Full corpus correctness validation beyond orphan sidecar detection
- Cross-environment CI coverage beyond the GitHub Actions workflow

---

## Public-safe claims

"Orphan metadata sidecars (sidecar files without a corresponding corpus
document) are detected and fail CI automatically. The corpus lint check is
deterministic and enforced via GitHub Actions."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| CI delivery commit | keystone-deploy `6275a07` | ci(kdat-021) |

---

## Verification and tests

- `scripts/test_lint_corpus_orphans.sh` — deterministic test harness
- `.github/workflows/corpus-lint.yml` — GitHub Actions corpus-lint workflow

---

## Known limitations and caveats

- Lint covers orphan sidecars (sidecar without document); does not cover
  documents without sidecars (missing metadata) as a separate check

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
