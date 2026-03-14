# KDAT-016 — Metadata Sidecar Always Applies on SHA-Match

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Ingest was fixed so that sidecar metadata changes (domain, content_kind,
owner, dates, status) are applied even when the document PDF SHA is unchanged
(previously a silent bug caused these updates to be dropped).

---

## What this milestone proves

- Sidecar comparison on SHA-match: all six fields (domain, content_kind, owner,
  effective_date, review_date, status_override) compared against DB
- If any field differs, a targeted UPDATE is applied and committed
- Silent bug fixed: missing `conn.commit()` after metadata-only UPDATE
- Action renamed: `updated_metadata` (was `metadata_updated`)
- Updated metadata counter added to ingest summary stats
- `corpus-ops.md` documents the metadata-only update workflow

---

## What this milestone does NOT prove

- Full idempotency guarantees for all ingest edge cases
- Concurrent ingest safety

---

## Public-safe claims

"Corpus ingest now applies sidecar metadata changes even when the document
content is unchanged (SHA-match path). A previously silent bug that dropped
metadata-only updates has been fixed. Verified by 9 test assertions."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `3adb050` | feat(kdat-016) |
| Deploy docs commit | keystone-deploy `d1ef8dc` | docs(kdat-016): corpus-ops.md |

---

## Verification and tests

- `api/tests/test_ingest_metadata_update.sh` — 9 assertions
  (SHA-match detection, field comparison, selective UPDATE, commit verification)

---

## Known limitations and caveats

- Applies to the SHA-match skip path in ingest; re-ingest on SHA change
  follows a different code path not specifically tested by this milestone

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
