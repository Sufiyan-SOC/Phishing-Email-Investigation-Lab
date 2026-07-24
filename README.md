# Phishing Email Investigation Lab

> A comprehensive end-to-end SOC Analyst portfolio analyzing phishing attack vectors including email header spoofing, malicious ISO payloads, social engineering PDFs, and multi-stage credential harvesting URLs.

---

## 📌 Project Overview

This repository showcases hands-on phishing investigations performed in a controlled lab environment. Each case follows a Security Operations Center (SOC) investigation workflow, from evidence collection and IOC extraction to threat intelligence correlation, analysis, and documentation.

---

## 🎯 Objectives

- Identify and extract Indicators of Compromise (IOCs) from phishing emails, attachments, and URLs.
- Analyze email headers to verify sender authenticity and identify spoofing techniques.
- Investigate malicious attachments using hashing and threat intelligence platforms.
- Analyze phishing URLs and redirection chains.
- Document findings using professional SOC-style incident reports.

---

## 🛠️ Skills Demonstrated

- Email Header Analysis
- Phishing Investigation
- IOC Extraction
- Threat Intelligence
- OSINT
- Digital Forensics
- MITRE ATT&CK Mapping
- Incident Report Writing

---

## 🧰 Tools Used

| Category | Tools |
|----------|-------|
| Email Analysis | Custom EML Extractor (`eioc.py`), MXToolbox |
| Threat Intelligence | VirusTotal, Cisco Talos, AbuseIPDB |
| OSINT | WHOIS Lookup, Urlscan.io |
| Linux Tools | Bash, grep, sha256sum |
| Hashing | MD5, SHA-1, SHA-256 |
| Reputation Services | IPInfo, AbuseIPDB, VirusTotal |

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
│
├── Case_02_Attachment_Analysis_ISO/
│   ├── Case_02_Report.md
│   └── screenshots/
│       ├── 01_email_with_iso_attachment.png
│       ├── 02_terminal_extracted_hashes.png
│       ├── 03_virustotal_malware_detection.png
│       └── 04_cisco_talos_threat_reputation.png
│
├── Case_03_Malicious_PDF_Analysis/
│   ├── Case_03_Report.md
│   └── screenshots/
│       ├── 01_amazon_pdf_lure_document.png
│       ├── 02_terminal_sha256_hash.png
│       └── 03_virustotal_pdf_detection.png
│
└── Case_04_Brand_Impersonation_URL_Amazon/
    ├── Case_04_Report.md
    └── screenshots/
        ├── 01_amazon_prime_phishing_email.png
        ├── 02_terminal_extracted_urls_headers.png
        ├── 03_whois_google_ip_info.png
        ├── 04_terminal_grep_extracted_domain.png
        ├── 05_virustotal_url_detection.png
        └── 06_urlscan_redirection_path.png
```

---

# 📁 Investigation Cases

## Case 01 – Email Header Analysis (Chase)

### Investigation Focus

- Email Header Analysis
- SPF/DKIM/DMARC Validation
- SMTP Relay Analysis
- Sender Infrastructure Verification

### Skills Used

- Email Header Parsing
- Reverse IP Lookup
- DMARC/SPF Verification
- IOC Extraction

### Tools Used

- MXToolbox
- AbuseIPDB
- WHOIS Lookup
- Linux Terminal (`eioc.py`)

### Report

- `Case_01_Header_Analysis_Chase/Case_01_Report.md`

### Screenshots

- 01_phishing_email_body.png
- 02_raw_email_headers.png
- 03_mxtoolbox_header_analysis.png
- 04_whois_ip_lookup.png
- 05_abuseipdb_reputation.png
- 06_terminal_extracted_headers.png

---

## Case 02 – Malicious ISO Attachment Analysis

### Investigation Focus

- Static Malware Analysis
- File Hash Calculation
- Threat Intelligence Correlation
- Attachment Reputation Analysis

### Skills Used

- Malware Hashing
- Threat Intelligence
- IOC Extraction

### Tools Used

- sha256sum
- VirusTotal
- Cisco Talos
- Python Script

### Report

- `Case_02_Attachment_Analysis_ISO/Case_02_Report.md`

### Screenshots

- 01_email_with_iso_attachment.png
- 02_terminal_extracted_hashes.png
- 03_virustotal_malware_detection.png
- 04_cisco_talos_threat_reputation.png

---

## Case 03 – Malicious PDF Analysis

### Investigation Focus

- PDF File Analysis
- Hash Verification
- Threat Intelligence Lookup
- Social Engineering Detection

### Skills Used

- PDF Forensics
- Hash Analysis
- IOC Extraction

### Tools Used

- sha256sum
- VirusTotal

### Report

- `Case_03_Malicious_PDF_Analysis/Case_03_Report.md`

### Screenshots

- 01_amazon_pdf_lure_document.png
- 02_terminal_sha256_hash.png
- 03_virustotal_pdf_detection.png

---

## Case 04 – Brand Impersonation & URL Analysis (Amazon)

### Investigation Focus

- URL Extraction
- Domain Analysis
- URL Reputation Analysis
- Redirection Chain Investigation

### Skills Used

- URL Analysis
- Domain Investigation
- Threat Intelligence
- IOC Extraction

### Tools Used

- grep
- VirusTotal
- WHOIS
- Urlscan.io

### Report

- `Case_04_Brand_Impersonation_URL_Amazon/Case_04_Report.md`

### Screenshots

- 01_amazon_prime_phishing_email.png
- 02_terminal_extracted_urls_headers.png
- 03_whois_google_ip_info.png
- 04_terminal_grep_extracted_domain.png
- 05_virustotal_url_detection.png
- 06_urlscan_redirection_path.png

---

# 🔍 Investigation Methodology

1. Initial Email Review
2. Evidence Collection
3. Email Header Analysis
4. IOC Extraction
5. Threat Intelligence Correlation
6. Reputation Analysis
7. MITRE ATT&CK Mapping
8. Risk Assessment
9. Documentation & Reporting

---

# 📊 Skills Matrix

| Skill | Case 1 | Case 2 | Case 3 | Case 4 |
|--------|:------:|:------:|:------:|:------:|
| Email Header Analysis | ✅ | ✅ | ✅ | ✅ |
| IOC Extraction | ✅ | ✅ | ✅ | ✅ |
| Threat Intelligence | ✅ | ✅ | ✅ | ✅ |
| WHOIS Analysis | ✅ |  |  | ✅ |
| VirusTotal |  | ✅ | ✅ | ✅ |
| URL Analysis |  |  | ✅ | ✅ |
| Hash Analysis |  | ✅ | ✅ |  |
| MITRE ATT&CK | ✅ | ✅ | ✅ | ✅ |
| Report Writing | ✅ | ✅ | ✅ | ✅ |

---

# 📚 Key Learning Outcomes

- Email authentication analysis (SPF, DKIM, DMARC)
- IOC extraction and documentation
- Static malware attachment analysis
- PDF and phishing URL investigation
- Threat intelligence correlation
- Professional SOC-style incident reporting

---


# 👤 Author

**Shaikh Sufiyan**
  
 
- **LinkedIn:** https://www.linkedin.com/in/shaikh-sufiyan-aab51a3b1
- **GitHub:** https://github.com/Sufiyan-SOC
- **Email:**  shaikh.sufiyan.sec@gmail.com










