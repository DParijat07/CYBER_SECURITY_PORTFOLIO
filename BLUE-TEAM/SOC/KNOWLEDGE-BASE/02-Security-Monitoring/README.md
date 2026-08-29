# Security Monitoring

> **Blue Team / SOC Practical Capability**

Security monitoring is the continuous collection, analysis, and correlation of security telemetry to identify suspicious activity, security incidents, and potential threats within an environment.

It connects the concepts learned in **SOC Fundamentals** with practical SOC operations.

```text
Assets
   ↓
Telemetry
   ↓
Collection
   ↓
Monitoring
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

## 1. Objectives

This section focuses on developing practical skills in:

* Security event monitoring
* Endpoint monitoring
* Windows monitoring
* Linux monitoring
* Network monitoring
* Authentication monitoring
* Application monitoring
* Security telemetry analysis
* SIEM-based monitoring
* Alert investigation
* Monitoring baselines
* Anomaly identification
* Security dashboard analysis

---

## 2. Security Monitoring Architecture

A typical monitoring architecture:

```text
                    ┌──────────────────┐
                    │     Endpoints    │
                    │ Windows / Linux  │
                    └────────┬─────────┘
                             │
                             ↓
                    ┌──────────────────┐
                    │    Telemetry     │
                    │ Logs / Events    │
                    │ Network / EDR    │
                    └────────┬─────────┘
                             │
                             ↓
                    ┌──────────────────┐
                    │ Collection Layer │
                    │ Agents / Sensors │
                    └────────┬─────────┘
                             │
                             ↓
                    ┌──────────────────┐
                    │       SIEM       │
                    │ Correlation      │
                    │ Detection        │
                    └────────┬─────────┘
                             │
                             ↓
                    ┌──────────────────┐
                    │   SOC Analyst    │
                    └──────────────────┘
```

---

# 3. Monitoring Domains

Security monitoring in this portfolio will cover:

```text
Security Monitoring
│
├── Windows
├── Linux
├── Network
├── Authentication
├── Endpoint
├── Application
├── DNS
├── Web
├── Firewall
├── Cloud
└── Identity
```

---

# 4. Windows Security Monitoring

Windows endpoints generate valuable security telemetry.

Important monitoring areas:

```text
Process Creation
User Logon
Failed Logons
Account Changes
Privilege Changes
Service Creation
Scheduled Tasks
PowerShell
Command Execution
File Activity
Network Connections
Security Configuration Changes
```

Important sources include:

```text
Windows Event Logs
Sysmon
PowerShell Logs
Security Logs
System Logs
Application Logs
```

---

# 5. Linux Security Monitoring

Linux monitoring includes:

```text
Authentication
SSH
Sudo
User Management
Process Activity
File Activity
Services
Cron
Network Connections
System Changes
```

Important sources:

```text
/var/log/auth.log
/var/log/syslog
/var/log/messages
journalctl
auditd
```

The exact locations depend on the Linux distribution and logging configuration.

---

# 6. Network Security Monitoring

Network monitoring focuses on communication between systems.

Monitor:

```text
Source IP
Destination IP
Port
Protocol
DNS
Connection Frequency
Traffic Volume
Network Direction
External Communication
```

Common tools:

```text
Wireshark
tcpdump
Zeek
Suricata
Firewall Logs
SIEM
```

---

# 7. Authentication Monitoring

Authentication events can reveal:

```text
Brute Force
Credential Abuse
Account Compromise
Password Spraying
Privilege Abuse
Unusual Login
Lateral Movement
```

Monitor:

```text
Username
Source IP
Destination
Timestamp
Success / Failure
Authentication Method
Device
Location
```

Example:

```text
Failed Login
      ↓
Multiple Attempts
      ↓
Successful Login
      ↓
Privileged Account
      ↓
Post-Login Activity
```

---

# 8. Endpoint Monitoring

Endpoint monitoring focuses on what happens on individual systems.

Monitor:

```text
Processes
Files
Users
Services
Applications
Network Connections
Persistence
Security Tools
Configuration Changes
```

Important endpoint telemetry:

```text
Process Creation
Parent-Child Relationships
Command Lines
File Creation
File Modification
Network Connections
User Activity
```

---

# 9. Process Monitoring

A SOC analyst should understand:

```text
Process
Parent Process
Child Process
User
Command Line
Executable Path
Timestamp
Network Connection
```

Example:

```text
WINWORD.EXE
      ↓
powershell.exe
      ↓
cmd.exe
      ↓
network connection
```

The relationship between processes can be more informative than the process name alone.

---

# 10. Network Connection Monitoring

Investigate:

```text
Which process created the connection?
Which user owns the process?
Which destination was contacted?
Is the destination expected?
How frequently does it communicate?
What protocol is being used?
```

Example:

```text
Unknown Process
      ↓
External IP
      ↓
Repeated Connections
```

This should trigger further investigation.

---

# 11. DNS Monitoring

DNS is an important source of security telemetry.

Monitor:

```text
Domain
Client
Query Frequency
Response
Rare Domains
New Domains
Unusual Subdomains
External DNS
```

Potential hunting signals include:

```text
Rare Domain
+
High Frequency
+
Suspicious Process
```

---

# 12. Web Monitoring

For web applications and servers monitor:

```text
HTTP Requests
HTTP Methods
Status Codes
Source IP
User-Agent
URLs
Parameters
Authentication
Errors
Response Size
```

Potential indicators:

```text
Repeated 404s
Repeated Authentication Failures
Suspicious Parameters
Unusual User-Agent
Abnormal Request Rate
```

---

# 13. Firewall Monitoring

Firewall telemetry can reveal:

```text
Blocked Connections
Allowed Connections
Port Scanning
Unexpected Outbound Traffic
Unexpected Inbound Traffic
Policy Violations
```

Important fields:

```text
Source
Destination
Port
Protocol
Action
Timestamp
Rule
```

---

# 14. Cloud Monitoring

As organizations move to cloud environments, security monitoring must include:

```text
Identity
API Activity
Authentication
Resource Changes
Network Activity
Configuration Changes
Storage Access
Privilege Changes
```

Examples:

```text
New IAM User
+
Access Key Creation
+
Privilege Change
```

may require investigation.

---

# 15. Application Monitoring

Applications can generate useful security telemetry.

Monitor:

```text
Authentication
Authorization
Errors
Administrative Actions
API Requests
Database Activity
File Uploads
Configuration Changes
```

For web applications:

```text
HTTP Logs
Application Logs
Authentication Logs
WAF Logs
Database Logs
```

---

# 16. Security Telemetry

Security monitoring depends on telemetry.

A useful model:

```text
Telemetry
   ↓
Visibility
   ↓
Detection
   ↓
Investigation
```

Poor telemetry creates:

```text
Blind Spots
```

Good telemetry improves:

```text
Detection
+
Investigation
+
Threat Hunting
```

---

# 17. Monitoring Baselines

Before identifying anomalies, understand normal behavior.

Example:

```text
Normal:
Admin server communicates with backup server
every night.
```

If the same server suddenly communicates with:

```text
Unknown External IP
```

the deviation becomes interesting.

Baseline:

```text
Normal Behavior
      ↓
Expected Pattern
      ↓
Detect Deviation
```

---

# 18. Security Monitoring vs Detection

Monitoring:

```text
"What is happening?"
```

Detection:

```text
"Does this activity match a suspicious pattern?"
```

Example:

```text
Monitoring:
PowerShell executed.

Detection:
PowerShell executed with suspicious encoded
command and external network communication.
```

Monitoring provides visibility.

Detection provides security decisions.

---

# 19. Monitoring vs Alerting

Not every event should generate an alert.

Example:

```text
10,000 normal login events
```

should not necessarily create:

```text
10,000 SOC alerts
```

Good security operations use:

```text
Telemetry
   ↓
Filtering
   ↓
Correlation
   ↓
Detection
   ↓
Alert
```

This reduces alert fatigue.

---

# 20. Monitoring Use Cases

Your portfolio should eventually implement monitoring use cases such as:

```text
01. Brute Force
02. Password Spraying
03. Suspicious Login
04. Privileged Account Activity
05. Suspicious PowerShell
06. Malware Execution
07. New Service
08. Scheduled Task
09. Suspicious Network Connection
10. DNS Anomaly
11. Lateral Movement
12. Data Exfiltration
13. Security Tool Tampering
14. Account Creation
15. Privilege Escalation
```

---

# 21. Security Monitoring Workflow

Use:

```text
Collect
  ↓
Normalize
  ↓
Enrich
  ↓
Monitor
  ↓
Correlate
  ↓
Detect
  ↓
Alert
  ↓
Investigate
  ↓
Respond
```

---

# 22. Home Lab Implementation

Your home lab can provide practical monitoring experience.

Example:

```text
Windows VM
    │
    ├── Windows Event Logs
    └── Sysmon
          │
          ↓
      Wazuh Agent
          │
          ↓
     Wazuh Manager
          │
          ↓
       Dashboard
          │
          ↓
     SOC Investigation
```

You can later add:

```text
Linux VM
Metasploitable
Network Traffic
Firewall
Suricata / Zeek
```

---

# 23. Monitoring Lab Scenarios

Create controlled scenarios such as:

### Scenario 1 — Brute Force

```text
Repeated Failed Login
        ↓
Wazuh
        ↓
Detection
        ↓
Alert
        ↓
Investigation
```

### Scenario 2 — PowerShell

```text
PowerShell Execution
        ↓
Sysmon
        ↓
Wazuh
        ↓
Detection
        ↓
Investigation
```

### Scenario 3 — Suspicious Network Activity

```text
Endpoint
   ↓
External Connection
   ↓
Network Telemetry
   ↓
SIEM
   ↓
Investigation
```

---

# 24. Monitoring Evidence

Every practical exercise should produce evidence.

Store:

```text
Screenshots/
Logs/
Queries/
Detection Rules/
Investigation Notes/
Reports/
MITRE Mappings/
```

Recommended structure:

```text
Security-Monitoring/
│
├── README.md
│
├── Windows/
├── Linux/
├── Network/
├── Authentication/
├── Endpoint/
├── DNS/
├── Web/
├── Firewall/
├── Cloud/
│
├── Labs/
├── Queries/
├── Detection-Evidence/
├── Screenshots/
└── Reports/
```

---

# 25. Portfolio Standard

For every monitoring use case, aim to document:

```text
1. Objective
2. Environment
3. Data Source
4. Telemetry
5. Attack / Simulation
6. Detection
7. Alert
8. Investigation
9. Evidence
10. MITRE ATT&CK
11. Response
12. Lessons Learned
```

This converts a simple lab into professional portfolio evidence.

---

# 26. Security Monitoring Metrics

Useful metrics include:

```text
Events Monitored
Alerts Generated
True Positives
False Positives
Detection Coverage
Mean Time to Detect
Mean Time to Investigate
Mean Time to Respond
Detection Gaps
```

These metrics can later be incorporated into your SOC flagship project.

---

# 27. Interview Preparation

You should be able to answer:

1. What is security monitoring?
2. What is security telemetry?
3. What is the difference between monitoring and detection?
4. What Windows logs are useful to a SOC?
5. What is Sysmon?
6. How would you monitor PowerShell?
7. How would you monitor brute-force attacks?
8. How would you monitor suspicious authentication?
9. How would you monitor network connections?
10. What is a security monitoring use case?
11. Why is baseline behavior important?
12. How does a SIEM help with monitoring?
13. What creates blind spots in monitoring?
14. How would you reduce alert fatigue?
15. What telemetry would you collect during an investigation?

---

# 28. Your Practical Goal

The objective of this section is not simply:

```text
"I studied security monitoring."
```

It should eventually demonstrate:

```text
I can identify
      ↓
what telemetry is required
      ↓
collect it
      ↓
monitor it
      ↓
identify suspicious behavior
      ↓
investigate it
      ↓
create/improve detections
      ↓
document the result
```

That is the transition from **SOC theory to practical SOC capability**.

---

# 29. Future Expansion

As your skills progress, this section can expand into:

```text
Security Monitoring
│
├── L1 Monitoring
├── L2 Investigation
├── L3 Advanced Monitoring
├── Threat Hunting
├── Detection Engineering
├── Network Detection
├── Endpoint Detection
├── Cloud Detection
└── Automated Monitoring
```

The long-term objective is to make the repository demonstrate a progression from:

```text
SOC L1
   ↓
SOC L2
   ↓
SOC L3
   ↓
Detection Engineering
   ↓
Threat Hunting
   ↓
Security Automation
```

---

## Key Principle

> **You cannot detect what you cannot see.**

Security monitoring therefore forms the foundation between your **SOC fundamentals** and the more advanced capabilities you will build later: **SIEM, detection engineering, threat intelligence, threat hunting, incident response, DFIR, automation, and your flagship SOC project.**
