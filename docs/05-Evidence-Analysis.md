# Evidence Analysis

## Overview

The investigation was conducted by analysing multiple forensic artifacts collected from the compromised Linux server.

Each evidence source contributed different information, allowing the complete attack sequence to be reconstructed through evidence correlation.

---

## Evidence Summary

| Evidence | Purpose | Key Findings |
|----------|---------|--------------|
| **auth.log** | Authentication events | Confirmed SSH brute-force attempts, successful login using the `deploy` account, privilege escalation, and creation of the `svc_backup` account. |
| **syslog** | System activity | Confirmed cron service activity and repeated execution of `.sysupd` every five minutes. |
| **bash_history_deploy_user** | User activity | Showed reconnaissance commands and successful privilege escalation using `sudo`. |
| **bash_history_root_shell** | Root activity | Revealed creation of `svc_backup`, download and execution of `.sysupd`, cron configuration, and attempted history deletion. |
| **crontab_svc_backup** | Persistence | Confirmed the cron configuration responsible for automatically executing `.sysupd`. |
| **ps_aux.txt** | Running processes | Confirmed that `.sysupd` was actively running under both `root` and `svc_backup`. |
| **ss_output.txt** | Network connections | Confirmed SSH access from the attacker and outbound communication between `.sysupd` and **185.220.101.47**. |
| **passwd** | User accounts | Confirmed the existence of the newly created privileged account (`svc_backup`) with UID 0. |
| **shadow** | Authentication database | Confirmed that a password had been assigned to `svc_backup`, allowing interactive authentication. |

---

## Evidence Correlation

The strongest findings in this investigation were supported by multiple independent evidence sources.

| Finding | Supporting Evidence |
|----------|---------------------|
| SSH compromise | auth.log + ss_output |
| Privilege escalation | bash_history_deploy_user + bash_history_root_shell |
| Creation of `svc_backup` | bash_history_root_shell + passwd + shadow |
| Persistence | bash_history_root_shell + crontab_svc_backup + syslog |
| Payload execution | bash_history_root_shell + ps_aux |
| Network communication | ss_output + bash_history_root_shell |

---

## Summary

No single evidence source was sufficient to reconstruct the complete attack.

By correlating authentication logs, Bash history, system logs, process information, network connections, and account databases, the complete attack lifecycle was reconstructed with a high level of confidence.