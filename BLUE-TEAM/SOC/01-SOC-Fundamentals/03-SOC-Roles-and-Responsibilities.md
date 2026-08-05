# 👥 SOC Roles & Responsibilities

> A SOC is a team-based security operation in which different roles work together to detect, investigate, respond to, and improve an organization's security posture.

The exact organizational structure varies between companies, but the responsibilities generally become more specialized as security operations mature.

---

# 1. SOC Organizational Structure

A simplified structure:

```text
SOC Manager
     │
     ├── SOC L1
     │
     ├── SOC L2
     │
     ├── SOC L3
     │
     ├── Detection Engineering
     │
     ├── Threat Intelligence
     │
     ├── Threat Hunting
     │
     └── Incident Response
```

In smaller organizations, one person may perform several of these functions.

In larger organizations, each may be a dedicated team.

---

# 2. SOC Manager

The SOC Manager is responsible for the overall operation and performance of the SOC.

## Key Responsibilities

* Team management
* Resource planning
* Shift planning
* Security operations strategy
* SLA management
* Incident coordination
* Performance monitoring
* Risk reporting
* Stakeholder communication
* Process improvement
* Training and development

## Typical Questions

The SOC Manager focuses on questions such as:

> Are we detecting threats effectively?

> Are incidents being handled within SLA?

> Do we have sufficient staffing?

> Where are the biggest operational gaps?

> What security capabilities need improvement?

---

# 3. SOC Analyst L1

SOC L1 is generally the entry-level operational role and is highly relevant for a cybersecurity fresher.

## Primary Objective

> **Monitor, triage, document and escalate security alerts.**

## Responsibilities

### Monitoring

* Monitor SIEM dashboards
* Monitor security alerts
* Review security events
* Identify unusual activity

### Initial Triage

* Validate the alert
* Identify affected asset
* Identify affected user
* Check timestamps
* Examine source/destination information
* Review related events

### IOC Analysis

Identify:

* IP addresses
* Domains
* URLs
* Hashes
* File names
* User accounts
* Hostnames

### Classification

Determine whether the alert is:

* Benign
* False Positive
* Suspicious
* True Positive
* Confirmed Incident

### Escalation

Escalate when:

* Severity is high
* Investigation exceeds L1 capability
* Critical assets are involved
* Privileged accounts are involved
* Multiple systems are affected
* Compromise is suspected

### Documentation

Record:

* What happened
* What evidence was found
* What was checked
* What conclusion was reached
* What action was taken

---

# 4. SOC L1 Daily Workflow

A simplified workflow:

```text
Login
  ↓
Check SOC Dashboard
  ↓
Review New Alerts
  ↓
Prioritize
  ↓
Select Alert
  ↓
Triage
  ↓
Investigate
  ↓
Document
  ↓
Close / Escalate
```

A good L1 analyst should develop the ability to investigate efficiently without jumping to conclusions.

---

# 5. SOC L2 Analyst

L2 performs deeper investigation after L1 escalation.

## Responsibilities

* Advanced alert investigation
* Event correlation
* Host investigation
* User/account investigation
* Threat analysis
* Root-cause analysis
* Threat hunting
* Detection tuning
* Incident support

## Typical Question

> **"What actually happened, how did it happen, and what is the scope?"**

---

# 6. SOC L2 Investigation

Example:

```text
L1 Alert
   ↓
Multiple failed logins
   ↓
L1 identifies successful login
   ↓
Escalate to L2
   ↓
L2 investigates account
   ↓
Correlates endpoint activity
   ↓
Finds suspicious PowerShell
   ↓
Identifies external connection
   ↓
Determines possible account compromise
```

L2 therefore moves beyond:

> "Is this alert real?"

toward:

> "What is the complete attack story?"

---

# 7. SOC L3 Analyst

L3 handles complex security problems.

## Responsibilities

* Advanced threat hunting
* Advanced incident investigation
* Detection engineering
* Malware analysis
* Digital forensics
* Advanced adversary analysis
* Complex incident response
* Security architecture support

L3 may also support L1 and L2 by developing investigation methods and improving detection capabilities.

---

# 8. Detection Engineer

Detection engineers convert threat intelligence and adversary behavior into detection logic.

## Responsibilities

* Develop detection rules
* Create SIEM queries
* Create EDR detections
* Map detections to ATT&CK techniques
* Test detections
* Tune detection logic
* Reduce false positives
* Improve detection coverage

Typical workflow:

```text
Threat
 ↓
Adversary Behavior
 ↓
TTP
 ↓
Telemetry
 ↓
Detection Logic
 ↓
Testing
 ↓
Deployment
 ↓
Monitoring
 ↓
Tuning
```

---

# 9. Threat Hunter

Threat hunters proactively search for threats that may not have generated an alert.

## Traditional SOC

```text
Alert
 ↓
Investigation
```

## Threat Hunting

```text
Hypothesis
 ↓
Search
 ↓
Query
 ↓
Analysis
 ↓
Finding
```

Example hypothesis:

> "An attacker may be using PowerShell for command execution inside the environment."

The hunter searches telemetry for evidence.

---

# 10. Incident Responder

Incident responders manage confirmed or significant security incidents.

## Responsibilities

* Incident containment
* Eradication
* Recovery
* Evidence preservation
* Incident coordination
* Root-cause analysis
* Post-incident review

Example:

```text
SOC
 ↓
Detection
 ↓
Investigation
 ↓
Confirmed Incident
 ↓
Incident Response
 ↓
Containment
 ↓
Eradication
 ↓
Recovery
```

---

# 11. Threat Intelligence Analyst

Threat intelligence analysts provide information about threats and adversaries.

They may research:

* Threat actors
* Malware
* Campaigns
* Infrastructure
* IOCs
* TTPs
* Vulnerabilities
* Attack techniques

Their output can support:

```text
Detection
Threat Hunting
Incident Investigation
Incident Response
Risk Management
```

---

# 12. Security Engineer

Security engineers build and maintain the technical security infrastructure.

Responsibilities may include:

* SIEM deployment
* EDR deployment
* Security integrations
* Network security
* Identity security
* Security architecture
* Detection infrastructure
* Security automation

They focus heavily on:

> **Building and maintaining security capability.**

---

# 13. Security Automation / SOAR Engineer

Automation specialists improve SOC efficiency.

They may build workflows such as:

```text
Alert
 ↓
Extract IOC
 ↓
Threat Intelligence Lookup
 ↓
Enrichment
 ↓
Risk Assessment
 ↓
Ticket Creation
 ↓
Analyst Notification
```

The goal is to reduce repetitive manual work.

---

# 14. Vulnerability Management Analyst

Vulnerability management is closely related to defensive security operations.

Responsibilities may include:

* Vulnerability scanning
* Risk prioritization
* Asset identification
* CVE analysis
* Remediation tracking
* Validation
* Reporting

Example:

```text
Scan
 ↓
Identify Vulnerability
 ↓
Assess Risk
 ↓
Prioritize
 ↓
Remediate
 ↓
Rescan
 ↓
Validate
```

---

# 15. SOC Analyst vs Vulnerability Analyst

These roles are related but different.

| SOC Analyst                | Vulnerability Analyst        |
| -------------------------- | ---------------------------- |
| Detects threats            | Identifies weaknesses        |
| Investigates alerts        | Analyzes vulnerabilities     |
| Handles incidents          | Tracks remediation           |
| Focuses on active activity | Focuses on security exposure |
| SIEM/EDR                   | Nessus/Qualys/Tenable etc.   |

Both contribute to reducing cyber risk.

---

# 16. GRC and SOC Collaboration

SOC teams generate valuable operational security information.

GRC teams use this information for:

* Risk assessment
* Compliance
* Audit evidence
* Control monitoring
* Incident reporting
* Security governance

Example:

```text
SOC
 ↓
Security Incident Data
 ↓
GRC
 ↓
Risk Assessment
 ↓
Control Improvement
 ↓
Management Reporting
```

This creates an important bridge between technical security and governance.

---

# 17. SOC and VAPT Collaboration

VAPT teams identify vulnerabilities and attack paths.

SOC teams determine whether suspicious activity associated with those attack paths can be detected.

Example:

```text
VAPT
 ↓
Identify Attack Path
 ↓
Simulate Attack
 ↓
Generate Telemetry
 ↓
SOC
 ↓
Detection
 ↓
Investigation
```

This creates a valuable:

> **Offense → Defense feedback loop**

---

# 18. SOC and Cloud Security

Cloud environments introduce additional monitoring requirements.

SOC analysts may investigate:

* Cloud authentication
* IAM changes
* API activity
* Storage access
* Resource creation
* Security-group changes
* Privilege escalation

Example:

```text
Cloud IAM Event
 ↓
SIEM
 ↓
Detection
 ↓
Alert
 ↓
SOC Investigation
```

---

# 19. SOC and IAM

Identity is one of the most important areas of modern security monitoring.

SOC analysts may investigate:

* Brute-force attempts
* Password spraying
* Impossible travel
* Privilege escalation
* MFA anomalies
* New account creation
* Suspicious login locations
* Service-account activity

Example:

```text
Multiple Failed Logins
        ↓
Successful Login
        ↓
Privilege Change
        ↓
Suspicious Activity
        ↓
SOC Investigation
```

---

# 20. SOC and AI

AI is increasingly becoming an augmentation layer for SOC operations.

Possible applications include:

### Alert Summarization

Convert complex alert data into a concise investigation summary.

### Investigation Assistance

Help analysts identify relevant events.

### IOC Enrichment

Provide additional context around:

* IPs
* Domains
* Hashes
* URLs

### Detection Development

Assist with:

* Query creation
* Detection-rule drafting
* ATT&CK mapping

### Reporting

Generate initial investigation reports for analyst review.

The correct model is:

```text
AI
 ↓
Assistance
 ↓
Human Verification
 ↓
Security Decision
```

---

# 21. Responsibility Matrix

A simplified responsibility model:

| Activity           | L1 | L2 | L3 | Detection Engineer | IR |
| ------------------ | -: | -: | -: | -----------------: | -: |
| Alert Monitoring   |  ✅ |  ◐ |  ◐ |                  ❌ |  ❌ |
| Initial Triage     |  ✅ |  ✅ |  ◐ |                  ❌ |  ◐ |
| Deep Investigation |  ❌ |  ✅ |  ✅ |                  ◐ |  ✅ |
| Threat Hunting     |  ❌ |  ✅ |  ✅ |                  ◐ |  ◐ |
| Detection Creation |  ❌ |  ◐ |  ✅ |                  ✅ |  ◐ |
| Incident Response  |  ◐ |  ✅ |  ✅ |                  ◐ |  ✅ |
| Malware Analysis   |  ❌ |  ◐ |  ✅ |                  ❌ |  ✅ |
| Documentation      |  ✅ |  ✅ |  ✅ |                  ✅ |  ✅ |
| Escalation         |  ✅ |  ✅ |  ✅ |                  ◐ |  ◐ |

Legend:

```text
✅ = Primary responsibility
◐ = Supporting responsibility
❌ = Usually not primary
```

Actual responsibilities vary between organizations.

---

# 22. Example Incident — Who Does What?

Consider a suspected ransomware incident.

### L1

```text
Detect Alert
 ↓
Triage
 ↓
Identify Affected Host
 ↓
Escalate
```

### L2

```text
Investigate Host
 ↓
Correlate Events
 ↓
Identify Attack Scope
 ↓
Determine Initial Attack Vector
```

### L3

```text
Advanced Analysis
 ↓
Adversary Behavior
 ↓
Detection Improvement
 ↓
Advanced Response Support
```

### Incident Response

```text
Contain
 ↓
Eradicate
 ↓
Recover
 ↓
Coordinate Incident
```

### Detection Engineering

```text
Analyze Attack
 ↓
Create / Improve Detection
 ↓
Test
 ↓
Deploy
```

---

# 23. Career Progression

A possible technical SOC progression:

```text
SOC Intern / Trainee
        ↓
SOC Analyst L1
        ↓
SOC Analyst L2
        ↓
SOC Analyst L3
        ↓
Senior Security Analyst
        ↓
Detection Engineer / Threat Hunter /
Incident Responder / Security Engineer
        ↓
Security Architect / Security Lead
```

There is no single mandatory career path.

Analysts can specialize based on interests and strengths.

---

# 24. My Learning Target

My initial goal is to become:

> **Job-ready for a SOC L1 / junior defensive-security role.**

The learning progression will be:

```text
SOC Fundamentals
       ↓
SOC L1
       ↓
SIEM
       ↓
Log Analysis
       ↓
Alert Triage
       ↓
Detection Rules
       ↓
Investigation
       ↓
Incident Response
       ↓
Threat Intelligence
       ↓
Threat Hunting
```

Later:

```text
SOC L2
 ↓
Advanced Investigation
 ↓
Detection Engineering
 ↓
Threat Hunting
 ↓
Advanced Incident Response
```

Eventually:

```text
SOC L3
 ↓
Advanced Detection
 ↓
Security Engineering
 ↓
Security Architecture
```

---

# 25. Practical Portfolio Mapping

This knowledge will not remain theoretical.

Each role will be connected to practical portfolio evidence.

## SOC L1

```text
SIEM Labs
Alert Triage
Log Analysis
TryHackMe SOC Rooms
Investigation Reports
```

## SOC L2

```text
Threat Hunting
Advanced Investigations
Detection Engineering
Incident Case Studies
```

## SOC L3

```text
Advanced Detection
Adversary Simulation
Malware Analysis
Complex Incident Response
```

## Detection Engineering

```text
Detection Rules
MITRE ATT&CK Mapping
Rule Testing
False-Positive Tuning
```

## Incident Response

```text
Incident Reports
Timeline Analysis
Containment Plans
Lessons Learned
```

---

# 26. Interview Questions I Should Be Able to Answer

After studying this document, I should be able to explain:

### Basic

* What does a SOC analyst do?
* What does an L1 analyst do?
* What does an L2 analyst do?
* What does an L3 analyst do?

### Operational

* When should L1 escalate an alert?
* What information should an analyst document?
* What is the difference between triage and investigation?
* What is the role of a detection engineer?

### Advanced

* How does threat hunting differ from alert-driven monitoring?
* How does SOC work with incident response?
* How does SOC work with VAPT?
* How does SOC work with GRC?
* How can AI augment SOC operations?

---

# 27. Key Takeaways

The most important responsibility boundaries are:

```text
L1
 ↓
Monitor + Triage + Escalate
```

```text
L2
 ↓
Investigate + Correlate + Hunt
```

```text
L3
 ↓
Advanced Investigation + Engineering
```

```text
Detection Engineer
 ↓
Build + Test + Tune Detections
```

```text
Threat Hunter
 ↓
Proactively Search for Threats
```

```text
Incident Responder
 ↓
Contain + Eradicate + Recover
```

```text
SOC Manager
 ↓
Operate + Manage + Improve the SOC
```

---

# ⭐ Core Principle

> **A SOC is a team sport. Effective cybersecurity operations depend on knowing who is responsible for monitoring, who investigates, who escalates, who responds, and who improves the defenses afterward.**

---

# 📚 Related Documents

Previous:

```text
01-What-is-SOC.md
02-SOC-People-Process-Technology.md
```

Next:

```text
04-SOC-Tiers-L1-L2-L3.md
```

Later:

```text
05-SOC-Workflow.md
06-Security-Telemetry.md
07-Logs-and-Events.md
```
