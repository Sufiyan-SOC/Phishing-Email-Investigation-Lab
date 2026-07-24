# Case 04 – Amazon Brand Impersonation & URL Analysis

---

# Executive Summary

> An unauthorized login alert email impersonating Amazon Prime Support was analyzed. The email claimed a suspicious login occurred from an Android device (IP `144.68.119.02`) and directed recipients to click a "Go to your account" link. Extracted URL investigation and sandbox tracing (`Urlscan.io`) uncovered a multi-stage redirection chain starting from `cabinetlekagni[.]com` and terminating on a active phishing host `sbffidserv.sviluppo[.]host` located in Italy.

---

# Incident Information

| Field | Details |
|-------|---------|
| Case ID | PHISH-2022-004 |
| Incident Type | Brand Impersonation / Credential Harvesting URL |
| Severity | High |
| Status | Closed / Remediated |
| Analyst | Security Operations Center (SOC) |
| Date | September 17, 2022 |

---

# Investigation Objective

Trace the origin IP address, extract embedded link targets from the email source, map the multi-stage URL redirection path, and identify destination phishing landing servers.

---

# Scope of Investigation

- Analysis of email body and envelope headers.
- Extracting hidden domains using command-line tools (`grep`).
- Domain WHOIS and VirusTotal URL reputation scanning.
- Dynamic URL analysis via `Urlscan.io` sandbox execution.

---

# Tools Used

- **Linux Terminal:** `eioc.py` and `grep` text processing tools.
- **DomainTools / WHOIS:** Identifying IP owner and server network allocations.
- **VirusTotal:** Checking destination domain reputation.
- **Urlscan.io:** Automated HTTP transaction mapping and redirection tracking.

---

# Evidence Collected

| Evidence | Screenshot |
|----------|------------|
| Amazon Prime Phishing Email | `screenshots/01_amazon_prime_phishing_email.png` |
| Terminal Extracted URLs & Headers | `screenshots/02_terminal_extracted_urls_headers.png` |
| WHOIS Google IP Lookup | `screenshots/03_whois_google_ip_info.png` |
| Terminal Grep Extracted Domain | `screenshots/04_terminal_grep_extracted_domain.png` |
| VirusTotal URL Detection | `screenshots/05_virustotal_url_detection.png` |
| Urlscan Redirection Path | `screenshots/06_urlscan_redirection_path.png` |

---

# Investigation Workflow

## Step 1 – Initial Email Review

### Observation
The email claims to be an automated notification from "Amazon Prime Support" stating that pending orders were canceled due to a forced login attempt from an Android device in the United States.

### Findings
- **Sender Header:** `cafepress@mail.cafepress.com` (Unrelated third-party domain).
- **Target User:** `asmith@hotmail.com`
- **Urgency Mechanism:** Threats of permanent account suspension within 24 hours.

![Amazon Prime Email](screenshots/01_amazon_prime_phishing_email.png)

---

## Step 2 – Header & Relay Inspection

### Technical Parameters
Extracted envelope attributes using command-line utilities:

- **X-Sender-IP:** `209.85.221.104`
- **Return-Path:** `msprvsl=XJgvrijdPKASn=bounces-098020-32419@tbh51blx.imdreampores.ovh`
- **Authentication:** `spf=none`, `dmarc=none`

### Findings
WHOIS investigation confirmed `209.85.221.104` belongs to Google LLC infrastructure (`mail-wr1-f104.google.com`), indicating the email was relayed through Google webmail servers.

![WHOIS Google IP](screenshots/03_whois_google_ip_info.png)

---

## Step 3 – URL Extraction & Filtering

### Analysis Performed
Isolated embedded HTTP/HTTPS links from the `.eml` body using `eioc.py` and filtered specific domains with `grep`.

### Findings
- Extracted primary target domain: `cabinetlekagni[.]com`
- Link structure: `hxxps[://]cabinetlekagni[.]com/`

![Terminal Extracted URLs](screenshots/02_terminal_extracted_urls_headers.png)
![Terminal Grep Domain](screenshots/04_terminal_grep_extracted_domain.png)

---

## Step 4 – VirusTotal URL Reputation Check

### Findings
Submitted `https://cabinetlekagni[.]com/` to VirusTotal:
- **Detection Score:** **12 / 92** Vendors flagged the URL as Malicious / Phishing.

![VirusTotal URL Detection](screenshots/05_virustotal_url_detection.png)

---

## Step 5 – Dynamic Sandbox Analysis (`Urlscan.io`)

### Analysis Performed
Analyzed the URL behavior on Urlscan.io to record dynamic HTTP requests and redirection chains.

### Findings
- **Initial Submitted URL:** `https://cabinetlekagni[.]com/`
- **Effective Redirect URL:** `https://sbffidserv.sviluppo[.]host/s/Dose/signin.php`
- **Target IP Address:** `149.62.187.89` (COLTENGINE Network, Italy 🇮🇹)
- **Verdict:** **Potentially Malicious / Active Phishing Engine**

![Urlscan Sandbox Result](screenshots/06_urlscan_redirection_path.png)

---

# Indicators of Compromise (IOCs)

## Domains & URLs

| Type | Indicator | Description |
|------|-----------|-------------|
| Initial URL | `hxxps[://]cabinetlekagni[.]com/` | Embedded Link in Email |
| Effective Redirect URL | `hxxps[://]sbffidserv.sviluppo[.]host/s/Dose/signin.php` | Terminating Phishing Landing Page |

---

## IP Addresses

| IP Address | Organization / Country | Role |
|------------|-----------------------|------|
| `209.85.221.104` | Google LLC (USA 🇺🇸) | Originating Relay IP |
| `149.62.187.89` | COLTENGINE Network (Italy 🇮🇹) | Host IP for Terminating Phishing Page |

---

## Senders & Envelope Headers

| Header | Value |
|--------|-------|
| Display From | `cafepress@mail.cafepress.com` |
| Return-Path | `msprvsl=XJgvrijdPKASn=bounces-098020-32419@tbh51blx.imdreampores.ovh` |

---

# MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Phishing: Spearphishing Link | T1566.002 |
| Redirection / Multi-Stage Target Proxy | T1090 |
| Credentials from Web Browsers | T1555.003 |

---

# Risk Assessment

| Category | Rating |
|----------|--------|
| Impact | High (Amazon Account & Credit Card Harvest) |
| Likelihood | High (Widespread Brand Recognition) |
| Overall Risk | **High** |

---

# Detection Opportunities

- **URL Sandbox Scanning:** Configure Secure Email Gateways (SEGs) to dynamically detonate embedded links at time-of-click.
- **Domain Reputation Rules:** Automatically quarantine incoming emails containing links to newly registered domains or domains with poor VirusTotal scores.

---

# Recommendations

- Add `cabinetlekagni[.]com` and `sbffidserv.sviluppo[.]host` to DNS Sinkhole and firewall perimeter blocklists.
- Block originating Return-Path domain `imdreampores.ovh`.
- Alert targeted user `asmith@hotmail.com` to reset credentials if the link was accessed.

---

# Conclusion

> Case 04 represents a multi-stage brand impersonation attack targeting Amazon Prime users. The attackers used Google mail relays to bypass basic server IP filters and employed an intermediate redirect domain (`cabinetlekagni[.]com`) leading to an Italian hosting provider running an active credential harvesting form.

---

# Lessons Learned

- Phishing links rarely lead directly to the final phishing site; attackers almost always use open redirects or compromised staging domains to evade static filters.
- Sandbox analysis tools like `Urlscan.io` are vital for revealing the true terminating URL in redirection chains.

---

# References

- [Urlscan.io Sandbox Analysis](https://urlscan.io/)
- [VirusTotal URL Scanner](https://www.virustotal.com/)
- [DomainTools WHOIS](https://www.domaintools.com/)
- 
