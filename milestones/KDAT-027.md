# KDAT-027 — KDAT Log Publisher + External CF Smoke Timer

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Needs review

---

## Summary

An automated KDAT log publisher regenerates `docs/kdat-log.md` from git history
across all three repos and pushes to a separate docs repo. A hardened external
Cloudflare smoke timer runs `smoke-cf-with-fix.sh` every 15 minutes: probe →
best-effort fix → re-check. Timer firing confirmed on a live system via journalctl.

---

## What this milestone proves

### Commit `d504cda` — Initial publisher + timer units

- `scripts/publish-kdat.sh`: idempotent KDAT log publisher — greps `kdat-` across
  keystone-gov, keystone-console, and keystone-deploy commit history, writes
  `docs/kdat-log.md`, copies to `keystone-docs/docs/kdat-log.md`, commits and
  pushes; fails with a clear error if `keystone-docs` repo is missing
- `docs/systemd/smoke-cf.service`: hardened oneshot user unit (`NoNewPrivileges`,
  `PrivateTmp`, `ProtectSystem=strict`); reads CF credentials from
  `~/.config/keystone/env`
- `docs/systemd/smoke-cf.timer`: initial version — fires hourly, `Persistent=true`
- `scripts/install-smoke-cf-timer.sh`: idempotent installer — copies units,
  daemon-reload, enable --now, prints next trigger
- `docs/public-access.md`: "External smoke timer" section with install, verify,
  and disable commands
- smoke-cf.sh result at time of commit: PASS 7 / FAIL 0 / SKIP 1
- systemd-analyze verify: clean (no errors or warnings) on new units

### Commit `36fe893` — Hardened timer + wrapper

- `scripts/smoke-cf-with-fix.sh`: three-step wrapper — runs `smoke-cf.sh`; on
  failure calls `public-fix.sh` (best-effort, once); re-runs `smoke-cf.sh` to
  confirm recovery; journal banners (`START` / `PASS` / `FAIL` / `RE-CHECK` /
  `RECOVERED`) delimit runs for unambiguous grep; never loops
- `docs/systemd/smoke-cf.service`: updated — `WorkingDirectory=%h/keystone/keystone-deploy`,
  `ExecStart` calls wrapper; hardened: `NoNewPrivileges`, `PrivateTmp`,
  `ProtectSystem=strict`, `ProtectHome=read-only`, `ReadWritePaths` for env dir
  and `/run/user` (needed by public-fix.sh systemctl --user calls)
- `docs/systemd/smoke-cf.timer`: changed to `OnCalendar=*:0/15` (fires at :00 :15
  :30 :45); `Persistent=true`
- `scripts/install-smoke-cf-timer.sh`: guards that `scripts/smoke-cf.sh` exists and
  is executable (auto-chmod if not); `enable --now`; prints journalctl and disable
  hints
- `docs/public-access.md`: "External smoke timer" section rewritten with install,
  optional service-token setup, log commands, manual run, and disable instructions
- Verification on live system:
  - smoke-cf.sh: PASS 7 / FAIL 0 / SKIP 1
  - systemd-analyze verify: clean (no errors or warnings)
  - Timer installed and active: next trigger confirmed in 12 minutes
  - list-timers: LAST=22:00:17, NEXT=22:15:00
  - journalctl tail: smoke-cf PASS banner confirmed in journal

---

## What this milestone does NOT prove

- Long-running timer reliability over days or weeks without drift or credential
  expiry
- Zero-maintenance operation — CF credentials will expire; the timer will fail
  silently without credential rotation
- Multi-host coordination — single-machine smoke only
- That `public-fix.sh` recovers from all failure modes (best-effort only; one attempt)
- CI-verifiable timer behavior — systemd timers cannot be fully exercised in a
  stateless CI runner
- `publish-kdat.sh` correctness in repos with non-standard KDAT commit labeling

---

## Public-safe claims

"An automated KDAT log publisher regenerates the milestone evidence log from git
history and pushes to the docs repo. A hardened Cloudflare Access smoke timer
fires every 15 minutes; on failure it attempts a best-effort fix and re-checks.
Timer firing was confirmed on a live system via journalctl. Smoke result at
delivery: PASS 7 / FAIL 0 / SKIP 1."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit 1 | keystone-deploy `d504cda` | Initial publisher + timer units; 5 files, 269 insertions |
| Delivery commit 2 | keystone-deploy `36fe893` | Hardened wrapper + 15-min timer; 6 files, 148 insertions |
| KDAT log publisher | `scripts/publish-kdat.sh` | Idempotent; fails clearly if keystone-docs missing |
| Smoke wrapper | `scripts/smoke-cf-with-fix.sh` | Three-step probe → fix → re-check |
| Service unit | `docs/systemd/smoke-cf.service` | Hardened oneshot user unit |
| Timer unit | `docs/systemd/smoke-cf.timer` | OnCalendar=*:0/15, Persistent=true |
| Timer installer | `scripts/install-smoke-cf-timer.sh` | Idempotent; guards executable check |
| Public access docs | `docs/public-access.md` | "External smoke timer" section |

Both commits are on `lrfd-backend-bootstrap`.

---

## Verification and tests

- smoke-cf.sh: **PASS 7 / FAIL 0 / SKIP 1** (T6 passes with service token; T8 skips if PDM off)
- systemd-analyze verify: clean on both service and timer units
- Timer confirmed active on live system:
  - `systemctl --user list-timers smoke-cf.timer` → LAST=22:00:17 NEXT=22:15:00
  - journalctl tail confirmed smoke-cf PASS banner in journal
- Guard: installer checks `scripts/smoke-cf.sh` exists and is executable before proceeding

No automated CI harness for timer firing (systemd constraint). Journal-confirmed
fire on live system is the primary runtime verification.

---

## Known limitations and caveats

- Publication status is "Needs review" because the 15-minute timer cannot be
  exercised in a stateless test environment. Timer firing was confirmed on the
  live system via journalctl, but this is environment-dependent.
- `public-fix.sh` is best-effort and runs once. If the root cause persists,
  the re-check will also fail; no retry loop.
- `publish-kdat.sh` requires a locally cloned `keystone-docs` repo at a known
  path; if absent, it fails with an explicit error (not silently).
- Timer runs as a user unit; `loginctl enable-linger` is required for it to
  survive user logout.
- CF credentials used by the timer will expire; rotation is manual.

---

## Source basis

Two commits on lrfd-backend-bootstrap. Date: 2026-03-14.

| Commit | Purpose |
|--------|---------|
| `d504cda` | Initial KDAT publisher + hourly smoke-cf timer units |
| `36fe893` | Hardened wrapper + 15-min timer; live-system timer fire verified |

keystone-deploy HEAD at delivery: `36fe893`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy

# Check timer status (requires live system with linger enabled):
systemctl --user status smoke-cf.timer

# Run smoke manually:
bash scripts/smoke-cf.sh
# Expected: PASS 7 / FAIL 0 / SKIP 1

# Run wrapper manually:
bash scripts/smoke-cf-with-fix.sh
# Expected: PASS banner in output; check journal for START / PASS banners
```
