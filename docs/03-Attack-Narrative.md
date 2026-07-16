# Attack Narrative

## Overview

This section reconstructs the attack sequence based on the forensic evidence collected during the investigation.

The reconstruction was developed by correlating authentication logs, Bash history, system logs, process information, network connections, and user account data.

---

## Attack Progression

The attack began with repeated SSH authentication attempts against multiple user accounts on the production Linux server **prod-linux-01**. These attempts originated from the external IP address **185.220.101.47** and targeted several usernames, including `admin`, `root`, `oracle`, `ubuntu`, `postgres`, and `deploy`.

After numerous failed attempts, the attacker successfully authenticated using the **deploy** account. The available evidence confirms the successful login but does not reveal how the credentials were obtained. Therefore, the method of credential compromise remains unknown.

Once access was established, the attacker performed basic reconnaissance to understand the compromised environment. Commands such as `whoami`, `id`, `uname -a`, and `cat /etc/os-release` were used to identify the current user, operating system, and available privileges. The attacker also reviewed the permissions available through `sudo`.

The attacker then successfully escalated privileges by executing `sudo su -`, gaining administrative access to the system.

With root privileges, a new account named **svc_backup** was created and configured with root-equivalent privileges (UID 0). A password was assigned to the account, allowing it to be used for future authentication.

To establish persistence, the attacker created a scheduled cron job that executed the file `/usr/local/bin/.sysupd` every five minutes under the `svc_backup` account. This allowed the payload to continue executing without requiring additional interactive logins.

The attacker downloaded the `.sysupd` executable from **185.220.101.47** using `wget`, saved it locally, granted execute permissions, and launched it in the background. The running process was detached from the shell using `disown`, ensuring that it continued running after the session ended.

Analysis of the process list confirmed that the payload was actively executing, while network analysis showed outbound communication between the compromised server and the same external IP address from which the payload had been downloaded.

Before ending the session, the attacker reviewed the recent authentication logs and attempted to clear the shell history using `history -c`. Although this suggests an effort to reduce forensic evidence, the Bash history was successfully recovered as part of the investigation.

---

## Summary

The reconstructed attack demonstrates a structured intrusion in which the attacker:

- Gained unauthorized SSH access.
- Performed reconnaissance.
- Escalated privileges.
- Established persistence.
- Executed an external payload.
- Maintained outbound communication.
- Attempted to reduce forensic evidence.

The available evidence supports this sequence with a high level of confidence. However, the functionality of the `.sysupd` payload and the method used to obtain the `deploy` account credentials remain unknown.