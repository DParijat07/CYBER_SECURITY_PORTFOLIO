# Security Monitoring

> **SOC L1 Fundamental**

Security monitoring is the continuous collection, analysis, and correlation of security-relevant data to identify suspicious activity, threats, vulnerabilities, and potential security incidents.

A SOC depends on effective monitoring to answer:

* What is happening?
* Where is it happening?
* Who is involved?
* Is the activity normal?
* Is it suspicious?
* What happened before and after?
* Does it indicate an attack?
* What action should be taken?

---

# 1. Security Monitoring — Big Picture

```text
Security Telemetry
        ↓
Data Collection
        ↓
Log Aggregation
        ↓
Normalization
        ↓
Detection
        ↓
Correlation
        ↓
Alert
        ↓
Investigation
        ↓
Response
```

A simple way to remember:

> **Collect → Detect → Investigate → Respond**

---

# 2. Why Security Monitoring Matters

Modern organizations generate enormous amounts of activity.

Examples:

```text
User Logins
Network Connections
DNS Requests
Process Execution
File Changes
Cloud Activity
Firewall Traffic
Email Activity
Authentication Events
Endpoint Activity
```

Security monitoring converts this raw activity into actionable security information.

Without monitoring:

```text
Attack
  ↓
No visibility
  ↓
Delayed detection
  ↓
Greater impact
```

With effective monitoring:

```text
Attack
  ↓
Telemetry
  ↓
Detection
  ↓
Alert
  ↓
Investigation
  ↓
Response
```

---

# 3. Security Monitoring vs General Monitoring

Not every monitoring activity is security monitoring.

### General IT Monitoring

Focuses on:

```text
CPU
Memory
Disk
Availability
Application Performance
Network Performance
```

### Security Monitoring

Focuses on:

```text
Authentication
Privilege Changes
Malware
Suspicious Processes
Network Threats
Account Abuse
Data Access
Lateral Movement
Command & Control
```

There can be overlap.

For example:

```text
CPU suddenly reaches 100%
```

is an IT monitoring event.

But:

```text
CPU suddenly reaches 100%
+
Unknown process
+
Outbound connection
```

may become security-relevant.

---

# 4. Security Monitoring Objectives

A SOC generally monitors to achieve:

### Detection

Identify potential threats.

### Investigation

Understand what happened.

### Response

Contain and remediate threats.

### Visibility

Understand activity across the environment.

### Compliance

Maintain evidence required by policies and regulations.

### Threat Hunting

Search proactively for suspicious behavior.

---

# 5. What Should a SOC Monitor?

A mature SOC monitors multiple layers.

```text
                    SECURITY MONITORING
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
    Network             Endpoint            Identity
       ↓                   ↓                   ↓
     DNS                Processes            Login
   Firewall             Files               MFA
     Proxy              Registry            Accounts
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ↓
                         Cloud
                           ↓
                    Applications
                           ↓
                        Email
```

---

# 6. Network Monitoring

Network monitoring provides visibility into communications.

Important telemetry includes:

```text
Source IP
Destination IP
Source Port
Destination Port
Protocol
Bytes
Packets
Timestamp
Domain
URL
Connection State
```

Security analysts may investigate:

```text
Port Scanning
C2
Data Exfiltration
Malicious DNS
Lateral Movement
Unusual Outbound Connections
```

---

# 7. Endpoint Monitoring

Endpoint monitoring focuses on individual systems.

Examples:

```text
Process Creation
File Creation
File Modification
Registry Changes
Services
Scheduled Tasks
User Activity
PowerShell
Command Shell
USB Activity
Security Tool Events
```

Important endpoint sources include:

```text
Windows Event Logs
Sysmon
EDR
Antivirus
Linux Logs
macOS Logs
```

---

# 8. Identity Monitoring

Identity is one of the most important monitoring areas.

Monitor:

```text
Successful Logins
Failed Logins
MFA Events
Password Changes
Account Creation
Account Deletion
Privilege Changes
Group Membership
Service Accounts
Administrative Activity
```

Example:

```text
User:
admin

Login:
Successful

Source:
Unknown Location

Device:
Unknown

Time:
03:12 AM
```

This should be investigated in context.

---

# 9. Cloud Monitoring

Cloud environments introduce additional telemetry.

Examples:

```text
Cloud Authentication
API Calls
IAM Changes
Security Group Changes
Storage Access
Key Creation
Resource Creation
Configuration Changes
```

A suspicious example:

```text
User
 ↓
Creates Access Key
 ↓
Creates Privileged IAM Role
 ↓
Accesses Sensitive Storage
```

This could indicate account compromise or privilege abuse.

---

# 10. Application Monitoring

Applications can generate valuable security telemetry.

Examples:

```text
Authentication
Authorization
API Requests
Errors
Administrative Actions
Data Access
Configuration Changes
```

Useful for detecting:

```text
Account Abuse
API Abuse
Injection
Unauthorized Access
Privilege Escalation
Data Access
```

---

# 11. Email Monitoring

Email is a major attack vector.

SOC teams may monitor:

```text
Sender
Recipient
Domain
URLs
Attachments
Email Headers
Authentication Results
SPF
DKIM
DMARC
```

Potential threats:

```text
Phishing
Malware
Business Email Compromise
Credential Theft
Malicious Attachments
```

---

# 12. Security Telemetry Sources

Common sources include:

```text
Windows Event Logs
Sysmon
Linux Logs
Firewall
IDS/IPS
DNS
Proxy
VPN
EDR
Antivirus
Email Security
Cloud Logs
Authentication Systems
Applications
Databases
```

These sources feed the SOC's visibility layer.

---

# 13. SIEM

A **Security Information and Event Management (SIEM)** platform centralizes security telemetry and provides capabilities such as:

```text
Log Collection
Normalization
Search
Correlation
Detection
Alerting
Dashboards
Investigation
Reporting
```

Examples include:

```text
Wazuh
Splunk
Microsoft Sentinel
Elastic Security
IBM QRadar
```

Your home lab can use:

```text
Windows
+
Sysmon
+
Wazuh
```

to demonstrate these concepts.

---

# 14. Security Monitoring Pipeline

A typical architecture:

```text
              DATA SOURCES
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
    Endpoint     Network     Identity
       │           │           │
       └───────────┼───────────┘
                   ↓
             SIEM / Platform
                   ↓
             Normalization
                   ↓
              Correlation
                   ↓
              Detection
                   ↓
                Alert
                   ↓
             SOC Analyst
                   ↓
              Investigation
                   ↓
              Response
```

---

# 15. Detection Rules

A detection rule identifies activity matching a defined condition.

Example:

```text
IF
failed_login_count > threshold
AND
time_window < threshold
THEN
generate alert
```

Another:

```text
IF
PowerShell
+
encoded command
+
suspicious parent process
THEN
generate high severity alert
```

Good detection rules should balance:

```text
Detection Capability
+
Accuracy
+
Context
+
Low False Positives
```

---

# 16. Correlation

Individual events may not be suspicious.

Correlation combines related events.

Example:

```text
Failed Login
      +
Successful Login
      +
New Device
      +
Privilege Change
      +
Sensitive File Access
```

This produces a stronger security signal.

---

# 17. Security Monitoring and Baselines

A SOC needs to understand normal activity.

This is called a **baseline**.

Example:

Normal:

```text
Employee logs in
09:00
from corporate network
using known device
```

Potential anomaly:

```text
Same employee
03:30 AM
unknown country
unknown device
```

The second event becomes more interesting because it deviates from the baseline.

---

# 18. Anomaly Detection

Anomaly detection identifies activity that differs from expected behavior.

Examples:

```text
Unusual Login Time
Unusual Location
Unusual Data Transfer
Unusual Process
Unusual DNS Query
Unusual Administrative Activity
```

However:

> **Anomaly does not automatically mean malicious.**

It means:

> **"This behavior is unusual and may require investigation."**

---

# 19. Security Monitoring Metrics

SOC teams can measure monitoring effectiveness using metrics such as:

### MTTD

**Mean Time to Detect**

How quickly threats are detected.

### MTTA

**Mean Time to Acknowledge**

How quickly analysts acknowledge an alert.

### MTTR

**Mean Time to Respond/Recover**

How quickly the organization responds to or recovers from an incident, depending on the organization's definition.

### False Positive Rate

How many alerts are incorrectly classified as threats.

### Detection Coverage

How much relevant threat activity can be detected.

---

# 20. MTTD Example

Suppose:

```text
Attack starts:
10:00

Detection:
10:08
```

Then:

```text
Detection Time = 8 minutes
```

Lower detection time generally means faster visibility.

---

# 21. MTTR Example

```text
Incident detected:
10:08

Containment completed:
10:38
```

Response time:

```text
30 minutes
```

Organizations may define MTTR differently, so always understand the metric definition being used.

---

# 22. Alert Fatigue

A major SOC problem is **alert fatigue**.

Suppose analysts receive:

```text
20,000 alerts/day
```

but:

```text
19,000
```

are low-value or false positives.

Analysts may become overwhelmed.

This can lead to:

```text
Missed Alerts
Delayed Investigation
Analyst Burnout
Poor Prioritization
```

Therefore:

> **More alerts do not necessarily mean better security.**

---

# 23. Improving Detection Quality

SOC teams can improve monitoring by:

```text
Tune Rules
Reduce False Positives
Add Context
Correlate Events
Prioritize Critical Assets
Use Threat Intelligence
Improve Telemetry
Create Baselines
Automate Repetitive Tasks
```

---

# 24. Security Monitoring and Asset Criticality

Not all systems have equal importance.

Example:

```text
Employee Laptop
     vs
Domain Controller
     vs
Production Database
```

A similar alert on each system may have very different risk.

Therefore detection should consider:

```text
Asset Criticality
+
User Privilege
+
Threat Context
+
Business Impact
```

---

# 25. Security Monitoring and User Context

Suppose:

```text
User:
Administrator
```

performs:

```text
PowerShell
```

This may deserve more attention than:

```text
Standard User
```

performing the same activity.

But:

> Administrative activity is not automatically malicious.

Always investigate context.

---

# 26. Security Monitoring and Threat Intelligence

Threat intelligence can enrich monitoring.

Example:

```text
Outbound Connection
       ↓
IP Reputation
       ↓
Known C2 Infrastructure
       ↓
Alert Priority Increases
```

Threat intelligence may provide:

```text
IP Reputation
Domain Reputation
Malware Hashes
Threat Actor Information
Campaign Information
TTPs
```

---

# 27. Security Monitoring and MITRE ATT&CK

Monitoring should ultimately support detection of adversary behavior.

Example:

```text
Telemetry
   ↓
PowerShell Activity
   ↓
Detection
   ↓
Alert
   ↓
MITRE ATT&CK
T1059.001
   ↓
Investigation
```

This connects your previous learning:

```text
Telemetry
   ↓
Event
   ↓
Alert
   ↓
IOC / IOA
   ↓
TTP
   ↓
MITRE ATT&CK
```

---

# 28. Security Monitoring and Cyber Kill Chain

Monitoring can also identify attack stages.

Example:

```text
Phishing
   ↓
Delivery

PowerShell
   ↓
Execution

Scheduled Task
   ↓
Persistence

C2 Connection
   ↓
Command & Control

Large Data Transfer
   ↓
Exfiltration
```

This allows the SOC to build an attack narrative.

---

# 29. L1 Monitoring Responsibilities

A SOC L1 analyst commonly focuses on:

```text
Monitor Alerts
Review Dashboards
Perform Initial Triage
Validate Alerts
Collect Evidence
Check Context
Search Related Events
Classify Alerts
Document Findings
Escalate Suspicious Activity
```

L1 is usually not expected to perform every advanced investigation.

Complex incidents may be escalated to:

```text
L2
L3
Threat Hunting
Incident Response
DFIR
Detection Engineering
```

---

# 30. Practical Alert Monitoring Workflow

```text
New Alert
   ↓
Read Alert Details
   ↓
Identify Asset
   ↓
Identify User
   ↓
Identify Source/Destination
   ↓
Review Trigger
   ↓
Check Related Events
   ↓
Enrich Indicators
   ↓
Assess Severity
   ↓
Classify
   ↓
Document
   ↓
Close / Escalate
```

---

# 31. Home Lab Implementation

Build a basic monitoring architecture:

```text
                 KALI
                  │
             Test Activity
                  │
                  ↓
             WINDOWS VM
                  │
                Sysmon
                  │
                  ↓
                Wazuh
                  │
                  ↓
             SOC Dashboard
                  │
                  ↓
             Alert Triage
```

Monitor:

```text
Process Creation
PowerShell
Authentication
File Creation
Network Connections
Scheduled Tasks
Registry Changes
```

---

# 32. Practical Exercise 1 — Login Monitoring

Generate:

```text
Multiple Failed Logins
```

Observe:

```text
Windows Event Logs
Wazuh
```

Document:

```text
Source
Target Account
Timestamp
Number of Attempts
Successful Login
Source IP
```

Then classify:

```text
Benign
Suspicious
True Positive
False Positive
```

based on your investigation.

---

# 33. Practical Exercise 2 — Process Monitoring

Generate controlled PowerShell activity.

Investigate:

```text
Process
Parent Process
User
Command Line
Timestamp
Child Process
Network Connection
```

Map the activity to:

```text
IOC
IOA
MITRE ATT&CK
```

---

# 34. Practical Exercise 3 — Network Monitoring

Generate controlled outbound connections.

Investigate:

```text
Source Host
Destination
Port
Protocol
Domain
Frequency
Process
```

Determine:

```text
Normal
Suspicious
Malicious
```

based on available evidence.

---

# 35. Practical Exercise 4 — Correlation

Create a controlled attack chain:

```text
Failed Login
      ↓
Successful Login
      ↓
PowerShell
      ↓
File Creation
      ↓
Network Connection
```

Your objective is to correlate the individual events.

Create:

```text
Timeline
IOC List
IOA Analysis
MITRE Mapping
Detection
Investigation
Conclusion
```

---

# 36. Portfolio Evidence

Create a practical project:

```text
Security-Monitoring-Lab/
│
├── README.md
├── Architecture.md
├── Data-Sources.md
├── Detection-Rules/
├── Alert-Investigations/
├── Correlation-Scenarios/
├── MITRE-Mapping/
├── Dashboards/
├── Screenshots/
└── Reports/
```

This becomes evidence that you understand:

```text
Telemetry
+
Monitoring
+
Detection
+
Triage
+
Investigation
```

rather than merely knowing SIEM terminology.

---

# 37. Interview Questions

### Fundamentals

1. What is security monitoring?
2. Why is security monitoring important?
3. What is security telemetry?
4. What data sources does a SOC monitor?
5. What is a SIEM?
6. What is EDR?
7. What is a baseline?

### SOC L1

8. What would you monitor in a SOC?
9. How do you investigate an alert?
10. How do you reduce false positives?
11. What causes alert fatigue?
12. How do you prioritize monitoring?
13. What is event correlation?

### Practical

14. How would you monitor suspicious PowerShell?
15. How would you monitor brute-force activity?
16. How would you detect C2?
17. How would you investigate unusual login activity?
18. How would you correlate multiple alerts?
19. What logs would you check after a suspicious login?

---

# 38. Key Takeaway

Security monitoring is the foundation connecting your SOC concepts:

```text
ASSETS
  ↓
TELEMETRY
  ↓
LOGS
  ↓
EVENTS
  ↓
DETECTION
  ↓
ALERTS
  ↓
TRIAGE
  ↓
INVESTIGATION
  ↓
INCIDENT
  ↓
RESPONSE
```

A strong SOC analyst understands that:

> **You cannot detect what you cannot observe.**

Therefore:

```text
Good Telemetry
      +
Good Detection
      +
Good Context
      +
Good Investigation
      =
Effective Security Monitoring
```

For your portfolio, the goal should ultimately be to demonstrate the complete chain in your home lab:

```text
Generate Activity
       ↓
Collect Telemetry
       ↓
Detect Activity
       ↓
Generate Alert
       ↓
Triage Alert
       ↓
Investigate
       ↓
Map IOC / IOA / ATT&CK
       ↓
Document
       ↓
Escalate / Respond
```

That practical workflow is the core of your future **SOC L1 portfolio**.
