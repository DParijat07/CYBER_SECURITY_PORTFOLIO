# MITRE ATT&CK Fundamentals

> **SOC L1 → L2 Fundamental**

**MITRE ATT&CK** is a globally used knowledge base of adversary behaviors based on real-world observations.

For a SOC analyst, ATT&CK provides a structured way to understand:

* What attackers are trying to achieve
* How they perform those activities
* Which behaviors can be detected
* Which security controls can detect or prevent them
* How incidents can be mapped to standardized techniques

---

# 1. What Does ATT&CK Mean?

**ATT&CK** stands for:

> **Adversarial Tactics, Techniques, and Common Knowledge**

It is maintained by **MITRE**.

The framework organizes adversary behavior into:

```text
TACTICS
   ↓
TECHNIQUES
   ↓
SUB-TECHNIQUES
   ↓
PROCEDURES
```

A simplified view:

```text
WHY?
 ↓
TACTIC

HOW?
 ↓
TECHNIQUE

MORE SPECIFIC HOW?
 ↓
SUB-TECHNIQUE

HOW EXACTLY?
 ↓
PROCEDURE
```

---

# 2. Why SOC Analysts Use MITRE ATT&CK

A SOC receives alerts such as:

```text
Suspicious PowerShell
Credential Dumping
Scheduled Task Creation
Remote Login
Unusual DNS Traffic
```

Without a framework, analysts may describe them differently.

ATT&CK provides a common language.

For example:

```text
Suspicious PowerShell
        ↓
Execution
        ↓
Command and Scripting Interpreter
        ↓
PowerShell
```

This makes investigations and reporting more standardized.

---

# 3. Tactics

A **tactic** represents the attacker's objective.

Think:

> **"Why is the attacker performing this activity?"**

Common ATT&CK Enterprise tactics include:

```text
Reconnaissance
Resource Development
Initial Access
Execution
Persistence
Privilege Escalation
Defense Evasion
Credential Access
Discovery
Lateral Movement
Collection
Command and Control
Exfiltration
Impact
```

Not every incident contains every tactic.

---

# 4. Initial Access

### Objective

Gain access to the target environment.

Examples include:

```text
Phishing
Exploit Public-Facing Application
Valid Accounts
External Remote Services
Drive-by Compromise
```

Example:

```text
Attacker
   ↓
Phishing Email
   ↓
Victim
   ↓
Initial Access
```

---

# 5. Execution

### Objective

Execute malicious code or commands.

Examples:

```text
PowerShell
Command Shell
Python
JavaScript
User Execution
Scheduled Task/Job
```

Example:

```text
Malicious Document
      ↓
PowerShell
      ↓
Payload Execution
```

---

# 6. Persistence

### Objective

Maintain access after initial compromise.

Examples:

```text
Scheduled Task/Job
Services
Registry Run Keys
Startup Items
Account Manipulation
Create or Modify System Process
```

Example:

```text
Malware
   ↓
Scheduled Task
   ↓
Runs automatically
```

---

# 7. Privilege Escalation

### Objective

Obtain higher privileges.

Example:

```text
Standard User
     ↓
Privilege Escalation
     ↓
Administrator / SYSTEM
```

Potential methods include:

```text
Exploiting Vulnerabilities
Misconfigured Permissions
Credential Abuse
Abusing Services
```

---

# 8. Defense Evasion

### Objective

Avoid detection or security controls.

Examples:

```text
Obfuscated Files
PowerShell Obfuscation
Disable Security Tools
Clear Windows Event Logs
Masquerading
File Deletion
```

Example:

```text
Malicious Command
      ↓
Obfuscation
      ↓
Reduced Visibility
```

---

# 9. Credential Access

### Objective

Obtain credentials.

Examples:

```text
Credential Dumping
Password Stores
Input Capture
Brute Force
OS Credential Dumping
Steal Web Session Cookie
```

Example:

```text
Compromised Host
      ↓
Credential Access
      ↓
Account Credentials
```

---

# 10. Discovery

### Objective

Understand the environment.

Attackers may discover:

```text
Users
Processes
Network Configuration
Systems
Services
Security Software
Domain Information
```

Example:

```text
Attacker
   ↓
Who am I?
   ↓
Who else exists?
   ↓
What systems exist?
   ↓
Where are valuable targets?
```

---

# 11. Lateral Movement

### Objective

Move from one compromised system to another.

Examples:

```text
Remote Services
SMB
RDP
SSH
Valid Accounts
Windows Admin Shares
```

Example:

```text
Workstation A
      ↓
Compromised Credentials
      ↓
Server B
```

---

# 12. Collection

### Objective

Gather information of interest.

Examples:

```text
Documents
Emails
Database Information
Screenshots
Clipboard Data
Browser Data
Archives
```

Example:

```text
Sensitive Files
      ↓
Collection
      ↓
Archive
```

---

# 13. Command & Control

### Objective

Communicate with compromised systems.

Examples:

```text
Application Layer Protocol
Web Protocols
DNS
Remote Access Software
Proxy
Encrypted Channel
```

Example:

```text
Compromised Host
      ↓
HTTPS
      ↓
Attacker Infrastructure
```

---

# 14. Exfiltration

### Objective

Steal data from the target environment.

Examples:

```text
Exfiltration Over Web Service
Exfiltration Over C2 Channel
Automated Exfiltration
Scheduled Transfer
```

Example:

```text
Sensitive Data
      ↓
Archive
      ↓
External Service
      ↓
Attacker
```

---

# 15. Impact

### Objective

Cause damage or achieve the final operational goal.

Examples:

```text
Data Destruction
Data Encrypted for Impact
Inhibit System Recovery
Service Stop
Resource Hijacking
```

Ransomware is a classic example.

```text
Compromise
   ↓
Privilege Escalation
   ↓
Lateral Movement
   ↓
Data Encryption
   ↓
Impact
```

---

# 16. Technique

A **technique** explains how an attacker achieves a tactical objective.

Example:

```text
TACTIC:
Execution

TECHNIQUE:
Command and Scripting Interpreter
```

Another:

```text
TACTIC:
Credential Access

TECHNIQUE:
OS Credential Dumping
```

---

# 17. Sub-Technique

A sub-technique provides more specific behavior.

Example:

```text
Command and Scripting Interpreter
             ↓
       PowerShell
```

The more specific classification improves:

* Detection
* Threat hunting
* Reporting
* Threat intelligence
* Security control mapping

---

# 18. Procedure

A **procedure** describes how a real threat actor or malware implements a technique.

Conceptually:

```text
Tactic
   ↓
Technique
   ↓
Sub-Technique
   ↓
Procedure
```

Example:

```text
Execution
   ↓
Command and Scripting Interpreter
   ↓
PowerShell
   ↓
Threat actor executes a PowerShell command
```

The procedure is the practical implementation.

---

# 19. ATT&CK IDs

ATT&CK techniques and sub-techniques have standardized identifiers.

For example:

```text
T1059
```

represents:

```text
Command and Scripting Interpreter
```

A sub-technique may be represented as:

```text
T1059.001
```

representing:

```text
PowerShell
```

These IDs are commonly used in:

* SOC reports
* Detection rules
* SIEM documentation
* Threat intelligence
* Incident response
* Threat hunting
* Security assessments

---

# 20. Example: Suspicious PowerShell

Suppose your SIEM produces:

```text
ALERT:
Encoded PowerShell Command
```

The investigation might identify:

```text
Process:
powershell.exe

Command:
Encoded command

Network:
External connection

File:
Payload downloaded
```

ATT&CK mapping:

```text
Tactic:
Execution

Technique:
Command and Scripting Interpreter

Sub-technique:
PowerShell

ID:
T1059.001
```

---

# 21. Example: Scheduled Task

Suppose you see:

```text
New Scheduled Task
      ↓
Executes suspicious executable
      ↓
Runs every hour
```

Possible ATT&CK mapping:

```text
Tactic:
Persistence

Technique:
Scheduled Task/Job
```

The analyst then investigates:

```text
Who created it?
What executable runs?
When was it created?
What account created it?
Is it authorized?
What network activity follows?
```

---

# 22. Example: Credential Dumping

Suppose EDR detects suspicious access to credential-related processes.

Investigation:

```text
Suspicious Process
      ↓
Credential-related memory access
      ↓
Potential credential dumping
```

Potential mapping:

```text
Tactic:
Credential Access

Technique:
OS Credential Dumping
```

The analyst should then determine:

```text
Host
User
Process
Parent Process
Command Line
Privileges
Related Network Activity
```

---

# 23. ATT&CK and Detection Engineering

ATT&CK is extremely useful when creating detection rules.

Instead of:

```text
Rule:
Suspicious PowerShell
```

document:

```text
Rule:
Suspicious PowerShell Execution

MITRE ATT&CK:
T1059.001

Tactic:
Execution

Data Sources:
Windows Event Logs
Sysmon
EDR

Severity:
High
```

This makes your detection engineering work much more professional.

---

# 24. ATT&CK and SIEM

A SIEM alert can contain:

```text
Alert
   ↓
Detection Rule
   ↓
MITRE Technique
   ↓
Tactic
```

Example:

```text
Alert:
Suspicious PowerShell

Detection:
Encoded PowerShell + unusual parent process

ATT&CK:
T1059.001

Tactic:
Execution
```

This allows SOC teams to understand what attacker behavior a detection covers.

---

# 25. ATT&CK and Threat Hunting

Threat hunting often begins with a behavior hypothesis.

Example:

> "An attacker may be using PowerShell for execution."

Hunter searches:

```text
PowerShell Events
      ↓
Command Lines
      ↓
Parent Processes
      ↓
Users
      ↓
Network Connections
```

Then maps findings to:

```text
T1059.001
```

This provides structured hunting.

---

# 26. ATT&CK and Incident Response

During an incident, analysts can create an ATT&CK timeline:

```text
Initial Access
      ↓
T1566 — Phishing
      ↓
Execution
      ↓
T1059.001 — PowerShell
      ↓
Persistence
      ↓
Scheduled Task
      ↓
Credential Access
      ↓
Credential Dumping
      ↓
C2
      ↓
Application Layer Protocol
```

This gives responders a clearer attack narrative.

---

# 27. ATT&CK vs Cyber Kill Chain

These frameworks answer different questions.

| Cyber Kill Chain            | MITRE ATT&CK                |
| --------------------------- | --------------------------- |
| Attack lifecycle            | Adversary behavior          |
| High-level model            | Detailed knowledge base     |
| 7 traditional stages        | Many tactics/techniques     |
| Good for attack progression | Good for technical analysis |
| Strategic overview          | Operational detail          |

Think:

```text
Kill Chain
   ↓
WHERE are we in the attack?

ATT&CK
   ↓
WHAT behavior is being used?
```

Use them together.

---

# 28. ATT&CK vs IOC

IOC:

```text
Malicious IP:
203.0.113.50
```

ATT&CK:

```text
Behavior:
Command and Control
```

The IOC tells you:

> **What artifact did I observe?**

ATT&CK tells you:

> **What adversary behavior does this represent?**

---

# 29. ATT&CK vs IOA

IOA:

```text
Encoded PowerShell
+
Suspicious parent process
```

ATT&CK:

```text
T1059.001
PowerShell
```

The IOA represents the suspicious behavior.

ATT&CK provides the standardized classification.

---

# 30. ATT&CK Navigator Concept

The **MITRE ATT&CK Navigator** can be used to visualize techniques.

Conceptually:

```text
ATT&CK Enterprise Matrix

Initial Access | Execution | Persistence | ...
       ✓             ✓           ✓
       ✓                         ✓
```

Security teams can use technique coverage to identify:

* Detection gaps
* Visibility gaps
* Control gaps
* Threat hunting priorities

---

# 31. Detection Coverage

Suppose your SOC has:

```text
100 Relevant Techniques
```

but your detection capability covers:

```text
35 Techniques
```

You have a potential detection coverage gap.

The goal is not simply:

> "Cover every ATT&CK technique."

Instead:

> **Prioritize techniques relevant to your organization's threats, technology, and risk.**

---

# 32. ATT&CK Data Sources

Detection depends on telemetry.

Examples:

```text
Windows Event Logs
Sysmon
EDR
Firewall
DNS
Proxy
Authentication Logs
Cloud Logs
Email Security
Network Traffic
```

Conceptually:

```text
ATT&CK Technique
       ↓
Required Evidence
       ↓
Data Source
       ↓
Detection
```

Example:

```text
PowerShell
   ↓
Process Creation / PowerShell Logs
   ↓
Sysmon / Windows Logs / EDR
   ↓
Detection Rule
```

---

# 33. Practical SOC Workflow

When investigating an alert:

```text
ALERT
  ↓
What happened?
  ↓
Collect evidence
  ↓
Identify behavior
  ↓
Identify TTP
  ↓
Map to ATT&CK
  ↓
Determine scope
  ↓
Assess severity
  ↓
Escalate / Respond
```

---

# 34. Practical Home Lab

Your existing lab is enough:

```text
Kali Linux
     +
Windows VM
     +
Sysmon
     +
Wazuh
```

Generate controlled activities:

```text
PowerShell
Scheduled Task
Failed Login
Process Creation
Network Connection
File Creation
```

Collect telemetry.

For each activity document:

```text
Event
IOC
IOA
Tactic
Technique
Sub-Technique
Detection
Evidence
Conclusion
```

---

# 35. Example ATT&CK Investigation

### Scenario

A Windows endpoint generates:

```text
Encoded PowerShell Alert
```

### Evidence

```text
User:
test-user

Process:
powershell.exe

Parent:
winword.exe

Command:
Encoded PowerShell

Network:
External connection
```

### Analysis

```text
Initial Activity:
Malicious document

Execution:
PowerShell

Network:
External communication
```

### ATT&CK Mapping

```text
Execution
   ↓
T1059.001
   ↓
PowerShell
```

Potential additional mappings may be identified after further investigation.

---

# 36. Portfolio Exercise

Create:

```text
MITRE-ATTACK-Lab/
│
├── README.md
├── ATTACK-Mapping.md
├── Detection-Rules/
├── Investigations/
├── Case-Studies/
├── Screenshots/
└── Evidence/
```

Each investigation should contain:

```text
Scenario
↓
Alert
↓
Evidence
↓
Analysis
↓
MITRE Mapping
↓
Detection
↓
Conclusion
```

---

# 37. Recommended Detection Documentation

For each detection rule:

```text
Detection Name:
Suspicious PowerShell Execution

Objective:
Detect potentially malicious PowerShell activity.

MITRE ATT&CK:
T1059.001

Tactic:
Execution

Data Sources:
Sysmon
Windows Event Logs
EDR

Trigger:
Encoded PowerShell + suspicious parent process

Severity:
High

False Positives:
Administrative scripts
Authorized automation

Investigation:
Review parent process,
command line,
user,
network activity,
and child processes.

Response:
Validate activity and escalate if malicious.
```

This format will become useful later when you build your **Detection Engineering** section.

---

# 38. Interview Questions

### Fundamentals

1. What is MITRE ATT&CK?
2. What does ATT&CK stand for?
3. What is a tactic?
4. What is a technique?
5. What is a sub-technique?
6. What is a procedure?
7. What is an ATT&CK technique ID?

### SOC

8. How is ATT&CK used by SOC analysts?
9. How do you map an alert to ATT&CK?
10. How is ATT&CK used in detection engineering?
11. How is ATT&CK used in threat hunting?
12. How can ATT&CK identify detection gaps?

### Practical

13. How would you map suspicious PowerShell?
14. How would you map credential dumping?
15. How would you map scheduled-task persistence?
16. How would you use ATT&CK during incident response?
17. What is the difference between ATT&CK and Cyber Kill Chain?

---

# 39. Key Takeaway

Remember the hierarchy:

```text
ATT&CK
   │
   ├── Tactic
   │      ↓
   │    Why?
   │
   ├── Technique
   │      ↓
   │    How?
   │
   ├── Sub-Technique
   │      ↓
   │    More specific how?
   │
   └── Procedure
          ↓
       How exactly?
```

And remember the SOC workflow:

```text
EVENT
  ↓
ALERT
  ↓
INVESTIGATION
  ↓
BEHAVIOR
  ↓
IOC / IOA
  ↓
MITRE ATT&CK
  ↓
TTP
  ↓
RISK
  ↓
RESPONSE
```

> **MITRE ATT&CK gives the SOC a standardized language for describing adversary behavior and connecting that behavior to detection, investigation, threat hunting, and response.**
