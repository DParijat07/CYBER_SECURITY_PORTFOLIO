# 🛡️ SOC — Security Operations Center

> **A structured SOC learning, detection engineering, incident response, and practical cybersecurity portfolio.**

This directory documents my journey from **SOC Analyst L1 → L2 → L3**, combining theoretical learning, hands-on home-lab exercises, detection engineering, incident investigation, security playbooks, TryHackMe labs, mini-projects, and an AI-assisted flagship SOC project.

The objective is not only to learn SOC concepts, but to build **demonstrable analyst capabilities through practical evidence, documentation, investigation, and repeatable workflows.**

---

## 🎯 Objectives

* Build strong **SOC Analyst L1 fundamentals**
* Progress systematically toward **SOC L2 and L3 capabilities**
* Develop practical **security monitoring and alert triage skills**
* Learn **log analysis and event investigation**
* Develop and test **detection rules**
* Practice **incident response workflows**
* Learn **MITRE ATT&CK-based investigation**
* Build reusable **SOC playbooks**
* Complete and document relevant **TryHackMe SOC/Blue Team labs**
* Build practical **mini-projects**
* Develop an AI-assisted **SOC flagship project**
* Maintain professional documentation that can demonstrate practical skills to recruiters and interviewers

---

# 🗺️ SOC Learning Roadmap

```text
SOC Fundamentals
       │
       ▼
SOC Analyst L1
       │
       ├── Security Monitoring
       ├── Log Analysis
       ├── Alert Triage
       ├── IOC Analysis
       ├── Basic Incident Response
       └── Ticket / Case Documentation
       │
       ▼
SOC Analyst L2
       │
       ├── Advanced Investigation
       ├── Threat Hunting
       ├── Detection Engineering
       ├── MITRE ATT&CK
       ├── Correlation
       └── Incident Investigation
       │
       ▼
SOC Analyst L3
       │
       ├── Advanced Threat Hunting
       ├── Detection Strategy
       ├── Threat Intelligence
       ├── Advanced Incident Response
       ├── Malware / Attack Analysis
       ├── Detection Engineering
       └── Security Architecture & Optimization
```

---

# 📚 SOC Learning Levels

## 🟢 Level 1 — SOC Analyst L1

**Primary focus:** Detection, monitoring, triage, investigation fundamentals, and incident documentation.

### Core Topics

* SOC fundamentals
* People, Process & Technology
* SOC architecture
* Security monitoring
* SIEM fundamentals
* Log management
* Windows Event Logs
* Sysmon
* Linux logs
* Authentication logs
* Network logs
* Firewall logs
* DNS logs
* Web server logs
* Alert generation
* Alert triage
* False positives
* True positives
* IOC identification
* IP/domain/hash investigation
* Basic threat intelligence
* Basic incident response
* Incident severity
* Incident classification
* Escalation
* Case management
* Security documentation
* SOC metrics and KPIs

### L1 Practical Skills

* Analyze Windows events
* Analyze Linux authentication logs
* Investigate failed login attempts
* Identify brute-force activity
* Investigate suspicious processes
* Investigate PowerShell activity
* Investigate suspicious network connections
* Identify common IOCs
* Perform basic alert triage
* Write SOC investigation notes
* Create incident timelines
* Escalate incidents appropriately

---

# 🟡 Level 2 — SOC Analyst L2

**Primary focus:** Advanced investigation, correlation, detection engineering, and threat hunting.

### Core Topics

* Advanced SIEM investigation
* Event correlation
* Detection engineering
* MITRE ATT&CK
* Threat hunting
* Advanced IOC analysis
* Endpoint investigation
* Network investigation
* Attack-chain analysis
* Persistence mechanisms
* Lateral movement
* Credential attacks
* PowerShell investigation
* Process analysis
* Windows internals
* Threat intelligence enrichment
* Incident scoping
* Root-cause analysis
* Detection tuning
* False-positive reduction

### L2 Practical Skills

* Build detection rules
* Correlate multiple events
* Map activity to MITRE ATT&CK
* Hunt for suspicious behavior
* Investigate attack chains
* Tune noisy detections
* Enrich alerts using threat intelligence
* Identify attacker TTPs
* Determine incident scope
* Perform deeper endpoint investigation

---

# 🔴 Level 3 — SOC Analyst L3

**Future learning scope**

**Primary focus:** Advanced detection strategy, threat hunting, incident response, and security engineering.

### Core Topics

* Advanced threat hunting
* Advanced detection engineering
* Threat intelligence
* Malware analysis fundamentals
* Advanced endpoint investigation
* Advanced network analysis
* Adversary emulation
* Attack-chain reconstruction
* Detection strategy
* Detection coverage
* SIEM optimization
* Security automation
* SOAR concepts
* Advanced incident response
* Forensic investigation fundamentals
* Threat actor profiling
* Detection gap analysis
* SOC architecture
* Security engineering

### L3 Practical Skills

* Develop advanced detections
* Conduct proactive threat hunts
* Investigate complex incidents
* Build detection coverage
* Identify detection gaps
* Improve SOC workflows
* Automate repetitive investigation tasks
* Develop advanced response procedures
* Mentor junior analysts

---

# 🔎 Detection Engineering

This section documents the process of converting security knowledge into **repeatable and testable detections**.

## Detection Lifecycle

```text
Threat / Attack Technique
          ↓
Understand TTP
          ↓
Identify Telemetry
          ↓
Create Detection Logic
          ↓
Test Detection
          ↓
Generate Alert
          ↓
Investigate
          ↓
Tune Detection
          ↓
Document
```

## Detection Categories

### Authentication

* Brute-force detection
* Password spraying
* Multiple failed logins
* Successful login after repeated failures
* Suspicious authentication location

### Endpoint

* Suspicious process creation
* PowerShell abuse
* Command-line execution
* LOLBin activity
* Suspicious parent-child processes
* Persistence activity

### Network

* Port scanning
* Suspicious outbound connections
* DNS anomalies
* Unusual network traffic
* Command-and-control indicators

### Windows

* Event ID 4624
* Event ID 4625
* Event ID 4688
* Event ID 4720
* Event ID 4728
* Event ID 4732
* Event ID 7045
* PowerShell Event ID 4104

### Web

* Web shell activity
* Suspicious HTTP requests
* Authentication attacks
* Directory traversal
* Command injection indicators

---

# 📖 SOC Playbooks

Playbooks document **what an analyst should do when a specific alert or incident occurs.**

## Playbook Structure

Each playbook should contain:

1. Purpose
2. Trigger
3. Severity
4. Required Data
5. Initial Triage
6. Investigation Steps
7. IOC Collection
8. MITRE ATT&CK Mapping
9. Containment
10. Eradication
11. Recovery
12. Escalation Criteria
13. False Positive Conditions
14. Evidence to Preserve
15. Closure Criteria
16. Lessons Learned

## Planned Playbooks

* Brute Force Investigation
* Password Spraying Investigation
* Phishing Investigation
* Malicious PowerShell Investigation
* Suspicious Process Investigation
* Malware Detection
* Account Compromise
* Privilege Escalation
* Suspicious Login
* Impossible Travel
* Endpoint Compromise
* Data Exfiltration
* C2 Communication
* Ransomware Detection
* Web Attack Investigation
* Insider Threat Investigation
* Suspicious DNS Activity
* Port Scanning
* Unauthorized Account Creation

---

# 🧪 SOC Home Lab

My home lab is used to reproduce security events, collect telemetry, generate alerts, investigate incidents, and validate detection rules.

## Planned Environment

```text
                    SOC LAB
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     Windows         Linux          Kali
     Endpoint        Server        Attacker
        │              │              │
        └─────── Security Events ────┘
                       │
                       ▼
                  Log Collection
                       │
                       ▼
                 SIEM / Analysis
                       │
                       ▼
                  Detection
                       │
                       ▼
                     Alert
                       │
                       ▼
                  Investigation
                       │
                       ▼
                Incident Report
```

## Lab Components

* Kali Linux
* Windows endpoint
* Windows Server / Active Directory — future
* Linux server
* Sysmon
* Wazuh
* Splunk — future/optional
* Wireshark
* Nmap
* Security Onion — future/optional
* Threat intelligence tools
* Vulnerable machines for controlled attack simulation

---

# 🧩 TryHackMe SOC / Blue Team Labs

TryHackMe rooms are used to reinforce theory through practical exercises.

## Documentation Standard

Every write-up should contain:

* Objective
* Scenario
* Concepts Learned
* Tools Used
* Investigation Method
* Commands / Queries
* Evidence
* Findings
* MITRE ATT&CK Mapping where applicable
* Lessons Learned

## Planned Categories

### SOC Fundamentals

* SOC Fundamentals
* Security Operations
* Incident Response

### Log Analysis

* Windows Event Logs
* Linux Logs
* Sysmon
* Log Investigation

### SIEM

* Wazuh
* Splunk
* SIEM Investigation

### Detection

* Detection Engineering
* Sigma
* SIEM Queries

### Threat Hunting

* Hunting
* MITRE ATT&CK
* TTP Analysis

### Incident Response

* Phishing
* Malware
* Brute Force
* Account Compromise
* Endpoint Investigation

---

# 🛠️ SOC Mini Projects

Mini-projects are designed to isolate individual SOC skills before combining them into larger systems.

## Planned Projects

### 01 — Brute Force Detection

Detect repeated authentication failures and identify the source.

**Skills:**

* Windows logs
* Linux logs
* Detection logic
* Alert triage

---

### 02 — PowerShell Detection

Identify suspicious PowerShell execution.

**Skills:**

* Sysmon
* Windows Event Logs
* PowerShell
* MITRE ATT&CK

---

### 03 — Suspicious Process Detection

Identify abnormal parent-child process relationships.

**Skills:**

* Sysmon Event ID 4688
* Process analysis
* Detection engineering

---

### 04 — Phishing Investigation

Investigate a simulated phishing incident.

**Skills:**

* Email analysis
* IOC extraction
* URL/domain investigation
* Threat intelligence

---

### 05 — Windows Account Compromise

Investigate suspicious authentication activity.

**Skills:**

* Windows Event Logs
* Authentication analysis
* Timeline construction

---

### 06 — Network Threat Investigation

Investigate suspicious network traffic.

**Skills:**

* Wireshark
* Network analysis
* IOC identification

---

# 🚩 Flagship Project

# SENTINEL-X

### AI-Augmented SOC Investigation Platform

SENTINEL-X is the flagship project of this SOC portfolio.

The project focuses on improving SOC investigation efficiency through **security telemetry, detection logic, MITRE ATT&CK mapping, AI-assisted investigation, and automated incident reporting.**

## Core Workflow

```text
Security Events
      ↓
Log Collection
      ↓
Event Parsing
      ↓
Detection Engine
      ↓
Alert
      ↓
Triage
      ↓
AI-Assisted Investigation
      ↓
MITRE ATT&CK Mapping
      ↓
Incident Timeline
      ↓
Risk Assessment
      ↓
Incident Report
```

## Core Capabilities

* Log ingestion
* Event parsing
* Detection rules
* Alert triage
* IOC extraction
* MITRE ATT&CK mapping
* Incident timeline generation
* AI-assisted investigation
* Investigation summarization
* Recommended response actions
* Incident report generation

## AI Philosophy

AI will be used as an **analyst-assistance layer**, not as an uncontrolled autonomous decision-maker.

```text
Security Telemetry
        ↓
Detection
        ↓
Human + AI Investigation
        ↓
Validation
        ↓
Final Security Decision
```

The objective is to demonstrate how AI can reduce repetitive SOC workload while maintaining **human validation and security accountability**.

---

# 📊 SOC Investigation Framework

Every major investigation will follow a consistent methodology:

```text
1. Alert
   ↓
2. Validate
   ↓
3. Scope
   ↓
4. Investigate
   ↓
5. Identify IOCs
   ↓
6. Identify TTPs
   ↓
7. Map to MITRE ATT&CK
   ↓
8. Determine Impact
   ↓
9. Contain / Recommend Response
   ↓
10. Document
   ↓
11. Close / Escalate
```

---

# 📁 Directory Structure

```text
SOC/
│
├── README.md
│
├── 01-SOC-Fundamentals/
│   ├── Notes/
│   ├── Concepts/
│   └── Cheat-Sheets/
│
├── 02-SOC-L1/
│   ├── Learning/
│   ├── Log-Analysis/
│   ├── Alert-Triage/
│   ├── IOC-Analysis/
│   └── Incident-Response/
│
├── 03-SOC-L2/
│   ├── Advanced-Investigation/
│   ├── Detection-Engineering/
│   ├── Threat-Hunting/
│   ├── MITRE-ATT&CK/
│   └── Threat-Intelligence/
│
├── 04-SOC-L3/
│   ├── Advanced-Threat-Hunting/
│   ├── Advanced-Detection/
│   ├── Malware-Analysis/
│   ├── Advanced-IR/
│   └── SOC-Engineering/
│
├── 05-Detection-Rules/
│   ├── Sigma/
│   ├── Wazuh/
│   ├── Splunk/
│   └── Other-Rules/
│
├── 06-Playbooks/
│   ├── Brute-Force/
│   ├── Phishing/
│   ├── PowerShell/
│   ├── Malware/
│   ├── Account-Compromise/
│   └── ...
│
├── 07-TryHackMe/
│   ├── SOC/
│   ├── Blue-Team/
│   ├── SIEM/
│   ├── Detection/
│   ├── Incident-Response/
│   └── Threat-Hunting/
│
├── 08-Mini-Projects/
│   ├── Brute-Force-Detection/
│   ├── PowerShell-Detection/
│   ├── Suspicious-Process/
│   ├── Phishing-Investigation/
│   └── ...
│
├── 09-Home-Lab/
│   ├── Architecture/
│   ├── Wazuh/
│   ├── Sysmon/
│   ├── Windows/
│   ├── Linux/
│   └── Attack-Simulations/
│
├── 10-Investigation-Reports/
│   ├── Alert-Triage/
│   ├── Incident-Reports/
│   └── Case-Studies/
│
└── 11-Flagship-Project/
    └── SENTINEL-X/
```

---

# 📈 Progress Tracking

| Area                  | Status |
| --------------------- | ------ |
| SOC Fundamentals      | ⬜      |
| SOC L1                | ⬜      |
| Log Analysis          | ⬜      |
| Alert Triage          | ⬜      |
| IOC Analysis          | ⬜      |
| Incident Response     | ⬜      |
| SIEM                  | ⬜      |
| Detection Engineering | ⬜      |
| SOC Playbooks         | ⬜      |
| MITRE ATT&CK          | ⬜      |
| Threat Intelligence   | ⬜      |
| Threat Hunting        | ⬜      |
| SOC L2                | ⬜      |
| SOC L3                | ⬜      |
| TryHackMe SOC Labs    | ⬜      |
| Home Lab              | ⬜      |
| Mini Projects         | ⬜      |
| SENTINEL-X            | ⬜      |

---

# 📌 Documentation Philosophy

This directory follows a simple principle:

> **Learn → Practice → Investigate → Document → Validate → Share**

Every major topic should ideally produce practical evidence.

For example:

```text
Learn Windows Event Logs
        ↓
Analyze Events in Home Lab
        ↓
Create Detection Rule
        ↓
Generate Alert
        ↓
Investigate Alert
        ↓
Write Playbook
        ↓
Document Case Study
        ↓
Publish Selected Learning
```

---

# 🔐 Ethics & Scope

All security testing and attack simulations documented in this repository are performed against:

* My own home-lab systems
* Intentionally vulnerable machines
* Authorized TryHackMe environments
* Authorized CTF environments
* Other explicitly authorized systems

No unauthorized systems, accounts, networks, or data are targeted.

---

# 🚀 Long-Term Vision

This SOC directory is intended to evolve with my cybersecurity career.

```text
SOC L1
  ↓
SOC L2
  ↓
SOC L3
  ↓
Threat Hunting / Detection Engineering
  ↓
Security Consulting
  ↓
GRC / Security Architecture
  ↓
Cybersecurity Leadership
```

The portfolio will continuously evolve from **learning documentation** into evidence of **professional security analysis, detection engineering, incident response, and consulting capability.**

---

## ⭐ Core Portfolio Assets

The most important outputs of this directory will eventually include:

* SOC knowledge base
* Detection rule library
* Security investigation playbooks
* TryHackMe write-ups
* Home-lab investigations
* Incident reports
* SOC case studies
* Detection engineering projects
* Mini-projects
* MITRE ATT&CK mappings
* AI-assisted security workflows
* **SENTINEL-X flagship project**

---

### Current Focus

> **SOC Analyst L1 — Build strong fundamentals, practice continuously, document everything, and create evidence of practical capability.**

**Next milestone:** Complete the SOC L1 knowledge foundation and begin building the home-lab detection and investigation workflow.
