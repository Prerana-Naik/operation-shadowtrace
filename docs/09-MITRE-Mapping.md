# MITRE ATT&CK Mapping

## Overview

The confirmed attacker activities observed during this investigation were mapped to the MITRE ATT&CK framework. This provides a standardized way of describing attacker behaviour and helps security teams compare incidents against known adversary techniques.

---

| MITRE Tactic | Technique | Evidence |
|--------------|-----------|----------|
| Initial Access | **T1110 – Brute Force** | Repeated SSH login attempts recorded in `auth.log`. |
| Initial Access | **T1078 – Valid Accounts** | Successful authentication using the compromised `deploy` account. |
| Discovery | **T1033 – System Owner/User Discovery** | `whoami` |
| Discovery | **T1082 – System Information Discovery** | `uname -a`, `/etc/os-release` |
| Privilege Escalation | **T1548 – Abuse Elevation Control Mechanism** | `sudo -l`, `sudo su -` |
| Persistence | **T1136 – Create Account** | Creation of the `svc_backup` account. |
| Persistence | **T1053.003 – Scheduled Task/Cron** | Scheduled execution of `.sysupd` using cron. |
| Command & Control | **T1105 – Ingress Tool Transfer** | Download of `.sysupd` using `wget`. |
| Defense Evasion | **T1070.003 – Clear Command History** | `history -c` |

---

## Summary

The investigation showed that the attacker followed several well-known attack techniques that align with the MITRE ATT&CK framework. Mapping these techniques provides a common language for documenting incidents and helps defenders recognize similar attack patterns in future investigations.