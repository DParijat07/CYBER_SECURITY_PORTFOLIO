# Threat Hunting

> **SOC L2 Foundation**

Threat Hunting is the proactive process of searching an environment for signs of malicious activity that may have bypassed existing security controls and detections.

Traditional SOC monitoring is primarily:

```text
Alert
  ↓
Investigation
  ↓
Response
```

Threat hunting reverses the starting point:

```text
Hypothesis
   ↓
Search
   ↓
Evidence
   ↓
Analysis
   ↓
Detection / Response
```

The fundamental question is:

> **"What malicious activity might already be present that our existing detections have not identified?"**

---

# 1. Threat Hunting vs Alert Investigation

These are related but different activities.

### Alert Investigation

```text
Detection
   ↓
Alert
   ↓
Analyst investigates
```

The SOC already has a reason to investigate.

### Threat Hunting

```text
Hypothesis
   ↓
Proactive Search
   ↓
Potential Threat
```

The analyst initiates the investigation.

---

# 2. Why Threat Hunting Matters

Attackers can bypass:

```text
Signature Detection
IOC-Based Detection
Known Malware Detection
Static Rules
```

Threat hunting attempts to discover:

```text
Unknown Activity
Suspicious Behavior
Hidden Persistence
Undetected Compromise
Living-off-the-Land Activity
Abnormal User Behavior
```

A mature SOC therefore combines:

```text
Monitoring
+
Detection
+
Threat Hunting
```

---

# 3. Threat Hunting Cycle

A practical hunting cycle:

```text
1. Hypothesis
      ↓
2. Data Collection
      ↓
3. Investigation
      ↓
4. Analysis
      ↓
5. Findings
      ↓
6. Detection Engineering
      ↓
7. Lessons Learned
```

Then:

```text
New Hypothesis
      ↓
New Hunt
```

Threat hunting is continuous.

---

# 4. Step 1 — Create a Hypothesis

A hunting hypothesis should be specific and testable.

Weak:

```text
"Let's look for hackers."
```

Better:

```text
"An attacker may be using PowerShell to download
payloads on Windows endpoints."
```

Even better:

```text
"An attacker may be using PowerShell spawned by
Office applications to download external content."
```

This gives you something measurable to search for.

---

# 5. Sources of Hunting Hypotheses

Hypotheses can come from:

```text
Threat Intelligence
Recent Incidents
MITRE ATT&CK
Vulnerability Intelligence
Security Research
New Malware
Industry Attacks
Internal Alerts
Previous Incidents
Anomalies
```

Example:

```text
Threat Report
     ↓
Attacker Uses PowerShell
     ↓
Hunt Environment
     ↓
Identify Similar Activity
```

---

# 6. Threat Hunting Based on MITRE ATT&CK

MITRE ATT&CK provides a useful framework for hunting.

Example:

```text
T1059.001
PowerShell
```

Hunt for:

```text
PowerShell Processes
Command Lines
Parent Processes
Network Connections
Encoded Commands
File Creation
```

Another example:

```text
Credential Access
```

Hunt for:

```text
Suspicious Credential Access
LSASS Access
Credential Dumping Indicators
```

Always base mappings on actual observed behavior.

---

# 7. Threat Hunting Data Sources

Good hunting requires good telemetry.

Common sources:

```text
SIEM
EDR
Sysmon
Windows Event Logs
Linux Logs
Firewall
DNS
Proxy
Authentication
Cloud Logs
Email Security
Network Traffic
Application Logs
```

For your home lab:

```text
Windows VM
   ↓
Sysmon
   ↓
Wazuh
   ↓
SIEM Analysis
   ↓
Threat Hunt
```

---

# 8. Telemetry Is the Foundation

You cannot hunt effectively for data you do not collect.

Example:

```text
Hunt:
Suspicious PowerShell

Required telemetry:
Process Creation
Command Line
Parent Process
User
Host
Network Connection
```

If command-line logging is missing:

```text
Hunt Quality
     ↓
Reduced
```

Therefore:

> **Threat hunting quality depends heavily on telemetry quality.**

---

# 9. Threat Hunting Methodology

A useful workflow:

```text
HYPOTHESIS
    ↓
IDENTIFY DATA
    ↓
QUERY
    ↓
FILTER
    ↓
CORRELATE
    ↓
INVESTIGATE
    ↓
VALIDATE
    ↓
DOCUMENT
```

---

# 10. Hunting for Suspicious PowerShell

Hypothesis:

```text
"An attacker may be abusing PowerShell for execution."
```

Search for:

```text
powershell.exe
pwsh.exe
EncodedCommand
Download
Invoke
WebClient
IEX
```

Then investigate:

```text
Parent Process
User
Command Line
Host
Network Destination
File Creation
```

---

# 11. Process Ancestry

Process relationships are extremely useful.

Example:

```text
explorer.exe
     ↓
WINWORD.EXE
     ↓
powershell.exe
     ↓
cmd.exe
     ↓
network utility
```

This is more informative than simply:

```text
powershell.exe exists
```

The question is:

> **"Why did this process start, and what did it do?"**

---

# 12. Living-off-the-Land

Attackers may use legitimate operating-system utilities instead of custom malware.

Examples include:

```text
PowerShell
cmd
WMI
Windows Script Host
Scheduled Tasks
Remote Services
Native Network Utilities
```

This can make detection harder.

Therefore, hunting should focus on:

```text
Tool
+
Context
+
Behavior
```

rather than simply:

```text
Tool = Malicious
```

---

# 13. Hunt for Persistence

Hypothesis:

```text
"An attacker may have established persistence on a Windows endpoint."
```

Search for:

```text
Scheduled Tasks
Services
Startup Items
Registry Run Keys
New Accounts
Unusual Applications
```

Then investigate:

```text
Creation Time
Creator
Command
Executable
User
Parent Process
Network Activity
```

---

# 14. Hunt for Suspicious Scheduled Tasks

Example:

```text
Scheduled Task Created
        ↓
Unknown Executable
        ↓
User-Writable Directory
        ↓
Runs Automatically
```

This combination deserves investigation.

However:

> **Scheduled tasks are legitimate administrative mechanisms too.**

Always investigate context.

---

# 15. Hunt for Suspicious Services

Search for:

```text
New Service
Unusual Service Name
Unknown Binary
Unexpected Service Account
Service Created During Incident
```

Example:

```text
New Service
   +
Unknown Binary
   +
External Connection
```

This creates a stronger hunting lead.

---

# 16. Hunt for Credential Access

Hypothesis:

```text
"An attacker may be attempting to obtain credentials
from Windows systems."
```

Search for relevant telemetry around:

```text
Credential Access
Authentication Anomalies
Sensitive Process Access
Suspicious Tools
Unexpected Privileged Activity
```

Then correlate:

```text
Host
User
Process
Command Line
Network Activity
```

---

# 17. Hunt for Lateral Movement

Hypothesis:

```text
"An attacker may have moved from one compromised
endpoint to another."
```

Search:

```text
Remote Logins
SMB
RDP
WinRM
SSH
Administrative Shares
Remote Services
```

Example:

```text
Host A
   ↓
Successful Remote Authentication
   ↓
Host B
   ↓
Process Execution
```

Then determine whether this was:

```text
Legitimate Administration
or
Potential Lateral Movement
```

---

# 18. Hunt for Account Anomalies

Search for:

```text
Impossible Travel
Unusual Login Time
New Device
New Location
Privileged Account Usage
Multiple Failed Logins
Unexpected Successful Login
```

Example:

```text
100 Failed Logins
      ↓
Successful Login
      ↓
New Device
      ↓
Privileged Account
```

This deserves investigation.

---

# 19. Hunt for Command-and-Control

Hypothesis:

```text
"An endpoint may be communicating with attacker-controlled
infrastructure."
```

Search for:

```text
Periodic Connections
Rare Domains
Suspicious IPs
Unusual DNS
Unexpected External Connections
Long-Lived Connections
Unusual User-Agent
```

Then correlate:

```text
Process
+
Destination
+
Frequency
+
User
+
Host
```

---

# 20. Beaconing

Some malware communicates periodically.

Example:

```text
10:00 → C2
10:01 → C2
10:02 → C2
10:03 → C2
```

Potential indicators:

```text
Regular Intervals
Similar Packet Sizes
Same Destination
Long-Term Communication
```

But legitimate applications can also communicate periodically.

Therefore:

> **Beacon-like behavior is a hunting signal, not automatic proof of C2.**

---

# 21. Hunt for DNS Anomalies

DNS can provide useful hunting signals.

Search for:

```text
Rare Domains
High Query Frequency
Long Domain Names
Unusual Subdomains
Newly Observed Domains
Suspicious TLDs
Potentially Encoded Queries
```

Example:

```text
Host
 ↓
Unusual DNS Queries
 ↓
Rare Domain
 ↓
External Connection
```

Investigate further.

---

# 22. Hunt for Data Exfiltration

Hypothesis:

```text
"An attacker may be attempting to move sensitive
information outside the organization."
```

Search for:

```text
Large Outbound Transfers
Unusual Uploads
Archive Creation
Cloud Uploads
Rare Destinations
Unusual Protocols
Sensitive File Access
```

Correlation:

```text
Sensitive File Access
       ↓
Archive Creation
       ↓
External Upload
```

This creates a strong investigation path.

---

# 23. Hunt for Ransomware Behavior

Search for behavior such as:

```text
Mass File Modification
Large Numbers of Renames
Suspicious Encryption Activity
Shadow Copy Manipulation
Backup Tampering
Security Tool Disablement
```

The goal is to detect behavior early rather than wait for a ransom note.

---

# 24. Hunt for Defense Evasion

Possible signals:

```text
Log Clearing
Security Tool Tampering
AV Disablement
Suspicious Process Injection
File Deletion
Configuration Changes
```

Example:

```text
Attacker
 ↓
Attempts Security Tool Modification
 ↓
Unusual Process
 ↓
External Connection
```

Investigate the complete chain.

---

# 25. IOC-Based Hunting

Suppose threat intelligence provides:

```text
Malicious Domain
```

Search:

```text
SIEM
DNS
Proxy
Firewall
EDR
```

Then:

```text
IOC
 ↓
Internal Occurrences
 ↓
Hosts
 ↓
Users
 ↓
Processes
 ↓
Timeline
```

This is one of the simplest forms of threat hunting.

---

# 26. TTP-Based Hunting

IOC-based hunting asks:

```text
"Have we seen this IP?"
```

TTP-based hunting asks:

```text
"Have attackers performed this behavior?"
```

Example:

```text
IOC Hunt:
Search malicious IP

TTP Hunt:
Search suspicious PowerShell
execution patterns
```

TTP hunting can remain useful even when infrastructure changes.

---

# 27. Anomaly-Based Hunting

Search for unusual activity.

Examples:

```text
Rare Process
Rare Destination
Rare User Behavior
Unusual Login
Unusual Data Transfer
Unusual Parent-Child Relationship
```

Example:

```text
User normally:
Office work

Today:
PowerShell
+
Archive Creation
+
External Upload
```

This deserves investigation.

---

# 28. Baseline Before Hunting

You need to understand normal behavior.

Example:

```text
Normal:
Backup Server → Cloud Storage

Abnormal:
Workstation → Unknown Cloud Storage
```

Without baseline knowledge, many legitimate activities may appear suspicious.

Therefore:

```text
Normal Behavior
      ↓
Baseline
      ↓
Detect Deviations
```

---

# 29. Threat Hunting Query

A hunting query should answer a specific question.

Example:

```text
Question:
Which endpoints executed PowerShell from Office applications
during the last 7 days?
```

Conceptually:

```text
Process = powershell.exe
AND
Parent = WINWORD.EXE / EXCEL.EXE / OUTLOOK.EXE
```

Then investigate the results.

---

# 30. Hunt Result Classification

Results can be classified as:

```text
Benign
Suspicious
Malicious
Inconclusive
```

Example:

```text
PowerShell
 ↓
IT Administration Script
 ↓
Known Administrator
 ↓
Approved Change
```

Likely benign.

Whereas:

```text
PowerShell
 ↓
Unknown User
 ↓
Encoded Command
 ↓
External Download
```

requires investigation.

---

# 31. Threat Hunting Decision Tree

```text
HUNT RESULT
     ↓
Expected?
 ┌───┴───┐
YES     NO
 ↓       ↓
Close   Investigate
         ↓
      Malicious?
      ┌───┴───┐
     YES      NO
      ↓        ↓
 Incident   Document
      ↓
 Response
```

---

# 32. Threat Hunting Documentation

Every hunt should document:

```text
Hunt ID
Date
Analyst
Hypothesis
Threat Context
Data Sources
Query
Time Range
Results
False Positives
Findings
IOCs
IOAs
MITRE ATT&CK
Detection Gap
Recommendations
```

---

# 33. Threat Hunting Report Template

```text
# Threat Hunt Report

## Hunt ID

## Date

## Analyst

## Hypothesis

## Threat Context

## Objective

## Data Sources

## Time Range

## Hunting Query

## Results

## Findings

## IOCs

## IOAs

## MITRE ATT&CK Mapping

## False Positives

## Detection Gaps

## Recommended Detection

## Risk Assessment

## Conclusion
```

---

# 34. Detection Engineering After Hunting

One of the most valuable outputs of threat hunting is a new detection.

Example:

```text
Hunt
 ↓
Suspicious PowerShell Pattern
 ↓
Confirmed Malicious
 ↓
Detection Rule
 ↓
SIEM Alert
```

This changes the environment from:

```text
Unknown Activity
```

to:

```text
Automatically Detected Activity
```

---

# 35. Threat Hunting Feedback Loop

```text
Threat Intelligence
       ↓
Hypothesis
       ↓
Threat Hunt
       ↓
Finding
       ↓
Detection Rule
       ↓
SOC Alert
       ↓
Incident
       ↓
Lessons Learned
       ↓
New Intelligence
```

This is a mature SOC capability.

---

# 36. Threat Hunting in Your Wazuh Lab

Your home lab can simulate this.

Architecture:

```text
Windows 11 VM
     ↓
Sysmon
     ↓
Wazuh Agent
     ↓
Wazuh Manager
     ↓
SIEM
     ↓
Threat Hunting
```

Create hunts for:

```text
PowerShell
Persistence
Brute Force
Lateral Movement
Suspicious DNS
Malware
Account Anomalies
C2
```

---

# 37. Home Lab Hunt Example

### Hypothesis

```text
"An attacker may use PowerShell to download and execute
a payload."
```

### Data

Collect:

```text
Process Creation
Command Line
Network Connections
File Creation
User
Timestamp
```

### Hunt

Search for:

```text
PowerShell
+
External Network Connection
+
File Creation
```

### Investigation

```text
PowerShell
 ↓
Download
 ↓
File Creation
 ↓
Execution
 ↓
Network Connection
```

Then map the observed behavior to ATT&CK as appropriate.

---

# 38. Portfolio Threat Hunting Directory

Add:

```text
Threat-Hunting/
│
├── README.md
│
├── Hypotheses/
│   ├── PowerShell/
│   ├── Persistence/
│   ├── Credential-Access/
│   ├── Lateral-Movement/
│   ├── C2/
│   └── Exfiltration/
│
├── Queries/
│
├── Case-Studies/
│
├── MITRE-Mapping/
│
├── Detection-Rules/
│
├── Screenshots/
│
└── Reports/
```

---

# 39. Recommended Portfolio Hunts

Start with:

```text
1. Suspicious PowerShell
2. Office → PowerShell
3. Scheduled Task Persistence
4. New Service Creation
5. Brute Force → Successful Login
6. Suspicious RDP
7. Lateral Movement
8. Rare DNS Domain
9. C2 Beaconing
10. Large Outbound Transfer
```

For each:

```text
Hypothesis
+
Query
+
Evidence
+
Analysis
+
ATT&CK
+
Detection
+
Report
```

---

# 40. Threat Hunting Metrics

You can measure hunting effectiveness.

Useful metrics:

```text
Hunts Completed
True Positives
False Positives
New IOCs
New Detections
Detection Gaps
Incidents Discovered
Mean Investigation Time
Coverage Improvement
```

Example:

```text
10 Hunts
 ↓
3 Suspicious Findings
 ↓
1 Confirmed Incident
 ↓
4 Detection Rules
```

This is excellent portfolio evidence.

---

# 41. Threat Hunting vs Threat Intelligence

Threat Intelligence:

```text
"What threats are relevant?"
```

Threat Hunting:

```text
"Can we find evidence of those threats here?"
```

Together:

```text
Threat Intelligence
       ↓
Hunting Hypothesis
       ↓
Internal Search
       ↓
Finding
```

---

# 42. Threat Hunting vs Incident Response

Threat Hunting:

```text
Proactive
```

Incident Response:

```text
Reactive
```

But they complement each other:

```text
Threat Hunt
     ↓
Find Hidden Threat
     ↓
Incident Declared
     ↓
Incident Response
```

---

# 43. Threat Hunting vs Vulnerability Management

Vulnerability management:

```text
Find weaknesses
```

Threat hunting:

```text
Find evidence of exploitation or malicious activity
```

Example:

```text
Critical Vulnerability
       ↓
Threat Intelligence:
Actively Exploited
       ↓
Threat Hunt
       ↓
Search Logs
       ↓
Potential Exploitation
```

These functions should work together.

---

# 44. Common Threat Hunting Mistakes

Avoid:

```text
Hunting without a hypothesis
Searching everything without purpose
Ignoring normal baselines
Relying only on IOCs
Ignoring behavioral indicators
Using poor telemetry
Not documenting queries
Not validating findings
Ignoring false positives
Failing to create detections from findings
```

A hunt should produce a useful conclusion.

---

# 45. Interview Questions

### Fundamentals

1. What is threat hunting?
2. How is threat hunting different from alert investigation?
3. What is a hunting hypothesis?
4. What data sources are required?
5. What is IOC-based hunting?
6. What is TTP-based hunting?
7. What is anomaly-based hunting?

### Practical

8. How would you hunt for PowerShell abuse?
9. How would you hunt for lateral movement?
10. How would you hunt for C2?
11. How would you hunt for persistence?
12. How would you turn a hunting result into a detection rule?

### Scenario

13. You suspect an attacker is using PowerShell in your environment. How would you hunt?

Strong answer:

```text
Create hypothesis
      ↓
Identify required telemetry
      ↓
Search PowerShell execution
      ↓
Analyze parent-child relationships
      ↓
Review command lines
      ↓
Check network connections
      ↓
Identify users/hosts
      ↓
Correlate with IOCs
      ↓
Map ATT&CK
      ↓
Validate findings
      ↓
Create detection if required
      ↓
Document results
```

---

# 46. Key Takeaway

Threat hunting changes your mindset from:

```text
"Which alert should I investigate?"
```

to:

```text
"What could be happening that our current
detections haven't found?"
```

The complete SOC hunting workflow:

```text
Threat Intelligence
       ↓
Hypothesis
       ↓
Telemetry
       ↓
Query
       ↓
Investigation
       ↓
IOC / IOA
       ↓
Correlation
       ↓
MITRE ATT&CK
       ↓
Finding
       ↓
Detection Engineering
       ↓
Incident Response
       ↓
Documentation
```

For your portfolio, the strongest evidence will not be a document saying **"I know threat hunting."**

It will be:

```text
10 Hunting Hypotheses
+
Real Wazuh/Sysmon Telemetry
+
Queries
+
Screenshots
+
Investigation Reports
+
MITRE ATT&CK Mapping
+
Detection Rules
```

That demonstrates progression from **SOC L1 monitoring → L2 investigation → proactive security operations**.
