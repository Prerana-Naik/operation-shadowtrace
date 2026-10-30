Digital Forensics | Incident Response | Linux | DFIR | MITRE ATT&CK | TryHackMe

# 🕵️ Operation ShadowTrace

> **A Linux Digital Forensics & Incident Response (DFIR) Case Study**

## 📖 Overview

Operation ShadowTrace is my first independent cybersecurity case study, created after completing the TryHackMe **Pre Security** and **Cyber Security 101** learning paths.

The objective of this project was to investigate a simulated Linux server compromise using forensic evidence, reconstruct the attack timeline, identify attacker activities, and produce a professional incident response report.

Rather than following a guided lab, this project was approached as a realistic DFIR investigation where conclusions were drawn only from the available evidence.

```text
External Attacker
        │
        ▼
SSH Brute Force
        │
        ▼
Compromised deploy Account
        │
        ▼
Privilege Escalation
        │
        ▼
Create svc_backup
        │
        ▼
Download .sysupd
        │
        ▼
Persistence via Cron
        │
        ▼
Network Communication
```
---

# 🎯 Objectives

The investigation aimed to answer the following questions:

- Was the Linux server compromised?
- How did the attacker gain access?
- What actions were performed after compromise?
- Was persistence established?
- Was malware executed?
- What Indicators of Compromise (IOCs) can be identified?
- What security improvements should be recommended?

---

# 🖥️ Investigation Scenario

A Linux production server (**prod-linux-01**) was reported to be behaving abnormally.

As the assigned DFIR analyst, my objective was to investigate the available forensic artifacts, reconstruct the incident timeline, identify attacker techniques, and determine the overall impact of the compromise.

---

# 🔍 Investigation Workflow

```text
Evidence Collection
        ↓
Evidence Analysis
        ↓
Evidence Correlation
        ↓
Timeline Reconstruction
        ↓
IOC Identification
        ↓
Incident Report
        ↓
Security Recommendations
```

---

# 📂 Repository Structure

```text
│
├───Docs
│       01-Executive-Summary.md
│       02-Scope.md
│       03-Attack-Narrative.md
│       04-Timeline.md
│       05-Evidence-Analysis.md
│       06-IOCs.md
│       07-Findings.md
│       08-Recommendations.md
│       09-MITRE-Mapping.md
│       10-Future-Investigation.md
│       11-Lessons-Learned.md
│
├───Evidence
│   │   EVIDENCE_MANIFEST.md
│   │
│   └───evidence
│           auth.log
│           bash_history_deploy_user
│           bash_history_root_shell
│           crontab_svc_backup
│           passwd
│           ps_aux.txt
│           shadow
│           ss_output.txt
│           syslog
│
└───Images
|        attack-timeline.png
|        evidence-correlation.png
|        investigation-workflow.png
|
|  .gitignore
│   LICENSE
│   README.md
```
---

# 🛠️ Evidence Analysed

- auth.log
- syslog
- passwd
- shadow
- bash_history_deploy_user
- bash_history_root_shell
- ps_aux
- ss_output
- crontab

---

# 🔎 Key Findings

The investigation confirmed:

- Successful SSH compromise of the `deploy` account.
- Privilege escalation to the root account.
- Creation of a hidden privileged account (`svc_backup`).
- Download and execution of the `.sysupd` payload.
- Persistence established using a scheduled cron job.
- Outbound communication with the external IP **185.220.101.47**.
- Attempted defense evasion by clearing shell history.

Although the compromise was confirmed, the exact functionality of the payload and any potential data exfiltration could not be determined from the available evidence.

---

# 🛡️ MITRE ATT&CK Techniques
```text
| Tactic | Technique |
|---------|-----------|
| Initial Access | Brute Force (T1110) |
| Initial Access | Valid Accounts (T1078) |
| Discovery | System Information Discovery (T1082) |
| Discovery | System Owner/User Discovery (T1033) |
| Privilege Escalation | Abuse Elevation Control Mechanism (T1548) |
| Persistence | Create Account (T1136) |
| Persistence | Scheduled Task/Cron (T1053.003) |
| Defense Evasion | Clear Command History (T1070.003) |
```
---

# 📚 Skills Demonstrated

- ✅ Linux Log Analysis
- ✅ Digital Forensics
- ✅ Incident Response
- ✅ Timeline Reconstruction
- ✅ Evidence Correlation
- ✅ IOC Identification
- ✅ MITRE ATT&CK Mapping
- ✅ Security Documentation
- ✅ Professional Report Writing

---

# 📖 Lessons Learned

This project reinforced the importance of:

- Following evidence instead of assumptions.
- Correlating multiple evidence sources.
- Separating confirmed findings from hypotheses.
- Documenting investigations in a professional manner.

---

# 🚀 Future Improvements

Future investigations could include:

- Memory forensics
- Malware analysis
- Threat intelligence enrichment
- Network packet analysis (PCAP)
- YARA rule development
- Cloud-based incident response scenarios

---

# ⚠️ Disclaimer

This repository is an educational case study created for learning Digital Forensics and Incident Response (DFIR).

The evidence package is intentionally simulated to provide a realistic investigation experience.

---

## 👩‍💻 Author

**Prerana Naik**

B.E. Computer Science & Engineering

Aspiring Security & GRC Professional

Building practical cybersecurity case studies as part of my learning journey.

# 🌱 Why I Built This Project

After completing foundational cybersecurity learning paths, I wanted to move beyond guided exercises and apply my knowledge to an independent investigation. Operation ShadowTrace represents my first attempt at approaching a cybersecurity problem the way a DFIR analyst would: by asking questions, examining evidence, correlating findings, and documenting conclusions based solely on available evidence.
