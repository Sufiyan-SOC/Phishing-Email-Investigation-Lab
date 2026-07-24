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





