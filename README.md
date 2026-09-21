# phishing-email-investigation
A cybersecurity project focused on analyzing phishing emails, investigating email headers, identifying malicious URLs and attachments, extracting IOCs, and documenting phishing indicators using SOC analysis techniques.

## 📌 Project Overview

This project focuses on the analysis of suspicious and potentially malicious phishing emails from a cybersecurity/SOC analyst perspective.

The objective is to investigate an email, identify indicators of compromise (IOCs), determine whether the email is legitimate or malicious, and document the findings.

The investigation includes:

* Email header analysis
* Sender and recipient analysis
* SPF, DKIM, and DMARC verification
* Suspicious URL analysis
* Attachment analysis
* Domain and IP investigation
* IOC extraction
* Social-engineering technique identification
* Risk assessment
* Incident-response recommendations

---

## 🎯 Objectives

The main objectives of this project are:

1. Identify phishing characteristics in an email.
2. Analyze email headers to determine the actual source of the message.
3. Investigate suspicious domains, URLs, and IP addresses.
4. Identify malicious or suspicious attachments.
5. Extract Indicators of Compromise (IOCs).
6. Determine the phishing techniques used by the attacker.
7. Assess the potential impact on the organization.
8. Provide recommendations for preventing similar attacks.

---

## 🛠️ Tools Used

| Tool                  | Purpose                                      |
| --------------------- | -------------------------------------------- |
| Email Header Analyzer | Analyze email routing and authentication     |
| VirusTotal            | Investigate URLs, domains, files, and hashes |
| URLScan.io            | Analyze suspicious URLs                      |
| WHOIS                 | Investigate domain registration information  |
| AbuseIPDB             | Check IP reputation                          |
| CyberChef             | Decode and analyze suspicious data           |
| MXToolbox             | Check email and DNS information              |
| Any.Run               | Sandbox analysis of suspicious files/URLs    |
| Wireshark             | Network traffic analysis                     |
| Splunk                | Log analysis and correlation                 |

> Only use authorized or safe samples for analysis. Do not open suspicious attachments or URLs directly on your normal computer.

---

# 📁 Project Structure

```text
phishing-email-analysis/
│
├── README.md
│
├── samples/
│   └── sample-email.txt
│
├── analysis/
│   ├── email-header-analysis.md
│   ├── url-analysis.md
│   ├── attachment-analysis.md
│   └── phishing-investigation.md
│
├── iocs/
│   └── iocs.csv
│
├── screenshots/
│   ├── header-analysis.png
│   ├── url-analysis.png
│   └── reputation-check.png
│
└── reports/
    └── phishing-analysis-report.pdf
```

---

# 🔎 Investigation Methodology

## 1. Collect the Email

The first step is to obtain the suspicious email in a safe format.

Recommended formats:

* `.eml`
* `.msg`
* Raw email headers
* Plain-text email

Important information to collect:

```text
From:
To:
Subject:
Date:
Reply-To:
Return-Path:
Message-ID:
Received:
Authentication-Results:
```

---

# 2. Analyze the Email Header

Email headers contain information about how an email traveled between mail servers.

Important fields include:

### From

Shows the displayed sender address.

Example:

```text
From: Microsoft Security <security@example.com>
```

The displayed sender should not automatically be trusted because attackers can spoof the visible address.

---

### Reply-To

Check whether replies are redirected to a different address.

Example:

```text
From: security@example.com
Reply-To: attacker@example.net
```

This can be a suspicious indicator.

---

### Return-Path

The Return-Path can provide additional information about the actual sending infrastructure.

Example:

```text
Return-Path: <mailer@suspicious-domain.com>
```

---

### Received Headers

`Received` headers show the path taken by the email through mail servers.

Example:

```text
Received: from mail.example.net
        by mail.company.com
```

These headers can help identify:

* Sending IP address
* Mail servers
* Routing path
* Potentially suspicious infrastructure

---

# 3. Check SPF

SPF stands for:

**Sender Policy Framework**

SPF helps determine whether a server is authorized to send email for a domain.

Example:

```text
spf=pass
```

or

```text
spf=fail
```

A failed SPF result can be a strong warning sign, although it does not by itself prove that an email is malicious.

---

# 4. Check DKIM

DKIM stands for:

**DomainKeys Identified Mail**

DKIM uses cryptographic signatures to help verify that an email was authorized by the sending domain and was not modified after signing.

Example:

```text
dkim=pass
```

or

```text
dkim=fail
```

---

# 5. Check DMARC

DMARC stands for:

**Domain-based Message Authentication, Reporting and Conformance**

DMARC combines domain alignment with SPF and DKIM results.

Example:

```text
dmarc=pass
```

or:

```text
dmarc=fail
```

Authentication failures should be investigated together with other evidence rather than treated as automatic proof of phishing.

---

# 6. Analyze the Sender

Investigate the sender address carefully.

Example:

```text
security@micros0ft-support.example
```

Potential red flags:

* Look-alike domains
* Misspelled company names
* Unexpected domains
* Free email providers
* Suspicious subdomains
* Mismatched sender and Reply-To addresses

Example:

```text
legitimate-domain.com
```

versus:

```text
legitmate-domain.com
```

The difference may be only one character.

Humans are remarkably good at not noticing one character when money or panic is involved.

---

# 7. Analyze the Subject

Look for social-engineering indicators such as:

```text
URGENT: Your account will be disabled
```

```text
Security Alert: Verify Your Account
```

```text
Payment Failed - Immediate Action Required
```

Common phishing themes include:

* Account suspension
* Password expiration
* Financial transactions
* Package delivery
* Payroll
* IT support
* MFA verification
* Password reset
* Tax or government notifications

---

# 8. Analyze URLs

Extract every URL contained in the email.

Example:

```text
https://login-example-security.com/verify
```

Investigate:

* Domain
* Subdomain
* URL path
* Redirects
* Domain age
* Reputation
* SSL certificate
* Hosting information
* URL reputation

Useful tools include:

* VirusTotal
* URLScan.io
* WHOIS

Do not visit suspicious URLs directly from your normal browser.

---

# 9. Analyze Attachments

Check whether the email contains attachments.

Examples:

```text
Invoice.pdf
Payment.xlsm
Document.docm
Security_Update.zip
```

Look for suspicious characteristics:

* Executable files
* Macro-enabled Office documents
* JavaScript files
* ZIP archives
* Password-protected archives
* Double extensions

Example:

```text
Invoice.pdf.exe
```

The filename may attempt to disguise an executable file as a PDF.

For suspicious files, calculate the SHA-256 hash:

```bash
sha256sum suspicious_file
```

Example:

```text
SHA256:
a1b2c3d4e5f6...
```

The hash can then be searched using malware-analysis services such as VirusTotal.

---

# 10. Extract Indicators of Compromise

Create an IOC list containing:

| IOC Type | Value                                               | Description               |
| -------- | --------------------------------------------------- | ------------------------- |
| Email    | [attacker@example.com](mailto:attacker@example.com) | Suspicious sender         |
| Domain   | suspicious-example.com                              | Phishing domain           |
| URL      | https://suspicious-example.com/login                | Credential harvesting URL |
| IP       | 203.0.113.10                                        | Suspicious infrastructure |
| SHA-256  | `<hash>`                                            | Attachment hash           |

Store the information in:

```text
iocs/iocs.csv
```

Example:

```csv
type,value,description
email,attacker@example.com,Suspicious sender
domain,suspicious-example.com,Phishing domain
url,https://suspicious-example.com/login,Credential harvesting URL
ip,203.0.113.10,Suspicious IP
sha256,<hash>,Suspicious attachment
```

---

# 11. Identify Phishing Techniques

Possible techniques include:

### Credential Harvesting

The attacker attempts to obtain:

* Username
* Password
* MFA code
* Banking credentials

### Spoofing

The attacker impersonates a trusted organization or person.

### Urgency

The victim is pressured to act immediately.

Example:

```text
Your account will be permanently disabled today.
```

### Fear

The email attempts to create panic.

Example:

```text
Unauthorized login detected.
Verify your account immediately.
```

### Brand Impersonation

The attacker imitates companies such as:

* Microsoft
* Google
* Apple
* Banks
* Delivery companies
* Cloud providers

---

# 12. Determine the Verdict

After collecting evidence, classify the email.

Possible verdicts:

```text
Benign
Suspicious
Phishing
Malware
Business Email Compromise
Spam
```

Example:

```text
Verdict: Phishing

Confidence: High

Reason:

1. Sender domain does not match the claimed organization.
2. SPF authentication failed.
3. Reply-To address points to another domain.
4. Email contains a suspicious login URL.
5. URL reputation indicates malicious activity.
6. Email uses urgency and account-suspension themes.
```

---

# 13. Risk Assessment

Assess the potential impact.

### Potential Impact

* Credential theft
* Account compromise
* Malware infection
* Data theft
* Financial fraud
* Business Email Compromise
* Lateral movement
* Unauthorized access

Example:

```text
Risk Level: High

Potential Impact:
Credential theft and account compromise.

Primary Attack Vector:
Malicious phishing URL.

Affected Users:
Employees receiving the email.

Recommended Action:
Block the malicious domain and URL, search mailboxes
for similar messages, reset credentials for affected users,
and monitor authentication logs.
```

---

# 14. Incident Response Recommendations

If the email is confirmed as malicious:

### Immediate Actions

1. Quarantine the email.
2. Block malicious domains and URLs.
3. Block identified malicious IP addresses where appropriate.
4. Search the organization for similar emails.
5. Identify users who clicked the link.
6. Reset compromised credentials.
7. Revoke suspicious sessions/tokens.
8. Scan affected systems.
9. Monitor authentication activity.
10. Document the incident.

---

# 📊 Example Investigation Summary

```text
=================================================
             PHISHING EMAIL ANALYSIS
=================================================

Email Subject:
Urgent: Your Account Requires Verification

Sender:
security@suspicious-example.com

Reply-To:
support@another-example.com

SPF:
FAIL

DKIM:
FAIL

DMARC:
FAIL

Suspicious URL:
https://suspicious-example.com/verify

Attachment:
None

Social Engineering:
Urgency + Account Suspension

IOC Identified:
Domain
URL
Email Address
IP Address

Verdict:
PHISHING

Risk:
HIGH

Primary Threat:
Credential Theft
=================================================
```

---

# 📈 SOC Analyst Skills Demonstrated

This project demonstrates practical knowledge of:

* Email security
* Phishing detection
* SOC investigation
* IOC extraction
* Threat intelligence
* OSINT
* Email authentication
* SPF
* DKIM
* DMARC
* URL analysis
* Malware analysis
* Incident response
* Security documentation

---

# 🔐 Safety

Only analyze emails and files that you are authorized to investigate.

For suspicious URLs:

```text
DO NOT open them directly.
```

For suspicious attachments:

```text
DO NOT execute them on your personal system.
```

Use an isolated virtual machine or appropriate malware-analysis sandbox.

---

# 📚 Learning Outcomes

After completing this project, you should be able to:

* Read and interpret email headers.
* Identify suspicious sender information.
* Understand SPF, DKIM, and DMARC.
* Analyze phishing URLs.
* Extract IOCs.
* Investigate suspicious attachments.
* Identify social-engineering techniques.
* Assess phishing risk.
* Produce a professional SOC investigation report.

---

# 🚀 Future Improvements

The project can be extended by adding:

* Splunk integration
* Wazuh integration
* Automated IOC extraction
* Python-based email parser
* VirusTotal API integration
* SIEM dashboards
* Automated phishing detection
* YARA rules for malicious attachments
* MITRE ATT&CK mapping
* Automated incident-response workflow

---

## 👨‍💻 Author

**Shafa CV**

Cybersecurity / SOC Analyst Learning Project

---

## 📌 Disclaimer

This project is intended for cybersecurity education, defensive security analysis, and authorized laboratory environments only.
