# Case 02 – Malicious ISO Attachment Analysis

---

# Executive Summary

> A spear-phishing email targeting finance operations was detected containing a compressed disk image file (`quotation.iso`). The lure impersonated a wire transfer payment notification ("Due Invoice Payment"). Static forensic analysis and hash extraction confirmed that the ISO container harbored a malicious executable belonging to known Trojan/Stealer malware families (`Trojan.Androm`, `Fareit`), flagged by 38 out of 59 security vendors.

---

# Incident Information

| Field | Details |
|-------|---------|
| Case ID | PHISH-2022-002 |
| Incident Type | Malicious Attachment Delivery / Trojan Malware |
| Severity | High |
| Status | Closed / Remediated |
| Analyst | Security Operations Center (SOC) |
| Date | September 16, 2022 |

---

# Investigation Objective

Analyze the suspicious attachment contained in the wire transfer email, extract cryptographic file hashes, evaluate malware classification through multi-AV threat intelligence, and establish endpoint detection coverage.

---

# Scope of Investigation

- Static extraction and hash generation (MD5, SHA-1, SHA-256) of the `.iso` file payload.
- Threat intelligence querying against VirusTotal and Cisco Talos Intelligence.
- Extraction of threat vendor signatures and MITRE ATT&CK mapping.

---

# Tools Used

- **Linux Terminal:** `sha256sum`, `md5sum`, and custom extraction script (`eioc.py`).
- **VirusTotal:** Multi-scanner malware engine & threat behavior analysis.
- **Cisco Talos Intelligence:** Threat reputation and malware family classification.

---

# Evidence Collected

| Evidence | Screenshot |
|----------|------------|
| Email with ISO Attachment | `screenshots/01_email_with_iso_attachment.png` |
| Terminal Extracted Hashes | `screenshots/02_terminal_extracted_hashes.png` |
| VirusTotal Malware Detection | `screenshots/03_virustotal_malware_detection.png` |
| Cisco Talos Reputation | `screenshots/04_cisco_talos_threat_reputation.png` |

---

# Investigation Workflow

## Step 1 – Initial Email Review

### Observation
An inbound message from `Paol.Reggiani@moss.it` requested urgent attention regarding a pending invoice wire transfer, urging the recipient to open the attached `quotation.iso` file.

### Findings
- Threat actors commonly use disk images (`.iso`, `.img`) to evade Secure Email Gateway (SEG) scanners, as ISO files mount natively in Windows without triggering macro warnings.
- Urgent financial wording was used to prompt immediate execution.

![Email Attachment Lure](screenshots/01_email_with_iso_attachment.png)

---

## Step 2 – Cryptographic Hash Extraction

### Hashes Generated
Extracted file checksums via Linux command-line utilities in an isolated analysis environment:

- **Filename:** `quotation.iso`
- **File Size:** ~112 KB
- **MD5:** `593b160f08cb36ebfa5b5fefddb15cf7`
- **SHA-1:** `8a12e3e571e21b71d932e6503c14d9e03fa37c3a`
- **SHA-256:** `75fdb848eac332b4ca7d88f497e7ba7ebbb9a798d825b28cf1f87b9d7149e87f`

### Findings
Generating unique cryptographic signatures allows safe threat intelligence lookups without executing the payload.

![Terminal Extracted Hashes](screenshots/02_terminal_extracted_hashes.png)

---

## Step 3 – Multi-AV Detection Analysis

### Analysis Performed
Queried the generated SHA-256 hash against VirusTotal intelligence feeds.

### Findings
- **Detection Ratio:** **38 / 59** Security Vendors flagged the file as malicious.
- **Classification Categories:** `trojan.androm/fareit`, `Win32:Trojan-gen`, `Trojan.GenericKD`.

![VirusTotal Analysis](screenshots/03_virustotal_malware_detection.png)

---

## Step 4 – Threat Intelligence Deep Dive

### Cisco Talos Results
Cross-referenced the hash against Cisco Talos reputation databases.

### Findings
- Verified high-severity threat rating.
- Identified primary target behaviors: Information stealing, dropping secondary payloads, and credential dumping.

![Cisco Talos Analysis](screenshots/04_cisco_talos_threat_reputation.png)

---

# Indicators of Compromise (IOCs)

## Hashes

| Hash Type | Value |
|-----------|-------|
| MD5 | `593b160f08cb36ebfa5b5fefddb15cf7` |
| SHA-1 | `8a12e3e571e21b71d932e6503c14d9e03fa37c3a` |
| SHA-256 | `75fdb848eac332b4ca7d88f497e7ba7ebbb9a798d825b28cf1f87b9d7149e87f` |

---

## Domains & Email Addresses

| Indicator | Description |
|-----------|-------------|
| `Paol.Reggiani@moss.it` | Compromised or spoofed sender address |
| `moss.it` | Sender Domain |

---

# MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Phishing: Spearphishing Attachment | T1566.001 |
| User Execution: Malicious File | T1204.002 |
| Virtualization/Sandbox Evasion: Container Files | T1497 |

---

# Risk Assessment

| Category | Rating |
|----------|--------|
| Impact | Critical (Potential Endpoint Compromise & Credential Theft) |
| Likelihood | Medium (Requires User Interaction to Mount and Execute) |
| Overall Risk | **High** |

---

# Detection Opportunities

- **Block Container Extensions:** Configure SEGs to block or quarantine inbound emails with `.iso`, `.img`, or compressed archive attachments from external sources.
- **EDR Hashes Block:** Populate EDR blocklists with the extracted SHA-256 hash.
- **Auto-Mount Monitoring:** Monitor Windows Event Logs for unexpected mounting of virtual disk images by non-administrative users.

---

# Recommendations

- Immediately deploy SHA-256 block rules across EDR and AV solutions.
- Restrict default Windows behavior for automatically mounting ISO files via Group Policy (GPO).
- Quarantine all incoming messages from `Paol.Reggiani@moss.it`.

---

# Conclusion

> Case 02 is a confirmed malicious attachment campaign delivering a Trojan payload contained in an ISO container. Multi-scanner detection confirmed a 38/59 malicious rating, demonstrating an intentional bypass strategy against traditional attachment filters.

---

# Lessons Learned

- Modern phishing campaigns frequently use `.iso` files to bypass legacy email security rules that only scrutinize executable extensions (`.exe`, `.scr`).
- Static analysis using cryptographic hashes quickly confirms threat status without risk of infection.

---

# References

- [VirusTotal Malware Database](https://www.virustotal.com/)
- [Cisco Talos Intelligence](https://talosintelligence.com/)
- 
