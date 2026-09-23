# Phishing Email Investigation Report

## 1. Executive Summary

This project investigates a suspicious phishing email requesting an urgent financial transfer of INR 18,75,000.

The email uses CEO impersonation, urgency, secrecy, a suspicious sender domain, and an external URL. Email headers, URL reputation, IP reputation, domain information, and encoded URL data were examined as part of the investigation.

## 2. Email Details

- Sender: Rajiv Mehra, CEO
- Sender Email: `rajiv.mehra@citiprepaid-salarysea-at.tk`
- Recipient: Priya Sharma
- Subject: `Confidential: Urgent payment approval required`
- Date: 23 July 2026
- Reply-To: `rajiv.mehra@citiprepaid-salarysea-at.tk`

## 3. Initial Phishing Indicators

The email contains several suspicious characteristics:

- Urgent request for an INR 18,75,000 wire transfer
- Payment deadline of 4:00 PM
- Request to keep the transaction confidential
- Sender claims to be a Chief Executive Officer
- Sender domain does not match the organization identity claimed in the email
- Suspicious external URL
- The email attempts to create pressure by describing a confidential acquisition

These characteristics are consistent with a potential phishing or business email compromise scenario.

## 4. Email Header Analysis

The email headers were examined to identify technical indicators.

### Authentication Results

- SPF: `PASS`
- DKIM: `NONE`
- DMARC: `PASS`

### Sender Information

- Sender IP: `98.177.68.12`
- Hostname: `mail.citiprepaid-salarysea-at.tk`
- X-Originating-IP: `98.177.68.12`
- Return-Path: `rajiv.mehra@citiprepaid-salarysea-at.tk`

### Microsoft Filtering

- SCL: `9`

The authentication results were documented, but passing SPF and DMARC alone does not establish that the email is legitimate. The sender domain and other email characteristics were also considered.

## 5. URL Analysis

The suspicious URL was extracted from the HTML source of the email without directly opening the website.

The URL begins with:

`http://adventure-nicaragua.net/`

The URL was analyzed using VirusTotal.

### Findings

- Protocol: HTTP
- Suspicious external domain
- URL associated with the financial-transfer request
- URL contains a `link=` parameter containing Base64-encoded data
- VirusTotal identified suspicious activity associated with the URL

## 6. CyberChef Analysis

The Base64-encoded portion of the URL was examined using CyberChef.

The available encoded value decoded to:

`http://adventur`

The encoded value available in the email artifact was incomplete, so the complete destination could not be determined from the available data.

## 7. IP Analysis

The sender IP address was identified from the email headers:

`98.177.68.12`

The IP was investigated using VirusTotal and was also checked using AbuseIPDB as part of the investigation.

## 8. Domain Analysis

The sender domain was identified as:

`citiprepaid-salarysea-at.tk`

The domain was investigated using VirusTotal and WHOIS Lookup.

WHOIS information available during the investigation included the domain's nameserver information.

## 9. Indicators of Compromise

### Email

`rajiv.mehra@citiprepaid-salarysea-at.tk`

### Domain

`citiprepaid-salarysea-at.tk`

### IP Address

`98.177.68.12`

### URL Domain

`adventure-nicaragua.net`

### Subject

`Confidential: Urgent payment approval required`

## 10. Evidence Collected

The following evidence was collected during the investigation:

- `01-email.png` — Original suspicious email
- `02-headers.png` — Email header information
- `03-authentication.png` — SPF, DKIM and DMARC results
- `04-url-analysis.png` — VirusTotal URL analysis
- `05-ip-analysis.png` — VirusTotal IP analysis
- `06-domain-analysis.png` — VirusTotal domain analysis
- `07-cyberchef.png` — Base64 decoding using CyberChef
- `08-abuseipdb.png` — AbuseIPDB IP analysis

## 11. Tools Used

- VirusTotal
- CyberChef
- WHOIS Lookup
- AbuseIPDB

## 12. Analysis Techniques

- Email Header Analysis
- URL Analysis
- IP Address Analysis
- Domain Analysis
- IOC Extraction
- Base64 Decoding

## 13. URLScan

URLScan was attempted during the investigation. However, the URL available in the email artifact was incomplete and the submission returned an HTTP 400 error.

No URLScan result was used as evidence.

## 14. Conclusion

The investigated email contains multiple indicators associated with a potential phishing or business email compromise attempt.

The main indicators include a suspicious sender domain, an urgent financial request, secrecy instructions, a suspicious external URL, an originating IP address, and encoded URL data.

The investigation produced a set of technical indicators that can be used for further threat hunting, monitoring, detection, and blocking.

All findings in this report are based on the evidence available in the email artifact and the analysis performed during this investigation.
