# Windows Monitoring

> **Blue Team → SOC → Security Monitoring → Windows**

Windows environments are among the most important monitoring targets for SOC teams because they commonly host user workstations, enterprise applications, servers, Active Directory infrastructure, and privileged accounts.

Effective Windows monitoring combines:

```text
Windows Event Logs
+
Sysmon
+
PowerShell Logging
+
Endpoint Security
+
Authentication Telemetry
+
Process Activity
+
Network Activity
```

The objective is not to collect every possible event blindly, but to obtain enough telemetry to answer:

> **Who did what, on which system, when, from where, and what happened next?**

---

# 1. Objectives

After completing this section, you should understand:

* Windows security monitoring fundamentals
* Windows Event Logs
* Security event IDs
* System and Application logs
* PowerShell logging
* Sysmon
* Process monitoring
* Authentication monitoring
* Account monitoring
* Privilege monitoring
* Network monitoring
* Persistence-related telemetry
* Windows services
* Scheduled tasks
* Windows Defender telemetry
* Event correlation
* Windows monitoring with Wazuh
* Practical Windows monitoring scenarios

---

# 2. Windows Monitoring Architecture

A simplified architecture:

```text
                 WINDOWS ENDPOINT
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   Event Logs       Sysmon       PowerShell
        │              │              │
        └──────────────┼──────────────┘
                       ↓
                 Wazuh Agent
                       ↓
                Wazuh Manager
                       ↓
                    SIEM
                       ↓
                 Detection
                       ↓
                    Alert
                       ↓
                SOC Analyst
```

---

# 3. Windows Event Logging

Windows records system and security activity through the Windows Event Log system.

Important channels include:

```text
Security
System
Application
PowerShell
Windows Defender
Task Scheduler
```

These events provide visibility into:

```text
Authentication
Process Activity
System Changes
Account Changes
Application Errors
Security Controls
```

---

# 4. Security Event Log

The Security log is particularly important for SOC analysts.

It can contain events related to:

```text
Logons
Logoff
Account Management
Privilege Use
Process Creation
Policy Changes
Object Access
```

Security events can help investigate:

```text
Brute Force
Credential Abuse
Privilege Escalation
Account Compromise
Lateral Movement
Persistence
```

---

# 5. Important Windows Event IDs

Some commonly encountered events:

| Event ID | Meaning                                       |
| -------: | --------------------------------------------- |
|     4624 | Successful logon                              |
|     4625 | Failed logon                                  |
|     4634 | Logoff                                        |
|     4648 | Logon using explicit credentials              |
|     4672 | Special privileges assigned to new logon      |
|     4688 | Process creation                              |
|     4720 | User account created                          |
|     4722 | User account enabled                          |
|     4725 | User account disabled                         |
|     4726 | User account deleted                          |
|     4728 | Member added to security-enabled global group |
|     4732 | Member added to security-enabled local group  |
|     4740 | Account locked out                            |
|     1102 | Security audit log cleared                    |

These IDs should be learned together with their **context**, rather than memorized as isolated numbers.

---

# 6. Successful Logon — Event 4624

Event 4624 indicates a successful logon.

Important investigation fields may include:

```text
Account Name
Account Domain
Logon Type
Source Network Address
Workstation Name
Authentication Package
Timestamp
```

Example investigation:

```text
User: Administrator
Host: SERVER01
Source IP: 10.10.10.50
Time: 02:13
```

The event itself is not necessarily malicious.

Context determines risk.

---

# 7. Failed Logon — Event 4625

Event 4625 indicates a failed logon.

Repeated failures can indicate:

```text
Brute Force
Password Spraying
Credential Mistakes
Misconfigured Services
Compromised Credentials
```

Example:

```text
4625
4625
4625
4625
4625
      ↓
Repeated Authentication Failure
```

A SOC analyst should examine:

```text
Source IP
Target Account
Frequency
Time Window
Logon Type
Related Successful Login
```

---

# 8. Logon Types

Logon Type provides useful context.

Common examples:

| Logon Type | General Meaning         |
| ---------: | ----------------------- |
|          2 | Interactive             |
|          3 | Network                 |
|          4 | Batch                   |
|          5 | Service                 |
|          7 | Unlock                  |
|          8 | NetworkCleartext        |
|          9 | NewCredentials          |
|         10 | RemoteInteractive / RDP |
|         11 | CachedInteractive       |

For example:

```text
4624
+
Logon Type 10
```

can indicate a successful Remote Desktop login.

---

# 9. RDP Monitoring

Remote Desktop Protocol is important to monitor in Windows environments.

Useful telemetry includes:

```text
Successful RDP Login
Failed RDP Login
Source IP
User
Time
Host
```

A suspicious pattern could be:

```text
Many Failed RDP Logins
        ↓
Successful RDP Login
        ↓
Privileged Account
        ↓
Suspicious Process
```

This sequence deserves investigation.

---

# 10. Explicit Credential Usage — Event 4648

Event 4648 can indicate a process attempted to log on using explicitly supplied credentials.

This can be legitimate:

```text
Administrative Activity
Service Operations
IT Management
```

But it may also be relevant during:

```text
Credential Abuse
Lateral Movement
Privilege Escalation
```

Always investigate it in context.

---

# 11. Special Privileges — Event 4672

Event 4672 indicates special privileges were assigned to a new logon.

This is particularly relevant for privileged accounts.

Example:

```text
Privileged Login
      ↓
4672
      ↓
Suspicious Activity?
```

Correlation with:

```text
4624
4688
4648
Network Activity
```

can provide a stronger picture.

---

# 12. Process Creation — Event 4688

Event 4688 records process creation when appropriate auditing is enabled.

Useful information may include:

```text
New Process
Creator Process
User
Command Line
Process ID
Parent Process
```

Example:

```text
winword.exe
     ↓
powershell.exe
     ↓
network connection
```

This can be significantly more interesting than an isolated PowerShell execution.

---

# 13. Process Monitoring

Important process-monitoring questions:

```text
What process started?
Who started it?
What was its parent?
What command line was used?
When did it start?
What did it connect to?
What files did it access?
```

A useful process tree:

```text
explorer.exe
     ↓
winword.exe
     ↓
powershell.exe
     ↓
cmd.exe
```

The process relationship provides important context.

---

# 14. Parent-Child Process Relationships

Parent-child relationships are useful for identifying suspicious execution chains.

Example:

```text
winword.exe
     ↓
powershell.exe
```

Potentially suspicious.

Another:

```text
services.exe
     ↓
svchost.exe
```

may be normal.

Therefore:

> **A suspicious process name alone is not enough.**

Context matters.

---

# 15. Sysmon

Sysmon is a Windows system-monitoring utility that can provide detailed telemetry.

It can monitor events such as:

```text
Process Creation
Network Connection
File Creation
Process Termination
DNS Query
Registry Activity
Driver Loading
```

Sysmon complements native Windows Event Logs.

---

# 16. Why Sysmon Is Valuable

Native Windows logging may provide:

```text
Process Created
```

Sysmon can provide richer context depending on configuration:

```text
Process
Parent Process
Command Line
Hash
User
Image
Network Connection
```

This can improve:

```text
Detection
Threat Hunting
Investigation
Incident Response
```

---

# 17. Sysmon Process Creation

One important Sysmon telemetry source is process creation.

A useful investigation may include:

```text
Image
Command Line
Parent Image
Parent Command Line
User
Hashes
Timestamp
```

Example:

```text
WINWORD.EXE
      ↓
POWERSHELL.EXE
      ↓
Encoded Command
```

This may warrant investigation.

---

# 18. PowerShell Monitoring

PowerShell is a legitimate administrative tool but is also frequently abused by attackers.

Monitor:

```text
PowerShell Execution
Command Line
Encoded Commands
Script Execution
Network Activity
Parent Process
User
```

Potentially suspicious pattern:

```text
Office Application
      ↓
PowerShell
      ↓
Encoded Command
      ↓
External Connection
```

Again, this is a detection lead, not automatic proof of compromise.

---

# 19. PowerShell Logging

Depending on configuration, useful PowerShell logging includes:

```text
Module Logging
Script Block Logging
Transcription
```

These can provide additional visibility into PowerShell activity.

A mature Windows monitoring environment should carefully balance:

```text
Visibility
Storage
Performance
Privacy
```

---

# 20. Windows Command-Line Monitoring

Command-line information can be extremely valuable.

Examples:

```text
cmd.exe
powershell.exe
wmic.exe
net.exe
whoami.exe
ipconfig.exe
schtasks.exe
sc.exe
```

The command itself provides context.

Example:

```text
whoami
```

is generally normal.

But:

```text
schtasks /create ...
```

may require investigation depending on context.

---

# 21. Account Creation

Monitor account-management events.

Important examples include:

```text
4720 — User Account Created
4722 — User Account Enabled
4725 — User Account Disabled
4726 — User Account Deleted
```

Potentially suspicious:

```text
Unexpected Account Creation
      ↓
Unexpected Group Membership
      ↓
Interactive Login
```

This can indicate persistence or administrative misuse.

---

# 22. Group Membership Changes

Monitor changes to privileged groups.

Examples:

```text
Administrators
Domain Admins
Enterprise Admins
Other Security-Enabled Groups
```

A suspicious sequence:

```text
User Account
     ↓
Added to Privileged Group
     ↓
Privileged Login
     ↓
Sensitive Activity
```

This should be investigated.

---

# 23. Account Lockout

Event 4740 can indicate account lockout.

Repeated lockouts may indicate:

```text
Brute Force
Password Spraying
Stale Credentials
Misconfigured Services
Compromised Systems
```

Investigate:

```text
Account
Source Host
Frequency
Time
Related Authentication Events
```

---

# 24. Security Log Cleared — Event 1102

Clearing the Security event log is highly security-relevant.

Event:

```text
1102
```

A possible investigation sequence:

```text
Privileged Login
      ↓
Administrative Activity
      ↓
Security Log Cleared
```

This may indicate an attempt to remove evidence.

However, legitimate administrative actions are possible, so context remains essential.

---

# 25. Windows Services

Windows services can provide useful security telemetry.

Monitor:

```text
Service Creation
Service Modification
Service Start
Service Stop
Service Account
Binary Path
```

Attackers may abuse services for:

```text
Persistence
Privilege Escalation
Execution
```

Example:

```text
New Service
     ↓
Unknown Binary
     ↓
Runs as SYSTEM
```

This deserves investigation.

---

# 26. Scheduled Tasks

Scheduled Tasks can be used legitimately for automation.

They can also support persistence.

Monitor:

```text
Task Creation
Task Modification
Task Execution
Task User
Command
Executable
Schedule
```

Example:

```text
New Scheduled Task
      ↓
PowerShell
      ↓
Suspicious Script
```

Potential persistence indicator.

---

# 27. Registry Monitoring

The Windows Registry contains important configuration information.

Security monitoring may focus on:

```text
Startup Locations
Services
Security Settings
Configuration Changes
Persistence Locations
```

Registry activity should be interpreted in context because legitimate software frequently modifies the registry.

---

# 28. Windows Defender Monitoring

Windows Defender can provide security telemetry such as:

```text
Malware Detection
Threat Name
File
Process
Action
Quarantine
Remediation
```

Example:

```text
Malware Detected
      ↓
File Quarantined
      ↓
Alert
      ↓
Investigate Related Activity
```

The SOC should correlate Defender events with:

```text
Process
User
Network
DNS
Authentication
```

---

# 29. Windows Firewall Monitoring

Windows Firewall can provide information about:

```text
Allowed Connections
Blocked Connections
Source
Destination
Port
Protocol
Application
```

Useful for identifying:

```text
Unexpected Network Connections
Suspicious Outbound Traffic
Unauthorized Services
Scanning
```

---

# 30. DNS Monitoring on Windows

Endpoint DNS activity can provide visibility into:

```text
Domain Queries
DNS Servers
Query Frequency
Response
```

Suspicious indicators can include:

```text
Random-Looking Domains
High Query Frequency
Known Malicious Domains
Unusual TLDs
Potential DNS Tunneling
```

DNS should be correlated with endpoint and network telemetry.

---

# 31. Windows Network Monitoring

Monitor:

```text
Source
Destination
Port
Protocol
Process
User
Timestamp
```

Example:

```text
powershell.exe
      ↓
10.0.0.15
      ↓
203.0.113.20:443
```

The connection alone may be legitimate.

The combination of:

```text
PowerShell
+
Suspicious Command
+
Unknown External Destination
```

may be more significant.

---

# 32. Windows Monitoring Through Wazuh

A basic architecture:

```text
Windows VM
    │
    ├── Security Logs
    ├── System Logs
    ├── PowerShell
    └── Sysmon
           │
           ↓
       Wazuh Agent
           │
           ↓
      Wazuh Manager
           │
           ↓
         SIEM
           │
           ↓
       Detection
           │
           ↓
         Alert
```

---

# 33. Wazuh Monitoring Objectives

In your home lab, configure monitoring for:

```text
Authentication
Process Creation
PowerShell
Account Changes
Privilege Changes
Scheduled Tasks
Services
Malware Detection
Network Activity
File Integrity
```

The goal is to build an actual Windows detection environment.

---

# 34. Practical Lab — Failed Login Detection

## Objective

Detect repeated Windows authentication failures.

### Generate controlled activity

Use your lab environment to produce several failed authentication attempts.

### Observe

Find:

```text
Event ID
4625
```

### Investigate:

```text
Username
Source
Time
Logon Type
Frequency
```

### Detection concept:

```text
Multiple 4625
+
Same Source
+
Short Time Window
```

### Output

Document:

```text
Alert
Timeline
Evidence
Analysis
Conclusion
```

---

# 35. Practical Lab — Suspicious Process

## Objective

Understand process telemetry.

Generate a controlled process execution.

Observe:

```text
4688
```

and/or Sysmon process telemetry.

Document:

```text
Process
Parent
User
Command Line
Timestamp
Host
```

Build a process tree:

```text
Parent
   ↓
Child
   ↓
Grandchild
```

---

# 36. Practical Lab — PowerShell Monitoring

## Objective

Understand PowerShell visibility.

Perform a harmless PowerShell command.

Observe:

```text
PowerShell Logs
Process Creation
Sysmon
Wazuh
```

Document:

```text
User
Host
Process
Parent Process
Command
Timestamp
```

Then compare:

```text
Normal PowerShell
vs
Suspicious PowerShell Pattern
```

---

# 37. Practical Lab — Account Monitoring

Create a controlled test account in your isolated lab.

Observe:

```text
4720
```

Then document:

```text
Account
Creator
Host
Time
Event ID
```

Delete or disable the test account after the exercise.

---

# 38. Practical Lab — Privileged Group Monitoring

In an isolated lab:

```text
Test User
   ↓
Add to Test/Administrative Group
   ↓
Observe Event
   ↓
Remove User
```

Document:

```text
Before
Change
After
Detection
Evidence
```

This demonstrates identity-security monitoring.

---

# 39. Practical Lab — Security Log Clearing

Only perform this inside your isolated lab.

Generate the corresponding event and observe:

```text
1102
```

Document:

```text
Who
When
Which Host
Event
Related Activity
```

The purpose is to understand how SOC analysts detect potential evidence destruction.

---

# 40. Windows Attack Chain Monitoring

A more advanced lab can correlate multiple events.

Example:

```text
Failed Login
     ↓
Successful Login
     ↓
Privileged Account
     ↓
PowerShell
     ↓
Process Creation
     ↓
Network Connection
```

The goal is to move from:

```text
Individual Events
```

to:

```text
Attack Narrative
```

---

# 41. Windows Investigation Questions

When investigating a Windows alert, ask:

### Identity

```text
Who?
Which account?
Privileged?
Expected?
```

### Host

```text
Which machine?
Critical?
Server?
Workstation?
```

### Process

```text
What executed?
Parent process?
Command line?
Hash?
```

### Network

```text
Destination?
Port?
Protocol?
External?
Known?
```

### Timeline

```text
What happened before?
What happened after?
```

---

# 42. Windows Monitoring Detection Examples

| Detection             | Primary Telemetry       |
| --------------------- | ----------------------- |
| Brute Force           | 4625                    |
| Successful Login      | 4624                    |
| Suspicious RDP        | 4624 / 4625             |
| Privileged Login      | 4672                    |
| Process Execution     | 4688 / Sysmon           |
| Account Creation      | 4720                    |
| Group Modification    | 4728 / 4732             |
| Account Lockout       | 4740                    |
| Log Clearing          | 1102                    |
| Suspicious PowerShell | PowerShell + Sysmon     |
| Persistence via Task  | Task Scheduler + Sysmon |
| Suspicious Service    | Service + Sysmon        |
| Malware               | Defender / EDR          |
| Network Activity      | Sysmon / Firewall       |

---

# 43. Windows Monitoring Blind Spots

Common weaknesses:

```text
Disabled Auditing
Missing Sysmon
Insufficient PowerShell Logging
No Command-Line Logging
Agent Offline
Poor Log Retention
No Network Visibility
No Centralized Collection
Missing Privileged Activity Monitoring
```

A SOC should continuously identify and remediate these gaps.

---

# 44. Windows Monitoring Baseline

Before declaring activity suspicious, establish normal behavior.

Example:

```text
Normal:
Administrator logs into server
during working hours
from approved workstation.
```

Potential anomaly:

```text
Administrator
+
3:00 AM
+
Unknown Host
+
RDP
+
PowerShell
```

The anomaly becomes more significant because it deviates from the baseline.

---

# 45. Windows Monitoring Evidence

For every Windows monitoring lab, capture:

```text
Event ID
Timestamp
Hostname
Username
Source IP
Destination
Process
Parent Process
Command Line
Detection Rule
Alert
Screenshot
Investigation Notes
```

Store evidence in your GitHub portfolio.

---

# 46. Recommended Portfolio Structure

For this file, practical work should live separately:

```text
04-Windows-Monitoring.md

Labs/
│
├── 01-Failed-Logon-Monitoring/
│   ├── README.md
│   ├── Evidence/
│   └── Report.md
│
├── 02-Process-Monitoring/
│
├── 03-PowerShell-Monitoring/
│
├── 04-Account-Monitoring/
│
├── 05-Privileged-Group-Monitoring/
│
├── 06-Scheduled-Task-Monitoring/
│
└── 07-Windows-Log-Clearing-Detection/
```

This makes the portfolio demonstrate:

```text
Knowledge
   ↓
Hands-On
   ↓
Detection
   ↓
Investigation
   ↓
Documentation
```

---

# 47. Interview Questions

### Fundamentals

1. What are Windows Event Logs?
2. What is Event ID 4624?
3. What is Event ID 4625?
4. What is Event ID 4688?
5. What is Sysmon?
6. Why is PowerShell monitoring important?
7. What is Event ID 1102?
8. What is the importance of Event ID 4672?
9. How do you monitor RDP?
10. How can you detect suspicious account creation?

### Scenario

> **You receive an alert for multiple failed Windows logins followed by a successful login. What would you do?**

Investigation:

```text
4625
 ↓
Source IP
 ↓
Target Account
 ↓
Frequency
 ↓
4624
 ↓
Successful Login
 ↓
Logon Type
 ↓
Host Activity
 ↓
Process Activity
 ↓
Network Activity
```

Then determine:

```text
True Positive?
False Positive?
Compromised Account?
Brute Force?
Password Spraying?
```

---

# 48. Key Takeaways

```text
1. Windows is a high-value SOC monitoring source.

2. Security Event Logs provide authentication and system visibility.

3. Sysmon provides detailed endpoint telemetry.

4. Event IDs provide useful investigation context.

5. Process trees are often more useful than isolated process names.

6. PowerShell requires strong monitoring because it is both legitimate and frequently abused.

7. Privileged account activity deserves additional scrutiny.

8. Account and group changes can reveal persistence or privilege escalation.

9. RDP activity should be monitored.

10. Security log clearing is highly security-relevant.

11. Endpoint telemetry should be correlated with network and identity data.

12. Wazuh can centralize Windows telemetry in a home lab.

13. Baselines help distinguish normal administrative activity from anomalies.

14. The objective is not simply collecting Windows logs.

15. The objective is turning Windows telemetry into actionable security detections.
```

---

# 49. Final Mental Model

```text
                    WINDOWS ENDPOINT
                           │
        ┌──────────────────┼──────────────────┐
        ↓                  ↓                  ↓
  Event Logs            Sysmon           PowerShell
        │                  │                  │
        ├──────────────┬───┴──────────────────┤
        ↓              ↓                      ↓
 Authentication     Process                Network
        │           Activity                Activity
        └──────────────┬──────────────────────┘
                       ↓
                  Wazuh Agent
                       ↓
                 Wazuh Manager
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
                       ↓
                 Investigation
                       ↓
                    Report
```

> **Windows monitoring is not about memorizing Event IDs. It is about using Windows telemetry to reconstruct user activity, process behavior, authentication, persistence, and network activity into an actionable security story.**
