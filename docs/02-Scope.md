# Scope of Investigation

## Objective

The objective of this investigation was to determine whether the production Linux server had been compromised, reconstruct the attack timeline, identify attacker activity, and recommend appropriate security improvements.

---

## Investigated System

| Item | Value |
|------|-------|
| Hostname | prod-linux-01 |
| Operating System | Linux |
| Primary Services | Apache, SSH, PostgreSQL |

---

## Investigation Time Window

- 21 June
- 22 June

---

## Evidence Reviewed

- auth.log
- syslog
- bash_history_deploy_user
- bash_history_root_shell
- crontab_svc_backup
- ps_aux.txt
- ss_output.txt
- passwd
- shadow

---

## Investigation Methodology

The investigation followed an evidence-driven approach.

Each forensic artifact was analyzed independently before being correlated with other evidence to reconstruct the complete attack timeline. Conclusions were based only on confirmed evidence, while unsupported assumptions were documented separately as limitations or future investigation items.