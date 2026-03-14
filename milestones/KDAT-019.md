# KDAT-019 — Domain + content_kind Governance

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

The metadata PATCH endpoint accepts domain and content_kind fields with
strict enum validation. The console exposes these as editable dropdowns.
A missing database GRANT was fixed.

---

## What this milestone proves

- API: `PATCH /documents/{id}/metadata` accepts `domain` (fire_ops,
  medical_emr, lrfd_protocol) and `content_kind` (procedure, requirements,
  reference) with 422 on unknown value
- `list_documents` supports domain and content_kind query filter params
- `change_requests` allowed keys include domain and content_kind
- `corpus_doc_events` before/after snapshots cover the new fields
- Console: domain + content_kind editable dropdowns in Edit and Propose Change
  forms (admin/custodian); filter dropdowns in DocumentsListPage
- Deploy: column-level `GRANT UPDATE ON domain` to `keystone_app` in
  `initdb/09-domain.sql` (previously missing, causing runtime permission error)

---

## What this milestone does NOT prove

- Arbitrary domain vocabularies beyond the stated three values
- Enforcement at the corpus ingestion level independent of sidecar files
  (sidecar validation is addressed in KDAT-013 and KDAT-016)

---

## Public-safe claims

"Corpus documents have domain and content type classifications, enforced by
enum validation in the API. Operators can filter and edit these fields through
the console. A runtime permission bug (missing GRANT on domain column) has
been fixed. Verified by 12 test assertions."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| API delivery commit | keystone-gov `e433b31` | feat(kdat-019) |
| Console delivery commit | keystone-console `9be0863` | feat(kdat-019) |
| Deploy fix commit | keystone-deploy `aafb1e8` | fix(kdat-019): missing GRANT |

---

## Verification and tests

- `api/tests/test_doc_kind_domain_patch.sh` — 12 assertions
  (valid domain/content_kind PATCH; 422 on invalid values; list filter params;
  event snapshot coverage)

---

## Known limitations and caveats

- Domain vocabulary is hard-coded to three values; adding domains requires
  a code change, not a configuration change
- GRANT fix required because the domain column was added in a prior migration
  without the runtime user permission

---

## Source basis

Branch delivery commits on lrfd-backend-bootstrap. Evidence log generated 2026-03-14.
