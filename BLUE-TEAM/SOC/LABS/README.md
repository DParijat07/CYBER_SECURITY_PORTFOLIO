# SOC Labs

## 1. Overview

This directory contains hands-on Security Operations Center (SOC) laboratories designed to demonstrate practical defensive cybersecurity skills.

The purpose of these labs is to convert theoretical SOC knowledge into practical, repeatable, and documented technical capability.

The learning approach is:

**Learn → Build → Simulate → Detect → Investigate → Document → Improve**

All laboratories are performed in authorized and controlled environments.

---

## 2. Objectives

The SOC Labs directory is designed to demonstrate practical capability in:

- Security Monitoring
- SIEM Operations
- Log Analysis
- Windows Security Monitoring
- Linux Security Monitoring
- Endpoint Monitoring
- Network Traffic Analysis
- IOC Investigation
- Threat Intelligence
- Threat Hunting
- Detection Engineering
- Incident Response
- Digital Forensics
- Vulnerability Monitoring
- Security Automation
- AI-Assisted SOC Workflows
- Security Documentation

---

## 3. Lab Philosophy

Each laboratory focuses on a specific SOC skill or operational capability.

The general workflow is:

Learn the Concept
↓
Prepare the Lab
↓
Configure the Tools
↓
Generate Security Activity
↓
Collect Telemetry
↓
Detect the Activity
↓
Investigate the Alert
↓
Analyze the Evidence
↓
Document the Findings
↓
Improve the Detection

The objective is not simply to make a security tool work.

The objective is to understand:

1. What happened?
2. Why did it happen?
3. What telemetry was generated?
4. Where was the telemetry collected?
5. How was the activity detected?
6. How would a SOC analyst investigate it?
7. What evidence supports the conclusion?
8. What response should be considered?
9. How can the detection or workflow be improved?

---

## 4. SOC Home Lab Environment

The primary SOC home-lab environment is based on VMware virtualization.

Current planned environment:

Windows 11 Host
├── VMware
│   ├── Kali Linux
│   ├── Kali Linux
│   ├── Windows 7
│   ├── Metasploitable 2
│   └── Ubuntu Server
│       └── Wazuh

The lab architecture may evolve as additional security monitoring, detection, investigation, automation, and AI capabilities are implemented.

---

## 5. Core Technologies

### 5.1 SIEM and Security Monitoring

- Wazuh
- Sysmon
- Windows Event Viewer
- Windows Event Logs
- Linux System Logs

### 5.2 Network Security

- Wireshark
- tcpdump
- Nmap

### 5.3 Threat Intelligence

- MITRE ATT&CK
- IOC Analysis
- Threat Intelligence Platforms
- Approved Threat Intelligence Sources

### 5.4 Vulnerability Management

- Nessus
- Nmap
- CVE Databases
- Vulnerability Intelligence Sources

### 5.5 Automation

- Python
- Bash
- REST APIs
- JSON
- SQLite

### 5.6 Documentation

- Markdown
- GitHub
- Screenshots
- Logs
- Investigation Reports

---

# 6. Lab Categories

## 6.1 Wazuh SIEM Labs

These labs focus on deploying, configuring, and operating Wazuh as the primary SIEM and security monitoring platform.

Topics include:

- Wazuh architecture
- Wazuh manager
- Wazuh agents
- Agent deployment
- Agent connectivity
- Log collection
- Security alerts
- Alert investigation
- Wazuh rules
- Wazuh dashboards
- File Integrity Monitoring
- Vulnerability Detection
- Security Configuration Assessment

---

## 6.2 Windows Security Monitoring Labs

These labs focus on monitoring Windows systems.

Topics include:

- Windows Event Logs
- Security Events
- Authentication Events
- Account Activity
- Process Creation
- PowerShell Activity
- Failed Logins
- Successful Logins
- Privilege-Related Events
- Suspicious Process Activity
- Endpoint Investigation

---

## 6.3 Linux Security Monitoring Labs

These labs focus on monitoring Linux systems.

Topics include:

- Linux Authentication Logs
- SSH Activity
- User Activity
- System Logs
- Process Activity
- Privilege-Related Events
- Login Monitoring
- Suspicious Command Activity
- Linux Endpoint Investigation

---

## 6.4 Sysmon Endpoint Monitoring Labs

These labs focus on Windows endpoint telemetry using Sysmon.

Topics include:

- Sysmon Installation
- Sysmon Configuration
- Process Creation
- Parent-Child Process Relationships
- Network Connections
- File Creation
- Registry Activity
- DNS Activity
- Process Investigation
- Endpoint Telemetry Analysis

---

## 6.5 Network Traffic Analysis Labs

These labs focus on network visibility and packet analysis.

Topics include:

- Packet Capture
- Packet Inspection
- TCP Analysis
- UDP Analysis
- DNS Analysis
- HTTP Analysis
- Network Connections
- Suspicious Traffic
- Network Indicators
- Traffic Investigation

Primary tools include:

- Wireshark
- tcpdump

---

## 6.6 IOC Investigation Labs

These labs focus on investigating Indicators of Compromise.

IOC types include:

- IP Addresses
- Domains
- URLs
- File Hashes
- Email Addresses
- Network Indicators
- Host Indicators

Activities include:

- IOC Validation
- IOC Normalization
- IOC Enrichment
- Reputation Analysis
- Internal Telemetry Correlation
- IOC Prioritization

---

## 6.7 Threat Intelligence Labs

These labs focus on transforming external threat information into actionable security intelligence.

Topics include:

- Threat Intelligence Lifecycle
- Intelligence Collection
- IOC Analysis
- Threat Actor Analysis
- Malware Intelligence
- TTP Analysis
- MITRE ATT&CK Mapping
- Intelligence Enrichment
- Threat Prioritization
- Intelligence Reporting

---

## 6.8 Threat Hunting Labs

These labs focus on proactively identifying suspicious activity.

Topics include:

- Hunting Hypotheses
- Data Source Selection
- Log Searching
- Behavioral Analysis
- IOC Hunting
- TTP Hunting
- MITRE ATT&CK Mapping
- Suspicious Activity Investigation
- Detection Gaps

General workflow:

Threat Intelligence
↓
Hunting Hypothesis
↓
Identify Data Sources
↓
Search Telemetry
↓
Analyze Results
↓
Validate Findings
↓
Create Detection

---

## 6.9 Detection Engineering Labs

These labs focus on creating and improving security detections.

Topics include:

- Detection Logic
- SIEM Rules
- Correlation
- Behavioral Detection
- IOC-Based Detection
- TTP-Based Detection
- Detection Testing
- False-Positive Analysis
- Detection Tuning
- MITRE ATT&CK Mapping

---

## 6.10 Phishing Analysis Labs

These labs focus on analyzing simulated phishing incidents.

Topics include:

- Email Analysis
- Email Headers
- Sender Information
- URLs
- Domains
- Attachments
- IOC Extraction
- Threat Intelligence
- User Impact
- Phishing Investigation

---

## 6.11 Incident Response Labs

These labs simulate the incident response lifecycle.

Topics include:

- Incident Identification
- Initial Triage
- Investigation
- Evidence Collection
- Containment
- Eradication
- Recovery
- Lessons Learned
- Incident Reporting

General workflow:

Preparation
↓
Detection
↓
Triage
↓
Investigation
↓
Containment
↓
Eradication
↓
Recovery
↓
Lessons Learned

---

## 6.12 Digital Forensics Labs

These labs focus on evidence-based investigation.

Topics include:

- Evidence Collection
- Evidence Preservation
- Timeline Analysis
- File Analysis
- Event Analysis
- System Artifacts
- Endpoint Investigation
- Forensic Documentation

---

## 6.13 Vulnerability Monitoring Labs

These labs focus on identifying and prioritizing vulnerabilities.

Topics include:

- Asset Discovery
- Vulnerability Scanning
- CVE Research
- Vulnerability Validation
- Risk Assessment
- Vulnerability Prioritization
- Remediation Planning
- Remediation Validation

---

## 6.14 SOC Automation Labs

These labs focus on automating repetitive SOC tasks.

Topics include:

- Python
- REST APIs
- JSON
- IOC Enrichment
- Alert Enrichment
- Log Processing
- Data Normalization
- Automated Reporting
- Security Workflow Automation

---

# 7. Lab Documentation Standard

Every major lab should contain the following sections.

## 7.1 Lab Title

Provide a clear and descriptive title.

## 7.2 Objective

Explain what the lab is designed to demonstrate.

## 7.3 Scenario

Describe the realistic security situation being simulated.

## 7.4 Scope

Clearly define the systems and activities included in the lab.

## 7.5 Environment

Document:

- Operating Systems
- Virtual Machines
- Network Configuration
- Security Tools
- Relevant Versions

## 7.6 Architecture

Document the technical architecture and telemetry flow.

## 7.7 Tools

List the tools used.

## 7.8 Procedure

Document the major steps performed.

## 7.9 Security Activity

Describe the authorized activity used to generate telemetry.

## 7.10 Telemetry

Document the logs, events, or network traffic generated.

## 7.11 Detection

Explain:

- What detected the activity?
- Which log source was used?
- Which rule or query triggered?
- What alert was generated?

## 7.12 Investigation

Document:

- Timestamp
- Host
- User
- Process
- Parent Process
- Network Activity
- IOC
- Related Events
- Investigation Timeline

## 7.13 Analysis

Explain what the evidence indicates.

Clearly distinguish between:

- Facts
- Observations
- Assumptions
- Conclusions

## 7.14 MITRE ATT&CK Mapping

Map relevant observed behaviors to appropriate MITRE ATT&CK techniques.

Only map techniques supported by evidence.

## 7.15 Response

Document the appropriate defensive response.

## 7.16 Evidence

Include relevant:

- Screenshots
- Logs
- Queries
- Command Output
- Detection Alerts
- Investigation Notes

## 7.17 Lessons Learned

Document the main technical and operational lessons.

## 7.18 Improvements

Explain how the monitoring, detection, investigation, or response process could be improved.

---

# 8. Recommended Lab Directory Structure

Each lab can use the following structure:

XX-Lab-Name/
├── README.md
├── screenshots/
├── evidence/
├── logs/
├── queries/
└── scripts/

Additional directories should only be added when they provide meaningful value.

---

# 9. Lab Naming Convention

Labs should use a consistent naming convention.

Format:

XX-Lab-Name

Examples:

- 01-Wazuh-SIEM-Lab
- 02-Windows-Security-Monitoring
- 03-Linux-Security-Monitoring
- 04-Sysmon-Endpoint-Monitoring
- 05-Network-Traffic-Analysis
- 06-IOC-Investigation
- 07-Threat-Hunting
- 08-Detection-Engineering
- 09-Phishing-Analysis
- 10-Incident-Response
- 11-Digital-Forensics
- 12-Vulnerability-Monitoring
- 13-SOC-Automation

---

# 10. Evidence Standard

Evidence should demonstrate actual hands-on work.

Examples include:

- Wazuh dashboard screenshots
- Wazuh alerts
- Windows Event Logs
- Sysmon events
- Linux logs
- Packet captures
- SIEM queries
- Threat intelligence results
- Detection rules
- Threat-hunting queries
- Investigation timelines
- Python scripts
- Automation results

Evidence should be clear enough for another person to understand what was performed.

---

# 11. Security and Privacy

Before publishing evidence to GitHub:

- Remove usernames where unnecessary.
- Remove passwords and credentials.
- Remove API keys.
- Remove tokens.
- Remove private IP information where appropriate.
- Remove personal information.
- Remove sensitive network details.
- Remove confidential logs.
- Review screenshots before publishing.

Never publish secrets or credentials.

---

# 12. Lab Safety

All activities must be performed in authorized environments.

Allowed environments include:

- Personally controlled systems
- Authorized virtual machines
- Intentionally vulnerable laboratory systems
- Approved datasets
- Authorized services

Do not perform unauthorized scanning, exploitation, credential attacks, persistence, privilege escalation, network attacks, or data collection against systems that you do not own or have explicit permission to test.

---

# 13. Lab Progression

The labs should gradually increase in complexity.

Fundamentals
↓
Monitoring
↓
Detection
↓
Investigation
↓
Threat Intelligence
↓
Threat Hunting
↓
Incident Response
↓
Digital Forensics
↓
Automation
↓
AI-Assisted SOC
↓
Integrated SOC Operations

---

# 14. AI-Assisted SOC Labs

AI can be integrated into selected laboratories as an analyst assistant.

Potential use cases include:

- Alert Summarization
- Log Summarization
- IOC Extraction
- Threat Intelligence Summarization
- Investigation Assistance
- Query Generation
- Report Drafting
- Documentation Assistance

Recommended workflow:

Security Data
↓
AI Assistance
↓
Preliminary Output
↓
Analyst Validation
↓
Confirmed Result

AI-generated information should not automatically be treated as a confirmed security finding.

---

# 15. Security Automation

Automation should focus on repetitive, predictable, and well-defined tasks.

Examples:

- IOC Enrichment
- Log Parsing
- Alert Enrichment
- Data Normalization
- Report Generation
- Threat Intelligence Processing
- KPI Calculation

High-impact security actions should have appropriate human approval.

---

# 16. Lab Completion Criteria

A lab can be marked complete when:

- [ ] Objective is defined.
- [ ] Scenario is documented.
- [ ] Environment is documented.
- [ ] Tools are documented.
- [ ] Lab was successfully configured.
- [ ] Security activity was generated.
- [ ] Telemetry was collected.
- [ ] Activity was detected.
- [ ] Investigation was performed.
- [ ] Evidence was collected.
- [ ] Findings were documented.
- [ ] MITRE ATT&CK mapping was completed where applicable.
- [ ] Lessons learned were documented.
- [ ] Improvements were identified.
- [ ] Sensitive information was removed.
- [ ] README.md was updated.

---

# 17. Labs vs Projects

Labs and projects have different purposes.

LABS

Individual Skill
↓
Tool Configuration
↓
Focused Exercise
↓
Investigation
↓
Evidence
↓
Documentation

PROJECTS

Multiple Skills
↓
Realistic Scenario
↓
Detection
↓
Investigation
↓
Response
↓
Automation
↓
Professional Reporting

Therefore:

**Labs = Individual Skill Evidence**

**Projects = End-to-End Capability Evidence**

---

# 18. Relationship With SOC Knowledge Base

The SOC knowledge directories provide the theoretical foundation.

SOC Knowledge Base
↓
Hands-on Labs
↓
SOC Projects
↓
Portfolio Evidence
↓
Job Readiness

The overall learning model is:

**Learn → Practice → Build → Investigate → Document → Showcase**

---

# 19. Relationship With SOC Projects

Individual labs provide building blocks for larger SOC projects.

Example:

Wazuh SIEM Lab
+
Windows Monitoring Lab
+
Sysmon Lab
+
Threat Intelligence Lab
+
Threat Hunting Lab
+
Incident Response Lab
↓
SOC Incident Investigation Project

This approach demonstrates how individual technical skills can be combined into an operational SOC workflow.

---

# 20. Portfolio Objective

The purpose of the SOC Labs directory is to demonstrate that cybersecurity knowledge can be converted into practical technical capability.

The target progression is:

**Learn → Practice → Detect → Investigate → Respond → Automate → Document → Demonstrate**

---

# 21. Career Relevance

The completed labs are intended to provide practical evidence for roles such as:

- SOC Analyst L1
- Junior SOC Analyst
- Cybersecurity Analyst
- Security Operations Intern
- Security Monitoring Analyst
- Threat Intelligence Analyst
- Vulnerability Management Analyst
- Junior Threat Hunter

The labs should prioritize practical SOC skills and job-relevant capabilities.

---

# 22. Final Principle

A successful SOC lab should not simply prove that a security tool can generate an alert.

It should demonstrate that the analyst understands:

**What happened → How it was detected → How it was investigated → What the evidence means → What action should be taken → How the process can be improved**

The ultimate purpose of this directory is to build credible, reproducible, and professional evidence of hands-on SOC capability.

---

# 23. Disclaimer

All activities documented in this directory are performed in authorized laboratory environments for educational and defensive cybersecurity purposes.

No unauthorized systems, networks, accounts, or infrastructure should be targeted.

---

# 24. Status

This directory is continuously updated as new SOC skills, tools, investigation techniques, detection workflows, automation capabilities, and AI-assisted security workflows are learned and practiced.
