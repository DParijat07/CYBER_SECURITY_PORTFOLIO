# Endpoint Monitoring

> **Blue Team → SOC → Security Monitoring → Endpoint Monitoring**

Endpoint monitoring is the process of collecting and analyzing security telemetry from workstations, laptops, servers, and other endpoint systems to detect suspicious activity, investigate incidents, and support response.

For a SOC analyst, endpoints are one of the most important sources of evidence because many attacks eventually involve:

```text
Process Execution
+
File Activity
+
User Activity
+
Network Connections
+
Authentication
+
Persistence
+
System Changes
```

The objective is:

> **Detect, investigate, and document malicious or anomalous activity occurring on endpoint systems.**

---

# 1. Objectives

After completing this section, you should understand:

* Endpoint monitoring fundamentals
* Windows endpoint telemetry
* Linux endpoint telemetry
* Windows Event Logs
* Sysmon
* Process monitoring
* File and directory monitoring
* PowerShell monitoring
* Command-line monitoring
* Persistence monitoring
* Authentication monitoring
* Network connection monitoring
* EDR and XDR concepts
* Endpoint-based detection
* Endpoint investigation
* SIEM integration
* Practical endpoint-monitoring labs

---

# 2. What Is an Endpoint?

An endpoint is a computing device that connects to an organization's environment.

Examples:

```text
Workstation
Laptop
Desktop
Server
Virtual Machine
Domain Controller
Application Server
Database Server
```

In a SOC environment, endpoints generate telemetry that can reveal:

```text
Who?
What?
When?
Where?
How?
```

---

# 3. Endpoint Monitoring Architecture

A simplified architecture:

```text
                    ENDPOINT
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
     Process          Files          Network
        │               │                │
        ↓               ↓                ↓
   Authentication   System Events   Connections
        │               │                │
        └───────────────┼────────────────┘
                        ↓
                   Endpoint Agent
                        │
                        ↓
                 Log Collection
                        │
                        ↓
                       SIEM
                        │
                   Correlation
                        │
                        ↓
                     Detection
                        │
                        ↓
                       Alert
                        │
                        ↓
                  SOC Analyst
```

---

# 4. Why Endpoint Monitoring Matters

Network telemetry may tell you:

```text
Host A connected to Host B.
```

Endpoint telemetry can tell you:

```text
PowerShell started.
 ↓
Encoded command executed.
 ↓
File downloaded.
 ↓
New process created.
 ↓
External connection established.
```

This provides much stronger investigative context.

---

# 5. Major Endpoint Telemetry

A SOC should monitor:

| Telemetry           | Security Value                         |
| ------------------- | -------------------------------------- |
| Process Creation    | Detect suspicious execution            |
| Command Line        | Understand attacker behavior           |
| File Activity       | Detect payloads/modification           |
| Registry            | Detect persistence/configuration       |
| Authentication      | Detect account abuse                   |
| Network Connections | Detect C2/lateral movement             |
| PowerShell          | Detect script-based attacks            |
| Services            | Detect persistence                     |
| Scheduled Tasks     | Detect persistence                     |
| Drivers             | Detect low-level activity              |
| Security Events     | Detect authentication/security changes |

---

# 6. Windows Endpoint Monitoring

Windows endpoints provide several valuable telemetry sources:

```text
Windows Event Logs
Sysmon
PowerShell Logs
Defender
EDR
Task Scheduler
Services
Registry
File System
```

A SOC analyst should understand how these sources complement each other.

---

# 7. Windows Event Logs

Important Windows logs include:

```text
Security
System
Application
PowerShell
```

The Security log is particularly important for:

```text
Authentication
Account Management
Privilege Use
Security Policy Changes
```

---

# 8. Important Windows Security Events

Examples include:

```text
4624 → Successful Logon
4625 → Failed Logon
4688 → Process Creation
4720 → User Account Created
4728 → Member Added to Global Security Group
4732 → Member Added to Local Security Group
4740 → Account Locked Out
4672 → Special Privileges Assigned
```

Event IDs should always be interpreted in context rather than treated as malicious by themselves.

---

# 9. Successful Logon Monitoring

A successful authentication event can provide:

```text
User
Source
Logon Type
Timestamp
Computer
Authentication
```

Example:

```text
User: administrator
Source: 10.10.10.25
Time: 02:30
```

If the account normally works during business hours, this could warrant investigation.

However:

> Unusual does not automatically mean malicious.

Always validate context.

---

# 10. Failed Logon Monitoring

Repeated failed authentication can indicate:

```text
Brute Force
Password Spraying
Credential Stuffing
Misconfiguration
User Error
```

A useful detection concept:

```text
Multiple Failed Logons
        ↓
Same Account / Multiple Accounts
        ↓
Short Time Window
        ↓
Successful Authentication
```

This should trigger investigation.

---

# 11. Process Monitoring

Process creation is one of the most valuable endpoint telemetry sources.

Monitor:

```text
Process Name
Parent Process
Command Line
User
PID
Timestamp
Executable Path
Hash
```

Example:

```text
WINWORD.EXE
     ↓
PowerShell.exe
     ↓
cmd.exe
     ↓
unknown.exe
```

This parent-child relationship may reveal suspicious execution.

---

# 12. Parent-Child Process Relationships

Normal:

```text
explorer.exe
      ↓
notepad.exe
```

Potentially suspicious:

```text
winword.exe
      ↓
powershell.exe
```

or:

```text
excel.exe
      ↓
cmd.exe
```

These are investigation signals, not automatic proof of compromise.

---

# 13. Command-Line Monitoring

Command-line arguments often provide additional context.

Example:

```text
powershell.exe -ExecutionPolicy Bypass ...
```

or:

```text
cmd.exe /c ...
```

or:

```text
rundll32.exe ...
```

A process name alone may not reveal the complete behavior.

Therefore:

> **Always inspect the command line when available.**

---

# 14. PowerShell Monitoring

PowerShell is widely used by administrators and developers.

It can also be abused by attackers.

Monitor:

```text
PowerShell Execution
Script Block Logging
Command Line
Encoded Commands
Download Activity
Child Processes
Network Connections
```

Example:

```text
powershell.exe
      ↓
Internet Connection
      ↓
File Download
      ↓
New Process
```

This sequence deserves investigation.

---

# 15. PowerShell Script Block Logging

Script Block Logging can provide visibility into executed PowerShell content.

Useful telemetry can include:

```text
Script
User
Process
Timestamp
Host
```

This can help the SOC reconstruct PowerShell-based activity.

---

# 16. Encoded PowerShell

Attackers may encode commands to make them harder to read.

Example indicator:

```text
powershell.exe
    -EncodedCommand
```

This alone does not prove malicious activity.

Investigate:

```text
Parent Process
User
Command
Destination
Downloaded Files
Follow-up Processes
```

---

# 17. Windows Command Shell Monitoring

Monitor suspicious use of:

```text
cmd.exe
powershell.exe
wscript.exe
cscript.exe
mshta.exe
rundll32.exe
regsvr32.exe
```

These utilities can be legitimate administrative tools but may also be abused.

The important principle is:

```text
Tool
+
Context
+
Command
+
Parent Process
+
User
=
Investigation
```

---

# 18. File Monitoring

Monitor important file activity:

```text
Create
Modify
Delete
Rename
Execute
Download
```

High-value locations may include:

```text
Startup Locations
Temporary Directories
User Profile Directories
System Directories
Application Directories
```

Unexpected executable creation can be suspicious.

---

# 19. File Extension Monitoring

Potentially interesting files include:

```text
.exe
.dll
.ps1
.bat
.cmd
.vbs
.js
.hta
.scr
```

However, legitimate software uses these formats too.

Therefore:

```text
Extension
+
Path
+
Parent Process
+
User
+
Hash
```

provides better context.

---

# 20. Hash Monitoring

File hashes can help identify known malware or compare files.

Common hashes:

```text
MD5
SHA-1
SHA-256
```

For modern security workflows, SHA-256 is generally preferred.

A SOC may compare a suspicious file hash against:

```text
Threat Intelligence
EDR
Malware Databases
Internal Blocklists
```

---

# 21. Persistence Monitoring

Attackers may attempt to maintain access after initial compromise.

Common persistence mechanisms include:

```text
Scheduled Tasks
Services
Startup Locations
Registry Run Keys
User Accounts
WMI
Startup Scripts
```

A SOC should monitor unexpected changes to these mechanisms.

---

# 22. Scheduled Task Monitoring

Example:

```text
User
 ↓
Creates Scheduled Task
 ↓
Task Executes PowerShell
 ↓
External Connection
```

Investigate:

```text
Task Name
Creator
Command
Execution Time
User
Parent Process
Destination
```

---

# 23. Windows Service Monitoring

Services can provide persistence.

Monitor:

```text
Service Created
Service Modified
Service Started
Service Stopped
Service Account
Binary Path
```

Suspicious example:

```text
New Service
 ↓
Unknown Executable
 ↓
Runs as SYSTEM
```

This should receive investigation priority.

---

# 24. Registry Monitoring

Important registry locations can contain persistence mechanisms.

Monitor security-sensitive changes such as:

```text
Run Keys
Services
Security Configuration
Defender Configuration
System Policies
```

Unexpected registry modifications should be correlated with:

```text
Process
User
Command Line
Timestamp
```

---

# 25. Authentication Monitoring

Endpoint authentication telemetry can reveal:

```text
Brute Force
Credential Theft
Lateral Movement
Account Abuse
Privilege Escalation
```

Monitor:

```text
Successful Logon
Failed Logon
Logoff
Account Lockout
Privilege Assignment
Remote Logon
```

---

# 26. Logon Types

Windows logon types provide useful context.

Examples:

```text
2  → Interactive
3  → Network
4  → Batch
5  → Service
7  → Unlock
10 → Remote Interactive
```

For example:

```text
Logon Type 10
```

can indicate a Remote Desktop-style interactive session.

Always interpret logon type together with the source, user, and environment.

---

# 27. Remote Access Monitoring

Monitor:

```text
RDP
SMB
WinRM
SSH
Remote Management
```

Potentially suspicious pattern:

```text
Compromised Workstation
        ↓
Remote Authentication
        ↓
Server
        ↓
Administrative Activity
```

This may indicate lateral movement.

---

# 28. Linux Endpoint Monitoring

Linux telemetry commonly includes:

```text
/var/log/auth.log
/var/log/syslog
/var/log/messages
auditd
journald
SSH Logs
Process Activity
Cron
Systemd
```

The exact locations vary by distribution and configuration.

---

# 29. Linux Authentication Monitoring

Monitor:

```text
SSH Login
Failed SSH Login
sudo
su
User Creation
Password Changes
```

Example:

```text
Multiple SSH Failures
        ↓
Successful Login
        ↓
sudo
        ↓
Sensitive Command
```

This deserves investigation.

---

# 30. Linux Process Monitoring

Important information includes:

```text
PID
PPID
User
Command
Path
Arguments
Timestamp
Network Connections
```

A suspicious process may be identified through:

```text
Unknown Binary
Unusual Parent
Unexpected User
Unusual Location
External Connection
```

---

# 31. Linux Privilege Monitoring

Monitor:

```text
sudo
su
User Group Changes
UID/GID Changes
Root Access
Sudoers Modification
```

Example:

```text
Normal User
 ↓
sudo
 ↓
Root
 ↓
Modify SSH Configuration
```

This requires investigation.

---

# 32. Cron Monitoring

Cron jobs can provide persistence.

Monitor:

```text
Crontab Creation
Modification
Execution
Unknown Commands
Network Activity
```

Example:

```text
New Cron Job
 ↓
curl / wget
 ↓
Downloads Script
 ↓
Executes
```

This is suspicious in many environments.

---

# 33. Systemd Monitoring

Linux services can also provide persistence.

Monitor:

```text
Service Creation
Service Modification
Service Start
Service Enable
Binary Path
User
```

Example:

```text
New Service
 ↓
Unknown Binary
 ↓
Enabled at Boot
```

Investigate.

---

# 34. Endpoint Network Monitoring

Endpoint network telemetry can reveal:

```text
Outbound Connections
Inbound Connections
Destination IP
Destination Port
Process
User
DNS
```

Example:

```text
powershell.exe
      ↓
Unknown External IP
      ↓
HTTPS
```

Correlate the process and destination.

---

# 35. Process-to-Network Correlation

This is extremely useful for SOC investigations.

Example:

```text
Suspicious Process
        ↓
Network Connection
        ↓
External IP
        ↓
DNS Query
```

Instead of investigating these events separately:

```text
Process
+
DNS
+
Network
```

correlate them into one timeline.

---

# 36. Endpoint DNS Monitoring

Monitor:

```text
Domain
Query Time
Process
User
Response
Destination IP
```

Potentially suspicious:

```text
Endpoint
 ↓
Newly Seen Domain
 ↓
PowerShell
 ↓
External Connection
```

This may indicate malware or simply legitimate software.

Investigate the context.

---

# 37. EDR

Endpoint Detection and Response (EDR) platforms provide deeper endpoint visibility.

Typical capabilities include:

```text
Process Monitoring
File Monitoring
Network Monitoring
Detection
Investigation
Threat Hunting
Response
```

An EDR can provide a timeline such as:

```text
User Login
 ↓
Office Application
 ↓
PowerShell
 ↓
File Creation
 ↓
Network Connection
 ↓
Suspicious Process
```

---

# 38. XDR

Extended Detection and Response expands correlation across multiple security domains.

Example:

```text
Endpoint
   +
Email
   +
Identity
   +
Network
   +
Cloud
   ↓
XDR
   ↓
Correlation
   ↓
Detection
```

This can help identify multi-stage attacks.

---

# 39. SIEM + Endpoint

A common SOC architecture:

```text
Windows
Linux
Servers
Workstations
     │
     ↓
Agents / Collectors
     │
     ↓
      SIEM
     │
     ├── Correlation
     ├── Detection
     ├── Dashboards
     └── Alerts
     │
     ↓
SOC Analyst
```

---

# 40. Wazuh + Endpoint Monitoring

Your home lab can use Wazuh to practice endpoint monitoring.

Example:

```text
Windows VM
     │
     ↓
Wazuh Agent
     │
     ↓
Wazuh Manager
     │
     ↓
Detection
     │
     ↓
Dashboard
     │
     ↓
SOC Investigation
```

You can monitor:

```text
Windows Events
Sysmon
File Integrity
Authentication
Vulnerability Data
Commands
Processes
```

---

# 41. Sysmon

Sysmon is highly valuable for Windows endpoint visibility.

Important event types include:

```text
Event ID 1  → Process Creation
Event ID 3  → Network Connection
Event ID 7  → Image Loaded
Event ID 8  → CreateRemoteThread
Event ID 10 → Process Access
Event ID 11 → File Creation
Event ID 12/13/14 → Registry Activity
Event ID 22 → DNS Query
```

Sysmon configuration determines which events are collected.

---

# 42. Process Creation Detection

A useful detection concept:

```text
Office Application
       ↓
PowerShell
       ↓
Network Connection
```

Potentially suspicious.

Another:

```text
Web Browser
       ↓
cmd.exe
```

Investigate the context.

---

# 43. Suspicious Parent-Child Chains

Examples worth investigating:

```text
winword.exe → powershell.exe
excel.exe → cmd.exe
outlook.exe → powershell.exe
browser.exe → cmd.exe
services.exe → unknown.exe
```

Again:

> **A suspicious process chain is an investigation signal, not proof of malicious activity.**

---

# 44. Endpoint Persistence Detection

Combine:

```text
New Process
+
New File
+
Registry Change
+
Scheduled Task
+
Service
```

Example:

```text
PowerShell
 ↓
Creates File
 ↓
Creates Scheduled Task
 ↓
Task Executes Script
```

This is a strong persistence investigation scenario.

---

# 45. Malware Investigation Workflow

When a suspicious process is detected:

```text
Alert
 ↓
Identify Host
 ↓
Identify User
 ↓
Identify Process
 ↓
Inspect Parent
 ↓
Inspect Command Line
 ↓
Inspect File
 ↓
Check Hash
 ↓
Check Network Connections
 ↓
Check Persistence
 ↓
Search Historical Activity
 ↓
Correlate SIEM Events
 ↓
Determine Impact
 ↓
Respond
```

---

# 46. Endpoint Investigation Questions

Always ask:

```text
Who executed it?
What executed?
Where did it execute?
When?
What was the parent process?
What arguments were used?
What files were created?
What network connections occurred?
Was persistence established?
Did the same activity occur elsewhere?
```

---

# 47. Practical Lab — Windows Event Monitoring

Use your Windows VM.

Generate controlled events:

```text
Successful Login
Failed Login
Process Creation
User Creation
Privilege Assignment
```

Collect:

```text
Event ID
User
Computer
Source
Timestamp
```

Document the observations.

---

# 48. Practical Lab — Sysmon

Install and configure Sysmon in your isolated Windows lab.

Generate controlled activity:

```text
cmd.exe
PowerShell
File Creation
DNS Query
Network Connection
```

Identify the relevant Sysmon events.

Create a small detection table:

| Activity           | Sysmon Event | Evidence             |
| ------------------ | -----------: | -------------------- |
| Process Creation   |            1 | Process + Command    |
| Network Connection |            3 | Source + Destination |
| File Creation      |           11 | Path + Process       |
| DNS Query          |           22 | Domain + Process     |

---

# 49. Practical Lab — PowerShell Monitoring

Generate legitimate PowerShell commands.

Observe:

```text
Process
Command Line
User
Parent
Network
```

Then create a controlled suspicious-looking sequence:

```text
PowerShell
 ↓
File Creation
 ↓
Network Connection
```

Investigate the complete chain.

---

# 50. Practical Lab — Persistence Monitoring

Create a disposable test persistence mechanism.

Choose:

```text
Scheduled Task
```

or:

```text
Test Windows Service
```

Monitor:

```text
Creator
Command
Path
Timestamp
Execution
```

Remove the persistence mechanism after the test.

---

# 51. Practical Lab — Linux Authentication

On your Linux/Kali lab:

Generate controlled:

```text
SSH Success
SSH Failure
sudo
su
```

Review the relevant logs.

Document:

```text
Source
User
Command
Timestamp
Result
```

---

# 52. Practical Lab — Endpoint Attack Timeline

Create a controlled scenario:

```text
User Login
 ↓
Suspicious Process
 ↓
PowerShell
 ↓
File Creation
 ↓
DNS Query
 ↓
Network Connection
 ↓
Persistence
```

Use:

```text
Windows Logs
+
Sysmon
+
Wazuh
+
Network Evidence
```

Reconstruct the timeline.

---

# 53. Practical Lab — Endpoint Detection Rule

Create a detection hypothesis:

> Detect PowerShell spawned by an Office application followed by an external network connection.

Conceptual logic:

```text
Parent Process = Office Application
        AND
Child Process = PowerShell
        AND
Network Connection = External
```

Document:

```text
Detection Name
Objective
Data Source
Logic
Severity
False Positives
Investigation Steps
Response
```

---

# 54. False Positives

Endpoint monitoring generates many legitimate alerts.

Examples:

```text
IT Administration
Software Deployment
Windows Updates
Backup Software
Monitoring Tools
Developer Activity
Security Testing
Automation
```

Therefore, detection engineering should consider:

```text
Baseline
Allowlist
User Context
Asset Context
Process Context
Time
Destination
```

---

# 55. Endpoint Monitoring Investigation Matrix

| Signal              | Possible Meaning            | Investigation         |
| ------------------- | --------------------------- | --------------------- |
| Failed Login        | Brute Force                 | Source + frequency    |
| PowerShell          | Admin / Attack              | Command + parent      |
| New Service         | Software / Persistence      | Binary + creator      |
| Scheduled Task      | Automation / Persistence    | Command + creator     |
| Unknown Process     | Malware / Software          | Hash + path           |
| External Connection | Normal / C2                 | Destination + process |
| Registry Change     | Configuration / Persistence | Key + process         |
| New User            | Admin / Persistence         | Creator + privileges  |
| Large File Creation | Backup / Ransomware         | Process + extension   |
| DNS Anomaly         | Normal / C2                 | Domain + process      |

---

# 56. Endpoint Monitoring Blind Spots

Common weaknesses include:

```text
No Sysmon
No EDR
No Command-Line Visibility
No PowerShell Logging
No Authentication Monitoring
No File Integrity Monitoring
No Network Correlation
Poor Log Retention
No Baseline
No Centralized SIEM
```

These gaps reduce detection capability.

---

# 57. Endpoint Security Baseline

A healthy monitoring baseline should include:

```text
Endpoint Inventory
+
User Inventory
+
Normal Processes
+
Normal Network Connections
+
Authentication Baseline
+
Security Logging
+
EDR / Agent Health
+
Critical File Monitoring
```

The SOC should also monitor whether security agents themselves are functioning.

---

# 58. Endpoint Agent Health

A security monitoring platform is only useful if its telemetry is available.

Monitor:

```text
Agent Online
Agent Offline
Logging Disabled
Sensor Disabled
Configuration Changed
Unusual Resource Usage
```

Example:

```text
Endpoint
 ↓
EDR Disabled
 ↓
Suspicious Activity
```

This should receive high investigation priority.

---

# 59. Endpoint Monitoring + Incident Response

Endpoint monitoring supports multiple IR stages:

```text
Preparation
 ↓
Detection
 ↓
Analysis
 ↓
Containment
 ↓
Eradication
 ↓
Recovery
 ↓
Lessons Learned
```

Endpoint telemetry provides evidence throughout the lifecycle.

---

# 60. Evidence Collection

For endpoint investigations collect:

```text
Hostname
IP
Username
Process
Parent Process
Command Line
File Path
File Hash
Event ID
Registry Change
Service
Scheduled Task
DNS
Network Connection
Timestamp
EDR Alert
SIEM Alert
Screenshots
Timeline
Conclusion
```

Maintain evidence integrity and follow organizational procedures.

---

# 61. Portfolio Lab Structure

Recommended structure:

```text
10-Endpoint-Monitoring.md

Labs/
│
├── 01-Windows-Event-Monitoring/
│   ├── README.md
│   ├── Evidence/
│   └── Investigation.md
│
├── 02-Sysmon-Monitoring/
│
├── 03-PowerShell-Monitoring/
│
├── 04-Process-Monitoring/
│
├── 05-Endpoint-Network-Monitoring/
│
├── 06-Persistence-Monitoring/
│
├── 07-Linux-Endpoint-Monitoring/
│
├── 08-Wazuh-Endpoint-Monitoring/
│
├── 09-Endpoint-Detection-Rule/
│
└── 10-Endpoint-Attack-Timeline/
```

---

# 62. Interview Questions

### Fundamentals

1. What is endpoint monitoring?
2. Why is endpoint telemetry important?
3. What is Sysmon?
4. What is EDR?
5. What is XDR?
6. What is the difference between SIEM and EDR?
7. What is process monitoring?
8. Why is command-line telemetry important?
9. What is parent-child process analysis?
10. Why should PowerShell activity be monitored?

### Windows

11. What is Event ID 4624?
12. What is Event ID 4625?
13. What is Event ID 4688?
14. What is Event ID 4720?
15. What is Event ID 4740?
16. What is Sysmon Event ID 1?
17. What is Sysmon Event ID 3?
18. What is Sysmon Event ID 22?

### Investigation

19. How would you investigate suspicious PowerShell?
20. How would you investigate a suspicious process?
21. How would you investigate a new Windows service?
22. How would you investigate a suspicious scheduled task?
23. How would you investigate an unusual RDP login?
24. How would you investigate a suspicious outbound connection?

---

# 63. Scenario-Based Interview Question

> **Wazuh generates an alert showing PowerShell spawned by Microsoft Word. What do you do?**

Investigation:

```text
Alert
 ↓
Identify Host
 ↓
Identify User
 ↓
Check Word Process
 ↓
Inspect PowerShell Command Line
 ↓
Check Parent/Child Relationship
 ↓
Check Files Created
 ↓
Check DNS
 ↓
Check Network Connections
 ↓
Check Persistence
 ↓
Search Same Activity Across Environment
 ↓
Determine Impact
```

Do not immediately isolate the system solely because Word launched PowerShell.

Validate the evidence first, unless organizational policy requires automatic containment for that detection.

---

# 64. Scenario-Based Interview Question

> **A Windows server suddenly starts connecting to an unfamiliar external IP. What do you investigate?**

```text
Endpoint
 ↓
Process Responsible
 ↓
Command Line
 ↓
User
 ↓
DNS
 ↓
Destination IP
 ↓
Port
 ↓
Historical Connections
 ↓
Threat Intelligence
 ↓
Other Hosts
```

Then determine whether the connection is:

```text
Legitimate
Suspicious
Malicious
Unknown
```

---

# 65. Scenario-Based Interview Question

> **A new Windows service appears on a production server. How would you investigate?**

Check:

```text
Service Name
 ↓
Binary Path
 ↓
Creator
 ↓
Creation Time
 ↓
Service Account
 ↓
File Hash
 ↓
Parent Process
 ↓
Network Connections
 ↓
Change Ticket
 ↓
Other Hosts
```

This separates legitimate administration from potential persistence.

---

# 66. Key Takeaways

```text
1. Endpoints provide high-value security telemetry.

2. Process creation is one of the most important endpoint signals.

3. Command-line visibility significantly improves investigation quality.

4. Parent-child process relationships provide valuable context.

5. PowerShell requires monitoring because it is both legitimate and frequently abused.

6. Authentication events help identify credential attacks and lateral movement.

7. Persistence mechanisms such as services and scheduled tasks require monitoring.

8. Endpoint network connections should be correlated with processes.

9. Sysmon provides detailed Windows telemetry.

10. EDR provides endpoint detection, investigation, and response capabilities.

11. XDR extends correlation beyond the endpoint.

12. Wazuh can provide valuable endpoint visibility in a home lab.

13. False positives must be investigated using context.

14. Endpoint agent health is itself a security-monitoring requirement.

15. A strong SOC analyst reconstructs endpoint activity as a timeline rather than investigating isolated events.
```

---

# 67. Final Mental Model

```text
                       ENDPOINT
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
    Process              Files              User
       │                   │                   │
       ↓                   ↓                   ↓
  Command Line         Registry          Authentication
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ↓
                       Sysmon / EDR
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
            DNS         Network       SIEM
              │            │            │
              └────────────┼────────────┘
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
                  Response / Report
```

> **Endpoint monitoring transforms raw host activity into security evidence. A SOC analyst's job is to connect processes, users, files, authentication, persistence, and network activity into a coherent timeline and determine whether the endpoint is compromised.**
