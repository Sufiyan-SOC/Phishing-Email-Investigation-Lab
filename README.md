# Phishing Email Investigation Lab

> A comprehensive end-to-end SOC Analyst portfolio analyzing real-world phishing attack vectors including email header spoofing, malicious ISO payloads, social engineering PDFs, and multi-stage credential harvesting URLs.

---

## 📌 Project Overview

This lab showcases hands-on investigations into four distinct phishing attack vectors. As part of a Security Operations Center (SOC) investigation workflow, each case covers the complete life cycle of an email-borne threat—from raw header parsing and Indicator of Compromise (IOC) extraction to threat intelligence correlation, sandbox behavior analysis, and defensive recommendations.

---

## 🎯 Objectives

- **Identify & Extract IOCs:** Perform rigorous analysis on raw `.eml` files, email headers, attachments, and URLs to isolate malicious indicators.
- **Trace Attack Infrastructure:** Map sender infrastructure, IP origins, domain WHOIS records, and multi-stage HTTP redirection paths.
- **Correlate Threat Intelligence:** Leverage multi-scanner platforms (VirusTotal, Cisco Talos, Urlscan.io) to classify malware strains and reputation scores.

---

## 🛠️ Skills Demonstrated

- Email Header Analysis
- Phishing Investigation
- IOC Extraction
- Threat Intelligence
- OSINT
- Digital Forensics
- MITRE ATT&CK Mapping
- Report Writing

---

## 🧰 Tools Used

| Category | Tools |
|----------|-------|
| **Email Analysis** | Custom EML Extractor (`eioc.py`), MXToolbox, Header Parsers |
| **Threat Intelligence** | VirusTotal, Cisco Talos Intelligence, AbuseIPDB |
| **OSINT** | DomainTools WHOIS Lookup, Urlscan.io |
| **Linux Tools** | Terminal, `grep`, `sha256sum`, Bash Shell |
| **Hashing** | MD5, SHA-1, SHA-256 Checksums |
| **Reputation Services** | IPInfo, AbuseIPDB, VirusTotal Community |

---

## 📂 Repository Structure

```text
Phishing-Email-Investigation-Lab/
├── README.md
├── Case_01_Header_Analysis_Chase/
│   ├── Case_01_Report.md
│   └── screenshots/
│       ├── 01_phishing_email_body.png
│       ├── 02_raw_email_headers.png
│       ├── 03_mxtoolbox_header_analysis.png
│       ├── 04_whois_ip_lookup.png
│       ├── 05_abuseipdb_reputation.png
│       └── 06_terminal_extracted_headers.png
├── Case_02_Attachment_Analysis_ISO/
│   ├── Case_02_Report.md
│   └── screenshots/
│       ├── 01_email_with_iso_attachment.png
│       ├── 02_terminal_extracted_hashes.png
│       ├── 03_virustotal_malware_detection.png
│       └── 04_cisco_talos_threat_reputation.png
├── Case_03_Malicious_PDF_Analysis/
│   ├── Case_03_Report.md
│   └── screenshots/
│       ├── 01_amazon_pdf_lure_document.png
│       ├── 02_terminal_sha256_hash.png
│       └── 03_virustotal_pdf_detection.png
└── Case_04_Brand_Impersonation_URL_Amazon/
    ├── Case_04_Report.md
    └── screenshots/
        ├── 01_amazon_prime_phishing_email.png
        ├── 02_terminal_extracted_urls_headers.png
        ├── 03_whois_google_ip_info.png
        ├── 04_terminal_grep_extracted_domain.png
        ├── 05_virustotal_url_detection.png
        └── 06_urlscan_redirection_path.png


# 📁 Investigation Cases
## Case 01 – Email Header Analysis (Chase)
### Scenario
An incoming email impersonated Chase Bank warning the target of an immediate account block due to "unusual activities," pressuring them to click a reactivation link.
### Investigation Focus
Analyzing display header spoofing, verifying DKIM/DMARC authentication alignment, and tracing originating SMTP relays.
### Skills Used
Email Header Parsing, Reverse IP Lookup, DMARC/SPF Verification, Sender Infrastructure Tracking.
### Tools Used
MXToolbox, AbuseIPDB, DomainTools, Terminal (eioc.py).
### Report
View Detailed Case 01 Report
### Screenshots
 * 01_phishing_email_body.png - Visual representation of spoofed email.
 * 02_raw_email_headers.png - Uncut email header source.
 * 03_mxtoolbox_header_analysis.png - DMARC alignment failure readout.
 * 04_whois_ip_lookup.png - WHOIS record for 185.70.40.140.
 * 05_abuseipdb_reputation.png - IP abuse reputation details.
 * 06_terminal_extracted_headers.png - CLI extraction of header attributes.
## Case 02 – Malicious ISO Attachment Analysis
### Scenario
A spear-phishing attack delivered a fake invoice document containing a compressed quotation.iso attachment to deploy secondary malware payloads.
### Investigation Focus
Static malware analysis, cryptographic hash extraction, disk image inspection, and threat family mapping.
### Skills Used
Malware Hashing, Multi-AV Detection Correlation, Threat Intelligence Lookup.
### Tools Used
Linux Shell (sha256sum), Custom Python Script, VirusTotal, Cisco Talos.
### Report
View Detailed Case 02 Report
### Screenshots
 * 01_email_with_iso_attachment.png - Lure email with .iso file attached.
 * 02_terminal_extracted_hashes.png - MD5, SHA-1, SHA-256 execution output.
 * 03_virustotal_malware_detection.png - 38/59 AV vendor detection score.
 * 04_cisco_talos_threat_reputation.png - Cisco Talos verdict (Trojan.Androm).
## Case 03 – Malicious PDF Analysis
### Scenario
An email carrying an Amazon account hold notification contained a deceptively clean PDF (Statement.pdf) designed to bypass standard Secure Email Gateways (SEGs).
### Investigation Focus
Identifying social engineering lures, extracting PDF document hashes, checking for homoglyph evasion techniques, and verifying URL redirects inside PDFs.
### Skills Used
PDF Forensics, Hash Computation, Evasion Technique Identification.
### Tools Used
Terminal (sha256sum), VirusTotal Static Analysis & Code Insights.
### Report
View Detailed Case 03 Report
### Screenshots
 * 01_amazon_pdf_lure_document.png - Visual preview of fake Amazon PDF.
 * 02_terminal_sha256_hash.png - SHA-256 calculation terminal prompt.
 * 03_virustotal_pdf_detection.png - 24/63 AV vendor detection & threat breakdown.
## Case 04 – Amazon Brand Impersonation & URL Analysis
### Scenario
A fake Amazon Prime notification alleged an "unauthorized login from an Android device" to coerce the recipient into clicking a credential harvesting link.
### Investigation Focus
Tracing multi-stage URL redirections, analyzing hosting infrastructure, and identifying intermediate phishing reverse proxies.
### Skills Used
URL Analysis, Redirection Path Mapping, Domain Analysis, Web Infrastructure Profiling.
### Tools Used
Terminal (grep filtering), VirusTotal, DomainTools, Urlscan.io.
### Report
View Detailed Case 04 Report
### Screenshots
 * 01_amazon_prime_phishing_email.png - Amazon Prime alert email interface.
 * 02_terminal_extracted_urls_headers.png - Extracted URLs and header data.
 * 03_whois_google_ip_info.png - Google LLC originating relay IP info.
 * 04_terminal_grep_extracted_domain.png - CLI filtering for target domain.
 * 05_virustotal_url_detection.png - VirusTotal detection for cabinetlekagni[.]com.
 * 06_urlscan_redirection_path.png - Urlscan.io sandbox result showing redirect to sbffidserv.sviluppo[.]host.
# 🔍 Investigation Methodology
 1. **Initial Email Review:** Perform visual assessment of the sender name, email body, urgency tone, and branding.
 2. **Evidence Collection:** Preserve raw .eml source code and compute file integrity checksums.
 3. **Header Analysis:** Examine From, Reply-To, Return-Path, Received hops, and SPF/DKIM/DMARC status.
 4. **IOC Extraction:** Extract IP addresses, URLs, domains, and cryptographic hashes using automated scripts.
 5. **Threat Intelligence:** Cross-reference extracted IOCs against global threat feeds.
 6. **Reputation Checks:** Assess host and IP reputation scores via AbuseIPDB and DomainTools.
 7. **MITRE ATT&CK Mapping:** Map adversary techniques (e.g., Phishing, Domain Spoofing, Malicious File) to the ATT&CK framework.
 8. **Risk Assessment:** Determine threat severity, impact level, and target exposure.
 9. **Documentation:** Document complete findings, IOC list, and actionable mitigation strategies.
# 📊 Skills Matrix
| Skill | Case 1 | Case 2 | Case 3 | Case 4 |
|---|---|---|---|---|
| Email Header Analysis | ✅ | ✅ | ✅ | ✅ |
| IOC Extraction | ✅ | ✅ | ✅ | ✅ |
| Threat Intelligence | ✅ | ✅ | ✅ | ✅ |
| WHOIS Analysis | ✅ |  |  | ✅ |
| VirusTotal |  | ✅ | ✅ | ✅ |
| URL Analysis |  |  | ✅ | ✅ |
| Hash Analysis |  | ✅ | ✅ |  |
| MITRE ATT&CK | ✅ | ✅ | ✅ | ✅ |
| Report Writing | ✅ | ✅ | ✅ | ✅ |
# 📚 Key Learning Outcomes
 * **Authentication Flaws & Spoofing:** Learned how attackers exploit display name spoofing (alerts@chase.com) while sending via third-party services (ProtonMail), and how DMARC misalignment reveals spoofing attempts.
 * **Payload Evasion Dynamics:** Understood how threat actors leverage disk image files (.iso) and PDF documents (.pdf) to bypass traditional Secure Email Gateway (SEG) filters.
 * **Redirection Chain Tracking:** Gained hands-on experience using sandbox tools like Urlscan.io to unveil multi-stage redirects leading to credential harvesting pages hosted on compromised infrastructure.
 * **Defensive IOC Hygiene:** Developed skills to extract clean, actionable Indicators of Compromise (IPs, Hashes, Domains) to feed into SIEM/EDR detection rules.



# 👤 Author
**Your Name**
 * **LinkedIn:** [Your LinkedIn Profile URL]
 * **GitHub:** [Your GitHub Profile URL]
 * **Email:** your.email@example.com
