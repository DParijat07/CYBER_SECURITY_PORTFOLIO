# Email Security Monitoring

> **Blue Team → SOC → Security Monitoring → Email Security Monitoring**

Email remains one of the most common initial access vectors in modern cyber attacks.

A SOC analyst must be able to monitor email activity, identify phishing indicators, investigate malicious messages, analyze attachments and links, trace sender infrastructure, identify compromised accounts, and correlate email activity with endpoint and identity telemetry.

The core SOC question is:

> **Did this email represent a legitimate business communication, a malicious attempt, or the beginning of an account compromise or malware infection?**

---

# 1. Objectives

After completing this section, you should understand:

* Email security monitoring fundamentals
* Email telemetry
* SMTP and email flow
* Email authentication
* SPF
* DKIM
* DMARC
* Email headers
* Phishing detection
* Business Email Compromise
* Malicious attachments
* Malicious URLs
* Spoofing
* Account compromise
* Email security gateways
* Email alerts
* SIEM integration
* Email incident investigation
* Email-based threat hunting

---

# 2. Why Email Monitoring Matters

Email can be used for:

```text
Phishing
Credential Theft
Malware Delivery
Business Email Compromise
Fraud
Account Takeover
Malicious Links
Malicious Attachments
Social Engineering
Initial Access
```

A common attack chain is:

```text
Attacker
   ↓
Phishing Email
   ↓
Victim Clicks Link
   ↓
Credential Theft
   ↓
Account Compromise
   ↓
Cloud / SaaS Access
   ↓
Further Attack
```

Therefore, email monitoring is closely connected to:

```text
Identity Security
Endpoint Security
Cloud Security
Network Security
Incident Response
```

---

# 3. Email Monitoring Architecture

A simplified architecture:

```text
                    INTERNET
                       │
                       ↓
                  SMTP / EMAIL
                       │
                       ↓
              Email Security Gateway
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       Filtering     Sandbox      URL Analysis
          │            │            │
          └────────────┼────────────┘
                       ↓
                  Mail Server
                       │
                       ↓
                     User
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
         Endpoint             Identity
             │                   │
             └─────────┬─────────┘
                       ↓
                      SIEM
                       ↓
                     SOC
```

---

# 4. Email Telemetry

Important email telemetry includes:

```text
Sender
Recipient
Timestamp
Subject
Message ID
Source IP
Destination
Attachment
URL
Authentication Result
SPF
DKIM
DMARC
Delivery Action
Gateway Verdict
User Action
```

Additional telemetry may include:

```text
Attachment Hash
URL Reputation
Sandbox Result
Click Event
Message Location
Quarantine Status
```

---

# 5. Email Flow

A simplified email flow:

```text
Sender
  ↓
SMTP Server
  ↓
Internet
  ↓
Recipient Mail Gateway
  ↓
Filtering
  ↓
Mailbox
  ↓
User
```

The SOC may monitor multiple stages of this flow.

---

# 6. SMTP

SMTP stands for:

> **Simple Mail Transfer Protocol**

It is primarily used for sending and transferring email.

Common ports:

```text
25
465
587
```

The SOC should understand that SMTP telemetry can provide useful information about:

```text
Sender
Recipient
Mail Server
Connection
Authentication
Delivery
```

---

# 7. Email Header Analysis

Email headers provide valuable investigation evidence.

Important fields include:

```text
From
To
Date
Subject
Message-ID
Received
Reply-To
Return-Path
Authentication-Results
DKIM-Signature
```

One of the most important fields is:

```text
Received
```

because multiple Received headers can help reconstruct the email's delivery path.

---

# 8. From vs Reply-To

A phishing email may appear to come from:

```text
From: support@example.com
```

but contain:

```text
Reply-To: attacker@example.net
```

This mismatch can be suspicious.

Investigate:

```text
From
Reply-To
Return-Path
Authentication Results
```

---

# 9. Return-Path

The Return-Path identifies where delivery-related bounce messages are directed.

A mismatch between:

```text
From
Return-Path
Reply-To
```

does not automatically mean malicious activity, but it can be a useful investigation indicator.

---

# 10. SPF

SPF stands for:

> **Sender Policy Framework**

SPF allows a domain owner to specify which mail servers are authorized to send email for the domain.

Conceptually:

```text
Domain
  ↓
SPF Policy
  ↓
Authorized Mail Servers
```

The recipient mail system can compare:

```text
Sending Server
vs
SPF Policy
```

Possible results include:

```text
Pass
Fail
SoftFail
Neutral
None
```

---

# 11. DKIM

DKIM stands for:

> **DomainKeys Identified Mail**

DKIM uses cryptographic signatures to help verify that an email was authorized by the sending domain and that signed portions of the message were not modified in transit.

Conceptually:

```text
Sender
 ↓
DKIM Signature
 ↓
Email
 ↓
Recipient
 ↓
Signature Verification
```

Possible result:

```text
Pass
Fail
```

---

# 12. DMARC

DMARC stands for:

> **Domain-based Message Authentication, Reporting and Conformance**

DMARC builds on SPF and DKIM.

Conceptually:

```text
SPF
+
DKIM
+
Domain Alignment
+
Policy
```

DMARC policies commonly include:

```text
none
quarantine
reject
```

---

# 13. SPF + DKIM + DMARC

Think of them as:

```text
SPF
 ↓
Is the sending server authorized?

DKIM
 ↓
Is there a valid cryptographic signature?

DMARC
 ↓
Does the message align with the domain's authentication policy?
```

A SOC analyst should understand all three because they provide important email-security telemetry.

---

# 14. Email Authentication Monitoring

Monitor:

```text
SPF Result
DKIM Result
DMARC Result
Domain
Sender
Source IP
Alignment
```

Potentially suspicious:

```text
SPF Fail
+
DKIM Fail
+
DMARC Fail
```

However:

> **Authentication failure alone does not prove phishing.**

Always consider context.

---

# 15. Phishing Monitoring

Phishing attempts commonly contain:

```text
Urgency
Credential Requests
Suspicious Links
Unexpected Attachments
Impersonation
Financial Requests
Account Warnings
Fake Login Pages
```

SOC analysts should examine:

```text
Sender
Domain
URL
Attachment
Authentication
Content
Recipient
User Action
```

---

# 16. Phishing Detection Workflow

```text
Email Alert
     ↓
Inspect Sender
     ↓
Inspect Domain
     ↓
Analyze Headers
     ↓
Check SPF/DKIM/DMARC
     ↓
Inspect URL
     ↓
Inspect Attachment
     ↓
Check Reputation
     ↓
Check Other Recipients
     ↓
Check User Interaction
     ↓
Correlate Endpoint
     ↓
Correlate Identity
     ↓
Determine Impact
```

---

# 17. Sender Analysis

Investigate:

```text
Display Name
Email Address
Domain
Source IP
Reply-To
Return-Path
Authentication
```

Example:

```text
Display Name:
Microsoft Support

Email:
support@micros0ft-example.com
```

Look for:

```text
Typosquatting
Lookalike Domains
Unexpected TLD
Domain Age
Brand Impersonation
```

---

# 18. Display Name Spoofing

An attacker may use:

```text
Display Name:
CEO Name

Actual Email:
attacker@example.net
```

This can fool users who focus only on the visible display name.

SOC monitoring should therefore distinguish:

```text
Display Name
vs
Actual Sender Address
```

---

# 19. Lookalike Domains

Attackers may register domains that resemble legitimate domains.

Example:

```text
legitimate:
company.com

lookalike:
cornpany.com
```

Other techniques include:

```text
Character Substitution
Extra Characters
Hyphenation
Different TLD
Subdomain Abuse
```

---

# 20. URL Monitoring

Inspect:

```text
URL
Domain
Path
Parameters
Protocol
Redirects
Reputation
```

Potential indicators:

```text
Unexpected Domain
URL Shortener
Credential Page
Multiple Redirects
Recently Registered Domain
Suspicious Path
```

---

# 21. URL Shorteners

Shortened URLs can hide the final destination.

Example:

```text
Email
 ↓
Short URL
 ↓
Redirect
 ↓
Credential Page
```

The SOC should analyze the complete redirect chain where safe and authorized.

---

# 22. Malicious Attachment Monitoring

Common attachment categories requiring additional scrutiny:

```text
Executable Files
Script Files
Macro-enabled Documents
Archives
Disk Images
HTML Files
Shortcut Files
```

The presence of an attachment alone does not prove maliciousness.

Investigate:

```text
Sender
Hash
File Type
Extension
Content
Sandbox Result
Recipient
User Action
```

---

# 23. Double Extension Detection

A suspicious filename may attempt to disguise its actual file type.

Example:

```text
Invoice.pdf.exe
```

A monitoring rule can identify:

```text
Multiple Extensions
+
Executable Extension
```

Investigate the actual file type rather than trusting the displayed filename.

---

# 24. Attachment Hashing

A file hash can help identify whether the same attachment was delivered to multiple users.

Common hashes:

```text
MD5
SHA-1
SHA-256
```

For modern security workflows, SHA-256 is commonly preferred.

Example:

```text
Email A
 ↓
Attachment
 ↓
SHA-256
 ↓
Search Across Environment
```

This can reveal campaign scope.

---

# 25. Attachment Campaign Analysis

Suppose:

```text
User A → invoice.zip
User B → invoice.zip
User C → invoice.zip
User D → invoice.zip
```

If the hashes match:

```text
Same Attachment
```

The SOC can investigate the event as a possible campaign rather than isolated emails.

---

# 26. Business Email Compromise

Business Email Compromise (BEC) involves abusing email or compromised accounts to conduct fraud or unauthorized activity.

Common scenarios:

```text
Fake Executive Request
Payment Fraud
Invoice Fraud
Vendor Impersonation
Credential Theft
Sensitive Information Request
```

---

# 27. BEC Detection

Potential indicators:

```text
Executive Impersonation
Urgent Payment Request
New Bank Details
Unusual Recipient
External Reply-To
Compromised Account
Unexpected Mailbox Rule
```

Example:

```text
CEO
 ↓
Urgent Payment Request
 ↓
New Bank Account
```

This should be treated as a high-risk scenario.

---

# 28. Compromised Email Account

An attacker who compromises an email account may:

```text
Read Messages
Send Phishing Emails
Create Rules
Delete Messages
Forward Messages
Access Sensitive Information
```

Monitor:

```text
Login
IP
Location
Mailbox Actions
Forwarding Rules
Inbox Rules
Sent Messages
```

---

# 29. Suspicious Mailbox Rules

Attackers may create rules to hide or redirect messages.

Example:

```text
Incoming Mail
     ↓
Contains "Invoice"
     ↓
Move to Hidden Folder
```

or:

```text
Incoming Mail
     ↓
Forward to External Address
```

Unexpected mailbox rules should be investigated.

---

# 30. Email Forwarding Monitoring

Monitor:

```text
Forwarding Enabled
Forwarding Destination
Rule Creation
Rule Modification
```

Potentially suspicious:

```text
Corporate Mailbox
 ↓
External Forwarding
 ↓
Unknown Domain
```

Possible explanations include:

```text
Compromise
Shadow IT
User Configuration
Business Requirement
```

---

# 31. OAuth / Application Access

Modern email platforms may allow third-party applications to access mail.

Monitor:

```text
Application Authorization
OAuth Consent
Permission Scope
Application
User
Timestamp
```

Suspicious example:

```text
User
 ↓
Unknown Application
 ↓
Mail.Read
 ↓
Large Mailbox Access
```

This can indicate malicious OAuth consent or application abuse.

---

# 32. Suspicious Login Monitoring

Email account authentication should be correlated with:

```text
Source IP
Location
Device
MFA
User Agent
Login Time
Previous Login
```

Potential anomaly:

```text
Normal:
India → Corporate Device → MFA

Unexpected:
Unknown Location → Unknown Device → Mail Access
```

Investigate rather than immediately declaring compromise.

---

# 33. Impossible Travel

Example:

```text
09:00 → Kolkata
09:20 → London
```

This could be:

```text
Compromise
VPN
Proxy
Travel
Geo-IP Error
```

Treat impossible travel as an investigation signal.

---

# 34. Mailbox Data Exfiltration

An attacker may attempt to collect email data.

Indicators can include:

```text
Large Mailbox Access
Unusual Search Activity
Mass Download
External Forwarding
OAuth Access
Unexpected API Usage
```

Correlate:

```text
Identity
Email
Cloud
Endpoint
```

---

# 35. Email Security Gateway

An email security gateway may provide:

```text
Spam Detection
Malware Detection
URL Filtering
Attachment Analysis
Sandboxing
Sender Reputation
Authentication Checks
Quarantine
```

The SOC should integrate relevant gateway alerts into the SIEM.

---

# 36. Email + SIEM Architecture

```text
Email Gateway
      │
      ↓
Mail Server
      │
      ├── Authentication Logs
      ├── Message Logs
      ├── URL Events
      ├── Attachment Events
      └── Mailbox Events
             │
             ↓
            SIEM
             │
       ┌─────┼─────┐
       ↓     ↓     ↓
    Identity Endpoint Network
       │     │     │
       └─────┼─────┘
             ↓
            SOC
```

---

# 37. Correlation Example — Phishing

```text
Phishing Email
      ↓
User Clicks Link
      ↓
Authentication Attempt
      ↓
Successful Login
      ↓
New Device
      ↓
Mailbox Access
```

This is significantly more suspicious than the original email alone.

---

# 38. Correlation Example — Malware

```text
Malicious Email
      ↓
Attachment Delivered
      ↓
User Opens File
      ↓
Process Created
      ↓
Network Connection
      ↓
Suspicious DNS
```

The SOC should correlate:

```text
Email
+
Endpoint
+
Network
```

---

# 39. Correlation Example — BEC

```text
Compromised Account
      ↓
Mailbox Access
      ↓
Create Forwarding Rule
      ↓
Send External Email
      ↓
Financial Request
```

This can indicate a BEC campaign.

---

# 40. Email Threat Hunting

Useful hunting questions:

```text
Which users received this email?

Which users clicked the URL?

Which users opened the attachment?

Did anyone authenticate after clicking?

Did the same sender target multiple users?

Was the attachment hash seen elsewhere?

Did the sender domain pass authentication?

Did the recipient account show suspicious login activity?
```

---

# 41. Email Investigation Flow

```text
Alert
 ↓
Identify Message
 ↓
Identify Sender
 ↓
Identify Recipients
 ↓
Analyze Headers
 ↓
Analyze Authentication
 ↓
Analyze URLs
 ↓
Analyze Attachments
 ↓
Search Campaign Scope
 ↓
Check User Interaction
 ↓
Check Identity Events
 ↓
Check Endpoint Events
 ↓
Check Network Events
 ↓
Determine Impact
 ↓
Contain
 ↓
Document
```

---

# 42. Email Incident Containment

Depending on the incident, actions may include:

```text
Quarantine Email
Remove Malicious Message
Block Sender
Block Domain
Block URL
Block File Hash
Reset Credentials
Revoke Sessions
Revoke OAuth Tokens
Disable Account
```

Actions should follow organizational procedures and authorization.

---

# 43. Practical Lab — Phishing Investigation

Use a controlled phishing simulation or authorized lab.

Create/document:

```text
Email
 ↓
Header Analysis
 ↓
SPF/DKIM/DMARC
 ↓
URL Analysis
 ↓
Attachment Analysis
 ↓
User Interaction
 ↓
Endpoint Correlation
```

Produce:

```text
Investigation Report
```

---

# 44. Practical Lab — Email Header Analysis

Take a legitimate test email.

Analyze:

```text
From
To
Reply-To
Return-Path
Received
Message-ID
Authentication-Results
SPF
DKIM
DMARC
```

Build the delivery path:

```text
Sender
 ↓
Mail Server
 ↓
Gateway
 ↓
Recipient
```

---

# 45. Practical Lab — Phishing Campaign Scope

Using authorized lab data:

```text
Sender
 ↓
Recipients
 ↓
Message ID
 ↓
URL / Attachment
 ↓
Hash
```

Search for other recipients who received the same campaign.

Document:

```text
Total Recipients
Clicked
Opened
Reported
Blocked
Compromised
```

---

# 46. Practical Lab — Malicious Attachment Investigation

Use a safe, authorized malware-analysis lab.

Collect:

```text
Filename
Extension
SHA-256
File Type
Sender
Recipients
Delivery Time
Detection
Sandbox Result
```

Do not execute unknown files on your normal workstation.

Use an isolated analysis environment.

---

# 47. Practical Lab — BEC Investigation

Simulate a legitimate test scenario:

```text
Compromised Test Account
 ↓
Mailbox Access
 ↓
Forwarding Rule
 ↓
External Message
```

Investigate:

```text
Login
Mailbox Activity
Rule Creation
Message
Recipient
Source IP
```

Build a timeline.

---

# 48. Practical Lab — Email + Endpoint Correlation

Controlled scenario:

```text
Email Delivered
      ↓
User Opens Attachment
      ↓
Process Created
      ↓
Network Connection
```

Correlate:

```text
Email Timestamp
Process Creation
Network Connection
Destination
```

Determine whether the events form a single attack chain.

---

# 49. Practical Lab — Email + Identity Correlation

Controlled scenario:

```text
Phishing Email
      ↓
User Click
      ↓
Login
      ↓
MFA Event
      ↓
Mailbox Access
```

Investigate:

```text
Source IP
Device
Authentication
MFA
Session
Mailbox Activity
```

---

# 50. Detection Matrix

| Threat               | Primary Telemetry | Useful Correlation |
| -------------------- | ----------------- | ------------------ |
| Phishing             | Email Gateway     | Identity           |
| Malicious Attachment | Email + Hash      | Endpoint           |
| Malicious URL        | URL Logs          | Browser/Endpoint   |
| BEC                  | Mailbox           | Identity           |
| Account Compromise   | Authentication    | Mailbox            |
| Password Attack      | Auth Logs         | Email              |
| Mailbox Rule Abuse   | Mailbox Logs      | Identity           |
| OAuth Abuse          | OAuth Logs        | Cloud              |
| Data Exfiltration    | Mailbox           | Network            |
| Spoofing             | SPF/DKIM/DMARC    | Headers            |
| Campaign             | Message ID/Hash   | Recipients         |

---

# 51. Email Security Investigation Checklist

## Sender

```text
Who sent it?
Is the domain legitimate?
Is the display name suspicious?
```

## Authentication

```text
SPF?
DKIM?
DMARC?
Alignment?
```

## Header

```text
Received path?
Reply-To?
Return-Path?
Message-ID?
```

## Content

```text
Urgency?
Credential request?
Financial request?
Unexpected attachment?
```

## URL

```text
Domain?
Redirect?
Reputation?
Destination?
```

## Attachment

```text
File type?
Hash?
Sandbox?
Campaign?
```

## User

```text
Did they open it?
Did they click?
Did they authenticate?
```

## Endpoint

```text
Process?
DNS?
Network?
File?
```

## Identity

```text
Login?
MFA?
Session?
Location?
```

---

# 52. Common Email Monitoring Blind Spots

```text
No Email Gateway Logs
No Header Visibility
No SPF Monitoring
No DKIM Monitoring
No DMARC Monitoring
No URL Telemetry
No Attachment Hashing
No Mailbox Audit Logs
No OAuth Monitoring
No Identity Correlation
No Endpoint Correlation
No Campaign Tracking
```

These gaps make phishing investigations significantly harder.

---

# 53. SOC Detection Rules

Example detection concepts:

### Rule 1 — Multiple Failed Logins

```text
Same User
+
Multiple Failed Logins
+
Short Time Window
```

### Rule 2 — Phishing + Login

```text
Suspicious Email
+
User Click
+
Authentication Event
```

### Rule 3 — Suspicious Attachment + Process

```text
Email Attachment
+
User Opens File
+
New Process
```

### Rule 4 — External Forwarding

```text
Mailbox Rule Created
+
External Destination
```

### Rule 5 — Suspicious OAuth

```text
Unknown Application
+
Mail Read Permission
+
Unexpected User
```

---

# 54. Email Alert Triage

When an email alert arrives:

```text
1. Identify sender
2. Identify recipients
3. Check authentication
4. Analyze headers
5. Analyze URLs
6. Analyze attachments
7. Determine campaign scope
8. Check user interaction
9. Correlate identity
10. Correlate endpoint
11. Determine impact
12. Contain
13. Document
```

---

# 55. Severity Considerations

A single suspicious email:

```text
Potentially Low / Medium
```

Phishing email clicked:

```text
Medium / High
```

Credential submission:

```text
High
```

Confirmed account compromise:

```text
High / Critical
```

Multiple compromised accounts:

```text
Critical
```

Severity depends on organizational impact and context.

---

# 56. Portfolio Deliverables

Create:

```text
09-Email-Security-Monitoring/

├── README.md
│
├── Labs/
│   ├── 01-Email-Header-Analysis/
│   ├── 02-Phishing-Investigation/
│   ├── 03-Malicious-URL-Analysis/
│   ├── 04-Malicious-Attachment-Analysis/
│   ├── 05-Phishing-Campaign-Analysis/
│   ├── 06-BEC-Investigation/
│   ├── 07-Mailbox-Rule-Investigation/
│   ├── 08-Email-Identity-Correlation/
│   └── 09-Email-Endpoint-Correlation/
│
├── Detection-Rules/
│   ├── phishing.yml
│   ├── suspicious_attachment.yml
│   ├── mailbox_forwarding.yml
│   └── suspicious_oauth.yml
│
└── Reports/
    ├── Phishing-Investigation-Report.md
    └── BEC-Investigation-Report.md
```

---

# 57. Interview Questions

### Fundamentals

1. What is phishing?
2. What is spear phishing?
3. What is Business Email Compromise?
4. What is email spoofing?
5. What is SPF?
6. What is DKIM?
7. What is DMARC?
8. What is the purpose of the Received header?
9. What is a Reply-To mismatch?
10. Why are email headers important?

### SOC Investigation

11. How would you investigate a phishing email?
12. How would you identify all users who received the same phishing campaign?
13. How would you investigate a malicious attachment?
14. How would you determine whether a user clicked a phishing link?
15. How would you correlate a phishing email with endpoint telemetry?
16. How would you detect BEC?
17. How would you investigate suspicious mailbox forwarding?
18. How would you detect compromised email accounts?
19. What logs would you collect during an email investigation?
20. How would you determine the severity of a phishing alert?

---

# 58. Interview Scenario

> **A user reports a suspicious email. The email appears to come from the CEO and requests an urgent financial transfer. How would you investigate?**

Start with:

```text
Display Name
 ↓
Actual Sender
 ↓
Domain
 ↓
Reply-To
 ↓
Return-Path
 ↓
Received Headers
 ↓
SPF
 ↓
DKIM
 ↓
DMARC
 ↓
URL / Attachment
 ↓
Other Recipients
 ↓
User Interaction
```

Then investigate:

```text
Identity
Endpoint
Mailbox
```

Finally determine:

```text
Spoofing?
Phishing?
BEC?
Compromised Account?
```

---

# 59. Interview Scenario — Malicious Attachment

> **A user opened an attachment received through email. What would you check?**

Investigate:

```text
Email
 ↓
Attachment Hash
 ↓
File Type
 ↓
User Action
 ↓
Process Creation
 ↓
Child Processes
 ↓
Network Connections
 ↓
DNS
 ↓
Persistence
```

Then determine whether the attachment resulted in endpoint compromise.

---

# 60. Key Takeaways

```text
1. Email is a major initial-access vector.

2. Email security monitoring requires visibility into messages, headers, authentication, URLs, attachments, and user activity.

3. SPF verifies authorized sending infrastructure.

4. DKIM provides cryptographic email signing.

5. DMARC provides domain-level authentication policy and alignment.

6. SPF, DKIM, and DMARC failures are useful signals but do not automatically prove maliciousness.

7. Header analysis is essential during phishing investigations.

8. Display-name spoofing can hide the actual sender.

9. Lookalike domains are common in phishing campaigns.

10. Malicious attachments should be analyzed using hashes, file types, sandbox results, and endpoint telemetry.

11. BEC requires monitoring of identity, mailbox, and financial/business activity.

12. Suspicious mailbox forwarding can indicate account compromise.

13. OAuth permissions should be monitored in modern cloud email environments.

14. Email incidents should be correlated with identity, endpoint, network, and cloud telemetry.

15. A SOC analyst should investigate the entire attack chain rather than the email alone.
```

---

# 61. Final Mental Model

```text
                       EMAIL
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
           Sender                Recipient
              │                     │
              ↓                     ↓
       SPF / DKIM / DMARC       Mailbox
              │                     │
              ↓                     ↓
        Email Gateway          User Action
              │                     │
       ┌──────┼──────┐              ↓
       ↓      ↓      ↓          Endpoint
      URL   File   Header            │
       │      │      │              ↓
       └──────┼──────┘          Network
              │                     │
              └──────────┬──────────┘
                         ↓
                        SIEM
                         ↓
                     Correlation
                         ↓
                      Detection
                         ↓
                        Alert
                         ↓
                  SOC Investigation
                         ↓
                       Timeline
                         ↓
                 Containment / Response
                         ↓
                       Report
```

> **Email security monitoring is not simply identifying phishing emails. It is the ability to trace an email from sender infrastructure through delivery and user interaction to identity, endpoint, network, and business impact.**
