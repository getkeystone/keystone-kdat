# KDAT-022 — Backup + Restore with Smoke Verification

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Ready to publish

---

## Summary

Operator-runnable backup and restore scripts with end-to-end smoke verification
guarantee that the Keystone stack can be recovered from a known-good state.

---

## What this milestone proves

- `scripts/backup.sh`: produces a dated `.tar.gz` archive containing PostgreSQL
  dump, active corpus files, and the active public signing key
- `scripts/restore.sh`: clean or `--fresh` restore from a backup archive;
  auto-invokes `smoke-web.sh` after restore to confirm stack health
- `scripts/test_backup_restore.sh`: fast end-to-end smoke: backup → restore → smoke
- `scripts/_deploy_env.sh`: shared env sourcing for PUBLISH_IP, PUBLISH_PORT,
  CORPUS_ROOT — used by backup and restore scripts
- `docs/backup-restore.md`: operator runbook covering backup, transfer, restore,
  and verify steps
- Verified run: backup produced `keystone-backup-20260314-144816Z.tar.gz`
  (140 MB, sha256 `fcaf54b5…`); restore + smoke returned 10 PASS / 0 FAIL

---

## What this milestone does NOT prove

- Continuous backup scheduling (cron/systemd timer is not included in this milestone)
- Cross-machine transfer automation (manual `scp` or `rsync` is the documented path)
- Point-in-time recovery beyond the latest backup
- Hot backup (database must be quiesced or consistent snapshot assumed)

---

## Public-safe claims

"Keystone provides operator-runnable backup and restore scripts. A backup
captures the database, active corpus, and public signing key into a dated archive.
Restore is smoke-verified automatically: the script re-runs the stack smoke test
after reload. End-to-end backup→restore→smoke was validated in a single run
returning 10 PASS / 0 FAIL."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit | keystone-deploy `6cb804a` | feat(kdat-022) — 6 files, 635 insertions |
| Backup script | `scripts/backup.sh` | Produces dated .tar.gz |
| Restore script | `scripts/restore.sh` | --fresh flag for clean reload |
| E2E smoke script | `scripts/test_backup_restore.sh` | backup → restore → smoke-web |
| Env helper | `scripts/_deploy_env.sh` | Shared env sourcing |
| Runbook | `docs/backup-restore.md` | Full operator runbook |

---

## Verification and tests

- `scripts/test_backup_restore.sh` — end-to-end: backup → restore → smoke-web.sh
- Verified run result: PASS 10 / FAIL 0 (smoke-web.sh post-restore)
- `.gitignore` updated to exclude `keystone-backup-*.tar.gz` from repo tracking

---

## Known limitations and caveats

- No scheduled backup automation in this milestone; scheduling is an operator
  responsibility after installation
- Backup scope is limited to the active corpus and single-node PostgreSQL dump;
  not tested across machines without manual transfer
- `--fresh` restore drops and recreates the database; operators must confirm
  before running in any environment with live data

---

## Source basis

Branch delivery commit on lrfd-backend-bootstrap. Date: 2026-03-14.
Commit SHA: `6cb804a8f650eb1abf62781b74522c459070c88e`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
bash scripts/backup.sh --out /tmp
bash scripts/restore.sh /tmp/keystone-backup-<timestamp>.tar.gz
# Smoke is auto-run by restore.sh; check for 10 PASS / 0 FAIL
```
