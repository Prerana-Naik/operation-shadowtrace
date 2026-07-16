# Evidence Package — prod-linux-01
**Case:** NorthWave Technologies — Suspicious Activity Investigation
**Received:** Monday, 13july 2026, 09:14 AM (per Arjun Mehta's email)
**Analyst:** Prerana Naik

## Contents

| File | What it is |
|---|---|
| `evidence/auth.log` | Simulated SSH/PAM/sudo authentication log for prod-linux-01 |
| `evidence/syslog` | Simulated system log — cron, kernel/apparmor, general daemon activity |
| `evidence/passwd` | Snapshot of `/etc/passwd` from the server |
| `evidence/shadow` | Snapshot of `/etc/shadow` (hashes are fabricated, non-functional — for account/UID analysis only, not cracking) |
| `evidence/ps_aux.txt` | Snapshot of `ps aux` taken during the investigation window |
| `evidence/ss_output.txt` | Snapshot of active network connections (`ss` output) |
| `evidence/crontab_svc_backup` | Contents of a crontab spool file found on disk |
| `evidence/bash_history_deploy_user` | Recovered `.bash_history` for the `deploy` account |
| `evidence/bash_history_root_shell` | Recovered `.bash_history` for a root shell session |

## Notes on realism
- Timestamps are internally consistent across all files (same host, same incident window).
- `bash_history` files use the `#<epoch>\ncommand` format produced when `HISTTIMEFORMAT` is set — this is how NorthWave's servers are configured.
- No file contains annotations, comments, or hints pointing to what is or isn't suspicious. You're reading these exactly as you would pull them off a real box.
- This is a **synthetic dataset** built for training purposes. IPs, hashes, and hostnames are fictional/non-functional.

## Your task
Everything else — timeline, IOC table, root cause, impact, recommendations, and the report — is yours to build. Good luck, Analyst. 🌱
