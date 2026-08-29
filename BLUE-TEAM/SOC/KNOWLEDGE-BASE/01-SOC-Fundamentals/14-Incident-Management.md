# Incident Management

> **SOC L1 → L2 Fundamental**

Incident management is the structured process of identifying, analyzing, containing, resolving, documenting, and learning from cybersecurity incidents.

A SOC does not stop at:

```text id="f2p5h8"
Alert → Investigation
```

When an alert is confirmed as a security incident, the organization needs a coordinated response:

```text id="e7t8u2"
Detection
   ↓
Validation
   ↓
Incident Declaration
   ↓
Analysis
   ↓
Containment
   ↓
Eradication
   ↓
Recovery
   ↓
Lessons Learned
```

The exact lifecycle varies between organizations and frameworks, but the underlying objective is the same:

> **Reduce the impact of a security incident and restore secure operations.**

---

# 1. What Is a Security Incident?

A security incident is an event that actually or potentially compromises:

* Confidentiality
* Integrity
* Availability
* Authentication
* Authorization
* Security controls

Examples:

```text id="p6h4f1"
Malware Infection
Account Compromise
Phishing Attack
Ransomware
Data Breach
Unauthorized Access
Credential Theft
C2 Activity
Insider Threat
Web Application Attack
```

Not every security event is an incident.

---

# 2. Event vs Alert vs Incident

```text id="0a6y6v"
EVENT
Something happened
        ↓
ALERT
Detection identified something suspicious
        ↓
INVESTIGATION
Analyst gathers evidence
        ↓
INCIDENT
Security impact / compromise is established
```

Example:

```text id="p9cl5e"
Event:
Failed Login

Alert:
50 failed logins

Investigation:
Successful login followed

Incident:
Account compromise suspected/confirmed
```

---

# 3. Incident Management Objectives

The major objectives are:

```text id="q1d8s7"
Detect Quickly
      ↓
Understand Scope
      ↓
Contain Threat
      ↓
Remove Threat
      ↓
Restore Operations
      ↓
Prevent Recurrence
```

A mature incident-management process should minimize:

* Business disruption
* Financial loss
* Data loss
* Downtime
* Regulatory impact
* Reputational damage

---

# 4. Incident Management Lifecycle

A practical lifecycle:

```text id="3u8q2p"
1. Preparation
       ↓
2. Detection & Identification
       ↓
3. Analysis / Triage
       ↓
4. Containment
       ↓
5. Eradication
       ↓
6. Recovery
       ↓
7. Lessons Learned
```

Some organizations combine or rename these phases.

---

# 5. Phase 1 — Preparation

Preparation happens **before an incident**.

Organizations prepare:

```text id="e0w3rx"
People
Processes
Technology
Policies
Playbooks
Communication Channels
Backups
Logging
Monitoring
Training
```

Examples:

```text id="8h7bq2"
SIEM
EDR
Firewall
Backup
Incident Response Plan
Contact List
Escalation Matrix
Forensic Tools
```

---

# 6. Why Preparation Matters

Without preparation:

```text id="h9x2m0"
Incident
   ↓
Confusion
   ↓
Delayed Decisions
   ↓
Greater Impact
```

With preparation:

```text id="s8u7k3"
Incident
   ↓
Playbook
   ↓
Defined Roles
   ↓
Defined Actions
   ↓
Faster Response
```

---

# 7. Incident Response Team

Depending on organization size, incident response may involve:

```text id="2p4y5s"
SOC L1
SOC L2
SOC L3
Incident Response
DFIR
Threat Intelligence
Security Engineering
IT
Cloud Team
Network Team
IAM Team
Legal
HR
Management
Communications
```

Not every incident requires everyone.

---

# 8. SOC L1 Role During an Incident

A SOC L1 analyst typically focuses on:

```text id="d5r0s8"
Alert Validation
Initial Triage
Evidence Collection
Context Gathering
Basic Investigation
Documentation
Escalation
Monitoring
```

L1 may identify:

```text id="9w0n2a"
"This activity appears malicious."
```

Then escalate to L2/IR according to the organization's process.

---

# 9. Phase 2 — Detection & Identification

An incident may be identified through:

```text id="p4s8z2"
SIEM Alert
EDR Alert
User Report
Threat Intelligence
Firewall
IDS/IPS
Email Security
Cloud Security
External Notification
```

Example:

```text id="w0s3ab"
EDR
 ↓
Suspicious PowerShell
 ↓
Malware Download
 ↓
C2 Connection
```

This may trigger incident investigation.

---

# 10. Initial Triage

Ask:

```text id="f2s5r7"
What happened?
When?
Which host?
Which user?
Which account?
What process?
What IP/domain?
What data?
Is it still active?
```

Then determine:

```text id="c8y3w1"
Potential Incident?
       ↓
YES → Continue
NO  → Close / Monitor
```

---

# 11. Incident Classification

Organizations may classify incidents by type.

Examples:

```text id="j1o4s6"
Malware
Phishing
Account Compromise
Data Breach
Ransomware
DDoS
Insider Threat
Unauthorized Access
Web Attack
Cloud Security Incident
```

Classification helps determine:

* Appropriate playbook
* Required responders
* Severity
* Communication
* Reporting requirements

---

# 12. Incident Severity

A common model:

```text id="4k8j1z"
Critical
High
Medium
Low
```

Severity may consider:

```text id="0n7c6m"
Business Impact
Asset Criticality
Data Sensitivity
User Privilege
Scope
Attack Activity
Availability Impact
Potential Damage
```

---

# 13. Incident Priority

Severity and priority should not be confused.

Example:

```text id="6n5b4d"
Medium Severity
+
Production Database
+
Sensitive Customer Data
```

may require immediate action.

Therefore:

> **Business context matters.**

---

# 14. Phase 3 — Analysis

Analysis determines:

```text id="x1d7q9"
What happened?
How did it happen?
When did it start?
Which systems are affected?
Which accounts are affected?
What attacker behavior occurred?
Is the attacker still active?
```

---

# 15. Timeline Reconstruction

Create a timeline.

Example:

```text id="2r8n1p"
09:41
Phishing email delivered

09:47
User clicked URL

09:48
Credentials submitted

09:52
Successful external login

09:54
PowerShell executed

09:56
Suspicious outbound connection

10:01
Security alert generated
```

This is much more useful than looking at individual alerts separately.

---

# 16. Scope Determination

Determine the blast radius.

Check:

```text id="p6f9r2"
Users
Hosts
Servers
Cloud Resources
Accounts
IP Addresses
Applications
Data
```

Example:

```text id="0q2k6a"
Host A
   ↓
Compromised

Host B
   ↓
Suspicious Login

Host C
   ↓
Same C2

Host D
   ↓
Credential Activity
```

This could indicate lateral movement.

---

# 17. Evidence Collection

Evidence may include:

```text id="e3n6p5"
Logs
Process Information
Command Lines
Network Connections
Files
Hashes
DNS
Authentication Events
EDR Telemetry
Email Headers
Cloud Logs
Screenshots
```

Important principle:

> **Collect evidence before changing or destroying it whenever possible and according to organizational procedures.**

---

# 18. IOC Collection

Collect:

```text id="g7m2k4"
IP Addresses
Domains
URLs
Hashes
File Names
Email Addresses
Registry Keys
File Paths
```

Example:

```text id="y1c4s8"
Malicious Hash
       ↓
Search SIEM
       ↓
Find Other Hosts
       ↓
Determine Scope
```

---

# 19. IOA Collection

Behavioral indicators may include:

```text id="d8p1k6"
Office → PowerShell
PowerShell → Download
Credential Dumping
Scheduled Task Creation
Mass File Encryption
Unusual Remote Login
```

IOAs help identify attacker activity even when specific IOCs change.

---

# 20. MITRE ATT&CK Mapping

During analysis, map attacker behavior.

Example:

```text id="9u2r5k"
Phishing
   ↓
Initial Access

PowerShell
   ↓
Execution

Scheduled Task
   ↓
Persistence

Credential Dumping
   ↓
Credential Access

C2
   ↓
Command & Control
```

This creates a structured attack narrative.

---

# 21. Cyber Kill Chain Mapping

You can also map the incident to the Cyber Kill Chain.

Example:

```text id="q0r3y7"
Delivery
   ↓
Phishing

Exploitation / Execution
   ↓
Malicious Script

Installation
   ↓
Persistence

C2
   ↓
External Communication

Actions on Objectives
   ↓
Data Theft
```

Using both frameworks gives complementary views.

---

# 22. Phase 4 — Containment

Containment attempts to stop the attacker from continuing.

Possible actions:

```text id="n7c2v4"
Isolate Endpoint
Disable Account
Block IP
Block Domain
Block Hash
Terminate Malicious Process
Revoke Sessions
Disable Compromised Credentials
Restrict Network Access
```

The exact action must follow organizational authorization and procedures.

---

# 23. Short-Term vs Long-Term Containment

### Short-Term

Immediate action to stop damage.

Example:

```text id="w3j7k1"
Compromised Laptop
      ↓
Network Isolation
```

### Long-Term

More stable controls while investigation continues.

Example:

```text id="c4q8n6"
Temporary Network Restriction
+
Credential Reset
+
Additional Monitoring
```

---

# 24. Containment Considerations

Before containment, consider:

```text id="p1x6s9"
Business Impact
Evidence Preservation
Affected Systems
Critical Services
Safety
Authorization
```

For example, immediately shutting down a critical production server may cause more damage than isolating it through a controlled network mechanism.

---

# 25. Phase 5 — Eradication

Eradication removes the attacker's presence.

Examples:

```text id="y7m2k5"
Remove Malware
Delete Persistence
Patch Vulnerability
Reset Credentials
Remove Unauthorized Accounts
Revoke Tokens
Remove Backdoors
Clean Compromised Systems
```

Example:

```text id="v4s8q2"
Malware
 ↓
Persistence
 ↓
Remove Malware
 ↓
Remove Persistence
 ↓
Patch Initial Vulnerability
```

---

# 26. Credential Remediation

If credentials may be compromised:

```text id="6k9r2b"
Reset Password
      ↓
Revoke Sessions
      ↓
Rotate Keys/Tokens
      ↓
Review MFA
      ↓
Monitor Account
```

For privileged accounts, additional controls may be required.

---

# 27. Phase 6 — Recovery

Recovery returns systems to normal secure operation.

Examples:

```text id="n5q8w3"
Restore Systems
Rebuild Hosts
Restore Backups
Validate Security
Monitor Systems
Return to Production
```

Recovery should not simply mean:

> "System is working again."

The system must be sufficiently trusted and monitored.

---

# 28. Recovery Validation

Before returning a system to normal operations:

```text id="k3v7p1"
Malware Removed?
Persistence Removed?
Vulnerability Fixed?
Credentials Rotated?
Security Controls Working?
Logs Available?
Monitoring Enabled?
```

Then:

```text id="m2d6x9"
Controlled Return
      ↓
Enhanced Monitoring
      ↓
Normal Operations
```

---

# 29. Phase 7 — Lessons Learned

After the incident, ask:

```text id="r7c1q4"
What happened?
Why did it happen?
Why wasn't it detected earlier?
Which control failed?
Which detection worked?
What should be improved?
```

This transforms an incident into organizational learning.

---

# 30. Root Cause Analysis

Identify the underlying cause.

Example:

```text id="s8m2q5"
Phishing Email
      ↓
User Clicked
      ↓
Credentials Stolen
      ↓
MFA Not Enabled
      ↓
Account Compromised
```

Possible root causes:

```text id="0h4t8k"
No MFA
Poor Email Filtering
User Awareness Gap
Weak Password
Insufficient Monitoring
```

The root cause is not necessarily the first event in the timeline.

---

# 31. Post-Incident Improvements

Possible improvements:

```text id="w5n1c7"
Enable MFA
Improve Email Filtering
Tune Detection Rules
Deploy EDR
Improve Logging
Patch Systems
Restrict Privileges
Improve Network Segmentation
Update Playbooks
Conduct Security Awareness Training
```

---

# 32. Incident Documentation

A professional incident report should contain:

```text id="q4x7m2"
Incident ID
Incident Type
Date/Time
Severity
Affected Assets
Affected Users
Summary
Initial Detection
Timeline
Indicators
Evidence
Attack Techniques
Scope
Containment
Eradication
Recovery
Root Cause
Impact
Lessons Learned
Recommendations
```

---

# 33. Example Incident Report

## Incident

```text id="1d7k9p"
INC-2026-001

Type:
Account Compromise

Severity:
High

Affected Asset:
WIN-CLIENT01

Affected Account:
administrator
```

### Summary

```text id="6y4p1r"
Multiple authentication failures were observed against
a privileged account, followed by a successful login from
an unusual source. Subsequent endpoint telemetry showed
PowerShell execution and outbound communication.
```

### Timeline

```text id="9n2c5v"
10:01 — Failed login
10:02 — Failed login
10:03 — Successful login
10:04 — PowerShell execution
10:05 — External connection
10:07 — Alert escalated
10:12 — Account disabled
10:20 — Endpoint isolated
```

---

# 34. Incident Evidence

Example:

```text id="3p8m1q"
Source IP:
198.51.100.10

Destination:
WIN-CLIENT01

Account:
administrator

Process:
powershell.exe

Domain:
suspicious-example.com
```

Additional evidence should be stored according to organizational evidence-handling procedures.

---

# 35. Incident Response Playbooks

A playbook is a predefined response procedure.

Common SOC playbooks:

```text id="v6q2k8"
Phishing
Malware
Ransomware
Brute Force
Account Compromise
Suspicious PowerShell
Data Exfiltration
DDoS
Insider Threat
Cloud Account Compromise
```

Example:

```text id="x9m3c5"
PHISHING PLAYBOOK

1. Validate email
2. Identify recipients
3. Check URL/attachment
4. Determine who interacted
5. Investigate endpoints
6. Remove email
7. Reset credentials if required
8. Block indicators
9. Monitor
10. Document
```

---

# 36. Incident Escalation

L1 should escalate when:

```text id="k8r2v6"
Confirmed compromise
High-value asset
Privileged account
Multiple systems
Data breach
Ransomware
Active C2
Potential lateral movement
Unclear high-risk activity
```

Example:

```text id="b5m7q1"
SOC L1
  ↓
SOC L2
  ↓
Incident Response
  ↓
DFIR / Security Engineering
```

The exact escalation path depends on the organization.

---

# 37. Communication During Incidents

Incident management may require communication with:

```text id="p3c7v9"
SOC
IT
Management
Legal
HR
Cloud Team
Network Team
Application Team
External Parties
```

Communication should be:

```text id="r1x5k8"
Accurate
Concise
Evidence-Based
Timely
Need-to-Know
```

Avoid speculation.

---

# 38. Evidence Preservation

During an incident:

```text id="f2q6n4"
Logs
Memory
Disk Evidence
Network Evidence
Email
Cloud Logs
Authentication Logs
```

may be important.

Do not casually:

```text id="a7k3p1"
Delete files
Clear logs
Reinstall systems
Modify evidence
```

before determining whether evidence needs to be preserved and following organizational procedures.

---

# 39. Incident Management in a SIEM

A SIEM can support:

```text id="h8n2c5"
Alert
 ↓
Case
 ↓
Investigation
 ↓
Evidence
 ↓
Comments
 ↓
Tasks
 ↓
Escalation
 ↓
Closure
```

Your Wazuh home lab can simulate parts of this workflow.

---

# 40. Practical Home Lab Scenario

Create a controlled incident:

```text id="z5m1q8"
Kali
 ↓
Controlled Attack Simulation
 ↓
Windows VM
 ↓
Sysmon
 ↓
Wazuh
 ↓
Detection
 ↓
Alert
 ↓
L1 Triage
 ↓
Incident Declaration
 ↓
Containment
 ↓
Eradication
 ↓
Recovery
 ↓
Report
```

Document every stage.

---

# 41. Portfolio Incident Case Study

Create:

```text id="d8q4m6"
Incident-Response-Lab/
│
├── README.md
├── Scenarios/
│   ├── Account-Compromise/
│   ├── Phishing/
│   ├── Malware/
│   └── Ransomware-Simulation/
│
├── Evidence/
├── Timelines/
├── IOC/
├── IOA/
├── MITRE-Mapping/
├── Playbooks/
├── Incident-Reports/
├── Screenshots/
└── Lessons-Learned/
```

Each case study should show:

```text id="j4r8v2"
Detection
   ↓
Triage
   ↓
Investigation
   ↓
Timeline
   ↓
Scope
   ↓
Containment
   ↓
Eradication
   ↓
Recovery
   ↓
Lessons Learned
```

---

# 42. Example SOC L1 Incident Comment

```text id="n7c3x9"
Investigation identified multiple failed authentication attempts
against a privileged account followed by a successful login from
an unusual source. Endpoint telemetry subsequently showed
PowerShell execution and external network communication.

The activity is inconsistent with the user's normal behavior
and may indicate account compromise.

Related authentication and endpoint events were reviewed.
The affected account and endpoint should be escalated for
further investigation and containment according to the incident
response procedure.
```

---

# 43. Interview Questions

### Fundamentals

1. What is incident management?
2. What is the difference between an event, alert, and incident?
3. What are the phases of incident response?
4. What is containment?
5. What is eradication?
6. What is recovery?
7. What is root cause analysis?

### SOC L1

8. What is the role of L1 during an incident?
9. When should an alert become an incident?
10. When should an L1 analyst escalate?
11. What evidence should be collected?
12. How do you determine incident scope?
13. How do you create an incident timeline?

### Scenario

14. A privileged account shows brute-force activity followed by a successful login. What do you do?

A strong answer:

```text id="e5m2r7"
Validate
 ↓
Review authentication logs
 ↓
Identify source
 ↓
Check successful login
 ↓
Check endpoint activity
 ↓
Review related alerts
 ↓
Determine scope
 ↓
Collect IOCs/IOAs
 ↓
Assess severity
 ↓
Escalate
 ↓
Contain according to authorization
 ↓
Document
```

---

# 44. Key Takeaway

Incident management is the bridge between:

```text id="u2m8c5"
SOC Monitoring
      ↓
Alert Management
      ↓
Incident Response
```

The complete lifecycle can be remembered as:

```text id="s6q1v9"
PREPARE
   ↓
DETECT
   ↓
ANALYZE
   ↓
CONTAIN
   ↓
ERADICATE
   ↓
RECOVER
   ↓
LEARN
```

For your SOC portfolio, do not merely write about incident response.

Build **controlled incident simulations** in your home lab and document:

```text id="k9x3p6"
Telemetry
+
Detection
+
Alert
+
Investigation
+
IOC/IOA
+
MITRE ATT&CK
+
Timeline
+
Containment
+
Recovery
+
Final Report
```

That is the difference between demonstrating **SOC theory** and demonstrating an actual **SOC investigation capability**.
