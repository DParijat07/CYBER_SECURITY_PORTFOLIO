# 🛡️ VAPT — Vulnerability Assessment & Penetration Testing

> **A practical Vulnerability Assessment and Penetration Testing (VAPT) portfolio documenting methodology, reconnaissance, enumeration, vulnerability discovery, validation, exploitation, risk assessment, reporting, remediation, and retesting.**

This directory contains my practical work in **Vulnerability Assessment and Penetration Testing**, with a focus on understanding vulnerabilities from both an offensive and defensive perspective.

The objective is to develop the ability to:

> **Discover → Validate → Exploit → Assess Impact → Report → Remediate → Retest**

All activities documented here are performed only in **authorized environments**, including my home lab, intentionally vulnerable machines, TryHackMe, CTF platforms, and other explicitly authorized targets.

---

# 🎯 Objectives

* Build a strong VAPT methodology
* Develop systematic reconnaissance skills
* Master scanning and enumeration
* Learn vulnerability discovery and validation
* Understand CVEs and CVSS
* Develop exploitation fundamentals
* Practice web application penetration testing
* Practice network penetration testing
* Develop Linux and Windows privilege-escalation skills
* Understand Active Directory attack fundamentals
* Learn vulnerability prioritization
* Develop professional VAPT reporting
* Practice remediation validation and retesting
* Automate repetitive VAPT tasks
* Integrate AI into VAPT workflows responsibly
* Build evidence through home-lab assessments, CTFs, and practical projects
* Develop consulting-oriented VAPT capabilities

---

# 🧭 VAPT Methodology

The VAPT lifecycle followed in this portfolio is:

```text
Scope & Authorization
        ↓
Information Gathering
        ↓
Reconnaissance
        ↓
Scanning
        ↓
Enumeration
        ↓
Vulnerability Discovery
        ↓
Vulnerability Validation
        ↓
Exploitation
        ↓
Privilege Escalation
        ↓
Impact Assessment
        ↓
Risk Assessment
        ↓
Reporting
        ↓
Remediation
        ↓
Retesting
        ↓
Final Assessment
```

Not every assessment requires exploitation.

A vulnerability may be considered sufficiently validated through safe evidence collection when exploitation could cause unnecessary impact.

---

# 01 — Scope & Rules of Engagement

Before testing begins, the assessment scope must be clearly defined.

## Scope

Document:

* Target IPs
* Hostnames
* Domains
* Applications
* APIs
* Network ranges
* Testing windows
* Excluded systems

## Rules of Engagement

Define:

* Authorized testing methods
* Prohibited activities
* Testing time
* Data-handling requirements
* Communication process
* Emergency contacts
* Stop conditions

## Deliverables

* Scope Document
* Rules of Engagement
* Asset List
* Testing Authorization

---

# 02 — Information Gathering

## Passive Reconnaissance

Topics:

* OSINT
* WHOIS
* DNS information
* Public IP ranges
* Subdomains
* Public technologies
* Email exposure
* Public repositories
* Search-engine intelligence

## Active Reconnaissance

Topics:

* Host discovery
* Network discovery
* Service discovery
* Application discovery

### Tools

* Nmap
* Amass
* Subfinder
* theHarvester
* WHOIS
* DNS tools

---

# 03 — Scanning

Scanning identifies reachable systems, ports and services.

## Topics

* Host discovery
* TCP scanning
* UDP scanning
* Port states
* Service detection
* Version detection
* OS detection
* NSE scripts
* Firewall behavior

### Primary Tool

**Nmap**

### Example Workflow

```text
Host Discovery
      ↓
Port Scan
      ↓
Service Detection
      ↓
Version Detection
      ↓
NSE Enumeration
```

---

# 04 — Enumeration

Enumeration attempts to obtain detailed information about discovered services.

## Services

### SMB

* Shares
* Users
* Domain information
* SMB versions
* Access permissions

### FTP

* Anonymous access
* Banner
* Version
* File exposure

### SSH

* Version
* Authentication methods
* Configuration

### HTTP/HTTPS

* Technologies
* Directories
* Virtual hosts
* Authentication
* Application endpoints

### DNS

* Records
* Nameservers
* Zone-transfer exposure
* Subdomains

### SNMP

* Community strings
* System information
* Network information

---

# 05 — Vulnerability Discovery

The objective is to identify weaknesses affecting:

* Applications
* Operating systems
* Network services
* Configurations
* Authentication
* Authorization
* Infrastructure

## Vulnerability Sources

* Nmap NSE
* Nessus
* OpenVAS / Greenbone
* Nikto
* SearchSploit
* CVE databases
* Vendor advisories
* Security research

---

# 06 — Vulnerability Validation

Automated scanner output is **not automatically treated as a confirmed vulnerability**.

Validation should determine:

```text
Scanner Finding
      ↓
Manual Verification
      ↓
Version / Configuration Check
      ↓
Exploitability Assessment
      ↓
Evidence
      ↓
Confirmed / False Positive
```

## Validation Principles

* Verify affected asset
* Verify affected version/configuration
* Understand vulnerability conditions
* Check exploitability
* Collect reproducible evidence
* Avoid unnecessary destructive testing

---

# 07 — Vulnerability Classification

Vulnerabilities will be categorized using established security references.

## Examples

* CVE
* CWE
* OWASP Top 10
* OWASP API Security Top 10
* CAPEC
* MITRE ATT&CK where applicable

---

# 08 — Risk Assessment

Technical severity alone does not always represent business risk.

Risk assessment will consider:

```text
Likelihood
     +
Technical Impact
     +
Business Impact
     +
Asset Criticality
     +
Exploitability
     ↓
Overall Risk
```

## Risk Categories

* Critical
* High
* Medium
* Low
* Informational

---

# 09 — CVSS

CVSS will be used to understand and communicate vulnerability severity.

The assessment may document:

* CVSS version
* Vector
* Base Score
* Temporal considerations
* Environmental considerations where applicable

CVSS will be treated as a **technical severity framework**, not a complete replacement for business-risk assessment.

---

# 10 — Exploitation

Where explicitly authorized and necessary, exploitation may be performed to validate impact.

## Topics

* Exploit research
* CVE analysis
* Proof-of-concept analysis
* Manual exploitation
* Metasploit
* Reverse shells
* Bind shells
* Payload concepts
* Exploit validation

## Exploitation Principle

> **Prove the vulnerability with the minimum necessary impact.**

The objective is validation, not uncontrolled compromise.

---

# 11 — Privilege Escalation

After controlled compromise, privilege escalation techniques may be investigated in authorized lab environments.

## Linux

* SUID/SGID
* Sudo
* Cron
* Capabilities
* Writable files
* PATH abuse
* Service misconfiguration
* Kernel vulnerabilities

### Resources

* LinPEAS
* GTFOBins

## Windows

* Services
* Scheduled Tasks
* Registry
* Token privileges
* Weak permissions
* Unquoted service paths
* Credential exposure
* DLL hijacking
* UAC concepts

### Resources

* WinPEAS
* LOLBAS

---

# 12 — Web Application VAPT

Web application testing is a major VAPT specialization.

## Testing Areas

### Reconnaissance

* Technology identification
* Directory discovery
* Endpoint discovery
* API discovery

### Authentication

* Weak authentication
* Credential attacks
* Session management
* MFA weaknesses

### Authorization

* IDOR
* Privilege escalation
* Access-control failures

### Input Validation

* SQL Injection
* XSS
* Command Injection
* SSTI
* Path Traversal

### File Handling

* Unrestricted upload
* File inclusion
* Path traversal

### Server-Side

* SSRF
* XXE
* Command execution
* Security misconfiguration

### API

* Authentication
* Authorization
* Rate limiting
* Input validation
* JWT security
* Excessive data exposure

### Tools

* Burp Suite
* Gobuster
* ffuf
* Nmap
* Nikto
* SQLMap

---

# 13 — Network VAPT

## Testing Areas

* Network discovery
* Port exposure
* Service vulnerabilities
* Weak protocols
* SMB security
* FTP security
* SSH security
* SNMP security
* Network segmentation
* Firewall exposure
* Misconfiguration

### Tools

* Nmap
* Wireshark
* Nessus
* Metasploit
* enum4linux

---

# 14 — Active Directory VAPT

Future specialization.

## Topics

* Domain enumeration
* Users and groups
* Kerberos
* LDAP
* SMB
* NTLM
* Kerberoasting
* AS-REP Roasting
* Credential attacks
* Privilege escalation
* Lateral movement
* Domain privilege abuse

All AD testing will be performed within an authorized lab environment.

---

# 15 — Evidence Collection

Every confirmed finding should have sufficient evidence.

## Evidence May Include

* Screenshots
* Command output
* Scanner output
* HTTP requests/responses
* Version information
* Configuration evidence
* Proof-of-concept results
* Relevant logs

Evidence should be:

* Reproducible
* Relevant
* Minimal
* Properly sanitized

---

# 16 — Professional VAPT Reporting

The final report should communicate technical findings to both technical and non-technical stakeholders.

## Report Structure

```text
Executive Summary
        ↓
Scope
        ↓
Methodology
        ↓
Asset Summary
        ↓
Risk Overview
        ↓
Detailed Findings
        ↓
Business Impact
        ↓
Technical Evidence
        ↓
Remediation
        ↓
Retest Results
        ↓
Conclusion
```

---

# 📋 Vulnerability Finding Template

Every major vulnerability will follow a consistent structure.

```text
Finding ID:
Finding Name:
Severity:
CVSS:
Affected Asset:
CWE/CVE:
Description:

Technical Details:

Evidence:

Impact:

Likelihood:

Business Impact:

Risk:

Remediation:

References:

Retest Status:
```

---

# 🔄 Remediation & Retesting

VAPT does not end with finding vulnerabilities.

The complete lifecycle is:

```text
Finding
   ↓
Recommendation
   ↓
Remediation
   ↓
Retest
   ↓
Validated / Not Validated
   ↓
Final Report
```

Retesting will verify whether the identified vulnerability has actually been addressed.

---

# 🧪 Home-Lab VAPT

My home lab is used to perform controlled vulnerability assessments and penetration tests.

## Current / Planned Targets

* Metasploitable 2
* Windows 7
* Windows 10/11
* DVWA
* OWASP Juice Shop
* VulnHub machines
* Active Directory lab — future

## Lab Workflow

```text
Kali Linux
    ↓
Reconnaissance
    ↓
Nmap
    ↓
Enumeration
    ↓
Vulnerability Assessment
    ↓
Exploitation
    ↓
Privilege Escalation
    ↓
Evidence Collection
    ↓
VAPT Report
```

---

# 🧪 TryHackMe & CTF Practice

TryHackMe and CTF platforms are used to develop practical offensive-security skills.

## Write-Up Standard

Each write-up should contain:

1. Objective
2. Scope
3. Reconnaissance
4. Enumeration
5. Vulnerability Discovery
6. Exploitation
7. Privilege Escalation
8. Evidence
9. Lessons Learned
10. Defensive / Remediation Perspective

Where applicable:

* CVE
* CVSS
* CWE
* OWASP category
* MITRE ATT&CK mapping

---

# 🛠️ VAPT Mini Projects

Planned projects include:

### 01 — Nmap Reconnaissance Automation

Automate authorized host and service discovery.

### 02 — Vulnerability Intelligence Tool

Enrich discovered vulnerabilities with CVE information.

### 03 — VAPT Risk Prioritization Engine

Prioritize vulnerabilities using severity, exploitability and asset context.

### 04 — VAPT Report Generator

Convert structured findings into professional assessment reports.

### 05 — Attack Surface Mapper

Visualize discovered hosts, services and applications.

### 06 — Web Security Testing Assistant

Organize authorized web-application assessment findings.

---

# 🤖 AI-Assisted VAPT

AI will be integrated as a **research, analysis and productivity assistant**.

Potential applications:

* Nmap output analysis
* Vulnerability explanation
* CVE research assistance
* Finding classification
* Risk-prioritization assistance
* Remediation suggestions
* Report drafting
* Evidence summarization
* Attack-path analysis
* Security research assistance
* Automation-script development

## AI Validation Principle

```text
AI Suggestion
      ↓
Security Professional Verification
      ↓
Technical Validation
      ↓
Final Assessment
```

AI-generated findings will never be treated as automatically confirmed vulnerabilities.

---

# 📁 Directory Structure

```text
VAPT/
│
├── README.md
│
├── 01-Methodology/
│   ├── VAPT-Methodology.md
│   ├── Rules-of-Engagement.md
│   └── Testing-Checklists/
│
├── 02-Reconnaissance/
│   ├── Passive-Recon/
│   ├── Active-Recon/
│   └── OSINT/
│
├── 03-Scanning/
│   ├── Nmap/
│   └── Network-Scanning/
│
├── 04-Enumeration/
│   ├── SMB/
│   ├── FTP/
│   ├── SSH/
│   ├── HTTP/
│   ├── DNS/
│   └── SNMP/
│
├── 05-Vulnerability-Assessment/
│   ├── Nessus/
│   ├── OpenVAS/
│   ├── CVE-Research/
│   ├── CVSS/
│   └── Validation/
│
├── 06-Web-VAPT/
│   ├── OWASP/
│   ├── Burp-Suite/
│   ├── API-Security/
│   └── Case-Studies/
│
├── 07-Network-VAPT/
│
├── 08-Exploitation/
│
├── 09-Privilege-Escalation/
│   ├── Linux/
│   └── Windows/
│
├── 10-Active-Directory/
│
├── 11-Home-Lab-Assessments/
│
├── 12-TryHackMe/
│
├── 13-CTF-Writeups/
│
├── 14-VAPT-Reports/
│
├── 15-Mini-Projects/
│
├── 16-Automation/
│
└── 17-AI-Assisted-VAPT/
```

---

# 📊 Progress Tracking

| Capability                   | Status |
| ---------------------------- | ------ |
| VAPT Methodology             | ⬜      |
| Scope & Rules of Engagement  | ⬜      |
| Reconnaissance               | ⬜      |
| Scanning                     | ⬜      |
| Enumeration                  | ⬜      |
| Vulnerability Discovery      | ⬜      |
| Vulnerability Validation     | ⬜      |
| CVE Research                 | ⬜      |
| CVSS                         | ⬜      |
| Exploitation                 | ⬜      |
| Linux Privilege Escalation   | ⬜      |
| Windows Privilege Escalation | ⬜      |
| Web VAPT                     | ⬜      |
| Network VAPT                 | ⬜      |
| API Security                 | ⬜      |
| Active Directory             | ⬜      |
| VAPT Reporting               | ⬜      |
| Remediation & Retesting      | ⬜      |
| Home-Lab Assessments         | ⬜      |
| TryHackMe                    | ⬜      |
| CTFs                         | ⬜      |
| Automation                   | ⬜      |
| AI-Assisted VAPT             | ⬜      |

---

# 📚 Documentation Philosophy

The VAPT learning process follows:

```text
Learn
  ↓
Research
  ↓
Recon
  ↓
Enumerate
  ↓
Assess
  ↓
Validate
  ↓
Exploit
  ↓
Document
  ↓
Report
  ↓
Remediate
  ↓
Retest
```

The goal is not simply to demonstrate:

> **"I can hack a machine."**

The goal is to demonstrate:

> **"I can systematically assess an environment, identify security weaknesses, validate their impact, communicate risk, recommend remediation, and verify the fix."**

---

# 🔐 Ethics & Authorization

All activities documented in this directory are performed only against:

* Personally controlled systems
* Home-lab environments
* Intentionally vulnerable machines
* Authorized TryHackMe rooms
* Authorized CTF environments
* Explicitly authorized client/test environments

No unauthorized systems, accounts, networks, or data are targeted.

---

# 🚀 Long-Term Development

My VAPT journey will progressively evolve from foundational testing toward professional security assessment and consulting.

```text
VAPT Fundamentals
       ↓
Network VAPT
       ↓
Web Application VAPT
       ↓
Advanced Vulnerability Assessment
       ↓
Windows / Linux Security
       ↓
Active Directory VAPT
       ↓
Cloud Security Testing
       ↓
API Security
       ↓
Enterprise VAPT
       ↓
Security Consulting
```

The long-term objective is to combine VAPT expertise with:

* SOC
* GRC
* IAM
* Cloud Security
* AI Security
* OT/ICS Security

to develop a broader cybersecurity consulting capability.

---

# ⭐ Core Portfolio Evidence

The primary outputs of this directory will include:

* VAPT methodology documentation
* Reconnaissance research
* Enumeration notes
* Vulnerability research
* CVE analysis
* CVSS assessments
* Home-lab penetration tests
* Professional VAPT reports
* Web-security assessments
* Network assessments
* TryHackMe write-ups
* CTF write-ups
* Privilege-escalation research
* Active Directory labs
* Automation tools
* AI-assisted VAPT workflows
* Security case studies
* Mini-projects

---

## 📌 Current Priority

> **Build strong VAPT fundamentals and demonstrate practical assessment capability through authorized labs and professional documentation.**

### Immediate Focus

1. VAPT methodology
2. Reconnaissance
3. Nmap
4. Enumeration
5. Vulnerability Assessment
6. CVE & CVSS
7. Vulnerability validation
8. Web VAPT
9. Linux privilege escalation
10. Windows privilege escalation
11. Professional VAPT reporting
12. Home-lab assessments
13. TryHackMe practice
14. CTF write-ups
15. VAPT automation
16. AI-assisted VAPT

**Learn → Recon → Enumerate → Assess → Validate → Exploit → Report → Remediate → Retest**
