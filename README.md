# 📧 Email Phishing / Business Email Compromise Investigation

## 📌 Project Overview

This project demonstrates a **SOC Analyst investigation of a suspicious email** suspected to be a **Business Email Compromise (BEC) / Executive Impersonation** attempt.

The email impersonates a Chief Executive Officer and requests an urgent **INR 18,75,000 wire transfer**. The investigation focuses on analyzing the email headers, sender information, authentication results, suspicious URL, network indicators, and social-engineering characteristics.

The objective is to follow a practical SOC investigation workflow and document the findings, Indicators of Compromise (IOCs), and recommended response actions.

---

## 🎯 Objectives

* Analyze a suspicious `.eml` file
* Investigate email headers
* Analyze sender and recipient information
* Examine SPF, DKIM, and DMARC results
* Identify suspicious domains and IP addresses
* Extract and investigate URLs
* Identify Indicators of Compromise (IOCs)
* Determine the likely attack type
* Document investigation findings
* Recommend incident-response actions

---

## 🛠️ Tools Used

| Tool                  | Purpose                                          |
| --------------------- | ------------------------------------------------ |
| Email Header Analysis | Analyze email routing and authentication headers |
| VirusTotal            | URL/domain/IP reputation investigation           |
| WHOIS                 | Domain registration investigation                |
| CyberChef             | Decode and analyze encoded data                  |
| GitHub                | Investigation documentation                      |

---

## 📂 Project Structure

```text
Email-Phishing-Investigation/
│
├── README.md
│
├── evidence/
│   ├── phishing-email.eml
│   └── screenshots/
│       ├── 01-email.png
│       ├── 02-headers.png
│       ├── 03-authentication.png
│       ├── 04-url-analysis.png
│       ├── 05-ip-analysis.png
│       ├── 06-domain-analysis.png
│       ├── 07-cyberchef.png
        └── 08-abuseipdb.png
        
│
├── investigation/
│   ├── email-analysis.md
│   ├── header-analysis.md
│   ├── url-analysis.md
│   └── ioc-list.md
│
└── report/
    └── incident-report.md
```

---

# 🔎 Investigation

## 1. Email Details

| Field        | Value                                            |
| ------------ | ------------------------------------------------ |
| Sender Name  | Rajiv Mehra, CEO                                 |
| Sender Email | `rajiv.mehra@citiprepaid-salarysea-at.tk`        |
| Recipient    | Priya Sharma                                     |
| Subject      | `Confidential: Urgent payment approval required` |
| Date         | 23 July 2026 11:48 UTC                           |
| Sending IP   | `98.177.68.12`                                   |
| Reply-To     | `rajiv.mehra@citiprepaid-salarysea-at.tk`        |
| Return-Path  | `rajiv.mehra@citiprepaid-salarysea-at.tk`        |

---

## 2. Sender Analysis

The email claims to be from:

**Rajiv Mehra — Chief Executive Officer**

and the signature identifies:

**Northstar Holdings**

However, the sender uses:

```text
citiprepaid-salarysea-at.tk
```

The sender domain does not correspond to the organization claimed in the email signature.

The `Reply-To`, `Return-Path`, and `Message-ID` also use the same domain.

### Finding

**Potential executive impersonation / Business Email Compromise.**

---

## 3. Email Header Analysis

The email originated from:

```text
mail.citiprepaid-salarysea-at.tk
```

with the IP address:

```text
98.177.68.12
```

The message was subsequently processed through Microsoft email infrastructure.

### Important Headers

```text
From:
rajiv.mehra@citiprepaid-salarysea-at.tk

Reply-To:
rajiv.mehra@citiprepaid-salarysea-at.tk

Return-Path:
rajiv.mehra@citiprepaid-salarysea-at.tk

X-Originating-IP:
98.177.68.12

X-Sender-IP:
98.177.68.12
```

---

## 4. SPF / DKIM / DMARC Analysis

The email authentication results were:

| Authentication | Result |
| -------------- | ------ |
| SPF            | PASS   |
| DKIM           | NONE   |
| DMARC          | PASS   |

### Assessment

SPF and DMARC passing do **not independently prove that the sender is the legitimate person represented in the email**.

The sender domain remains suspicious because it does not correspond to the organization claimed in the email.

Authentication results were therefore considered together with the sender identity, domain, email content, and requested financial action.

---

## 5. Subject Analysis

### Subject

```text
Confidential: Urgent payment approval required
```

The subject contains several social-engineering characteristics:

* Urgency
* Confidentiality
* Financial request
* Pressure to act quickly

These characteristics warranted further investigation.

---

## 6. Email Body Analysis

The email requests:

```text
INR 18,75,000
```

to be transferred to a new consulting partner.

The message also specifies a deadline:

```text
Before 4:00 PM
```

The sender claims to be in a confidential meeting and unable to take calls.

The recipient is instructed:

```text
Do not discuss this request with anyone
```

The recipient is also asked to reply after the transfer has been submitted.

### Suspicious Characteristics

* Large financial request
* Urgent deadline
* Executive impersonation
* Request for secrecy
* Claim that the sender cannot take calls
* External payment-instruction URL

---

# 🌐 URL Investigation

The email contains the following URL:

```text
http://adventure-nicaragua.net/index.php?option=com_mailto&tmpl=component&link=aHR0cDovL2FkdmVudHVyZ.
```

The URL is presented as:

```text
Review Payment Instructions
```

The domain does not obviously correspond to the organization represented in the email.

### Safety

The URL should be investigated using security-analysis tools rather than directly opened in a normal browser.

### Tools

* VirusTotal
* URLScan
* WHOIS
* CyberChef

---

# 🌐 URL / Domain Indicators

### Sender Domain

```text
citiprepaid-salarysea-at[.]tk
```

### URL Domain

```text
adventure-nicaragua[.]net
```

### Sending Host

```text
mail.citiprepaid-salarysea-at[.]tk
```

### Sending IP

```text
98[.]177[.]68[.]12
```

Indicators are defanged to reduce the risk of accidental interaction.

---

# 🔐 IOC Table

| IOC Type | Indicator                                   | Description             |
| -------- | ------------------------------------------- | ----------------------- |
| Email    | `rajiv.mehra@citiprepaid-salarysea-at[.]tk` | Claimed CEO sender      |
| Domain   | `citiprepaid-salarysea-at[.]tk`             | Sender domain           |
| IP       | `98[.]177[.]68[.]12`                        | Sending IP              |
| Hostname | `mail.citiprepaid-salarysea-at[.]tk`        | Sending hostname        |
| Domain   | `adventure-nicaragua[.]net`                 | Payment URL domain      |
| URL      | `hxxp://adventure-nicaragua[.]net/...`      | Payment-instruction URL |

---

# 🕒 Investigation Timeline

| Time         | Event                                                 |
| ------------ | ----------------------------------------------------- |
| 11:48:18 UTC | Email generated                                       |
| 11:48:22 UTC | Email received by Microsoft protection infrastructure |
| 11:48:23 UTC | Email processed through Microsoft frontend transport  |
| 11:48:24 UTC | Message processed by mailbox infrastructure           |
| 11:48:25 UTC | Message processing completed                          |

---

# ⚠️ Attack Classification

## Potential Business Email Compromise (BEC)

### Category

**Executive Impersonation / Financial Fraud Attempt**

The primary objective indicated by the email is to convince the recipient to make a financial transfer.

The email does not primarily request a password or other credentials. Instead, it attempts to influence the recipient into performing a financial transaction.

---

# 🧩 MITRE ATT&CK Mapping

Potentially relevant technique:

### T1566.002 — Phishing: Spearphishing Link

The email contains an external URL presented as payment instructions.

Additional MITRE ATT&CK mappings should only be added when supported by investigation evidence.

---

# 🚨 Recommended SOC Response

## Immediate Actions

1. Do not initiate the requested wire transfer.
2. Do not open the suspicious URL.
3. Preserve the original `.eml` file and headers.
4. Report the email to the SOC/security team.
5. Quarantine the email.

## Investigation

6. Search the mail environment for the sender domain.
7. Search for the sending IP.
8. Search for the suspicious URL/domain.
9. Identify other recipients of the message.
10. Determine whether any user clicked the URL.
11. Determine whether any financial transaction was attempted.

## Containment

12. Block confirmed malicious domains and URLs.
13. Block confirmed malicious infrastructure where appropriate.
14. Remove related phishing emails from affected mailboxes.

## Recovery

15. Contact the finance team if a transaction was attempted.
16. Verify financial requests through an independent communication channel.
17. Continue monitoring affected accounts and systems.
18. Document the incident and update detection rules.

---

# 📝 Final Assessment

The investigated email contains multiple characteristics consistent with a **potential Business Email Compromise / executive impersonation attempt**.

Key observations include:

* Sender claims to be a CEO.
* Sender domain does not correspond to the organization represented.
* Email requests an INR 18,75,000 wire transfer.
* Message creates urgency with a 4:00 PM deadline.
* Recipient is instructed not to discuss the request.
* Payment instructions are provided through an external domain.
* Sending IP and domains can be extracted as investigation indicators.
* SPF passed, DKIM was absent, and DMARC passed; these authentication results do not independently establish the legitimacy of the claimed identity.

---

# 📚 Skills Demonstrated

This project demonstrates practical skills in:

* Email Header Analysis
* Phishing Investigation
* Business Email Compromise Analysis
* Email Authentication Analysis
* SPF / DKIM / DMARC
* IOC Extraction
* URL Investigation
* Domain Investigation
* IP Investigation
* Threat Intelligence
* Social Engineering Analysis
* Incident Response
* MITRE ATT&CK Mapping
* Security Documentation


---

