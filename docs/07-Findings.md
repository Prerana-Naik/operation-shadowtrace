# Investigation Findings

## Confirmed Findings

The investigation confirmed the following activities:

- Successful SSH compromise of the `deploy` account.
- Privilege escalation to the root account.
- Creation of a hidden privileged account (`svc_backup`).
- Assignment of a password to the new account.
- Download and execution of the `.sysupd` payload.
- Persistence established using a scheduled cron job.
- Outbound communication with the external IP address **185.220.101.47**.
- Attempted defense evasion through Bash history clearing.

---

## Suspected Findings

The following observations remain unconfirmed:

- `.sysupd` is suspected to be malicious.
- Possible malware activity.
- Possible data exfiltration.
- Additional persistence mechanisms may exist.

These observations require further investigation before they can be confirmed.

---

## Unknowns

The investigation could not determine:

- How the `deploy` credentials were obtained.
- The exact functionality of `.sysupd`.
- Whether sensitive data was accessed or stolen.
- The identity of the attacker.
- Whether additional systems were affected.

---

## Incident Severity

**Severity:** High

### Justification

The incident resulted in:

- Unauthorized remote access.
- Root privilege escalation.
- Persistent attacker access.
- Execution of an external payload.
- Ongoing outbound communication.

Although destructive activity or data theft could not be confirmed, the compromise represents a High Severity security incident requiring immediate remediation.