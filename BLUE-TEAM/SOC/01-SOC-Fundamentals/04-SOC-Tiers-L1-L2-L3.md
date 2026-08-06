# 🛡️ SOC Tiers — L1, L2 & L3

> SOC tiers represent different levels of security monitoring, investigation, analysis, and response capability. The exact responsibilities vary by organization, but the progression generally moves from **initial alert triage → deeper investigation → advanced analysis and engineering**.

---

# 1. SOC Tier Overview

A simplified SOC structure is:

```text
                    SECURITY ALERT
                          │
                          ▼
                    ┌───────────┐
                    │  SOC L1   │
                    │ Monitoring│
                    │  & Triage │
                    └─────┬─────┘
                          │
                ┌─────────┴─────────┐
                │                   │
              Close              Escalate
                                    │
                                    ▼
                              ┌───────────┐
                              │  SOC L2   │
                              │  Deep     │
                              │Investigation
                              └─────┬─────┘
                                    │
                              ┌─────┴─────┐
                              │           │
                           Resolve     Escalate
                                          │
                                          ▼
                                    ┌───────────┐
                                    │  SOC L3   │
                                    │ Advanced  │
                                    │ Analysis  │
                                    └───────────┘
```

The basic progression is:

```text
L1 → Detect & Triage
L2 → Investigate & Analyze
L3 → Engineer & Resolve Complex Threats
```

---

# 2. SOC L1

## Primary Role

SOC L1 is the first operational layer responsible for monitoring security alerts and performing initial investigation.

The primary objective is:

> **Determine whether an alert requires further action.**

---

# 3. SOC L1 Responsibilities

Typical responsibilities include:

* Monitor SIEM dashboards
* Review incoming alerts
* Prioritize alerts
* Perform initial triage
* Validate alerts
* Identify affected assets
* Identify affected users
* Analyze basic logs
* Investigate IOCs
* Check threat intelligence
* Identify false positives
* Document findings
* Escalate suspicious activity

---

# 4. L1 Mental Model

L1 should think:

```text
What happened?
      ↓
Is this expected?
      ↓
Is this suspicious?
      ↓
What evidence do I have?
      ↓
Does this require escalation?
```

L1 should avoid immediately assuming:

> "This is definitely an attack."

Instead:

> **Validate first.**

---

# 5. L1 Alert Triage

A practical triage workflow:

```text
ALERT
  ↓
Read Alert
  ↓
Understand Detection
  ↓
Identify Asset
  ↓
Identify User
  ↓
Check Timestamp
  ↓
Review Related Events
  ↓
Check IOC
  ↓
Assess Context
  ↓
Classify
```

Possible outcomes:

```text
False Positive
Benign Positive
Suspicious
True Positive
Confirmed Incident
```

---

# 6. L1 Investigation Example

Suppose the SOC receives:

```text
Alert:
Multiple Failed Login Attempts

User:
administrator

Source:
192.168.1.50

Severity:
Medium
```

L1 should investigate:

```text
How many attempts?
 ↓
Which accounts?
 ↓
Which source?
 ↓
Was there a successful login?
 ↓
Is the source known?
 ↓
Was the activity expected?
 ↓
Any activity after login?
```

If a successful login is followed by suspicious endpoint activity, escalation becomes appropriate.

---

# 7. L1 Escalation

L1 should escalate when:

* Compromise is suspected
* High-value assets are involved
* Privileged accounts are involved
* Multiple systems are affected
* The investigation requires advanced analysis
* Evidence suggests active attack activity
* Incident response may be required
* The analyst cannot confidently determine the outcome

---

# 8. Good L1 Escalation

A useful escalation contains evidence.

```text
Alert:
Suspicious PowerShell Execution

Host:
WIN-CLIENT01

User:
admin

Observed:
Encoded PowerShell command

Related Activity:
External connection to suspicious IP

Timeline:
10:03 — User login
10:05 — PowerShell execution
10:06 — External connection

Assessment:
Potential malicious execution

Recommended:
L2 investigation
```

Bad escalation:

```text
"Suspicious alert. Please investigate."
```

---

# 9. SOC L2

## Primary Role

L2 analysts perform deeper investigations and handle escalated cases.

The primary question changes from:

> **"Is this alert suspicious?"**

to:

> **"What actually happened, how did it happen, and what is the scope?"**

---

# 10. L2 Responsibilities

Typical responsibilities include:

* Advanced alert investigation
* Event correlation
* Timeline reconstruction
* Host investigation
* User investigation
* Threat intelligence analysis
* IOC enrichment
* Attack-chain analysis
* Root-cause analysis
* Threat hunting
* Detection tuning
* Incident response support
* L1 guidance
* Case escalation

---

# 11. L2 Investigation Model

```text
L1 Escalation
      ↓
Validate Evidence
      ↓
Expand Investigation
      ↓
Correlate Events
      ↓
Build Timeline
      ↓
Identify Attack Technique
      ↓
Determine Scope
      ↓
Identify Root Cause
      ↓
Recommend Response
```

---

# 12. Event Correlation

L2 should connect multiple sources.

Example:

```text
Authentication Logs
        +
Endpoint Logs
        +
DNS Logs
        +
Firewall Logs
        +
EDR Telemetry
        ↓
Complete Attack Story
```

Example sequence:

```text
09:58
Failed authentication

10:00
Successful authentication

10:03
PowerShell execution

10:04
Encoded command

10:05
DNS query

10:06
External network connection

10:08
Suspicious file creation
```

L2 analyzes the complete sequence rather than individual events.

---

# 13. Attack Timeline

A timeline helps reconstruct attacker activity.

```text
Initial Access
      ↓
Execution
      ↓
Persistence
      ↓
Privilege Escalation
      ↓
Credential Access
      ↓
Discovery
      ↓
Lateral Movement
      ↓
Command & Control
      ↓
Impact
```

Not every incident will contain every stage.

---

# 14. L2 Threat Intelligence

L2 may enrich:

```text
IP Addresses
Domains
URLs
File Hashes
Email Addresses
Malware Families
Threat Actors
```

The objective is to understand:

```text
Who / What?
     ↓
Known Threat?
     ↓
Associated Campaign?
     ↓
Related Infrastructure?
     ↓
Expected TTPs?
```

---

# 15. L2 MITRE ATT&CK Mapping

L2 should map observed behavior to ATT&CK techniques where appropriate.

Example:

```text
PowerShell
    ↓
Command and Scripting Interpreter
    ↓
PowerShell
```

Another example:

```text
Credential Dumping
    ↓
Credential Access
```

Mapping helps:

* Describe attacker behavior
* Identify additional investigation paths
* Improve detections
* Identify defensive gaps

---

# 16. L2 Root-Cause Analysis

The objective is to determine:

```text
What happened?
      ↓
How did the attacker gain access?
      ↓
Why was it possible?
      ↓
What allowed persistence?
      ↓
Why wasn't it detected earlier?
      ↓
What controls failed?
```

Example:

```text
Phishing Email
      ↓
Credential Theft
      ↓
Account Compromise
      ↓
VPN Access
      ↓
Internal Discovery
```

Possible root causes:

* Weak authentication
* Lack of MFA
* User credential exposure
* Excessive privileges
* Missing detection
* Vulnerable endpoint
* Poor segmentation

---

# 17. SOC L3

## Primary Role

L3 represents the advanced technical layer of the SOC.

The focus moves toward:

```text
Advanced Investigation
Detection Engineering
Threat Hunting
Malware Analysis
Digital Forensics
Adversary Analysis
Security Engineering
```

The exact responsibilities vary considerably between organizations.

---

# 18. L3 Responsibilities

Typical responsibilities can include:

* Complex incident investigation
* Advanced threat hunting
* Malware analysis
* Digital forensics
* Detection engineering
* Advanced detection tuning
* Adversary analysis
* Detection architecture
* Security engineering
* Advanced incident response
* Supporting security architecture decisions
* Developing investigation methodologies

---

# 19. L3 Mental Model

L3 asks:

```text
What happened?
      ↓
How did it happen?
      ↓
Why wasn't it detected?
      ↓
What techniques were used?
      ↓
What detection gaps exist?
      ↓
How do we prevent recurrence?
```

The focus becomes increasingly systemic.

---

# 20. Detection Engineering

L3 or dedicated detection engineers may develop sophisticated detections.

Workflow:

```text
Threat Intelligence
       ↓
Threat Behavior
       ↓
MITRE ATT&CK
       ↓
Required Telemetry
       ↓
Detection Logic
       ↓
Testing
       ↓
False Positive Analysis
       ↓
Tuning
       ↓
Deployment
```

---

# 21. Threat Hunting

Threat hunting differs from traditional alert monitoring.

### Alert-driven SOC

```text
Detection
   ↓
Alert
   ↓
Investigation
```

### Threat Hunting

```text
Hypothesis
   ↓
Search
   ↓
Analysis
   ↓
Finding
   ↓
Detection Improvement
```

Example hypothesis:

> "An attacker may be using PowerShell to execute commands on endpoints."

The hunter searches available telemetry for evidence.

---

# 22. Advanced Incident Response

L3 may support complex incidents such as:

```text
Ransomware
Advanced Persistent Threats
Large-scale Account Compromise
Data Exfiltration
Supply-chain Compromise
Advanced Malware
Insider Threat
```

Activities may include:

```text
Forensics
Malware Analysis
Adversary Tracking
Containment Strategy
Eradication
Recovery
Post-Incident Analysis
```

---

# 23. L1 vs L2 vs L3

| Capability            | L1       | L2       | L3                 |
| --------------------- | -------- | -------- | ------------------ |
| Alert Monitoring      | Primary  | Support  | Support            |
| Initial Triage        | Primary  | Advanced | Advanced           |
| Log Analysis          | Basic    | Advanced | Advanced           |
| Event Correlation     | Basic    | Primary  | Advanced           |
| IOC Analysis          | Basic    | Advanced | Advanced           |
| Threat Intelligence   | Basic    | Primary  | Advanced           |
| Threat Hunting        | Limited  | Yes      | Advanced           |
| Detection Engineering | Limited  | Support  | Primary / Advanced |
| Incident Response     | Escalate | Support  | Advanced           |
| Malware Analysis      | No       | Limited  | Yes                |
| Digital Forensics     | No       | Limited  | Advanced           |
| Root Cause Analysis   | Limited  | Primary  | Advanced           |
| Detection Tuning      | Limited  | Yes      | Advanced           |
| Security Engineering  | No       | Limited  | Yes                |

This is a generalized model; organizations structure SOC roles differently.

---

# 24. Example: Phishing Incident

Consider a malicious phishing email.

### L1

```text
Receive Alert
      ↓
Check Sender
      ↓
Check URL
      ↓
Check Attachment
      ↓
Check User
      ↓
Check IOC Reputation
      ↓
Determine Suspicious?
      ↓
Escalate
```

### L2

```text
Investigate Email
      ↓
Analyze URL
      ↓
Analyze Attachment
      ↓
Search Other Recipients
      ↓
Check Authentication
      ↓
Check Endpoint Activity
      ↓
Build Timeline
      ↓
Determine Scope
```

### L3

```text
Advanced Analysis
      ↓
Malware / Payload Analysis
      ↓
Identify TTPs
      ↓
Identify Detection Gaps
      ↓
Develop Detection
      ↓
Improve Defensive Controls
```

---

# 25. Example: Ransomware Incident

### L1

```text
Ransomware Alert
      ↓
Validate
      ↓
Identify Host
      ↓
Identify User
      ↓
Escalate Immediately
```

### L2

```text
Investigate Host
      ↓
Identify Initial Access
      ↓
Search Other Hosts
      ↓
Determine Scope
      ↓
Identify Attack Chain
      ↓
Support Containment
```

### L3

```text
Advanced Forensics
      ↓
Malware Analysis
      ↓
Adversary Analysis
      ↓
Root Cause
      ↓
Detection Improvements
      ↓
Long-Term Defensive Recommendations
```

---

# 26. Tier Boundaries Are Not Absolute

Real organizations may use different structures.

For example:

```text
SOC L1
SOC L2
SOC L3
Detection Engineering
Threat Intelligence
Threat Hunting
Incident Response
DFIR
Security Engineering
```

These may be separate teams rather than hierarchical SOC tiers.

Therefore:

> **SOC tiers should be understood as capability levels rather than universal job titles.**

---

# 27. Skills Required for L1

### Knowledge

```text
Networking
Windows
Linux
Security Fundamentals
Common Attack Techniques
MITRE ATT&CK
```

### Technical

```text
SIEM
Log Analysis
IOC Analysis
Basic Network Analysis
Ticketing
Documentation
```

### Professional

```text
Communication
Attention to Detail
Analytical Thinking
Escalation
Time Management
```

---

# 28. Skills Required for L2

Build on L1 with:

```text
Advanced SIEM
Advanced Log Analysis
Threat Intelligence
Event Correlation
Threat Hunting
Incident Investigation
Root Cause Analysis
Detection Tuning
MITRE ATT&CK
```

---

# 29. Skills Required for L3

Build on L2 with:

```text
Advanced Threat Hunting
Detection Engineering
Digital Forensics
Malware Analysis
Advanced Incident Response
Adversary Analysis
Security Engineering
Automation
Detection Architecture
```

---

# 30. Recommended Learning Progression

For this portfolio:

```text
SOC Fundamentals
       ↓
Networking Fundamentals
       ↓
Windows + Linux
       ↓
Security Logs
       ↓
SIEM
       ↓
Alert Triage
       ↓
IOC Analysis
       ↓
Incident Investigation
       ↓
SOC L1
       ↓
Threat Intelligence
       ↓
Detection Engineering
       ↓
Threat Hunting
       ↓
Incident Response
       ↓
SOC L2
       ↓
Digital Forensics
       ↓
Malware Analysis
       ↓
Advanced Detection
       ↓
SOC L3
```

---

# 31. Practical Evidence by Tier

## L1 Evidence

```text
Alert Triage Reports
Log Analysis Labs
SIEM Dashboards
IOC Investigations
Basic Playbooks
TryHackMe SOC Labs
```

## L2 Evidence

```text
Advanced Investigations
Threat Hunting Reports
Detection Rules
Attack Timelines
Incident Case Studies
MITRE ATT&CK Mapping
```

## L3 Evidence

```text
Advanced Detection Engineering
Malware Analysis
Forensic Investigations
Complex Incident Response
Adversary Simulation
Detection Architecture
```

---

# 32. Portfolio Evidence Standard

Every practical exercise should answer:

```text
1. What was the objective?
2. What environment was used?
3. What activity was simulated?
4. What telemetry was generated?
5. What detection occurred?
6. How was it investigated?
7. What evidence was found?
8. What was the conclusion?
9. What response was recommended?
10. What could be improved?
```

---

# 33. Interview Readiness

For SOC L1 interviews, I should be able to explain:

### SOC

* What is a SOC?
* What does an L1 analyst do?
* What is alert triage?
* What is escalation?
* What is the difference between an event and an incident?

### Technical

* How do you investigate a failed login?
* How do you investigate suspicious PowerShell?
* What logs would you check?
* How would you investigate a suspicious IP?
* How does a SIEM work?
* What is MITRE ATT&CK?

### Practical

* How did you build your SOC lab?
* What detections did you create?
* How did you generate telemetry?
* How did you investigate an alert?
* What did you document?

---

# 34. Personal Capability Target

The initial professional target is:

> **SOC L1 / Junior Security Analyst readiness.**

The portfolio should first demonstrate:

```text
                 SOC L1
                   │
        ┌──────────┼──────────┐
        ↓          ↓          ↓
     SIEM       Triage      Logs
        ↓          ↓          ↓
   Detection   Investigation IOC
        └──────────┼──────────┘
                   ↓
             Documentation
                   ↓
              Escalation
```

After gaining sufficient practical experience, the roadmap can expand toward:

```text
SOC L2
   ↓
Threat Hunting
   ↓
Detection Engineering
   ↓
Incident Response
   ↓
SOC L3
```

---

# ⭐ Key Principle

> **L1 identifies and validates. L2 investigates and correlates. L3 solves complex problems and improves the organization's ability to detect and respond.**

The goal of this portfolio is not to claim L2/L3 expertise prematurely.

It is to **build and document the capabilities progressively**, so the evidence grows alongside actual skill.
