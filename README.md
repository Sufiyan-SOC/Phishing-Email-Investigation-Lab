🛡️ Phishing Email Investigation Lab

«A hands-on SOC Analyst portfolio focused on investigating real-world phishing attacks through email header analysis, malicious attachment analysis, URL investigation, IOC extraction, threat intelligence correlation, and professional incident reporting.»

---

📌 Overview

This repository demonstrates practical phishing investigations performed in a controlled lab environment. Each investigation follows a structured SOC workflow, from evidence collection to IOC extraction, threat intelligence validation, risk assessment, MITRE ATT&CK mapping, and incident documentation.

The objective is to demonstrate practical skills commonly used by SOC Analysts during phishing investigations.

---

🎯 Objectives

- Investigate phishing emails using industry-standard SOC methodologies.
- Analyze email headers to validate sender authenticity.
- Extract Indicators of Compromise (IOCs).
- Investigate malicious attachments and phishing URLs.
- Correlate findings using multiple threat intelligence platforms.
- Produce professional SOC-style incident reports.

---

💼 Skills Demonstrated

- Phishing Email Investigation
- Email Header Analysis
- IOC Extraction
- Threat Intelligence Analysis
- OSINT Investigation
- Static Malware Analysis
- URL & Domain Investigation
- Email Authentication (SPF, DKIM, DMARC)
- MITRE ATT&CK Mapping
- SOC Incident Documentation

---

🛠️ Tools & Platforms

Email Analysis

- Custom EML Extractor (eioc.py)
- MXToolbox

Threat Intelligence

- VirusTotal
- Cisco Talos
- AbuseIPDB

OSINT

- WHOIS
- Urlscan.io
- IPInfo

Linux Utilities

- Bash
- grep
- sha256sum

Hashing

- MD5
- SHA-1
- SHA-256

---

## 📂 Repository Structure

```text
Phishing-Email-Investigation-Lab/

├── README.md

├── Case_01_Header_Analysis_Chase/
│   ├── Case_01_Report.md
│   └── screenshots/

├── Case_02_Attachment_Analysis_ISO/
│   ├── Case_02_Report.md
│   └── screenshots/

├── Case_03_Malicious_PDF_Analysis/
│   ├── Case_03_Report.md
│   └── screenshots/

└── Case_04_Brand_Impersonation_URL_Amazon/
    ├── Case_04_Report.md
    └── screenshots/
```



---

🔎 Investigation Cases

Case 01 — Email Header Analysis (Chase)

Focus

- Email Header Analysis
- SPF, DKIM & DMARC Validation
- SMTP Path Analysis
- Sender Infrastructure Verification

Primary Tools

- MXToolbox
- WHOIS
- AbuseIPDB
- eioc.py

---

Case 02 — Malicious ISO Attachment

Focus

- Static Malware Analysis
- File Hash Verification
- Threat Intelligence Correlation

Primary Tools

- sha256sum
- VirusTotal
- Cisco Talos

---

Case 03 — Malicious PDF Analysis

Focus

- PDF Investigation
- Hash Analysis
- Threat Intelligence Validation

Primary Tools

- sha256sum
- VirusTotal

---

Case 04 — Brand Impersonation & URL Investigation

Focus

- URL Extraction
- Domain Investigation
- URL Reputation Analysis
- Redirect Chain Analysis

Primary Tools

- VirusTotal
- WHOIS
- Urlscan.io
- grep

---

🔄 Investigation Workflow

1. Initial Email Review
2. Evidence Collection
3. Email Header Analysis
4. IOC Extraction
5. Threat Intelligence Correlation
6. Malware / URL Analysis
7. MITRE ATT&CK Mapping
8. Risk Assessment
9. Incident Documentation

---

📊 Investigation Coverage

This lab includes practical investigations covering:

- Email Header Spoofing
- SPF, DKIM & DMARC Validation
- Malicious ISO Attachments
- Malicious PDF Attachments
- Brand Impersonation
- Credential Harvesting URLs
- URL Reputation Analysis
- Domain Investigation
- Hash Analysis
- IOC Extraction
- Threat Intelligence Correlation

---

🎓 Key Learning Outcomes

- Email authentication verification
- Phishing IOC identification
- Static attachment analysis
- URL and domain investigation
- Threat intelligence correlation
- Professional incident documentation
- MITRE ATT&CK mapping
- SOC investigation methodology

---

👤 Author

Shaikh Sufiyan

GitHub: https://github.com/Sufiyan-SOC

LinkedIn: https://www.linkedin.com/in/shaikh-sufiyan-aab51a3b1

Email: shaikh.sufiyan.sec@gmail.com
