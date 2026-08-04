# 🔴 Red Team — Offensive Cybersecurity

> **A practical offensive-security learning and portfolio repository focused on reconnaissance, vulnerability assessment, penetration testing, exploitation, privilege escalation, web security, Active Directory security, and controlled adversary simulation.**

This directory documents my journey into **offensive cybersecurity**, with a primary focus on **Vulnerability Assessment and Penetration Testing (VAPT)**.

It combines theoretical learning, authorized hands-on labs, home-lab assessments, TryHackMe and CTF write-ups, vulnerability research, exploitation practice, penetration-testing methodologies, professional security reports, and practical projects.

The objective is to understand how attacks work so that vulnerabilities can be **identified, validated, documented, prioritized, and remediated effectively**.

---

# 🎯 Objectives

* Build strong offensive-security fundamentals
* Develop practical VAPT capabilities
* Learn systematic reconnaissance and enumeration
* Understand vulnerability discovery and validation
* Develop exploitation fundamentals
* Learn privilege escalation techniques
* Develop web application security skills
* Learn Active Directory attack fundamentals
* Understand common network attacks
* Practice controlled attack simulations
* Develop professional penetration-testing methodology
* Produce professional VAPT reports
* Complete and document authorized labs and CTFs
* Build practical offensive-security mini-projects
* Integrate automation and AI where appropriate
* Develop skills that support future security consulting work

---

# 🧭 Offensive Security Roadmap

```text
Offensive Security Fundamentals
            │
            ▼
Reconnaissance
            │
            ▼
Scanning & Enumeration
            │
            ▼
Vulnerability Assessment
            │
            ▼
Penetration Testing
            │
      ┌─────┼──────────────┐
      │     │              │
      ▼     ▼              ▼
    Web    Network         AD
 Security  Security      Security
      │     │              │
      └─────┼──────────────┘
            ▼
       Exploitation
            │
            ▼
    Privilege Escalation
            │
            ▼
     Post-Exploitation
            │
            ▼
   Validation & Evidence
            │
            ▼
     Risk Assessment
            │
            ▼
   Professional Reporting
```

---

# 🧩 Offensive Security Domains

| Domain                       | Focus                                              |
| ---------------------------- | -------------------------------------------------- |
| 🔎 Reconnaissance            | Passive and active information gathering           |
| 🌐 Scanning                  | Host, port and service discovery                   |
| 🧭 Enumeration               | Identifying services, users and attack surfaces    |
| 🛡️ Vulnerability Assessment | Discovering and prioritizing vulnerabilities       |
| ⚔️ Penetration Testing       | Controlled validation and exploitation             |
| 🌐 Web Security              | Web application vulnerability testing              |
| 🖥️ Network Security         | Network service and infrastructure testing         |
| 🏢 Active Directory          | Enterprise identity and domain attack fundamentals |
| 🔐 Privilege Escalation      | Linux and Windows privilege escalation             |
| 🦠 Exploitation              | Controlled exploitation of vulnerabilities         |
| 🔬 Post-Exploitation         | Understanding impact after compromise              |
| 📋 Reporting                 | Professional security findings and remediation     |
| ⚙️ Automation                | Automating repetitive assessment tasks             |

---

# 🔎 Reconnaissance

Reconnaissance is the foundation of offensive security.

## Topics

* Passive reconnaissance
* Active reconnaissance
* OSINT
* DNS reconnaissance
* WHOIS
* Subdomain discovery
* Technology identification
* Email discovery
* Public exposure analysis
* Attack-surface identification

## Tools

* Nmap
* Amass
* Subfinder
* theHarvester
* DNS tools
* WHOIS
* Google dorks
* Shodan — where authorized
* Other OSINT tools

---

# 🌐 Scanning & Enumeration

## Topics

* Host discovery
* Port scanning
* Service detection
* Version detection
* OS detection
* Banner grabbing
* Network enumeration
* SMB enumeration
* FTP enumeration
* SSH enumeration
* HTTP enumeration
* SNMP enumeration
* DNS enumeration

## Primary Tool

**Nmap**

Additional tools will be documented as they are learned and validated in authorized environments.

---

# 🛡️ Vulnerability Assessment

The vulnerability-assessment workflow will focus on identifying, validating, prioritizing and documenting weaknesses.

## Workflow

```text
Asset Discovery
      ↓
Service Enumeration
      ↓
Vulnerability Discovery
      ↓
Vulnerability Validation
      ↓
Risk Assessment
      ↓
Evidence Collection
      ↓
Remediation Recommendation
      ↓
Professional Report
```

## Topics

* Vulnerability identification
* CVE research
* CVSS
* Vulnerability validation
* False-positive analysis
* Risk prioritization
* Exploitability
* Business impact
* Remediation
* Retesting

## Tools

* Nmap
* Nessus
* OpenVAS / Greenbone
* Nikto
* SearchSploit
* Metasploit
* Burp Suite

---

# ⚔️ Penetration Testing

Penetration testing will focus on controlled exploitation to validate the practical impact of identified vulnerabilities.

## Methodology

```text
1. Scope
2. Reconnaissance
3. Scanning
4. Enumeration
5. Vulnerability Analysis
6. Exploitation
7. Privilege Escalation
8. Post-Exploitation
9. Evidence Collection
10. Risk Analysis
11. Reporting
12. Remediation
13. Retesting
```

---

# 🌐 Web Application Security

## Topics

* HTTP/HTTPS
* Authentication
* Authorization
* Session management
* Input validation
* SQL Injection
* XSS
* Command Injection
* File Upload vulnerabilities
* Path Traversal
* SSRF
* XXE
* IDOR
* Security misconfiguration
* API security
* JWT security
* Business logic vulnerabilities

## Tools

* Burp Suite
* Gobuster
* ffuf
* Nmap
* Nikto
* SQLMap — only in authorized environments

Web-security learning will be aligned with **OWASP Top 10** and practical application-security testing methodologies.

---

# 🏢 Active Directory Security

Future learning area focused on understanding enterprise identity infrastructure and common attack paths.

## Topics

* Active Directory fundamentals
* Domain architecture
* Users and groups
* Kerberos
* LDAP
* SMB
* NTLM
* Domain enumeration
* Privilege escalation
* Credential attacks
* Kerberoasting
* AS-REP Roasting
* Pass-the-Hash
* Lateral movement
* Domain privilege abuse

## Planned Lab

```text
                    AD LAB
                       │
             ┌─────────┴─────────┐
             │                   │
       Domain Controller      Windows Clients
             │                   │
             └─────────┬─────────┘
                       │
                    Kali
                 Test Attacker
```

All testing will be performed inside an authorized lab.

---

# 🐧 Linux Privilege Escalation

## Topics

* SUID/SGID
* File permissions
* Cron jobs
* PATH abuse
* Sudo configuration
* Weak credentials
* Writable files
* Capabilities
* Kernel vulnerabilities
* Service misconfiguration

## Tools / Resources

* LinPEAS
* GTFOBins
* Linux enumeration tools

---

# 🪟 Windows Privilege Escalation

## Topics

* Windows services
* Registry
* Scheduled tasks
* Weak permissions
* Unquoted service paths
* Credential storage
* Token privileges
* DLL hijacking
* UAC concepts
* Misconfigured applications

## Tools / Resources

* WinPEAS
* PowerShell
* Seatbelt
* LOLBAS

---

# 💥 Exploitation

This section documents controlled exploitation techniques used in authorized labs.

## Topics

* Exploit research
* CVE analysis
* Proof of Concept analysis
* Metasploit
* Manual exploitation
* Reverse shells
* Bind shells
* Payload concepts
* Exploit validation

The objective is to understand **why an exploit works**, not simply execute automated exploitation tools.

---

# 🧪 Home Lab

The home lab provides an isolated environment for offensive-security experimentation.

## Current / Planned Environment

```text
                     OFFENSIVE LAB
                           │
             ┌─────────────┼─────────────┐
             │             │             │
           Kali       Vulnerable VM   Windows
          Attacker       Target        Target
             │             │             │
             └─────────────┼─────────────┘
                           │
                    Controlled Testing
```

### Planned / Existing Targets

* Metasploitable 2
* Windows 7
* Windows 10/11
* Vulnerable web applications
* DVWA
* OWASP Juice Shop
* VulnHub machines
* Active Directory lab — future

---

# 🧰 Tools

The toolset will evolve as practical skills develop.

### Reconnaissance

* Nmap
* Amass
* Subfinder
* theHarvester

### Enumeration

* Nmap
* Gobuster
* ffuf
* enum4linux
* smbclient

### Vulnerability Assessment

* Nessus
* OpenVAS / Greenbone
* Nmap NSE
* Nikto

### Exploitation

* Metasploit
* SearchSploit
* Burp Suite

### Web Security

* Burp Suite
* Gobuster
* ffuf
* SQLMap

### Privilege Escalation

* LinPEAS
* WinPEAS
* GTFOBins
* LOLBAS

---

# 🧪 TryHackMe & CTF Practice

Practical labs will be used to reinforce offensive-security concepts.

## Write-up Standard

Each write-up should document:

1. Objective
2. Scope
3. Reconnaissance
4. Enumeration
5. Vulnerability Identification
6. Exploitation
7. Privilege Escalation
8. Evidence
9. Lessons Learned
10. Remediation / Defensive Perspective

Where appropriate, write-ups will also include:

* CVE references
* CVSS
* MITRE ATT&CK mapping
* OWASP mapping
* Attack-chain analysis

---

# 📋 VAPT Reports

Professional reporting is a core part of this portfolio.

## Report Structure

```text
Executive Summary
        ↓
Scope
        ↓
Methodology
        ↓
Asset Discovery
        ↓
Findings
        ↓
Evidence
        ↓
Risk Rating
        ↓
Business Impact
        ↓
Technical Impact
        ↓
Remediation
        ↓
Retest
```

## Finding Structure

Each vulnerability should contain:

* Finding Title
* Severity
* Affected Asset
* Description
* Technical Details
* Evidence
* Impact
* Risk
* Remediation
* References

---

# 🛠️ Mini Projects

Mini-projects will be used to build individual offensive-security capabilities.

Examples:

### 01 — Network Reconnaissance Automation

Automate basic host and service discovery.

### 02 — Vulnerability Report Generator

Convert assessment findings into structured reports.

### 03 — Web Directory Enumeration Tool

Automate authorized web-content discovery.

### 04 — IOC / Vulnerability Research Tool

Enrich identified vulnerabilities with security intelligence.

### 05 — VAPT Risk Prioritization

Prioritize findings using technical severity and business context.

### 06 — Attack Surface Mapper

Map discovered hosts, services and applications.

---

# 🤖 AI & Automation

AI will be used as a **security-assistance and productivity layer**, not as a replacement for security judgment.

Potential applications:

* Vulnerability explanation
* CVE research assistance
* Finding summarization
* Risk prioritization assistance
* Report drafting
* Remediation recommendation
* Enumeration-result analysis
* Script generation assistance
* Attack-path analysis
* Security research assistance

Every AI-generated security conclusion should be **manually validated** before being treated as a final assessment result.

---

# 📚 Documentation Philosophy

The offensive-security learning process follows:

```text
Learn
  ↓
Research
  ↓
Practice
  ↓
Enumerate
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

The objective is to demonstrate not only that I can exploit a vulnerability, but that I can understand:

> **What is vulnerable → Why it is vulnerable → How it can be exploited → What the impact is → How it should be fixed.**

---

# 📊 Progress Tracking

| Domain                          | Status |
| ------------------------------- | ------ |
| Offensive Security Fundamentals | ⬜      |
| Reconnaissance                  | ⬜      |
| Scanning                        | ⬜      |
| Enumeration                     | ⬜      |
| Vulnerability Assessment        | ⬜      |
| Penetration Testing             | ⬜      |
| Web Security                    | ⬜      |
| Network Security                | ⬜      |
| Linux Privilege Escalation      | ⬜      |
| Windows Privilege Escalation    | ⬜      |
| Active Directory                | ⬜      |
| Exploitation                    | ⬜      |
| Post-Exploitation               | ⬜      |
| VAPT Reporting                  | ⬜      |
| TryHackMe                       | ⬜      |
| CTFs                            | ⬜      |
| Home Lab                        | ⬜      |
| Mini Projects                   | ⬜      |
| Automation                      | ⬜      |
| AI-Assisted Security            | ⬜      |

---

# 🔐 Ethics & Authorization

All offensive-security activities documented in this repository are conducted only against:

* Personally controlled home-lab systems
* Intentionally vulnerable machines
* Authorized TryHackMe environments
* Authorized CTF environments
* Explicitly authorized systems

No unauthorized systems, accounts, networks, or data are targeted.

---

# 🚀 Long-Term Development

This directory will evolve alongside my cybersecurity career.

```text
Offensive Security Fundamentals
            ↓
Vulnerability Assessment
            ↓
Penetration Testing
            ↓
Web Security
            ↓
Enterprise / AD Security
            ↓
Advanced VAPT
            ↓
Security Consulting
            ↓
Security Architecture / GRC
```

My primary offensive-security specialization is **Vulnerability Assessment and Penetration Testing (VAPT)**, with penetration testing developed as a complementary capability.

The long-term objective is to combine offensive-security knowledge with defensive security, GRC, cloud, IAM, and emerging security domains to develop a broader **security consulting capability**.

---

# ⭐ Core Portfolio Assets

The major outputs of this directory will include:

* Offensive-security knowledge base
* Reconnaissance documentation
* Enumeration notes
* Vulnerability research
* VAPT assessments
* Professional VAPT reports
* Home-lab penetration tests
* TryHackMe write-ups
* CTF write-ups
* Web-security case studies
* Privilege-escalation research
* Active Directory labs
* Security automation projects
* AI-assisted security workflows
* Vulnerability research
* Mini-projects

---

## 📌 Current Priority

> **Build strong VAPT fundamentals first and develop practical evidence through authorized labs and professional documentation.**

Immediate focus:

1. Reconnaissance
2. Scanning
3. Enumeration
4. Vulnerability Assessment
5. Web Security
6. Exploitation Fundamentals
7. Linux Privilege Escalation
8. Windows Privilege Escalation
9. VAPT Reporting
10. Home-Lab Assessments
11. TryHackMe Practice
12. CTF Write-ups
13. Mini Projects

**Learn → Practice → Validate → Document → Report → Remediate → Retest**
