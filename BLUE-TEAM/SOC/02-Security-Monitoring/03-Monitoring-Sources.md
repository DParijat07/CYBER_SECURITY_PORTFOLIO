# Monitoring Sources

> **Blue Team → SOC → Security Monitoring**

Monitoring sources are the systems, devices, applications, security controls, and services that generate security-relevant telemetry.

A SOC analyst cannot investigate what the organization cannot observe. Therefore, understanding **where security telemetry comes from** is fundamental to effective security monitoring.

The basic relationship is:

```text
Monitoring Source
       ↓
Security Event
       ↓
Telemetry / Log
       ↓
Collection
       ↓
SIEM
       ↓
Detection
       ↓
Alert
       ↓
Investigation
```

---

# 1. Objectives

After completing this section, you should understand:

* What monitoring sources are
* Major categories of security telemetry
* Endpoint sources
* Network sources
* Identity sources
* Application sources
* Database sources
* Cloud sources
* Security-control sources
* Email sources
* Authentication sources
* Vulnerability-management sources
* Threat-intelligence sources
* Typical SOC use cases for each source
* Strengths and limitations of different telemetry sources

---

# 2. What Is a Monitoring Source?

A monitoring source is any system or security control that produces information useful for detecting, investigating, or responding to security events.

Examples:

```text
Windows
Linux
Firewall
IDS/IPS
DNS
Proxy
EDR
VPN
Active Directory
Cloud
Applications
Databases
Email
WAF
```

A single security incident may involve multiple sources.

Example:

```text
Email
  ↓
User Click
  ↓
Endpoint
  ↓
PowerShell
  ↓
DNS
  ↓
External Connection
  ↓
Firewall
```

A SOC needs visibility across this chain.

---

# 3. Major Monitoring Source Categories

```text
                    MONITORING SOURCES
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
    Endpoint            Network             Identity
       │                   │                   │
 Windows / Linux       Firewall / DNS       AD / IAM
 EDR / Sysmon          IDS / Proxy          VPN / SSO
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ↓
                    Applications
                           │
                 Web / API / Database
                           │
                           ↓
                         Cloud
                           │
              Audit / IAM / Network / Storage
                           │
                           ↓
                     Security Tools
                           │
             WAF / AV / DLP / Vulnerability
                           │
                           ↓
                          SIEM
```

---

# 4. Endpoint Sources

Endpoints are one of the most important sources of security telemetry.

Examples:

```text
Windows Workstations
Windows Servers
Linux Servers
macOS
Virtual Machines
Laptops
```

Endpoint telemetry may include:

```text
Process Creation
File Activity
Registry Changes
User Activity
Network Connections
Service Creation
Scheduled Tasks
Command Execution
Authentication
```

---

# 5. Windows Event Logs

Windows generates multiple categories of security-relevant events.

Important sources include:

```text
Security
System
Application
PowerShell
Windows Defender
Task Scheduler
```

Examples of security-relevant events:

```text
4624 → Successful Logon
4625 → Failed Logon
4688 → Process Creation
4720 → User Account Created
4728 → User Added to Security Group
```

These events can support detection of:

```text
Brute Force
Account Creation
Privilege Abuse
Suspicious Processes
Lateral Movement
```

---

# 6. Sysmon

Sysmon provides detailed Windows telemetry.

It can monitor activities such as:

```text
Process Creation
Network Connections
File Creation
Process Termination
DNS Queries
Registry Activity
Driver Loading
```

Example:

```text
User
 ↓
PowerShell
 ↓
Process Creation
 ↓
Network Connection
 ↓
Sysmon
 ↓
SIEM
```

Sysmon is particularly useful for endpoint detection and investigation.

---

# 7. Linux Sources

Linux systems generate multiple logs.

Common locations include:

```text
/var/log/auth.log
/var/log/syslog
/var/log/messages
```

Modern Linux systems may also use:

```text
journalctl
systemd-journald
auditd
```

Useful telemetry includes:

```text
SSH Authentication
sudo Usage
Process Activity
Service Activity
System Events
User Activity
```

---

# 8. Authentication Sources

Authentication systems are high-value monitoring sources.

Examples:

```text
Active Directory
LDAP
SSO
VPN
IAM
MFA
Identity Providers
```

Monitor:

```text
Successful Login
Failed Login
Password Change
MFA Failure
Account Lockout
Privilege Change
New Account
Group Membership
```

---

# 9. Active Directory

Active Directory provides valuable identity telemetry.

Monitor events involving:

```text
User Accounts
Computer Accounts
Groups
Kerberos
NTLM
Authentication
Privilege Changes
Domain Controllers
```

Potential detections:

```text
Password Spraying
Brute Force
Account Creation
Privilege Escalation
Suspicious Authentication
Lateral Movement
```

Domain Controllers are therefore critical monitoring sources.

---

# 10. VPN Sources

VPN systems provide visibility into remote access.

Typical fields:

```text
Username
Source IP
Destination
Login Time
Logout Time
Authentication Result
Device
Location
```

Useful detections:

```text
Repeated Failed Login
Unusual Location
Impossible Travel
Compromised Account
After-Hours Access
```

---

# 11. Network Sources

Network infrastructure provides visibility into communication.

Common sources:

```text
Firewall
Router
Switch
IDS
IPS
Proxy
DNS
NetFlow
Network Sensors
```

Network telemetry can reveal:

```text
Scanning
C2 Communication
Malware Traffic
Data Exfiltration
Unauthorized Services
Suspicious Connections
```

---

# 12. Firewall Logs

Firewalls can record:

```text
Source IP
Destination IP
Source Port
Destination Port
Protocol
Action
Bytes
Timestamp
```

Example:

```text
10.0.0.15
     ↓
203.0.113.50:4444
     ↓
DENIED
```

Firewall monitoring can help identify:

```text
Port Scanning
Blocked Connections
Unexpected Outbound Traffic
Unauthorized Services
Suspicious External Communication
```

---

# 13. IDS/IPS

Intrusion Detection and Prevention Systems monitor network activity for known malicious patterns or suspicious behavior.

Examples:

```text
Suricata
Snort
```

IDS:

```text
Detect
 ↓
Alert
```

IPS:

```text
Detect
 ↓
Block / Prevent
```

Typical telemetry:

```text
Source
Destination
Protocol
Signature
Rule
Severity
Timestamp
Action
```

---

# 14. DNS Monitoring

DNS is a valuable source for detecting suspicious activity.

Monitor:

```text
Domain
Source Host
Query Type
Response
Frequency
Timestamp
```

Potential detections:

```text
Malicious Domains
DNS Tunneling
DGA Domains
Command-and-Control
Suspicious Newly Registered Domains
```

Example:

```text
Endpoint
   ↓
Repeated DNS Queries
   ↓
Random-Looking Domains
   ↓
Threat Intelligence Match
   ↓
Investigation
```

---

# 15. Proxy Logs

Web proxies provide visibility into outbound web activity.

Typical fields:

```text
User
Source IP
URL
Domain
HTTP Method
Status Code
Bytes
User Agent
Timestamp
```

Useful for detecting:

```text
Malicious Websites
Phishing
Command & Control
Unauthorized Downloads
Data Exfiltration
```

---

# 16. Web Application Sources

Web applications generate important security telemetry.

Examples:

```text
Web Server Logs
Application Logs
API Logs
WAF Logs
Authentication Logs
```

Monitor:

```text
HTTP Requests
Response Codes
Authentication
File Uploads
Administrative Actions
API Calls
Errors
```

---

# 17. Web Server Logs

Common web servers:

```text
Apache
Nginx
IIS
```

Typical fields:

```text
Timestamp
Client IP
HTTP Method
URI
Status Code
User Agent
Response Size
```

Example:

```text
GET /login
POST /login
GET /admin
GET /api/users
```

Patterns may reveal:

```text
Scanning
Brute Force
Path Enumeration
Exploitation Attempts
```

---

# 18. WAF Logs

A Web Application Firewall monitors HTTP traffic and applies security rules.

Monitor:

```text
SQL Injection
XSS
Path Traversal
Malicious Requests
Bot Activity
Rate Limiting
Blocked Requests
```

Example:

```text
Internet
   ↓
WAF
   ↓
Suspicious HTTP Request
   ↓
Blocked
   ↓
WAF Log
   ↓
SIEM
```

---

# 19. API Monitoring

Modern applications heavily depend on APIs.

Monitor:

```text
API Endpoint
User
Token
Source IP
HTTP Method
Response
Status Code
Request Frequency
```

Potential detections:

```text
API Abuse
Credential Abuse
Broken Authentication
Enumeration
Excessive Requests
Unauthorized Access
```

---

# 20. Database Monitoring

Databases contain highly sensitive information.

Sources may include:

```text
Database Audit Logs
Authentication Logs
Query Logs
Administrative Logs
```

Monitor:

```text
Login
Query
Data Access
Privilege Changes
Schema Changes
Administrative Actions
```

Potential detections:

```text
Unauthorized Data Access
Privilege Abuse
Mass Data Extraction
Suspicious Administrative Activity
```

---

# 21. Email Security Sources

Email is a major attack vector.

Monitoring sources include:

```text
Email Gateway
Microsoft 365
Google Workspace
Email Security Platform
Mail Server
```

Monitor:

```text
Sender
Recipient
Subject
Attachment
URL
Delivery Status
Authentication Results
```

Potential detections:

```text
Phishing
Malware
Business Email Compromise
Credential Theft
Malicious Attachments
```

---

# 22. Endpoint Security Tools

Security products themselves generate telemetry.

Examples:

```text
Antivirus
EDR
XDR
Host Firewall
DLP
Application Control
```

Telemetry may include:

```text
Malware Detection
Process Activity
File Quarantine
Network Activity
Behavioral Detection
Policy Violation
```

EDR is particularly valuable because it provides endpoint context.

---

# 23. Antivirus Telemetry

Antivirus systems can report:

```text
Detection
File
Hash
Process
User
Host
Action
Severity
```

Example:

```text
Malicious File
   ↓
AV Detection
   ↓
Quarantine
   ↓
Alert
   ↓
SIEM
```

---

# 24. EDR Telemetry

EDR platforms can provide rich endpoint information.

Typical telemetry:

```text
Process Tree
Command Line
File Hash
Network Connection
Parent Process
User
Host
Registry Activity
Persistence Mechanisms
```

Example:

```text
winword.exe
     ↓
powershell.exe
     ↓
encoded command
     ↓
external connection
```

This context can significantly improve investigation.

---

# 25. Cloud Monitoring Sources

Cloud environments provide specialized telemetry.

Examples:

```text
AWS CloudTrail
Azure Activity Logs
Microsoft Entra ID Logs
Google Cloud Audit Logs
Cloud Firewall Logs
Cloud DNS
Cloud Storage Logs
```

Monitor:

```text
IAM
API Calls
Resource Creation
Resource Deletion
Configuration Changes
Storage Access
Network Changes
```

---

# 26. Cloud IAM Sources

Identity is central to cloud security.

Monitor:

```text
Login
MFA
Access Key
Role Assumption
Permission Changes
Account Creation
Privilege Changes
```

Example:

```text
User
 ↓
Unusual Login
 ↓
Access Key Created
 ↓
Privilege Escalation
 ↓
Sensitive Resource Access
```

This sequence should be investigated.

---

# 27. Cloud Storage Sources

Monitor access to:

```text
Object Storage
File Storage
Databases
Backups
Sensitive Data
```

Potential detections:

```text
Mass Download
Public Exposure
Unusual Access
Unauthorized Account
Large Data Transfer
```

---

# 28. Vulnerability Management Sources

Vulnerability scanners provide security posture information.

Examples:

```text
Nessus
OpenVAS
Qualys
Rapid7
```

They can provide:

```text
Vulnerability
Asset
CVSS
Affected Service
Evidence
Remediation
```

This telemetry can enrich SOC investigations.

Example:

```text
Suspicious Activity
      +
Known Vulnerable Host
      ↓
Higher Investigation Priority
```

---

# 29. Asset Inventory Sources

Security monitoring needs to know what assets exist.

Sources:

```text
CMDB
Asset Management
Cloud Inventory
Network Discovery
Endpoint Management
```

Useful information:

```text
Hostname
IP
Owner
Operating System
Business Criticality
Location
Installed Software
```

Asset context improves alert prioritization.

---

# 30. Threat Intelligence Sources

Threat intelligence provides external context.

Examples:

```text
Malicious IP
Malicious Domain
File Hash
URL
Threat Actor
Campaign
TTP
```

Example:

```text
Observed IP
    ↓
Threat Intelligence Lookup
    ↓
Known Malicious
    ↓
Alert Enrichment
```

Threat intelligence should be treated as context, not automatic proof of compromise.

---

# 31. Security Control Sources

Almost every security control can become a monitoring source.

```text
Firewall
IDS/IPS
WAF
EDR
DLP
Antivirus
Email Gateway
VPN
IAM
MFA
CASB
NAC
```

The SOC can aggregate telemetry from these controls into a central platform.

---

# 32. Physical and Environmental Sources

In larger environments, physical security systems may also contribute to security monitoring.

Examples:

```text
Badge Access
Door Controllers
CCTV
Data Center Sensors
```

Example:

```text
Badge Access
+
VPN Login
+
Unusual Time
```

may provide useful investigative context.

---

# 33. Application and Business Sources

Security incidents can also be detected through business activity.

Examples:

```text
Transaction Systems
HR Systems
ERP
CRM
Payment Systems
```

Monitor for:

```text
Unusual Transactions
Privilege Abuse
Mass Data Access
Account Misuse
```

Security monitoring therefore extends beyond traditional security tools.

---

# 34. Monitoring Source → Security Value

| Source                | Primary Visibility               |
| --------------------- | -------------------------------- |
| Windows Logs          | Authentication & system activity |
| Sysmon                | Detailed endpoint behavior       |
| Linux Logs            | Linux activity                   |
| EDR                   | Endpoint behavior                |
| Firewall              | Network connections              |
| IDS/IPS               | Network threats                  |
| DNS                   | Domain activity                  |
| Proxy                 | Web activity                     |
| WAF                   | Web attacks                      |
| VPN                   | Remote access                    |
| AD                    | Identity activity                |
| IAM                   | Cloud identity                   |
| Email                 | Phishing & email threats         |
| Database              | Data access                      |
| Cloud Audit           | Cloud activity                   |
| Vulnerability Scanner | Security weaknesses              |
| Threat Intelligence   | External threat context          |
| Asset Inventory       | Asset context                    |

---

# 35. One Event, Multiple Sources

A major advantage of centralized monitoring is correlation.

Consider a phishing attack:

```text
Email Gateway
      ↓
Malicious Email
      ↓
Endpoint
      ↓
Browser
      ↓
PowerShell
      ↓
DNS
      ↓
Firewall
      ↓
External IP
```

The individual events may exist in different systems.

A SIEM can correlate them.

```text
Email
 +
Endpoint
 +
DNS
 +
Network
 =
Attack Story
```

---

# 36. Source Reliability

Not every source is equally reliable.

Consider:

```text
Source A
"User logged in."

Source B
"User logged in from IP X,
using device Y,
at time Z."
```

Source B provides more context.

However, richer telemetry may also create:

```text
Higher Storage
Higher Processing
Higher Cost
More Noise
```

Monitoring architecture therefore requires balancing:

```text
Visibility
+
Cost
+
Performance
+
Risk
```

---

# 37. Source Prioritization

Not every organization needs every possible log.

Prioritize sources based on:

```text
Asset Criticality
Threat Exposure
Business Risk
Attack Surface
Compliance
Detection Requirements
Incident History
```

For example:

```text
Critical Server
      ↓
High Monitoring Priority
```

while:

```text
Low-Risk Test System
      ↓
Lower Priority
```

---

# 38. Minimum Monitoring Sources for a Small Organization

A basic environment should ideally have visibility into:

```text
Endpoints
Authentication
Firewall
DNS
Network
Email
Critical Applications
Cloud
```

For a SOC lab, start smaller:

```text
Windows
Linux
Firewall / Network
Authentication
Wazuh
```

Then expand.

---

# 39. Your Home-Lab Monitoring Sources

Your current lab can demonstrate:

```text
Windows 11 Host
        │
        ├── Windows VM
        │      ├── Windows Events
        │      └── Sysmon
        │
        ├── Kali Linux
        │      └── Linux Telemetry
        │
        ├── Metasploitable 2
        │      └── Service / System Logs
        │
        └── Wazuh
               ├── Agent Data
               ├── Detection
               └── Alerts
```

Later you can add:

```text
Suricata
Zeek
Nessus
Cloud Logs
```

---

# 40. Monitoring Source Mapping

For every source in your portfolio, document:

```text
Source Name
Purpose
Telemetry Generated
Important Fields
Collection Method
Detection Opportunities
Example Attack
Example Alert
Limitations
```

Example:

```text
Source:
Sysmon

Purpose:
Endpoint visibility

Telemetry:
Process + Network + File Activity

Detection:
Suspicious PowerShell

Attack:
Malware Execution

Evidence:
Sysmon Event + SIEM Alert
```

---

# 41. Monitoring Source Health

A source is useful only when it is actually generating telemetry.

Monitor:

```text
Agent Online
Event Rate
Last Event
Collection Errors
Parsing Errors
Storage
Connectivity
```

Example:

```text
Windows Endpoint
     ↓
Expected: 500 events/hour
Actual: 0
     ↓
Monitoring Gap
```

The absence of telemetry can itself be a security concern.

---

# 42. Common Monitoring Gaps

Common problems include:

```text
Missing Logs
Disabled Logging
Agent Offline
Incorrect Configuration
Insufficient Retention
Unparsed Logs
Missing Cloud Logs
Unmonitored Assets
Clock Synchronization Problems
```

A mature SOC regularly performs **telemetry coverage reviews**.

---

# 43. Source-to-Detection Mapping

A strong SOC maps monitoring sources to detection requirements.

Example:

| Detection                  | Primary Source                      |
| -------------------------- | ----------------------------------- |
| Brute Force                | Authentication logs                 |
| Suspicious PowerShell      | Sysmon / EDR                        |
| Port Scan                  | Firewall / IDS                      |
| DNS Tunneling              | DNS                                 |
| Phishing                   | Email Gateway                       |
| Web Attack                 | WAF / Web Logs                      |
| Cloud Privilege Escalation | Cloud IAM                           |
| Malware                    | EDR / Antivirus                     |
| Data Exfiltration          | Proxy / Firewall / DLP              |
| Lateral Movement           | Endpoint + Authentication + Network |

This is the beginning of **detection coverage engineering**.

---

# 44. Practical Lab Exercise

## Lab: Identify Your Monitoring Sources

### Objective

Identify every available security telemetry source in your home lab.

### Step 1 — Inventory

Document:

```text
Windows
Kali
Metasploitable
Wazuh
Network
```

### Step 2 — Identify Telemetry

For each system:

```text
What logs exist?
What events are generated?
What security information is available?
```

### Step 3 — Connect Sources

Where possible:

```text
Endpoint
   ↓
Agent
   ↓
Wazuh
```

### Step 4 — Generate Activity

Perform controlled activities:

```text
Login
Failed Login
Process Execution
Network Connection
File Creation
```

### Step 5 — Observe

Find the corresponding telemetry in Wazuh.

### Step 6 — Document

Record:

```text
Source
Event
Timestamp
User
Host
Detection
Evidence
```

---

# 45. Portfolio Evidence

For this topic, maintain:

```text
Screenshots/
    ├── Windows-Events/
    ├── Sysmon/
    ├── Linux-Logs/
    ├── Wazuh/
    └── Network/

Queries/
    ├── Authentication.md
    ├── Process-Monitoring.md
    └── Network-Monitoring.md

Reports/
    └── Monitoring-Source-Assessment.md
```

The goal is to demonstrate that you can identify **real telemetry sources**, not simply list them.

---

# 46. Interview Questions

### Fundamentals

1. What is a monitoring source?
2. What are common SOC data sources?
3. Why are Windows Event Logs important?
4. What is Sysmon?
5. What is EDR telemetry?
6. What information can firewall logs provide?
7. Why is DNS useful for security monitoring?
8. What information does a VPN log provide?
9. What is the importance of Active Directory logs?
10. What is cloud audit logging?

### Scenario

**Question:**

> An analyst receives a suspicious login alert. Which monitoring sources would you check?

A strong answer:

```text
Authentication Logs
       ↓
AD / IAM
       ↓
VPN
       ↓
Endpoint
       ↓
Firewall
       ↓
DNS
       ↓
Threat Intelligence
```

Then correlate:

```text
User
Source IP
Device
Time
Location
Authentication Method
Related Activity
```

---

# 47. Key Takeaways

```text
1. Monitoring sources generate security telemetry.

2. Endpoints provide host-level visibility.

3. Network devices provide communication visibility.

4. Identity systems provide authentication visibility.

5. Applications provide business and application-level visibility.

6. Cloud systems provide infrastructure and API visibility.

7. Security tools provide specialized detections.

8. Threat intelligence provides external context.

9. Asset inventory provides business context.

10. Multiple sources should be correlated.

11. Missing telemetry creates monitoring blind spots.

12. Monitoring sources should be prioritized according to risk.

13. Source health must itself be monitored.

14. Good monitoring depends on both coverage and context.
```

---

# 48. Final Mental Model

```text
                    MONITORING SOURCES
                           │
        ┌──────────────────┼──────────────────┐
        ↓                  ↓                  ↓
     Endpoint            Network           Identity
        │                  │                  │
   Windows/Linux      Firewall/DNS       AD/IAM/VPN
   Sysmon/EDR         IDS/IPS/Proxy       SSO/MFA
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ↓
                     Applications
                           │
                    Web/API/Database
                           ↓
                          Cloud
                           ↓
                    Security Tools
                           ↓
                          SIEM
                           ↓
                      Correlation
                           ↓
                       Detection
                           ↓
                          Alert
                           ↓
                      Investigation
```

> **A SOC's visibility is only as strong as the quality, coverage, and context of the monitoring sources feeding it.**
