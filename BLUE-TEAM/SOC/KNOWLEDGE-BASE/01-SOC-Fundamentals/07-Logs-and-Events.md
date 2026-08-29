# 📝 Logs and Events

> Logs and events are fundamental sources of evidence for SOC monitoring, detection, investigation, and incident response.

A SOC analyst must be able to read individual events, understand their fields, correlate related events, and reconstruct activity over time.

---

# 1. What Is a Log?

A log is a recorded message describing an activity or condition.

Example:

```text
User authentication failed
```

A log may contain:

```text
Timestamp
Source
User
Host
Event Type
Result
Source IP
Destination
Message
```

---

# 2. What Is an Event?

An event represents an observable occurrence.

Examples:

```text
Login
Process Creation
File Creation
Network Connection
Account Modification
DNS Query
Service Creation
```

A log is often the stored representation of an event.

---

# 3. Why Logs Matter

Logs allow analysts to:

* Detect suspicious activity
* Investigate incidents
* Build timelines
* Identify affected systems
* Identify users
* Find IOCs
* Correlate events
* Support forensic analysis
* Validate security controls

---

# 4. Common Log Sources

## Windows

```text
Security
System
Application
PowerShell
Sysmon
Defender
```

## Linux

```text
auth.log
syslog
journal
audit logs
application logs
```

## Network

```text
Firewall
IDS / IPS
DNS
Proxy
VPN
Router
Switch
NetFlow
```

## Application

```text
Web Server
Database
API
Authentication
Application Errors
```

## Cloud

```text
IAM
API
Audit
Network
Storage
Configuration
```

---

# 5. Important Log Fields

A SOC analyst should understand common fields.

```text
Timestamp
Hostname
Username
Source IP
Destination IP
Source Port
Destination Port
Protocol
Process
Parent Process
Command Line
Event ID
Action
Status
File
Hash
URL
Domain
```

---

# 6. Timestamp

Timestamp tells the analyst when an activity occurred.

Example:

```text
2026-08-06 10:15:32
```

Accurate time is critical for incident timelines.

Important considerations:

```text
Time Zone
Clock Synchronization
Timestamp Format
Event Generation Time
Ingestion Time
```

---

# 7. Source and Destination

Network events commonly contain:

```text
Source
Destination
```

Example:

```text
Source:
192.168.1.25

Destination:
8.8.8.8
```

The analyst should determine:

> Which system initiated the communication?

---

# 8. User Information

Authentication and endpoint events may identify:

```text
Username
Account Type
Domain
Privilege Level
Authentication Method
```

A privileged account performing unusual activity deserves additional investigation.

---

# 9. Process Information

Endpoint events may include:

```text
Process Name
PID
Parent Process
Command Line
User
Path
Hash
```

Example:

```text
Parent:
winword.exe

Child:
powershell.exe
```

The parent-child relationship can provide important attack context.

---

# 10. Event IDs

Windows environments use Event IDs to identify specific types of events.

Examples include:

```text
4624 — Successful Logon
4625 — Failed Logon
4688 — Process Creation
```

Event IDs should always be interpreted with their surrounding context.

---

# 11. Authentication Logs

Authentication logs are extremely valuable for SOC analysts.

Investigate:

```text
Failed Logins
Successful Logins
Multiple Attempts
New Locations
New Devices
Privileged Accounts
Service Accounts
```

Example pattern:

```text
20 Failed Logins
       ↓
Successful Login
       ↓
New Geographic Location
       ↓
Privilege Change
```

This may warrant investigation.

---

# 12. Process Creation Logs

Process creation telemetry can reveal:

```text
Execution
Parent-Child Relationships
Command Lines
Users
Malicious Tools
Scripting
Living-off-the-Land Activity
```

Example:

```text
powershell.exe
-c
EncodedCommand
```

should receive additional scrutiny depending on context.

---

# 13. Network Logs

Network logs can reveal:

```text
Connections
Scanning
Unusual Ports
External Communication
DNS Activity
C2 Patterns
Data Transfer
```

Example:

```text
Internal Host
      ↓
Rare External IP
      ↓
Repeated Connections
      ↓
Unusual Port
```

This may indicate suspicious behavior.

---

# 14. DNS Logs

DNS logs can be valuable for identifying:

* Suspicious domains
* Malware infrastructure
* Phishing
* C2
* Newly observed domains
* Unusual query patterns

Example:

```text
Host
 ↓
DNS Query
 ↓
Suspicious Domain
 ↓
Connection
```

DNS should therefore be correlated with endpoint and network telemetry.

---

# 15. Firewall Logs

Firewall logs can show:

```text
Source
Destination
Port
Protocol
Action
Timestamp
```

Example:

```text
Source: 192.168.1.20
Destination: 203.0.113.10
Port: 443
Action: Allowed
```

A single allowed connection is not necessarily malicious.

Context matters.

---

# 16. Sysmon

Sysmon provides detailed Windows telemetry useful for defensive monitoring.

Depending on configuration, it can provide information about:

```text
Process Creation
Network Connections
File Creation
DNS
Registry Activity
Process Access
```

Sysmon is especially useful for:

> **Endpoint detection and investigation.**

---

# 17. Log Levels

Applications commonly use levels such as:

```text
DEBUG
INFO
NOTICE
WARNING
ERROR
CRITICAL
```

These levels do not automatically correspond to security severity.

For example:

```text
ERROR ≠ Security Incident
```

The analyst must interpret the event in context.

---

# 18. Log Correlation

One log rarely tells the complete story.

Example:

```text
Event 1
Failed Login

Event 2
Successful Login

Event 3
PowerShell Execution

Event 4
External Connection

Event 5
File Creation
```

Correlation creates:

```text
Attack Story
```

---

# 19. Timeline Analysis

Convert logs into chronological order.

Example:

```text
09:58 — Failed Login
10:00 — Failed Login
10:01 — Successful Login
10:04 — PowerShell
10:05 — Network Connection
10:08 — File Creation
```

This helps answer:

> What happened first?

> What happened next?

> What was the likely attack sequence?

---

# 20. False Positives

A log or alert can appear suspicious while being legitimate.

Example:

```text
PowerShell Execution
```

Possible explanations:

```text
Malware
Administrator
Software Update
IT Automation
Monitoring Tool
```

Therefore:

> **An event is evidence, not automatically a conclusion.**

---

# 21. Log Analysis Methodology

Use this workflow:

```text
1. Identify the event
       ↓
2. Understand the fields
       ↓
3. Identify the user
       ↓
4. Identify the host
       ↓
5. Check timestamp
       ↓
6. Examine related events
       ↓
7. Check IOC
       ↓
8. Correlate telemetry
       ↓
9. Determine context
       ↓
10. Classify
       ↓
11. Document
```

---

# 22. Example Investigation

### Initial Event

```text
4625
Failed Login
User: administrator
Source IP: 192.168.1.50
```

### Investigation

Search for:

```text
Previous failed logins
Successful login
Source IP history
Other affected accounts
Privilege changes
Endpoint activity
Network activity
```

### Hypothetical Result

```text
15 failed logins
      ↓
Successful login
      ↓
New PowerShell process
      ↓
External connection
```

The analyst now has a stronger basis for escalation.

---

# 23. Log Analysis Questions

For every suspicious event:

### Who?

Who performed the action?

### What?

What happened?

### When?

When did it happen?

### Where?

Which host or system?

### Source?

Where did the activity originate?

### Destination?

Where did it go?

### Why?

Is there a legitimate explanation?

### What next?

What activity followed?

---

# 24. Log Retention

Organizations must determine how long logs should be retained based on:

* Business requirements
* Regulatory requirements
* Security requirements
* Storage capacity
* Investigation requirements
* Legal requirements

Longer retention can help investigations but increases storage and management requirements.

---

# 25. Log Integrity

Logs are security evidence.

Controls should protect them against:

```text
Unauthorized Modification
Deletion
Tampering
Loss
Incomplete Collection
```

Centralized collection can reduce dependence on local log storage.

---

# 26. Log Normalization

Different systems may represent the same concept differently.

Example:

```text
src_ip
source_ip
client_ip
remote_address
```

Normalization maps them into a consistent structure.

This improves:

```text
Search
Correlation
Detection
Analytics
Reporting
```

---

# 27. SIEM and Logs

A SIEM generally performs functions such as:

```text
Collection
Parsing
Normalization
Storage
Search
Correlation
Detection
Alerting
Visualization
```

Conceptually:

```text
Logs
 ↓
SIEM
 ↓
Correlation
 ↓
Detection
 ↓
Alert
 ↓
SOC Analyst
```

---

# 28. Practical Lab

The home lab should include exercises for:

```text
Windows Authentication
Windows Process Creation
PowerShell
Sysmon
Linux Authentication
Network Connections
DNS
Firewall
```

For each lab:

```text
Generate Activity
      ↓
Collect Logs
      ↓
Find Event
      ↓
Analyze Fields
      ↓
Correlate
      ↓
Determine Context
      ↓
Document
```

---

# 29. Log Analysis Portfolio Evidence

Each practical exercise should produce:

```text
Lab Objective
Environment
Activity Generated
Raw Event
Important Fields
Analysis
Related Events
Timeline
Finding
Conclusion
Detection Opportunity
```

Screenshots should be used where they add meaningful evidence.

Sensitive information should never be published.

---

# 30. SOC Analyst Log Analysis Checklist

```text
[ ] Timestamp checked
[ ] Time zone verified
[ ] Host identified
[ ] User identified
[ ] Source identified
[ ] Destination identified
[ ] Event type identified
[ ] Process identified
[ ] Parent process checked
[ ] Command line checked
[ ] Related events searched
[ ] IOC investigated
[ ] Timeline created
[ ] Legitimate explanation considered
[ ] Severity assessed
[ ] Conclusion documented
[ ] Escalation performed if required
```

---

# ⭐ Core Principle

> **Good SOC analysts do not merely read logs. They turn individual events into context, context into evidence, and evidence into defensible security decisions.**
