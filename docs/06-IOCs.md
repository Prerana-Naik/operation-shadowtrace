# Indicators of Compromise (IOCs)

## Overview

The following Indicators of Compromise (IOCs) were identified during the investigation.

These artifacts may assist defenders in detecting similar activity in other systems.

---

## External IP Address

| Type | Value |
|------|-------|
| Attacker IP | **185.220.101.47** |

---

## Compromised Account

- deploy

---

## Malicious Account

- svc_backup

---

## Downloaded Payload

- /usr/local/bin/.sysupd

---

## Download URL

- http://185.220.101.47:8000/sysupd

---

## Persistence Mechanism

```text
*/5 * * * * /usr/local/bin/.sysupd >/dev/null 2>&1
```

---

## Suspicious Commands

- sudo su -
- useradd
- passwd
- wget
- chmod +x
- disown -a
- history -c
- ps aux | grep sysupd

---

## Important File Paths

- /usr/local/bin/.sysupd
- /var/spool/cron/crontabs/svc_backup
- /var/log/auth.log

---

## Hostname

- prod-linux-01