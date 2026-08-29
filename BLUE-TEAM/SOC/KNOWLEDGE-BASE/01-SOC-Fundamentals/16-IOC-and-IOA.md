# IOC and IOA

> **SOC L1 Fundamental**

Indicators of Compromise (IOCs) and Indicators of Attack (IOAs) are important sources of evidence used by SOC analysts to identify, investigate, and understand suspicious or malicious activity.

A simple distinction:

```text
IOC = Evidence associated with compromise

IOA = Evidence associated with attack behavior
```

A strong SOC analyst should not rely on only one.

```text
IOC
 +
IOA
 +
Context
 +
Telemetry
 =
Better Detection & Investigation
```

---

# 1. What Is an IOC?

An **Indicator of Compromise (IOC)** is an observable artifact that may indicate that a system, account, network, or environment has been compromised.

Common IOCs include:

```text
IP Address
Domain
URL
File Hash
Filename
Malicious File
Email Address
Registry Key
File Path
Mutex
Certificate
User Account
```

Example:

```text
Endpoint
   ↓
Connects to suspicious IP
   ↓
IP appears in threat intelligence
   ↓
Potential IOC
```

Important:

> **An IOC is evidence, not automatically proof of compromise.**

---

# 2. What Is an IOA?

An **Indicator of Attack (IOA)** focuses on behavior associated with an attack.

Examples:

```text
Office → PowerShell
PowerShell → Download
Credential Dumping
New Service Creation
Scheduled Task Creation
Mass File Modification
Suspicious Remote Login
Privilege Escalation
Lateral Movement
```

IOAs attempt to answer:

> **"What is the attacker doing?"**

rather than:

> **"Which artifact did the attacker leave behind?"**

---

# 3. IOC vs IOA

| IOC          | IOA                      |
| ------------ | ------------------------ |
| Artifact     | Behavior                 |
| IP           | Suspicious process chain |
| Domain       | Credential dumping       |
| Hash         | Lateral movement         |
| URL          | Persistence              |
| File         | PowerShell abuse         |
| Registry key | Remote execution         |

Example:

```text
IOC:
203.0.113.10

IOA:
PowerShell connecting to external infrastructure
```

The combination is stronger.

---

# 4. Why IOCs Matter

IOCs help analysts:

```text
Detect
Investigate
Correlate
Scope
Hunt
Block
Contain
```

Example:

```text
Malicious Hash
      ↓
Search SIEM / EDR
      ↓
Find 3 endpoints
      ↓
Determine Scope
```

---

# 5. Why IOAs Matter

Attackers can easily change static indicators.

For example:

```text
Old IP
   ↓
New IP
```

or:

```text
Old Hash
   ↓
Modified Malware
   ↓
New Hash
```

But the attacker may still perform:

```text
PowerShell
Credential Dumping
Scheduled Task
C2
```

Therefore:

> **Behavior-based detection can be more resilient to changing IOCs.**

---

# 6. Common IOC Categories

## IP Addresses

Examples:

```text
IPv4
IPv6
```

Use cases:

```text
C2
Scanning
Malware Distribution
Brute Force
Data Exfiltration
```

---

# 7. Domains

Examples:

```text
malicious-example.com
suspicious-domain.example
```

Used for:

```text
C2
Phishing
Malware Hosting
Credential Theft
```

---

# 8. URLs

A URL provides more detail than a domain.

Example:

```text
https://example.com/login/update
```

Investigate:

```text
Domain
Path
Parameters
Redirects
Reputation
Certificate
```

---

# 9. File Hashes

Hashes uniquely represent file content.

Common examples:

```text
MD5
SHA-1
SHA-256
```

SHA-256 is commonly preferred for modern integrity and malware identification workflows.

Example:

```text
Malicious File
      ↓
SHA-256
      ↓
Search Threat Intelligence
```

---

# 10. File Names

Example:

```text
invoice.exe
update.ps1
document.js
```

Filename alone is weak evidence because attackers can rename files.

Better:

```text
Filename
+
Hash
+
Path
+
Process
+
Behavior
```

---

# 11. File Paths

Examples:

```text
%TEMP%
AppData
Startup
System directories
Unusual user directories
```

Suspicious combinations may include:

```text
Unusual Path
+
Executable
+
Network Connection
```

---

# 12. Registry Indicators

Windows attackers may modify registry locations for:

```text
Persistence
Configuration
Execution
Security Tool Tampering
```

Example:

```text
Registry Modification
       ↓
Persistence
       ↓
Potential IOA
```

---

# 13. Email Indicators

Useful indicators include:

```text
Sender
Sender Domain
Recipient
Reply-To
URL
Attachment Hash
Attachment Name
Email Headers
```

Example:

```text
Suspicious Sender
      +
Malicious URL
      +
Credential Harvesting
```

creates stronger evidence.

---

# 14. Network Indicators

Network-related indicators include:

```text
IP
Domain
Port
Protocol
URL
DNS Query
TLS Certificate
User-Agent
```

Example:

```text
Endpoint
 ↓
DNS Query
 ↓
Suspicious Domain
 ↓
Connection
 ↓
Potential C2
```

---

# 15. Account Indicators

Identity-related indicators can include:

```text
Username
Account
Source IP
Login Location
Device
Session
Authentication Method
```

Example:

```text
Privileged Account
+
Unusual Location
+
New Device
+
Successful Login
```

This is an important investigation signal.

---

# 16. IOC Reliability

Not all indicators are equally useful.

Consider:

```text
IOC
 ↓
Source
 ↓
Age
 ↓
Confidence
 ↓
Context
```

Questions:

```text
Is it from a trusted source?
Is it current?
Has it been independently confirmed?
Does it appear in our environment?
Is it relevant to the incident?
```

---

# 17. IOC Aging

Indicators can become outdated.

Example:

```text
Malicious IP
     ↓
Infrastructure Changes
     ↓
IP Reassigned
     ↓
Current Activity May Be Benign
```

Therefore:

> **Always consider indicator freshness.**

---

# 18. IOC Confidence

Use a confidence model such as:

```text
High
Medium
Low
Unknown
```

Example:

```text
High:
Multiple trusted sources confirm malicious activity

Medium:
One reliable source + internal suspicious activity

Low:
Unverified community report

Unknown:
No supporting context
```

---

# 19. IOC Enrichment

Enrichment adds context.

Example:

```text
IOC:
203.0.113.10

       ↓

Reputation
WHOIS
ASN
DNS
Threat Reports
Historical Observations
Malware Associations
```

Then:

```text
IOC
 ↓
Context
 ↓
Risk Assessment
```

---

# 20. Internal IOC Search

External intelligence is only part of the investigation.

Always ask:

> **Have we seen this IOC internally?**

Search:

```text
SIEM
EDR
Firewall
DNS
Proxy
Email
Cloud Logs
Authentication Logs
```

Example:

```text
Malicious Domain
      ↓
SIEM Search
      ↓
12 Hosts
      ↓
Potential Wider Incident
```

---

# 21. IOC Correlation

One IOC can become more meaningful when correlated.

Example:

```text
Suspicious IP
     +
Malware Hash
     +
Suspicious Process
     +
Abnormal Login
```

This creates stronger evidence.

---

# 22. IOC Lifecycle

A useful operational lifecycle:

```text
Discover
   ↓
Validate
   ↓
Enrich
   ↓
Classify
   ↓
Search
   ↓
Correlate
   ↓
Detect
   ↓
Block / Monitor
   ↓
Retire
```

---

# 23. IOC Blocking

Organizations may block:

```text
IP
Domain
URL
Hash
Email Sender
```

through:

```text
Firewall
DNS Security
Proxy
EDR
Email Security
WAF
```

But blocking should follow authorization and change-management procedures.

---

# 24. IOC Limitations

IOCs are useful but imperfect.

Attackers can:

```text
Change IP
Change Domain
Modify Malware
Change Hash
Use Legitimate Services
Compromise Infrastructure
```

Therefore:

```text
IOC-only Detection
        ↓
Can be bypassed
```

A stronger approach is:

```text
IOC
+
Behavior
+
Context
```

---

# 25. Common IOA Categories

IOAs commonly describe:

```text
Execution
Persistence
Privilege Escalation
Defense Evasion
Credential Access
Discovery
Lateral Movement
Collection
Command & Control
Exfiltration
```

These align naturally with MITRE ATT&CK concepts.

---

# 26. Process-Based IOAs

Examples:

```text
Office → PowerShell
Browser → Command Shell
Unknown Process → Credential Tool
System Process → Suspicious Child Process
```

Process ancestry is highly valuable.

Example:

```text
WINWORD.EXE
     ↓
powershell.exe
     ↓
cmd.exe
     ↓
network utility
```

This deserves investigation.

---

# 27. Command-Line IOAs

Command-line telemetry can reveal attacker behavior.

Examples:

```text
Encoded PowerShell
Suspicious Download Command
Credential Dumping Command
Remote Execution
Security Tool Modification
```

A command should always be evaluated in context.

---

# 28. Persistence IOAs

Examples:

```text
Scheduled Task
New Service
Startup Folder
Registry Run Key
Cron Job
New Account
```

Example:

```text
Unknown Process
     ↓
Creates Scheduled Task
     ↓
Executes at Login
```

Potential persistence behavior.

---

# 29. Credential Access IOAs

Examples:

```text
Credential Dumping
Password Database Access
LSASS Access
Browser Credential Access
Suspicious Authentication
```

A SOC analyst should understand that credential-access behavior can be highly sensitive and should be investigated according to organizational procedures.

---

# 30. Discovery IOAs

Attackers often perform discovery before moving further.

Examples:

```text
System Information
User Enumeration
Network Discovery
Process Discovery
Service Discovery
Domain Discovery
```

Example:

```text
Compromised Host
      ↓
System Discovery
      ↓
Network Discovery
      ↓
Lateral Movement
```

---

# 31. Lateral Movement IOAs

Examples:

```text
Remote Desktop
SMB
WinRM
SSH
Remote Services
Administrative Shares
Remote Execution
```

Example:

```text
Host A
  ↓
Remote Authentication
  ↓
Host B
```

Correlate with identity and network telemetry.

---

# 32. Command-and-Control IOAs

Potential behaviors:

```text
Periodic Connections
Unusual External Destination
Beacon-like Traffic
DNS Tunneling
Unusual Protocol
Suspicious User-Agent
```

Example:

```text
Endpoint
 ↓
Every 60 seconds
 ↓
External IP
 ↓
Small outbound packets
```

This may warrant investigation.

---

# 33. Exfiltration IOAs

Examples:

```text
Large Outbound Transfer
Unusual Cloud Upload
Archive Creation
Sensitive Data Access
Unusual External Destination
```

Example:

```text
Sensitive Files
      ↓
Archive Created
      ↓
External Upload
```

This is potentially high-risk behavior.

---

# 34. Defense Evasion IOAs

Examples:

```text
Log Clearing
Security Tool Modification
AV Disablement
Process Injection
File Deletion
Timestamp Manipulation
```

Example:

```text
Attacker
 ↓
Attempts to Disable Security Controls
 ↓
Potential Defense Evasion
```

---

# 35. IOA + IOC Combination

Consider:

```text
IOC:
Known malicious domain

IOA:
PowerShell communicating with the domain
```

This is stronger than:

```text
IOC only
```

Another:

```text
IOC:
Suspicious IP

IOA:
Credential dumping
+
Periodic outbound communication
```

Now the analyst has multiple signals.

---

# 36. IOC + IOA Investigation Model

Use:

```text
IOC
 ↓
Where did we see it?
 ↓
Which host?
 ↓
Which user?
 ↓
Which process?
 ↓
What happened before?
 ↓
What happened after?
 ↓
What behavior occurred?
 ↓
What other IOCs appeared?
```

This builds an attack narrative.

---

# 37. IOC and IOA in MITRE ATT&CK

Example:

```text
IOC:
Malicious PowerShell download URL

IOA:
PowerShell executing download

MITRE:
T1059.001
PowerShell
```

Another:

```text
IOC:
Remote C2 IP

IOA:
Periodic outbound communication

MITRE:
Command and Control technique
```

The exact ATT&CK mapping should be based on observed behavior.

---

# 38. Practical Investigation — Suspicious PowerShell

Alert:

```text
Suspicious PowerShell
```

Collect:

```text
Process
Parent Process
Command Line
User
Host
File
Hash
Network Connection
Destination
```

Then identify:

```text
IOC
+
IOA
+
MITRE ATT&CK
```

Example:

```text
WINWORD.EXE
      ↓
powershell.exe
      ↓
Download
      ↓
File Creation
      ↓
External Connection
```

---

# 39. Practical Investigation — Brute Force

Alert:

```text
Multiple Failed Logins
```

Collect:

```text
Source IP
Username
Target Host
Attempt Count
Time Window
Successful Login
Device
Location
```

Potential IOC:

```text
Source IP
```

Potential IOA:

```text
Repeated Authentication Attempts
```

Then investigate:

```text
Failed Logins
 ↓
Successful Login
 ↓
Post-Authentication Activity
```

---

# 40. Practical Investigation — Malware

Alert:

```text
Malware Detected
```

Collect:

```text
Hash
Filename
Path
Process
Parent Process
User
Host
Network Connections
Persistence
```

Then search:

```text
Hash
Domain
IP
Filename
```

across the environment.

---

# 41. IOC/IOA Investigation Workflow

```text
ALERT
  ↓
Extract Indicators
  ↓
Classify IOC / IOA
  ↓
Validate
  ↓
Enrich
  ↓
Search Internal Telemetry
  ↓
Correlate
  ↓
Build Timeline
  ↓
Map ATT&CK
  ↓
Determine Scope
  ↓
Assess Risk
  ↓
Escalate / Contain
  ↓
Document
```

---

# 42. Home Lab Exercise

Use:

```text
Kali
 +
Windows VM
 +
Sysmon
 +
Wazuh
```

Generate controlled suspicious activity.

Collect:

```text
Process
Command Line
Network
Authentication
File Activity
```

Then identify:

```text
IOC
IOA
MITRE ATT&CK
```

Create a report.

---

# 43. Portfolio Project

Create:

```text
IOC-IOA-Investigation/
│
├── README.md
│
├── IOC-Analysis/
│   ├── IP/
│   ├── Domain/
│   ├── URL/
│   ├── Hash/
│   └── File/
│
├── IOA-Analysis/
│   ├── Execution/
│   ├── Persistence/
│   ├── Credential-Access/
│   ├── Discovery/
│   ├── Lateral-Movement/
│   └── Command-and-Control/
│
├── Case-Studies/
├── Detection-Rules/
├── MITRE-Mapping/
├── Screenshots/
└── Reports/
```

Recommended minimum:

```text
10 IOC investigations
+
10 IOA investigations
+
5 combined IOC/IOA case studies
+
MITRE ATT&CK mapping
```

---

# 44. IOC Investigation Template

```text
# IOC Investigation

## IOC

## IOC Type

## Source

## First Observed

## Last Observed

## Reputation

## Confidence

## Threat Context

## Internal Occurrences

## Related Hosts

## Related Users

## Related Processes

## Related Network Activity

## Associated IOAs

## MITRE ATT&CK

## Risk Assessment

## Recommended Action

## Conclusion
```

---

# 45. IOA Investigation Template

```text
# IOA Investigation

## Observed Behavior

## Host

## User

## Timestamp

## Parent Process

## Child Process

## Command Line

## Network Activity

## Related IOCs

## Timeline

## MITRE ATT&CK

## Scope

## Risk

## Recommended Action

## Conclusion
```

---

# 46. Common SOC Mistakes

Avoid:

```text
IOC = automatically malicious
IOA = automatically malicious
Relying only on reputation
Ignoring timestamps
Ignoring internal context
Ignoring process ancestry
Ignoring user context
Ignoring asset criticality
Failing to search historical telemetry
Failing to correlate multiple indicators
```

The correct mindset is:

```text
Indicator
   ↓
Evidence
   ↓
Context
   ↓
Analysis
   ↓
Conclusion
```

---

# 47. Interview Questions

### Fundamentals

1. What is an IOC?
2. What is an IOA?
3. What is the difference between IOC and IOA?
4. Give examples of IOCs.
5. Give examples of IOAs.
6. Why are IOAs useful against changing IOCs?
7. What is IOC enrichment?

### Practical

8. How would you investigate a suspicious IP?
9. How would you investigate a malicious hash?
10. How would you investigate suspicious PowerShell?
11. How would you determine whether an IOC is relevant?
12. How do you search an IOC across an enterprise?
13. How can IOCs be used for threat hunting?

### Scenario

14. Your SIEM detects communication with a known malicious IP. What do you do?

Strong answer:

```text
Identify source host
      ↓
Identify user/process
      ↓
Validate destination
      ↓
Threat intelligence enrichment
      ↓
Search historical logs
      ↓
Check other hosts
      ↓
Review process behavior
      ↓
Identify related IOCs/IOAs
      ↓
Map ATT&CK
      ↓
Determine scope
      ↓
Assess severity
      ↓
Escalate / contain
      ↓
Document
```

---

# 48. Key Takeaway

Remember:

```text
IOC = WHAT artifact is associated with the attack?

IOA = WHAT behavior indicates the attack?
```

A strong investigation combines:

```text
IOC
+
IOA
+
Telemetry
+
Threat Intelligence
+
User Context
+
Asset Context
+
MITRE ATT&CK
```

Your SOC workflow should eventually look like:

```text
Alert
 ↓
IOC / IOA
 ↓
Enrichment
 ↓
Internal Search
 ↓
Correlation
 ↓
Timeline
 ↓
MITRE ATT&CK
 ↓
Scope
 ↓
Risk
 ↓
Response
 ↓
Documentation
```

This is the practical foundation for moving from **SOC L1 alert triage** toward **SOC L2 investigation and threat hunting**.
