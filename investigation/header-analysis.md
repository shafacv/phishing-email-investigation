# Header Analysis

## Header Findings

### Sender IP

- Sender IP: `98.177.68.12`
- Hostname: `mail.citiprepaid-salarysea-at.tk`

### SPF

- Result: `PASS`
- The sending IP `98.177.68.12` is authorized by the sender domain.

### DKIM

- Result: `NONE`
- The email was not signed with DKIM.

### DMARC

- Result: `PASS`
- Header From domain: `citiprepaid-salarysea-at.tk`

### Sender Information

- From: `rajiv.mehra@citiprepaid-salarysea-at.tk`
- Reply-To: `rajiv.mehra@citiprepaid-salarysea-at.tk`
- Return-Path: `rajiv.mehra@citiprepaid-salarysea-at.tk`
- X-Originating-IP: `98.177.68.12`

### Microsoft Filtering

- SCL: `9`
- The message was classified with a high spam confidence level.

## Analysis

The email passed SPF and DMARC, but DKIM was not present. Passing SPF or DMARC alone does not prove that an email is legitimate. The sender domain itself is suspicious and does not match the organization identity claimed in the email.

The originating IP was also investigated separately using VirusTotal.

## Conclusion

The header information provides several useful indicators for investigation, including the sender domain, originating IP address, authentication results, and Microsoft filtering information.
