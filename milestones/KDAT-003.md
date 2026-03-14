# KDAT-003 — Document Governance UI + APIs

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Document governance APIs and console UI: searchable document registry,
detail views, review queue, and metadata PATCH with an immutable audit trail.

---

## What this milestone proves

- `GET /documents` — paginated, filterable document list (q, status, owner, overdue_only)
- `GET /documents/review-queue` — grouped review queue (overdue, missing_owner, missing_review_date, draft_or_superseded)
- `GET /documents/{id}` — full metadata + chunk/page statistics
- `PATCH /documents/{id}/metadata` — custodian/admin-only; validates status/dates; writes before/after snapshot to `corpus_doc_events`
- Console Documents page (`/documents`): searchable table with status filter, overdue badge, pagination
- Console Document Detail (`/documents/:id`): metadata display, inline Edit Metadata form
- Console Review Queue (`/documents/review-queue`): four grouped sections with counts
- Database migration: `corpus_doc_events` table with index and GRANT to `keystone_app`

---

## What this milestone does NOT prove

- Enterprise document management at scale
- Integration with external DMS systems
- Full-text content search within documents
- Role-based access beyond custodian/admin distinction
- Compliance with any document retention regulation

---

## Public-safe claims

"Keystone AI's governance API provides a document registry with review queues
and audited metadata patching. Changes are captured as before/after events.
Operators can filter and review the document corpus through the console.
Verified by 9 contract test assertions."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `5e99424` | feat(doc-governance): KDAT-003 |
| Console delivery commit | keystone-console `45ef66a` | feat(ui): KDAT-003 Documents page |
| Deploy / migration commit | keystone-deploy `09effe8` | ops: KDAT-003 corpus_doc_events migration |

---

## Verification and tests

- `api/tests/test_doc_governance.sh` — 9 assertions
  - Covers: list, review-queue grouping, detail, metadata PATCH, audit event write

---

## Known limitations and caveats

- Tested at demonstration scale, not at large-corpus volume
- Review queue grouping depends on metadata completeness in the seeded corpus

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Commit SHAs recorded in
evidence log generated 2026-03-14.
