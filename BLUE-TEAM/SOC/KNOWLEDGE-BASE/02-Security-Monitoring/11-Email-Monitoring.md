# Email Monitoring

## 1. Introduction

Email monitoring is the process of collecting, analyzing, and correlating email-related security telemetry to detect phishing, malicious attachments, credential theft, malware delivery, business email compromise, account compromise, and other email-based threats.

Email remains one of the most common initial access vectors used by attackers.

From a SOC perspective, email monitoring helps analysts answer:

* Who sent the email?
* Who received it?
* Where did it originate?
* What links or attachments were included?
* Was the email delivered?
* Did the recipient open or interact with it?
* Did the user click a malicious link?
* Was an attachment downloaded?
* Did the activity lead to endpoint or account compromise?

A complete monitoring process connects:

```text
Email
  ↓
Email Security Gateway
  ↓
User Interaction
  ↓
Endpoint
  ↓
Identity
  ↓
Network
  ↓
SIEM
  ↓
SOC Investigation
```

---

## 2. Why Email Monitoring Is Important

Organizations use email for:

* Business communication
* File sharing
* Account notifications
* Financial transactions
* Customer communication
* Password resets
* Internal communication

Because email is trusted and widely used, attackers frequently abuse it for:

* Phishing
* Malware delivery
* Credential harvesting
* Business Email Compromise (BEC)
* Spear phishing
* Malicious links
* Malicious attachments
* Social engineering
* Account takeover

Effective email monitoring provides early visibility into these attacks.

---

## 3. Objectives of Email Monitoring

The primary objectives are:

1. Detect phishing attempts
2. Identify malicious attachments
3. Detect malicious URLs
4. Identify spoofed senders
5. Detect compromised accounts
6. Monitor suspicious email behavior
7. Identify malware delivery
8. Detect credential harvesting attempts
9. Correlate email activity with endpoint events
10. Support incident investigation and response

---

## 4. Email Security Telemetry

Important email telemetry can come from:

* Mail servers
* Email security gateways
* Microsoft 365
* Google Workspace
* Secure Email Gateways
* Endpoint security platforms
* DNS logs
* Proxy logs
* Web gateway logs
* SIEM platforms

Typical information includes:

```text
Sender
Recipient
Timestamp
Source IP
Destination
Subject
Message ID
Attachment name
Attachment type
URL
Delivery status
Authentication results
Spam score
Malware verdict
User interaction
```

---

## 5. Email Authentication Monitoring

Email authentication technologies help determine whether a message is legitimate.

Important mechanisms include:

### SPF

**Sender Policy Framework (SPF)** helps identify whether the sending server is authorized to send email for a domain.

Example:

```text
SPF Result: PASS
```

or:

```text
SPF Result: FAIL
```

An SPF failure does not automatically mean an email is malicious, but it can increase suspicion.

---

### DKIM

**DomainKeys Identified Mail (DKIM)** uses cryptographic signatures to help verify that an email was authorized by the sending domain and was not altered in transit.

Example:

```text
DKIM: PASS
```

or:

```text
DKIM: FAIL
```

---

### DMARC

**Domain-based Message Authentication, Reporting, and Conformance (DMARC)** uses SPF and DKIM results together with domain alignment policies.

Possible results include:

```text
DMARC: PASS
DMARC: FAIL
```

SOC analysts should consider authentication results together with other indicators rather than treating a single result as definitive.

---

## 6. Important Email Log Fields

A SOC analyst should examine fields such as:

```text
Timestamp
Sender
Recipient
Sender Domain
Recipient Domain
Source IP
Message ID
Subject
Attachment
Attachment Hash
URL
SPF Result
DKIM Result
DMARC Result
Spam Score
Malware Verdict
Delivery Action
User Action
```

Example:

```text
Timestamp: 2026-08-14 09:21:31
Sender: security-alert@example.com
Recipient: employee@example.org
Source IP: 185.XX.XX.25
SPF: FAIL
DKIM: FAIL
DMARC: FAIL
Attachment: invoice.zip
Verdict: Suspicious
Action: Quarantined
```

This event should be investigated because multiple indicators suggest possible malicious email activity.

---

## 7. Phishing Monitoring

Phishing attempts attempt to trick users into performing actions that benefit an attacker.

Common phishing objectives include:

* Credential theft
* Malware installation
* Financial fraud
* Account takeover
* Delivery of malicious payloads
* Information gathering

Common indicators include:

```text
Urgent language
Unexpected attachments
Suspicious URLs
Look-alike domains
Domain impersonation
Authentication failures
Unusual sender
Unexpected password-reset requests
Requests for financial information
```

---

## 8. Spear Phishing

Spear phishing is targeted phishing directed at a specific individual or organization.

Example:

```text
Attacker
   ↓
Research employee
   ↓
Impersonate manager
   ↓
Send targeted email
   ↓
Request sensitive information
```

SOC analysts should pay attention to:

* Executive impersonation
* Vendor impersonation
* Internal-domain spoofing
* Personalized messages
* Unusual requests
* Requests involving payments or credentials

---

## 9. Business Email Compromise

Business Email Compromise (BEC) involves using compromised or impersonated email accounts to conduct fraud or other malicious activity.

Example:

```text
Compromised Executive Account
            ↓
        Email Employee
            ↓
"Urgent payment required"
            ↓
      Financial Loss
```

Indicators may include:

* Unusual login activity
* New forwarding rules
* Suspicious mailbox rules
* Unusual sending behavior
* Requests for money transfers
* Requests for sensitive documents
* Login from unusual locations
* Sudden changes in communication patterns

---

## 10. Malicious Attachment Monitoring

Attachments are commonly used to deliver malware.

Potentially suspicious attachment types include:

```text
.exe
.scr
.js
.vbs
.ps1
.bat
.cmd
.iso
.img
.zip
.rar
```

However, file extension alone does not determine whether a file is malicious.

The analyst should examine:

* File hash
* File type
* Sender reputation
* Attachment behavior
* Sandbox verdict
* User interaction
* Endpoint activity after execution

Example attack chain:

```text
Email
  ↓
Malicious Attachment
  ↓
User Opens File
  ↓
Process Execution
  ↓
PowerShell
  ↓
Network Connection
  ↓
Possible Malware Infection
```

---

## 11. Malicious URL Monitoring

Email links can redirect users to:

* Credential phishing pages
* Malware downloads
* Exploit kits
* Fake login portals
* Malicious websites

Important URL indicators include:

```text
Newly registered domain
Look-alike domain
IP address instead of domain
URL shortener
Suspicious TLD
Encoded parameters
Multiple redirects
Domain mismatch
```

Example:

```text
Displayed:
https://microsoft.com

Actual:
https://microsoft-login-example.com
```

This should be investigated as potential impersonation.

---

## 12. Email Spoofing

Email spoofing occurs when attackers manipulate email information to make a message appear to originate from a trusted sender.

Example:

```text
Displayed Sender:
ceo@company.com

Actual Sending Infrastructure:
Unknown External Server
```

SOC analysts should examine:

* SPF
* DKIM
* DMARC
* Return-Path
* Received headers
* Source IP
* Domain age/reputation
* Message routing

---

## 13. Email Header Analysis

Email headers provide useful information about the message's journey.

Important fields include:

```text
From
To
Date
Subject
Message-ID
Return-Path
Received
Reply-To
Authentication-Results
X-Originating-IP
```

Example:

```text
From: manager@example.com
Reply-To: attacker@malicious-domain.example
```

A mismatch between `From` and `Reply-To` can be suspicious.

However, legitimate applications can also produce header differences, so context is important.

---

## 14. Email Monitoring in a SOC

Email security telemetry should be integrated into the SIEM.

Example:

```text
Email Server
     ↓
Email Security Gateway
     ↓
Email Logs
     ↓
Log Collector
     ↓
SIEM
     ↓
Correlation Rules
     ↓
SOC Analyst
```

The SOC should correlate email events with:

* Identity logs
* Endpoint logs
* DNS logs
* Proxy logs
* Firewall logs
* EDR alerts
* Cloud security logs

---

## 15. Example Email Attack Correlation

Consider the following sequence:

```text
09:00
Phishing email delivered
       ↓
09:05
User clicks malicious URL
       ↓
09:06
Browser accesses suspicious domain
       ↓
09:07
PowerShell starts on endpoint
       ↓
09:08
Endpoint connects to external IP
       ↓
09:10
Suspicious authentication event
```

Individually, some events may not be sufficient to confirm compromise.

Together, they provide strong evidence of a possible attack chain.

---

## 16. Detection Rules

### Rule 1 — Multiple Phishing Emails

```text
IF
same suspicious sender
sends emails
to multiple employees

THEN
generate alert
```

Severity:

```text
Medium
```

---

### Rule 2 — Authentication Failure

```text
IF
SPF = FAIL
AND
DKIM = FAIL
AND
DMARC = FAIL

THEN
increase email risk score
```

The event should be correlated with sender reputation and content indicators.

---

### Rule 3 — Malicious Attachment

```text
IF
email contains suspicious attachment
AND
security engine detects malware

THEN
generate high-priority alert
```

Severity:

```text
High
```

---

### Rule 4 — User Clicks Malicious URL

```text
IF
user clicks URL
AND
URL is classified as malicious

THEN
correlate with endpoint activity
```

Severity:

```text
High
```

---

### Rule 5 — Suspicious Mailbox Rule

```text
IF
new mailbox forwarding rule is created
AND
destination is external
AND
user did not normally create forwarding rules

THEN
generate alert
```

This can be an indicator of account compromise.

---

## 17. Email Account Compromise Monitoring

Monitor for:

```text
Unusual login location
Impossible travel
Multiple failed logins
New MFA configuration
New forwarding rules
New inbox rules
Mass email sending
Unusual recipients
Unusual attachments
Password reset
Session anomalies
```

Example:

```text
Normal:
User sends 30 emails/day

Observed:
User sends 2,000 emails in 30 minutes
```

Possible explanations include:

* Compromised account
* Spam campaign
* Malware
* Automated business process

Investigation is required.

---

## 18. Email Monitoring With Endpoint Telemetry

Email monitoring becomes significantly more useful when combined with endpoint monitoring.

Example:

```text
Phishing Email
      ↓
User Opens Attachment
      ↓
WINWORD.EXE
      ↓
PowerShell
      ↓
Suspicious Script
      ↓
Network Connection
      ↓
EDR Alert
```

The SOC can correlate the original email with the endpoint activity to establish the attack timeline.

---

## 19. SOC Email Triage Process

### Step 1 — Identify the Email

Determine:

```text
Sender
Recipient
Timestamp
Subject
Message ID
```

### Step 2 — Analyze Sender

Check:

```text
Domain
Source IP
Reputation
SPF
DKIM
DMARC
```

### Step 3 — Analyze Content

Look for:

```text
Urgency
Credential requests
Financial requests
Suspicious links
Attachments
Impersonation
Social engineering
```

### Step 4 — Analyze URLs

Check:

```text
Domain
Reputation
Redirects
Registration information
Threat intelligence
```

### Step 5 — Analyze Attachments

Check:

```text
File type
Hash
Malware verdict
Sandbox results
Execution history
```

### Step 6 — Check User Interaction

Determine whether the recipient:

```text
Opened the email
Clicked a link
Downloaded attachment
Executed attachment
Submitted credentials
```

### Step 7 — Correlate

Check:

```text
Identity logs
Endpoint logs
DNS logs
Proxy logs
EDR alerts
Network traffic
```

### Step 8 — Determine Severity

Classify the event:

```text
False Positive
Low
Medium
High
Critical
```

### Step 9 — Respond

Possible actions include:

```text
Quarantine email
Block sender
Block domain
Block malicious URL
Remove malicious messages
Reset compromised credentials
Isolate endpoint
Escalate incident
```

---

## 20. Example SOC Alert

```text
Alert:
Potential Phishing Email

Severity:
High

Sender:
finance-department@external-example.com

Recipient:
employee01@company.com

SPF:
FAIL

DKIM:
FAIL

DMARC:
FAIL

URL:
https://example-suspicious-domain.com/login

URL Verdict:
Malicious

User Action:
Clicked URL

Endpoint:
WIN-CLIENT-01
```

### Analyst Comment

```text
A suspicious email was delivered to an employee and contained
a URL classified as malicious. SPF, DKIM, and DMARC authentication
checks failed. The recipient clicked the URL, requiring endpoint,
identity, DNS, and network telemetry correlation to determine
whether credentials were submitted or additional malicious
activity occurred.
```

---

## 21. Email Monitoring Best Practices

Organizations should:

* Deploy secure email gateways
* Enable SPF
* Configure DKIM
* Implement DMARC
* Monitor email authentication failures
* Scan attachments
* Scan URLs
* Monitor mailbox rules
* Monitor suspicious forwarding
* Protect privileged accounts
* Enable MFA
* Integrate email telemetry with the SIEM
* Train users to identify phishing
* Maintain incident-response procedures
* Regularly review email security policies

---

## 22. Common Email Security Tools

### Email Security

Examples:

* Microsoft Defender for Office 365
* Google Workspace security controls
* Proofpoint
* Mimecast
* Secure Email Gateways

### SIEM

Examples:

* Wazuh
* Splunk
* Microsoft Sentinel
* IBM QRadar

### Endpoint Security

Examples:

* Microsoft Defender for Endpoint
* CrowdStrike Falcon
* SentinelOne

---

## 23. Email Monitoring Investigation Checklist

```text
[ ] Identify sender
[ ] Identify recipient
[ ] Check timestamp
[ ] Analyze sender domain
[ ] Check source IP
[ ] Check SPF result
[ ] Check DKIM result
[ ] Check DMARC result
[ ] Analyze email headers
[ ] Inspect URLs
[ ] Inspect attachments
[ ] Check attachment hash
[ ] Check threat intelligence
[ ] Determine whether user clicked
[ ] Determine whether attachment was opened
[ ] Check endpoint telemetry
[ ] Check DNS activity
[ ] Check network activity
[ ] Check authentication events
[ ] Check mailbox rules
[ ] Determine whether credentials were exposed
[ ] Determine severity
[ ] Document findings
[ ] Escalate if required
```

---

## 24. Key Takeaways

Email monitoring provides the SOC with visibility into one of the most common attack vectors.

A SOC analyst should be able to analyze:

```text
Email Metadata
      ↓
Sender Authentication
      ↓
Headers
      ↓
URLs
      ↓
Attachments
      ↓
User Interaction
      ↓
Endpoint Activity
      ↓
Identity Activity
      ↓
Network Activity
      ↓
Incident Investigation
```

The most important skills are:

* Phishing detection
* Email header analysis
* SPF/DKIM/DMARC analysis
* Malicious URL detection
* Attachment analysis
* BEC detection
* Email account compromise detection
* SIEM correlation
* Endpoint correlation
* SOC triage and incident response

**Effective email monitoring does not stop at identifying a suspicious message. The SOC must determine whether the user interacted with it and whether that interaction resulted in credential theft, malware execution, account compromise, or further stages of an attack.**
