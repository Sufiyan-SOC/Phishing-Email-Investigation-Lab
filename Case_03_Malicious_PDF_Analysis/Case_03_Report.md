
# Case 03 – Malicious PDF Analysis

---

# Executive Summary

> A social engineering phishing email disguised as an Amazon Customer Support alert delivered a PDF document named `Statement.pdf`. The document notified the recipient of an "unusual payment activity hold" and contained embedded hyperlink buttons. Forensic inspection identified high-pressure social engineering and homoglyph character substitutions designed to evade automated email filters. Multi-AV analysis yielded a **24/63** detection score.

---

# Incident Information

| Field | Details |
|-------|---------|
| Case ID | PHISH-2022-003 |
| Incident Type | Malicious PDF Document / Social Engineering Lure |
| Severity | Medium-High |
| Status | Closed / Remediated |
| Analyst | Security Operations Center (SOC) |
| Date | September 16, 2022 |

---

# Investigation Objective

Inspect the embedded structural components of `Statement.pdf`, calculate unique file hashes, evaluate vendor detection scores, and identify embedded phishing URLs.

---

# Scope of Investigation

- File hash extraction and integrity verification.
- Structural inspection for embedded scripts, objects, and external hyperlinks.
- Multi-scanner threat correlation on VirusTotal.

---

# Tools Used

- **Linux Terminal:** `sha256sum` utility.
- **VirusTotal:** Document analysis and vendor signature verification.
- **Pdfid / Pdf-parser (Conceptual):** Document object inspection.

---

# Evidence Collected

| Evidence | Screenshot |
|----------|------------|
| Amazon PDF Lure Document | `screenshots/01_amazon_pdf_lure_document.png` |
| Terminal SHA-256 Output | `screenshots/02_terminal_sha256_hash.png` |
| VirusTotal PDF Detection | `screenshots/03_virustotal_pdf_detection.png` |

---

# Investigation Workflow

## Step 1 – Initial Document Review

### Observation
The file `Statement.pdf` displays an Amazon Customer Service header claiming account restrictions due to unauthorized payment activity. A prominent "Verify Now" button redirects users to an external web page.

### Findings
- The PDF contains no automated exploit code or active macros.
- It relies entirely on social engineering coercion to trick recipients into clicking embedded credential-harvesting links.

![PDF Document Preview](screenshots/01_amazon_pdf_lure_document.png)

---

## Step 2 – File Integrity & Cryptographic Hash Extraction

### Hashes Generated
Executed static hashing in the terminal:

- **Filename:** `Statement.pdf`
- **File Size:** ~30.78 KB
- **SHA-256:** `e90e263bce015c0ad6640d2581582aee4f940accc18d688a25d9a319e39c4110`

### Findings
Generating the SHA-256 hash allowed identification of pre-analyzed samples in threat databases.

![Terminal SHA256 Output](screenshots/02_terminal_sha256_hash.png)

---

## Step 3 – Multi-AV Detection & Threat Analysis

### Analysis Performed
Queried `e90e263bce015c0ad6640d2581582aee4f940accc18d688a25d9a319e39c4110` on VirusTotal.

### Findings
- **Detection Score:** **24 / 63** Security Vendors flagged as Malicious.
- **Vendor Classifications:** `Trojan:PDF/Agent.DE`, `PDF:MalwareX-gen [Phish]`, `Phish.PDF.Amazon`.
- Automated code insights highlighted the use of homoglyph character substitutions to bypass keyword-based content inspection engines.

![VirusTotal Detection](screenshots/03_virustotal_pdf_detection.png)

---

# Indicators of Compromise (IOCs)

## File Hashes

| Hash Type | Value |
|-----------|-------|
| SHA-256 | `e90e263bce015c0ad6640d2581582aee4f940accc18d688a25d9a319e39c4110` |

---

## Impersonated Brand

| Brand | Targeted Domain |
|-------|-----------------|
| Amazon Customer Support | `amazon.com` (Spoofed Display Lure) |

---

# MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Phishing: Spearphishing Attachment | T1566.001 |
| Deception: Homoglyph Attack | T1036.005 |
| User Execution: Malicious Link | T1204.001 |

---

# Risk Assessment

| Category | Rating |
|----------|--------|
| Impact | Medium (Credential Theft) |
| Likelihood | High (Plausible E-commerce Lure) |
| Overall Risk | **Medium-High** |

---

# Detection Opportunities

- **PDF Embedded Link Rewriting:** Implement Secure Email Gateway link rewriting (URL defense) to inspect links inside incoming PDF attachments.
- **Homoglyph Detection:** Configure content inspection rules to detect Cyrillic/Latin character substitution anomalies in incoming documents.

---

# Recommendations

- Add SHA-256 hash `e90e263bce015c0ad6640d2581582aee4f940accc18d688a25d9a319e39c4110` to gateway blocklists.
- Train users to navigate directly to official merchant portals instead of clicking links inside PDF statements.

---

# Conclusion

> Case 03 is a social engineering PDF attachment attack targeting Amazon credentials. By leveraging clean PDF document structures and character substitution techniques, the payload partially evades static filters while directing users to credential harvesting infrastructure.

---

# Lessons Learned

- Attackers frequently use PDF attachments as "clickable containers" to bypass traditional SEG link scanners.
- Static file hashing remains a fast and reliable method for identifying previously seen malicious documents.

---

# References

- [VirusTotal Intelligence](https://www.virustotal.com/)
- [PDF Security Best Practices - CISA](https://www.cisa.gov/)
- 
