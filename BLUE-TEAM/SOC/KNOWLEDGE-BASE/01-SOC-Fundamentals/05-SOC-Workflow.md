# 🔄 SOC Workflow

> A SOC workflow defines how security events move from initial detection through triage, investigation, response, documentation, and continuous improvement.

The objective is to create a **repeatable, measurable, and evidence-driven security operations process**.

---

# 1. SOC Workflow Overview

A simplified SOC workflow is:

```text
Security Event
      ↓
Data Collection
      ↓
Detection
      ↓
Alert Generation
      ↓
Alert Triage
      ↓
Investigation
      ↓
Classification
      ↓
Escalation
      ↓
Incident Response
      ↓
Recovery
      ↓
Documentation
      ↓
Lessons Learned
      ↓
Detection Improvement
```

Not every event becomes an incident.

```text
Event → Alert → Investigation → Incident
```

These are different stages.

---

# 2. Security Event

A security event is an observable activity occurring within an environment.

Examples:

* User login
* Failed login
* Process execution
* File creation
* DNS request
* Network connection
* Firewall block
* Account modification
* USB insertion
* PowerShell execution

An event by itself does not necessarily indicate malicious activity.

Example:

```text
User successfully logged in
```

This is an event.

It becomes more interesting when combined with context:

```text
Successful login
+
Unusual country
+
Impossible travel
+
New device
+
Privileged account
```

---

# 3. Data Collection

SOC platforms collect telemetry from multiple sources.

```text
Endpoints
Servers
Network Devices
Firewalls
Applications
Identity Systems
Cloud Platforms
Email Systems
Security Tools
        ↓
     SIEM
```

Common data sources include:

* Windows Event Logs
* Sysmon
* Linux logs
* Firewall logs
* DNS logs
* Proxy logs
* VPN logs
* Authentication logs
* EDR telemetry
* Cloud logs
* Application logs

---

# 4. Detection

Detection logic identifies activity that may represent malicious or suspicious behavior.

Example:

```text
Multiple failed authentication attempts
        +
Successful login
        +
Unusual source IP
```

A detection rule may generate an alert.

Detection can be:

### Signature-Based

Looks for known patterns.

### Behavioral

Looks for suspicious behavior.

### Anomaly-Based

Identifies deviations from expected behavior.

### Threat Intelligence-Based

Uses known malicious indicators.

---

# 5. Alert Generation

When detection logic matches telemetry, the SOC platform generates an alert.

A typical alert contains:

```text
Alert ID
Timestamp
Severity
Rule Name
Source
Destination
User
Host
IP
Domain
Process
Description
MITRE ATT&CK Technique
```

Example:

```text
Alert:
Suspicious PowerShell Execution

Severity:
High

Host:
WIN-CLIENT01

User:
student

Process:
powershell.exe
```

---

# 6. Alert Prioritization

SOC analysts cannot investigate every alert with equal urgency.

A practical priority model:

```text
Critical
   ↓
High
   ↓
Medium
   ↓
Low
   ↓
Informational
```

Priority should consider:

```text
Severity
+
Asset Criticality
+
User Privilege
+
Threat Intelligence
+
Attack Context
+
Potential Impact
```

---

# 7. SOC L1 Triage

The first analyst determines whether the alert deserves further investigation.

Basic triage questions:

### What happened?

Identify the activity.

### When did it happen?

Determine the timestamp.

### Where did it happen?

Identify affected systems.

### Who was involved?

Identify the user/account.

### Is it expected?

Check normal business behavior.

### Is there evidence of malicious activity?

Review available telemetry.

---

# 8. Triage Decision

The analyst generally reaches one of several outcomes:

```text
          Alert
            ↓
         Triage
            ↓
    ┌───────┼────────┐
    ↓       ↓        ↓
False    Benign   Suspicious
Positive    ↓        ↓
    ↓      Close   Investigate
  Close              ↓
                 Escalate
```

Possible classifications:

* False Positive
* Benign Positive
* Suspicious
* True Positive
* Confirmed Incident

---

# 9. Investigation

Investigation attempts to understand the complete security story.

The analyst examines:

```text
User
Host
Process
Network
File
Authentication
Timeline
IOC
Threat Intelligence
Related Events
```

The key objective is **correlation**.

One event may appear harmless.

Multiple correlated events may reveal an attack.

---

# 10. Event Correlation

Example:

```text
10:00
Failed Login

10:02
Failed Login

10:03
Successful Login

10:05
PowerShell Execution

10:06
Encoded Command

10:07
External Network Connection
```

Individually:

```text
Login
PowerShell
Network Connection
```

may not immediately prove compromise.

Together they form a suspicious sequence.

---

# 11. Attack Timeline

A timeline helps analysts reconstruct what happened.

Example:

```text
10:00 ─ Failed authentication
10:02 ─ Failed authentication
10:03 ─ Successful authentication
10:05 ─ PowerShell execution
10:06 ─ Suspicious command
10:07 ─ Network connection
10:10 ─ File creation
10:15 ─ Alert generated
```

Timeline construction is one of the most useful SOC investigation skills.

---

# 12. IOC Investigation

Investigate indicators such as:

```text
IP Address
Domain
URL
File Hash
Filename
Email Address
Hostname
Registry Key
Process
```

Possible enrichment sources include:

* Threat intelligence platforms
* Internal security tools
* DNS information
* WHOIS information
* Reputation services
* Sandbox analysis

The objective is to determine:

> Is the indicator known, suspicious, malicious, or legitimate?

---

# 13. MITRE ATT&CK Mapping

Investigations should identify attacker behavior where possible.

Example:

```text
PowerShell
      ↓
MITRE ATT&CK
      ↓
Command and Scripting Interpreter:
PowerShell
```

Mapping helps analysts understand:

* What the attacker is doing
* Which stage of the attack is involved
* What additional activity may be expected
* Which detections should exist

---

# 14. Escalation

L1 should escalate when:

* High-impact assets are involved
* Privileged accounts are involved
* Compromise is suspected
* Multiple systems are affected
* Evidence is insufficient
* Investigation requires advanced expertise
* Incident response is required

Escalation should contain useful context.

Bad escalation:

> "Please investigate."

Good escalation:

```text
Alert:
Suspicious PowerShell

Affected Host:
WIN-CLIENT01

User:
admin

Observed:
Encoded PowerShell command

Related Activity:
External connection to suspicious IP

Assessment:
Potential compromise

Recommended:
L2 investigation and endpoint containment review
```

---

# 15. Incident Response

Confirmed incidents move into response.

Typical lifecycle:

```text
Preparation
     ↓
Detection
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

---

# 16. Containment

The objective is to prevent further damage.

Possible actions:

* Isolate endpoint
* Disable compromised account
* Block malicious IP
* Block domain
* Remove malicious email
* Restrict network communication

Actions should follow organizational procedures and authorization.

---

# 17. Eradication

Remove the underlying cause.

Examples:

* Remove malware
* Remove persistence
* Reset compromised credentials
* Patch vulnerable systems
* Remove malicious accounts
* Correct security configurations

---

# 18. Recovery

Restore normal operations.

Activities may include:

* Restore systems
* Re-enable accounts
* Validate security controls
* Monitor affected assets
* Perform additional scans
* Confirm attacker removal

---

# 19. Documentation

Every significant investigation should produce evidence.

Recommended structure:

```text
Incident ID
Alert Summary
Detection Time
Affected Assets
Affected Users
Initial Findings
Investigation
Timeline
IOCs
MITRE ATT&CK
Impact
Response
Root Cause
Recommendations
Lessons Learned
```

---

# 20. Closure

An alert should only be closed after sufficient evidence has been documented.

Example:

```text
Classification:
False Positive

Reason:
Activity generated by approved administrative script.

Evidence:
Known administrator
Approved change ticket
Expected execution time
Known script hash

Action:
Detection closed
```

---

# 21. Lessons Learned

Post-incident analysis asks:

```text
What happened?
Why did it happen?
How was it detected?
What failed?
What worked?
How can detection improve?
How can prevention improve?
```

This converts an incident into organizational learning.

---

# 22. Detection Improvement

SOC operations should be a continuous feedback loop.

```text
Incident
   ↓
Investigation
   ↓
Root Cause
   ↓
Detection Gap
   ↓
New Detection
   ↓
Testing
   ↓
Deployment
   ↓
Future Detection
```

This is where SOC operations connect with **detection engineering**.

---

# 23. SOC Workflow Metrics

Useful operational metrics include:

### MTTD

Mean Time to Detect

### MTTA

Mean Time to Acknowledge

### MTTR

Mean Time to Respond / Recover

### False Positive Rate

Percentage of alerts incorrectly identified as malicious.

### Escalation Rate

Percentage of alerts escalated to higher-level analysts.

### Detection Coverage

How effectively important attack behaviors are detected.

Metrics should be interpreted in context rather than optimized blindly.

---

# 24. L1 → L2 → L3 Workflow

```text
                  ALERT
                    ↓
                  L1
             Triage / Validate
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
       Close               Escalate
                              ↓
                             L2
                    Deep Investigation
                              ↓
                     ┌────────┴────────┐
                     ↓                 ↓
                  Resolve          Escalate
                                       ↓
                                      L3
                             Advanced Analysis
                                       ↓
                              Detection / Response
```

---

# 25. SOC Workflow — Portfolio Implementation

This workflow will be reproduced in the home lab.

```text
Attack Simulation
       ↓
Telemetry Generation
       ↓
Wazuh / SIEM
       ↓
Detection Rule
       ↓
Alert
       ↓
L1 Triage
       ↓
Investigation
       ↓
MITRE Mapping
       ↓
Incident Decision
       ↓
Response
       ↓
Professional Report
       ↓
Detection Improvement
```

---

# ⭐ Core Principle

> **A mature SOC does not simply process alerts. It continuously transforms security telemetry into detection, investigation, response, and improved defensive capability.**
