# Future Investigation

## Overview

Although the investigation successfully reconstructed the attack timeline, some questions remain unanswered due to the limited evidence available.

The following activities are recommended if additional evidence becomes available.

---

## Malware Analysis

The investigation confirmed that the `.sysupd` executable was downloaded, executed, and configured for persistence.

However, the actual executable was **not included** in the evidence package.

If the file becomes available, the following steps should be performed:

- Calculate its SHA-256 hash.
- Check its reputation using VirusTotal.
- Perform static malware analysis.
- Perform dynamic malware analysis in a secure sandbox.
- Determine whether it performs:
  - Command and Control (C2)
  - Credential theft
  - Data exfiltration
  - Additional persistence
  - Lateral movement

---

## Root Cause Investigation

The investigation confirmed that the `deploy` account was compromised.

However, the exact method used to obtain the credentials remains unknown.

Further investigation should include:

- Reviewing authentication logs from additional systems.
- Checking for password reuse.
- Reviewing the organization's password policy.
- Reviewing the SSH configuration.
- Verifying whether Multi-Factor Authentication (MFA) was enabled.
- Investigating possible phishing or credential leakage.

---

## Evidence Integrity

This case study focused on analysing the available evidence rather than collecting it.

In a real-world investigation, additional forensic procedures should include:

- Creating forensic disk images.
- Calculating SHA-256 hashes for collected evidence.
- Maintaining chain of custody documentation.
- Preserving original evidence before analysis.

---

## Summary

The available evidence was sufficient to reconstruct the attack, but additional forensic artifacts would be required to fully understand the attacker's objectives and the complete impact of the compromise.