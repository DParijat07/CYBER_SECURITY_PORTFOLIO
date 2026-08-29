# Cyber Kill Chain

> **SOC L1 → L2 Fundamental**

The **Cyber Kill Chain** is a model used to describe the stages an attacker may move through during a cyberattack.

It helps defenders understand:

* How an attack progresses
* Where an attacker can be detected
* Where defensive controls can interrupt the attack
* How multiple alerts can be correlated into an attack story

The traditional Cyber Kill Chain contains **seven stages**:

```text
1. Reconnaissance
       ↓
2. Weaponization
       ↓
3. Delivery
       ↓
4. Exploitation
       ↓
5. Installation
       ↓
6. Command & Control
       ↓
7. Actions on Objectives
```

> **Important:** Real-world attacks do not always follow these stages in a strict linear order.

---

# 1. Why SOC Analysts Learn the Kill Chain

A single alert often provides only a small piece of an attack.

For example:

```text
Alert 1:
Phishing Email

Alert 2:
Malicious Attachment

Alert 3:
PowerShell Execution

Alert 4:
Outbound Connection

Alert 5:
Credential Access
```

Individually, these may look unrelated.

When correlated:

```text
Phishing
   ↓
Malware Execution
   ↓
Command Execution
   ↓
C2
   ↓
Credential Access
```

the SOC can begin to understand the attack lifecycle.

---

# 2. The Seven Stages

```text
RECONNAISSANCE
      ↓
WEAPONIZATION
      ↓
DELIVERY
      ↓
EXPLOITATION
      ↓
INSTALLATION
      ↓
COMMAND & CONTROL
      ↓
ACTIONS ON OBJECTIVES
```

Each stage represents a different point where defenders may detect or disrupt the attacker.

---

# 3. Stage 1 — Reconnaissance

## Objective

The attacker gathers information about the target.

Possible information:

```text
IP Addresses
Domains
Employees
Email Addresses
Technology Stack
Open Ports
Public Services
Cloud Infrastructure
Organizational Information
```

### Example

An attacker researches:

```text
company.com
     ↓
DNS Information
     ↓
Subdomains
     ↓
Public Services
     ↓
Employee Information
```

---

# 4. Reconnaissance Techniques

Examples include:

```text
OSINT
DNS Enumeration
WHOIS
Search Engines
Social Media Research
Port Scanning
Service Enumeration
```

Some reconnaissance activity may occur outside the organization's network.

Therefore:

> **Not all reconnaissance can be detected using internal SIEM telemetry.**

---

# 5. SOC Detection Opportunities

Defenders may monitor:

```text
Unusual DNS Activity
Port Scanning
Web Enumeration
Repeated Connection Attempts
External Reconnaissance
```

Example:

```text
One external IP
      ↓
Scans 500 ports
      ↓
Across multiple hosts
      ↓
Within several minutes
```

This may indicate reconnaissance.

---

# 6. Stage 2 — Weaponization

## Objective

The attacker prepares a malicious payload or attack mechanism.

Examples:

```text
Malware
Backdoor
Malicious Document
Exploit
Payload
Phishing Kit
Malicious Script
```

Conceptually:

```text
Exploit / Payload
       +
Delivery Method
       ↓
Weaponized Attack
```

---

# 7. Important SOC Consideration

Weaponization often happens **before the attack reaches the victim environment**.

Therefore, traditional endpoint telemetry may not show this stage.

Threat intelligence may provide visibility through:

```text
Malware Reports
Threat Actor Reports
Malware Samples
Phishing Campaign Intelligence
Threat Feeds
```

---

# 8. Stage 3 — Delivery

## Objective

The attacker delivers the weaponized payload to the target.

Common delivery methods:

```text
Phishing Email
Malicious Attachment
Malicious Link
Compromised Website
Drive-by Download
USB Device
Network Service
```

Example:

```text
Attacker
   ↓
Phishing Email
   ↓
Employee
   ↓
Malicious Attachment
```

---

# 9. SOC Detection at Delivery

Possible telemetry:

```text
Email Gateway
Email Security
Proxy Logs
DNS Logs
Web Logs
Endpoint Logs
```

Analysts may investigate:

```text
Sender
Recipient
URL
Domain
Attachment
Hash
Email Headers
```

---

# 10. Stage 4 — Exploitation

## Objective

The attacker exploits a vulnerability or takes advantage of user interaction to execute malicious activity.

Examples:

```text
Software Vulnerability
Browser Exploit
Document Exploit
Credential Exploitation
Misconfiguration
User Execution
```

Example:

```text
Malicious Document
       ↓
User Opens File
       ↓
Exploit Executes
       ↓
Malicious Process
```

---

# 11. SOC Detection at Exploitation

Possible indicators:

```text
Unexpected Process Creation
Office Application → PowerShell
Browser → Suspicious Process
Exploit-like Behavior
Abnormal Memory Activity
Unexpected Child Process
```

Example:

```text
WINWORD.EXE
      ↓
powershell.exe
      ↓
network connection
```

This process relationship can be highly valuable to defenders.

---

# 12. Stage 5 — Installation

## Objective

The attacker establishes persistence or installs malicious components.

Examples:

```text
Malware Installation
Scheduled Task
Service Creation
Registry Run Key
Startup Folder
Persistence Mechanism
Backdoor
```

Example:

```text
Malicious File
     ↓
Persistence Mechanism
     ↓
Survives Reboot
```

---

# 13. SOC Detection at Installation

Defenders may monitor:

```text
New Services
Scheduled Tasks
Registry Changes
Startup Entries
New Executables
Suspicious File Creation
Persistence-related Events
```

Example:

```text
Unknown executable
      ↓
Creates scheduled task
      ↓
Runs at system startup
```

This may indicate persistence.

---

# 14. Stage 6 — Command & Control

## Objective

The compromised system communicates with attacker-controlled infrastructure.

This is commonly abbreviated as:

```text
C2
```

or:

```text
C&C
```

---

# 15. Common C2 Channels

Examples include:

```text
HTTP/HTTPS
DNS
SSH
Email
Web Services
Custom Protocols
```

Attackers may attempt to make C2 traffic resemble normal traffic.

---

# 16. SOC Detection at C2

Network defenders may look for:

```text
Repeated Outbound Connections
Beaconing
Unusual Domains
Rare DNS Requests
Suspicious IPs
Abnormal Ports
Long-lived Connections
Unexpected External Communication
```

Example:

```text
Host
 ↓
Connection
 ↓
Wait
 ↓
Connection
 ↓
Wait
 ↓
Connection
```

Repeated periodic communication may be suspicious.

---

# 17. Beaconing

**Beaconing** refers to repeated communication between a compromised system and external infrastructure.

Conceptually:

```text
10:00 → C2
10:05 → C2
10:10 → C2
10:15 → C2
10:20 → C2
```

Regular timing can be an indicator of automated communication.

However:

> Periodic traffic alone does not prove malicious activity.

Context is required.

---

# 18. Stage 7 — Actions on Objectives

## Objective

The attacker executes the final goal of the operation.

Possible objectives:

```text
Data Theft
Financial Fraud
Credential Theft
Ransomware
Espionage
Destruction
Persistence
Resource Hijacking
Business Disruption
```

---

# 19. Example: Data Theft

```text
Compromise
    ↓
Discovery
    ↓
Identify Sensitive Data
    ↓
Collect Data
    ↓
Compress Data
    ↓
Exfiltrate
```

SOC telemetry might include:

```text
Large Outbound Transfer
Unusual Destination
Archive Creation
Cloud Upload
Rare Protocol Usage
```

---

# 20. Example: Ransomware

```text
Initial Access
      ↓
Execution
      ↓
Persistence
      ↓
Privilege Escalation
      ↓
Lateral Movement
      ↓
File Encryption
      ↓
Impact
```

Possible defensive telemetry:

```text
Mass File Modification
Shadow Copy Deletion
Suspicious Process Execution
Credential Access
Lateral Movement
High Volume File Writes
```

---

# 21. Kill Chain as a Defensive Model

The biggest value of the model is:

> **Break the attack at the earliest practical stage.**

Example:

```text
Reconnaissance
      ↓
     BLOCK
```

or:

```text
Delivery
      ↓
Email Security
      ↓
     BLOCK
```

or:

```text
Exploitation
      ↓
Endpoint Detection
      ↓
     BLOCK
```

or:

```text
C2
      ↓
Network Detection
      ↓
     BLOCK
```

Multiple defensive layers create multiple opportunities to stop the attack.

---

# 22. Detection Opportunities

| Kill Chain Stage | Example Evidence      | Defensive Control   |
| ---------------- | --------------------- | ------------------- |
| Reconnaissance   | Scanning              | IDS/Firewall        |
| Weaponization    | Malware intelligence  | Threat Intelligence |
| Delivery         | Phishing email        | Email Security      |
| Exploitation     | Exploit behavior      | EDR/IPS             |
| Installation     | Persistence           | EDR                 |
| C2               | Beaconing             | Network Monitoring  |
| Actions          | Data theft/ransomware | DLP/EDR/SIEM        |

---

# 23. Kill Chain Investigation Example

Imagine the SOC receives:

```text
Alert 1:
Malicious Email

Alert 2:
User Opened Attachment

Alert 3:
PowerShell Execution

Alert 4:
Suspicious External Connection

Alert 5:
Large Data Transfer
```

Map them:

```text
Delivery
   ↓
Exploitation / Execution
   ↓
Command & Control
   ↓
Actions on Objectives
```

Now the SOC has an attack narrative rather than isolated alerts.

---

# 24. Kill Chain vs IOC/IOA/TTP

These concepts complement each other.

```text
Cyber Kill Chain
      ↓
WHEN in the attack lifecycle?
```

```text
IOC
      ↓
WHAT artifact indicates compromise?
```

```text
IOA
      ↓
WHAT suspicious behavior is occurring?
```

```text
TTP
      ↓
HOW does the attacker operate?
```

Together:

```text
Attack Stage
     +
IOC
     +
IOA
     +
TTP
     ↓
Attack Story
```

---

# 25. Kill Chain vs MITRE ATT&CK

These frameworks are related but different.

### Cyber Kill Chain

Focuses on:

> **Stages of an attack**

### MITRE ATT&CK

Focuses on:

> **Adversary tactics and techniques**

Simplified:

```text
Cyber Kill Chain
       ↓
Attack Lifecycle

MITRE ATT&CK
       ↓
Adversary Behavior
```

A SOC analyst can use both.

---

# 26. Example Mapping

Consider malicious PowerShell execution.

### Kill Chain

```text
Exploitation
     ↓
Execution
```

### IOC

```text
Malicious IP
```

### IOA

```text
Encoded PowerShell
+
Suspicious parent process
```

### MITRE ATT&CK

```text
Execution
   ↓
Command and Scripting Interpreter:
PowerShell
```

This provides multiple analytical perspectives.

---

# 27. Limitations of the Kill Chain

The traditional model has limitations.

Real attacks may:

* Skip stages
* Repeat stages
* Run stages simultaneously
* Start with compromised credentials
* Begin with an existing foothold
* Move laterally before persistence
* Use legitimate tools
* Operate across cloud environments

Therefore:

> **Do not force every incident into a perfect seven-stage sequence.**

Use the model as an analytical aid.

---

# 28. SOC L1 Application

As an L1 analyst, you do not need to perform an advanced kill-chain analysis for every alert.

But you should recognize:

```text
Delivery
Execution
Persistence
C2
Impact
```

and understand when multiple alerts may represent different stages of the same attack.

---

# 29. SOC L1 Investigation Example

### Alert

```text
Suspicious PowerShell Execution
```

L1 should ask:

```text
What executed PowerShell?
        ↓
Who executed it?
        ↓
What command was executed?
        ↓
Was a file downloaded?
        ↓
Was there network communication?
        ↓
Was persistence created?
        ↓
Are there other related alerts?
```

These questions help determine where the activity fits within the attack lifecycle.

---

# 30. Practical Home Lab

Use:

```text
Kali Linux
      +
Windows VM
      +
Sysmon
      +
Wazuh
```

Generate controlled activity such as:

```text
PowerShell Execution
        ↓
File Creation
        ↓
Scheduled Task
        ↓
Network Connection
```

Collect the resulting telemetry.

Then create an attack timeline:

```text
T+00
PowerShell executed

T+01
File created

T+02
Scheduled task created

T+03
Outbound connection
```

Map the activity to:

```text
Kill Chain
+
IOC
+
IOA
+
TTP
+
MITRE ATT&CK
```

---

# 31. Portfolio Exercise

Create:

```text
Cyber-Kill-Chain-Lab/
│
├── README.md
├── Scenario.md
├── Attack-Timeline.md
├── Kill-Chain-Mapping.md
├── IOC-List.md
├── IOA-Analysis.md
├── MITRE-Mapping.md
├── Detection.md
├── Investigation.md
├── Recommendations.md
└── Screenshots/
```

This can later become one of your SOC case studies.

---

# 32. Interview Questions

You should be able to answer:

### Fundamentals

1. What is the Cyber Kill Chain?
2. Who developed the traditional Cyber Kill Chain?
3. What are the seven stages?
4. Why is the Kill Chain useful for defenders?
5. What is reconnaissance?
6. What is weaponization?
7. What is C2?

### SOC

8. How can a SOC use the Kill Chain?
9. How can you identify C2 activity?
10. How can you detect persistence?
11. How can phishing fit into the Kill Chain?
12. What is the difference between Kill Chain and MITRE ATT&CK?

### Practical

13. How would you map a phishing incident?
14. How would you investigate suspicious PowerShell?
15. How would you identify where an attacker is in the Kill Chain?
16. Can an attacker skip Kill Chain stages?

---

# 33. Key Takeaway

```text
RECONNAISSANCE
       ↓
WEAPONIZATION
       ↓
DELIVERY
       ↓
EXPLOITATION
       ↓
INSTALLATION
       ↓
COMMAND & CONTROL
       ↓
ACTIONS ON OBJECTIVES
```

The SOC analyst's goal is not simply to identify that an attack happened.

The analyst should understand:

```text
WHERE
the attacker is in the lifecycle

WHAT
evidence exists

HOW
the attacker is operating

WHAT
has already happened

WHAT
may happen next
```

> **The Cyber Kill Chain gives the SOC a way to turn individual security events into an attack lifecycle.**
