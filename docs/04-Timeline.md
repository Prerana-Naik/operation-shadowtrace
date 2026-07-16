# Timeline Reconstruction

## Overview

This timeline reconstructs the attack by correlating evidence from authentication logs, Bash history, system logs, process information, network connections, and user account records.

The events are presented in chronological order to illustrate the complete attack lifecycle.

---

| Date & Time | Event | Evidence |
|-------------|-------|----------|
| **21 Jun – 23:41:07** | Repeated SSH brute-force attempts began against multiple user accounts from **185.220.101.47**. | auth.log |
| **22 Jun – 02:03:15** | Successful SSH authentication using the **deploy** account. | auth.log |
| **Immediately after login** | The attacker performed reconnaissance using `whoami`, `id`, `uname -a`, and `cat /etc/os-release`. | bash_history_deploy_user |
| **Following reconnaissance** | Available sudo permissions were enumerated using `sudo -l`. | bash_history_deploy_user |
| **Shortly afterwards** | Root privileges were obtained using `sudo su -`. | bash_history_deploy_user |
| **Root session** | The attacker verified administrative access using `whoami`. | bash_history_root_shell |
| **Next** | A new privileged account (`svc_backup`) was created with UID 0 and configured for interactive login. | bash_history_root_shell + passwd + shadow |
| **Next** | A cron job was created to execute `/usr/local/bin/.sysupd` every five minutes. | bash_history_root_shell + crontab_svc_backup |
| **Next** | The `.sysupd` payload was downloaded from **185.220.101.47** using `wget`. | bash_history_root_shell |
| **Next** | Execute permissions were granted using `chmod +x`. | bash_history_root_shell |
| **Next** | The payload was executed in the background and detached using `disown -a`. | bash_history_root_shell |
| **Next** | The attacker confirmed that the payload was running using `ps aux \| grep sysupd`. | bash_history_root_shell + ps_aux |
| **Next** | The attacker reviewed the last entries of `auth.log`. | bash_history_root_shell |
| **Final attacker command** | An attempt was made to clear the shell history using `history -c`. | bash_history_root_shell |
| **22 Jun – 02:16:03** | A login session for the newly created `svc_backup` account was opened. | auth.log |
| **22 Jun – 02:16:45** | The `svc_backup` session was closed. | auth.log |
| **22 Jun – 02:17:03** | The cron daemon reloaded the new crontab associated with `svc_backup`. | syslog |
| **22 Jun – 02:20:00 onwards** | `.sysupd` began executing automatically every five minutes through the cron service. | syslog + crontab_svc_backup |
| **During execution** | Network communication between `.sysupd` and **185.220.101.47** was observed. | ss_output |
| **Evidence snapshot** | Process analysis confirmed that `.sysupd` was actively running under both `root` and `svc_backup`. | ps_aux |

---

# Timeline Summary

The reconstructed timeline shows a clear progression of attacker activity:

1. Initial Access through SSH brute-force.
2. Successful compromise of the `deploy` account.
3. Reconnaissance of the compromised system.
4. Privilege escalation to the root account.
5. Creation of a hidden privileged account (`svc_backup`).
6. Download and execution of the `.sysupd` payload.
7. Persistence established through a scheduled cron job.
8. Outbound communication with the external attacker.
9. Attempted defense evasion by clearing command history.

The consistency of events across multiple evidence sources provides high confidence in the reconstructed attack sequence.