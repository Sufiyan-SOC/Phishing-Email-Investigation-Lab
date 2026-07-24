
# Case 01 – Email Header Analysis (Chase Bank Phishing)

---

# Executive Summary

> An email impersonating Chase Bank was detected targeting an end-user with a high-urgency account suspension lure ("Your Bank Account has been blocked"). Header analysis revealed display name spoofing (`alerts@chase.com`) routed through an unauthorized external mail relay (`185.70.40.140`) hosted by ProtonMail. DMARC and DKIM authentication failed alignment, confirming domain spoofing and credential harvesting intent.

---

# Incident Information

| Field | Details |
|-------|---------|
| Case ID | PHISH-2022-001 |
| Incident Type | Brand Impersonation / Email Header Spoofing |
| Severity | High |
| Status | Closed / Remediated |
| Analyst | Security Operations Center (SOC) |
| Date | September 16, 2022 |

---

# Investigation Objective

Determine the authenticity of the incoming Chase Bank email notification, identify header spoofing techniques, trace the origin IP address, evaluate domain reputation, and extract Indicators of Compromise (IOCs) for defensive containment.

---

# Scope of Investigation

- Analysis of the raw `.eml` email body, display headers, and routing paths.
- Evaluation of email security protocol alignments (SPF, DKIM, and DMARC).
- WHOIS and Threat Intelligence reputation analysis on originating IP infrastructure.

---

# Tools Used

- **Linux Terminal:** Custom extraction tool (`eioc.py`) for automated header parsing.
- **MXToolbox Header Analyzer:** Parsing authentication parameters (`Authentication-Results`).
- **WHOIS Search (DomainTools / ARIN):** Inspecting IP owner and netblock details.
- **AbuseIPDB:** Assessing threat score and reporting history of originating IP.

---

# Evidence Collected

| Evidence | Screenshot |
|----------|------------|
| Email Body | `screenshots/01_phishing_email_body.png` |
| Raw Email Headers | `screenshots/02_raw_email_headers.png` |
| MXToolbox Analysis | `screenshots/03_mxtoolbox_header_analysis.png` |
| WHOIS Lookup | `screenshots/04_whois_ip_lookup.png` |
| AbuseIPDB Lookup | `screenshots/05_abuseipdb_reputation.png` |
| Terminal Analysis | `screenshots/06_terminal_extracted_headers.png` |

---

# Investigation Workflow

## Step 1 – Initial Email Review

### Observation
The email claims to originate from `alerts@chase.com` notifying the user that their account has been temporarily blocked due to unauthorized sign-in attempts from an unrecognised device. It urges the recipient to click a link immediately to restore access.

### Findings
- Visual elements (logo, fonts) mimic official Chase Bank communications.
- Creates psychological pressure by setting a strict time limit before "permanent account closure."
- Embedded links do not point to official `chase.com` domains.

![Email Body](screenshots/01_phishing_email_body.png)

---

## Step 2 – Raw Header Extraction

### Header Fields Reviewed

- **From:** `alerts@chase.com`
- **Reply-To / Return-Path:** `kellyellin426@proton.me`
- **Received:** `from mail-40140.protonmail.ch (185.70.40.140)`
- **Message-ID:** `<185.70.40.140.protonmail.ch.msgid>`
- **SPF:** `Fail` (Originating IP `185.70.40.140` is not authorized by `chase.com` SPF policy)
- **DKIM:** `Fail / Unsigned`
- **DMARC:** `Fail` (`action=none` / `p=reject`)
- **X-Originating-IP:** `185.70.40.140`

### Findings
Significant misalignment exists between the displayed `From` address (`alerts@chase.com`) and the actual envelope sender / `Return-Path` (`kellyellin426@proton.me`).

![Raw Email Headers](screenshots/02_raw_email_headers.png)

---

## Step 3 – Header Analysis

### Analysis Performed
Imported the header into MXToolbox Header Analyzer and executed custom terminal header parser scripts to map relay paths.

### Findings
- **Sender Spoofing:** The sender forged the `From` header to appear as Chase Bank.
- **Authentication Breakdown:** SPF and DMARC failed completely because `chase.com` SPF record does not include ProtonMail relays.

![MXToolbox Analysis](screenshots/03_mxtoolbox_header_analysis.png)
![Terminal Analysis](screenshots/06_terminal_extracted_headers.png)

---

## Step 4 – IP Address Investigation

### WHOIS Analysis
Investigated the originating IP `185.70.40.140` to identify hosting providers and geolocation.

### Findings
- **ISP / Organization:** Proton AG (ProtonMail Infrastructure)
- **ASN:** AS209854
- **Country:** Switzerland 🇨🇭
- **Network Range:** `185.70.40.0/22`

![WHOIS Lookup](screenshots/04_whois_ip_lookup.png)

---

## Step 5 – Reputation Analysis

### AbuseIPDB Results
Cross-referenced IP `185.70.40.140` against global abuse databases.

### Findings
- The IP address is associated with public webmail/relay infrastructure frequently abused by adversaries to send spoofed phishing communications.
- High report volume for spam and phishing distribution.

![AbuseIPDB Lookup](screenshots/05_abuseipdb_reputation.png)

---

# Indicators of Compromise (IOCs)

## Domains

| Domain | Description |
|---------|-------------|
| `chase.com` | Spoofed Legitimate Brand Domain |
| `proton.me` | Domain used in envelope Return-Path |
| `protonmail.ch` | Originating Mail Relay Server Domain |

---

## IP Addresses

| IP Address | Reputation |
|------------|------------|
| `185.70.40.140` | Malicious / Suspicious (Proton AG Relay abused for Phishing) |

---

## Email Addresses

| Email | Description |
|-------|-------------|
| `alerts@chase.com` | Spoofed Sender Header |
| `kellyellin426@proton.me` | Actual Adversary Envelope Sender / Return-Path |

---

## Message-ID

| Value |
|-------|
| `<185.70.40.140.protonmail.ch.msgid>` |

---

# MITRE ATT&CK Mapping

| Technique | ATT&CK ID |
|-----------|-----------|
| Phishing: Spearphishing Link | T1566.002 |
| Forge Program Header (Display Name Spoofing) | T1036.007 |
| Subvert Network Defenses: Email Authentications | T1566 |

---

# Risk Assessment

| Category | Rating |
|----------|--------|
| Impact | High (Potential Financial & Credential Compromise) |
| Likelihood | High (Plausible Social Engineering Lure) |
| Overall Risk | **High** |

---

# Detection Opportunities

- **DMARC Strict Enforcement:** Create SIEM alerts for inbound emails where DMARC evaluation yields `fail` with domain mismatch (`Header From` vs `Return-Path`).
- **Display Name Impersonation Rules:** Configure Secure Email Gateways (SEGs) to flag messages using major financial brand names in the display header if originating outside authorized netblocks.
- **External Sender Callouts:** Tag incoming external emails with a warning banner when sender domains do not match SPF alignment.

---

# Recommendations

- **Immediate Action:** Block the malicious sender envelope address (`kellyellin426@proton.me`) across SEG filters.
- **Email Security Rule:** Enforce `p=reject` policy handling for DMARC failures on inbound email gateways.
- **User Training:** Conduct awareness training focusing on verifying email header addresses rather than relying on visual display names.

---

# Conclusion

> Case 01 is a confirmed phishing attempt utilizing display name spoofing. The attacker forged the `alerts@chase.com` identity while sending the email through a free ProtonMail account (`kellyellin426@proton.me`). Email authentication checks (SPF/DMARC) successfully failed, providing clear indicators for automated blocklisting and threat containment.

---

# Lessons Learned

- Display names in email clients can be easily forged; raw headers must always be evaluated.
- DMARC/SPF checks provide immediate validation of spoofing attempts.
- Automated header parsing scripts significantly speed up triage time in SOC workflows.

---

# References

- [MXToolbox Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)
- [AbuseIPDB Threat Intelligence](https://www.abuseipdb.com/)
- [DomainTools WHOIS](https://www.domaintools.com/)
- [RFC 5322 - Internet Message Format](https://tools.ietf.org/html/rfc5322)
- 
