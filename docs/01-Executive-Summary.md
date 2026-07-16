# Executive Summary

## Case Information

| Item | Details |
|------|---------|
| **Case Name** | Operation ShadowTrace |
| **Organization** | NorthWave Technologies |
| **Investigation Type** | Linux Digital Forensics & Incident Response (DFIR) |
| **Severity** | High |
| **Affected Host** | prod-linux-01 |
| **Investigation Period** | 21–22 June |
| **Analyst** | Prerana Naik |

---

## Executive Summary

Operation ShadowTrace investigated a suspected compromise of the production Linux server **prod-linux-01** belonging to **NorthWave Technologies**.

Analysis of the provided forensic evidence confirmed that an external attacker successfully gained access to the server through SSH by compromising the `deploy` account. After obtaining access, the attacker performed reconnaissance, escalated privileges to the root account, created a new privileged user (`svc_backup`), and established persistence using a scheduled cron job.

Further investigation showed that an external executable named `.sysupd` was downloaded, executed, and repeatedly launched every five minutes. Network analysis confirmed outbound communication between the compromised server and the external IP address **185.220.101.47**.

Although the compromise, persistence mechanism, and network communication were confirmed, the available evidence was insufficient to determine the exact functionality of the `.sysupd` payload or confirm whether sensitive data was accessed or exfiltrated.

The incident was assessed as **High Severity** due to the confirmed compromise of a production server, successful privilege escalation, persistent attacker access, and continued outbound communication.

---

## Key Outcomes

- ✅ SSH compromise confirmed.
- ✅ Root privilege escalation confirmed.
- ✅ Hidden privileged account (`svc_backup`) created.
- ✅ Persistent cron-based execution established.
- ✅ External payload (`.sysupd`) downloaded and executed.
- ✅ Outbound communication with the attacker confirmed.
- ❓ Malware functionality and data exfiltration could not be confirmed.

---

## Business Impact

The investigation confirmed that the production Linux server was successfully compromised and persistent access was established.

Although no evidence confirmed data theft or service disruption, unauthorized root-level access to a business-critical server represents a significant security risk. Immediate containment, credential rotation, and system remediation would be required in a real-world incident.