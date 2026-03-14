# KDAT-026 — Public Demo Reset Timer

**Status:** Proven
**Evidence class:** Proven on current branch
**Publication status:** Needs review

---

## Summary

A hardened systemd timer runs `public-reset.sh` daily at 04:15 to restore
the public demo to a known-good state; the installer enforces `PUBLIC_DEMO_MODE=1`
and a reset token as prerequisites, preventing accidental installation on
non-demo systems.

---

## What this milestone proves

- `scripts/public-reset.sh`: extended with preflights — refuses to run if
  `PUBLIC_DEMO_MODE != 1` or `PUBLIC_DEMO_RESET_TOKEN` is unset; prevents
  silent failures in production-adjacent environments
- `docs/systemd/public-reset.service`: hardened oneshot systemd user unit
  (`NoNewPrivileges`, `PrivateTmp`, `ProtectSystem=strict`); reads env from
  `~/.config/keystone/env`
- `docs/systemd/public-reset.timer`: daily at 04:15 local time, `Persistent=true`
  (fires on next start if missed)
- `scripts/install-public-reset-timer.sh`: idempotent installer — copies units,
  runs `systemctl --user daemon-reload`, enables and starts timer; refuses
  installation if `PUBLIC_DEMO_MODE != 1` or token unset
- `docs/public-access.md`: "Daily reset timer" section with install/verify
  commands and guard demonstration output
- Guard verified: running installer with `PUBLIC_DEMO_MODE=0` outputs
  `[FAIL] PUBLIC_DEMO_MODE is not enabled (got '0').` and exits non-zero
- Active timer verified: `systemctl --user status public-reset.timer` →
  `active (waiting) Trigger: 04:15:00 ADT; 15h left`

---

## What this milestone does NOT prove

- That the timer fires correctly in all timezone and DST configurations
- That `public-reset.sh` fully resets all state in every possible corpus
  configuration (corpus content is environment-specific)
- Automated CI verification of the timer firing (systemd timers cannot be
  fully exercised in a stateless CI runner)
- Multi-host or coordinated reset for distributed deployments

---

## Public-safe claims

"A systemd user-unit timer runs the demo reset script daily at 04:15.
The installer enforces prerequisites: `PUBLIC_DEMO_MODE=1` and a reset
token must be set. Installation without these conditions is refused with
an explicit error. The timer is hardened with `NoNewPrivileges`,
`PrivateTmp`, and `ProtectSystem=strict`."

---

## Evidence and artifacts

| Item | Location | Notes |
|------|----------|-------|
| Delivery commit | keystone-deploy `3d27116` | test(kdat-026) — 5 files, 217 insertions |
| Reset script (extended) | `scripts/public-reset.sh` | Preflights: PDM check + token check |
| Systemd service unit | `docs/systemd/public-reset.service` | Hardened oneshot unit |
| Systemd timer unit | `docs/systemd/public-reset.timer` | Daily 04:15, Persistent=true |
| Installer | `scripts/install-public-reset-timer.sh` | Idempotent; refuses if guards fail |
| Docs | `docs/public-access.md` | "Daily reset timer" section |

---

## Verification and tests

- Guard test: run installer with `PUBLIC_DEMO_MODE=0` → exits with
  `[FAIL] PUBLIC_DEMO_MODE is not enabled` (non-zero exit code)
- Active timer check: `systemctl --user status public-reset.timer` →
  `active (waiting) Trigger: 04:15:00 ADT`
- Reset confirmation: `journalctl --user -u public-reset.service -n 50`
  → `[PASS] Demo state reset complete.`

No automated CI harness for the timer firing itself (systemd constraint).
Guard behavior (installer refusal) is the primary verifiable assertion.

---

## Known limitations and caveats

- Publication status is "Needs review" because the daily timer trigger cannot
  be exercised in a stateless test environment. The guard behavior and unit
  configuration are verified; the actual daily fire requires a live system
  with linger enabled.
- `Persistent=true` means the timer fires on the next system start if it
  missed its window; this is intentional but should be documented for operators
  who restart the host during the 04:15 window.
- Timer runs as a user unit; `loginctl enable-linger` is required for it to
  survive user logout.

---

## Source basis

Branch delivery commit on lrfd-backend-bootstrap. Date: 2026-03-14.
Commit SHA: `3d27116afe54c544fe0ed2944900065f5f489b09`

---

## Fastest verification method

```bash
cd ~/keystone/keystone-deploy
# Verify the guard (safe — does not install anything):
bash scripts/install-public-reset-timer.sh
# Expected with PUBLIC_DEMO_MODE=0: [FAIL] PUBLIC_DEMO_MODE is not enabled

# With PUBLIC_DEMO_MODE=1 and token set — verify timer is active:
systemctl --user status public-reset.timer
```
