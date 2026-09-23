# URL Analysis

## URL Extraction

The suspicious URL was extracted from the HTML source of the phishing email. The URL was not opened directly in a browser to avoid interacting with the potentially malicious website.

The extracted URL is:

http://adventure-nicaragua.net/index.php?option=com_mailto&tmpl=component&link=...

## URL Analysis Using VirusTotal

The extracted URL was submitted to VirusTotal for security analysis.

### Findings

- Protocol: HTTP
- Domain: `adventure-nicaragua.net`
- The URL received a suspicious/malicious detection from security analysis.
- The domain is unrelated to the organization identity claimed by the sender.
- The URL contains a `link=` parameter containing Base64-encoded data.

### Evidence

Screenshot:

`04-url-analysis.png`

## Base64 Analysis Using CyberChef

The `link=` parameter contains Base64-encoded data beginning with:

`aHR0cDovL2FkdmVudHVyZ...`

The available Base64 value was decoded using CyberChef.

### Decoded Result

The available encoded portion decoded to:

`http://adventur`

The Base64 value available in the email artifact was incomplete, so the complete destination could not be determined from this value alone.

### Evidence

Screenshot:

`08-cyberchef.png`

## URLScan Analysis

URLScan was attempted using the suspicious URL. However, the URL available in the email artifact was incomplete, and the submission returned an HTTP 400 error.

Therefore, no URLScan result was used as evidence in this investigation.

## URL Indicators

- Suspicious external domain: `adventure-nicaragua.net`
- HTTP rather than HTTPS
- Base64-encoded URL parameter
- URL associated with an urgent financial-transfer request
- Suspicious VirusTotal result

## Conclusion

The URL is a significant indicator of compromise (IOC) in this phishing investigation. It contains a suspicious external domain and an encoded parameter. VirusTotal was used for URL analysis, while CyberChef was used to examine the encoded value.

The URL should not be opened directly. It should be retained as an IOC for detection, blocking, and further investigation.
