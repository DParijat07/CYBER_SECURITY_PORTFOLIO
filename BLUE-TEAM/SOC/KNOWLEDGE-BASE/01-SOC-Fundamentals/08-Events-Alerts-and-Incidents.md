# Events, Alerts & Incidents

> **SOC L1 Fundamental**

Understanding the difference between **events, alerts, and incidents** is one of the most important concepts for a SOC analyst. Not every event is an alert, and not every alert is an incident.

---

## 1. The Basic Relationship

```text
EVENT
  ↓
Detection Logic
  ↓
ALERT
  ↓
Investigation / Triage
  ↓
INCIDENT
```

A simple way to remember:

```text
Event    → Something happened
Alert    → Something potentially suspicious happened
Incident → Confirmed or suspected security event requiring response
```

---

# 2. What Is a Security Event?

A **security event** is an observable occurrence within a system, network, application, or security control.

Examples:

* User login
* Failed login attempt
* File creation
* Process execution
* DNS request
* Network connection
* Firewall connection
* USB device insertion
* Password change
* Account creation
* PowerShell execution

An event by itself does **not necessarily mean malicious activity**.

### Example

```text
User: admin
Action: Login
Source IP: 10.10.10.25
Time: 10:32:14
Result: Success
```

This is a security-relevant event.

It could be:

```text
Normal administrator activity
```

or:

```text
Compromised account activity
```

Additional context is required.

---

# 3. What Is an Alert?

An **alert** is a notification generated when security monitoring or detection logic identifies activity that may require investigation.

Typical alert sources include:

* SIEM
* EDR
* IDS/IPS
* Firewall
* Antivirus
* Email security
* Cloud security platforms
* Identity security systems

### Example

A SIEM may detect:

```text
50 failed login attempts
        +
1 successful login
        +
Same source IP
```

The detection rule may generate:

```text
ALERT:
Possible Brute-Force Attack
```

The alert tells the SOC:

> **"This activity deserves investigation."**

It does not automatically prove that an attack occurred.

---

# 4. What Is an Incident?

A **security incident** is a security event or series of events that has been determined to represent an actual or suspected compromise, violation, or threat requiring a response.

Examples:

* Confirmed malware infection
* Compromised user account
* Successful phishing attack
* Ransomware execution
* Unauthorized access
* Data exfiltration
* Confirmed malicious persistence

An incident normally requires coordinated response.

---

# 5. Event vs Alert vs Incident

| Concept  | Meaning                                  | Example             |
| -------- | ---------------------------------------- | ------------------- |
| Event    | Something happened                       | User logged in      |
| Alert    | Detection identified suspicious activity | 100 failed logins   |
| Incident | Security threat requiring response       | Account compromised |

---

# 6. Event → Alert → Incident

Consider a brute-force scenario.

### Step 1 — Events

```text
10:01 → Failed login
10:01 → Failed login
10:02 → Failed login
10:02 → Failed login
10:03 → Failed login
...
```

Each is an individual event.

---

### Step 2 — Detection

The SIEM rule identifies:

```text
More than 20 failed logins
from the same source
within 5 minutes
```

---

### Step 3 — Alert

The SIEM generates:

```text
HIGH:
Possible Brute-Force Attack
```

---

### Step 4 — Investigation

The analyst checks:

```text
Source IP
Target Account
Authentication Logs
Successful Login
User Context
Geolocation
Historical Activity
Endpoint Activity
```

---

### Step 5 — Incident

Suppose the analyst discovers:

```text
20 failed logins
      ↓
Successful login
      ↓
New device
      ↓
Suspicious PowerShell
      ↓
External C2 connection
```

The activity may now be classified as a:

```text
CONFIRMED SECURITY INCIDENT
```

---

# 7. Not Every Event Is an Alert

A large enterprise can generate millions of events.

For example:

```text
10,000,000 Events
        ↓
Detection Rules
        ↓
50,000 Relevant Events
        ↓
5,000 Alerts
        ↓
500 Investigations
        ↓
50 Confirmed Incidents
```

The exact numbers vary enormously by environment.

The important principle is:

> **Security monitoring reduces a huge volume of raw telemetry into actionable information.**

---

# 8. Not Every Alert Is an Incident

This is extremely important for SOC L1 analysts.

An alert may be:

```text
False Positive
      OR
Benign Activity
      OR
Suspicious Activity
      OR
True Positive
      OR
Confirmed Incident
```

For example:

```text
Alert:
Multiple Failed Logins
```

Investigation reveals:

```text
User forgot password
```

Result:

```text
Benign Activity
```

Another investigation:

```text
Alert
 ↓
Successful Login
 ↓
Unknown Device
 ↓
Impossible Travel
 ↓
MFA Bypass Evidence
```

Result:

```text
Potential Account Compromise
```

---

# 9. False Positive

A **false positive** occurs when a detection generates an alert for activity that is not actually malicious.

Example:

```text
Detection:
Multiple failed logins

Alert:
Possible Brute Force

Investigation:
Employee repeatedly entered incorrect password
```

Conclusion:

```text
False Positive / Benign Activity
```

The analyst should document why the alert was closed.

---

# 10. True Positive

A **true positive** occurs when the detection correctly identifies activity matching the intended suspicious or malicious behavior.

Example:

```text
Detection:
PowerShell encoded command

Investigation:
Command executed by malicious process
      ↓
External connection
      ↓
Known malicious infrastructure
```

Conclusion:

```text
True Positive
```

However:

> **True Positive does not automatically mean "confirmed incident."**

The context and organization's incident classification criteria matter.

---

# 11. Alert Severity

Alerts are commonly assigned severity levels such as:

```text
LOW
MEDIUM
HIGH
CRITICAL
```

Severity may depend on:

```text
Impact
+
Likelihood
+
Asset Criticality
+
User Privilege
+
Threat Intelligence
+
Attack Stage
+
Confidence
```

### Example

A failed login on a normal workstation:

```text
LOW / MEDIUM
```

A successful privileged-account login from suspicious infrastructure:

```text
HIGH / CRITICAL
```

---

# 12. Alert Priority vs Severity

These concepts should not be treated as identical.

### Severity

Represents the potential seriousness of the activity.

### Priority

Represents how urgently the SOC should respond.

Example:

```text
Alert A
Severity: High
Priority: Medium
```

because the affected system may be isolated and the activity is no longer active.

Another:

```text
Alert B
Severity: High
Priority: Critical
```

because an active attack is currently targeting a critical production system.

---

# 13. Alert Context

An alert without context is difficult to investigate.

A useful alert may contain:

```text
Alert ID
Timestamp
Source IP
Destination IP
Username
Hostname
Process
Command Line
File Hash
Domain
URL
Detection Rule
Severity
MITRE ATT&CK Technique
Related Events
```

The more useful context available, the faster the analyst can investigate.

---

# 14. Alert Enrichment

SOC analysts often enrich alerts with additional information.

Example:

```text
Suspicious IP
      ↓
Threat Intelligence
      ↓
VirusTotal
      ↓
WHOIS
      ↓
DNS Information
      ↓
Historical SIEM Events
      ↓
Reputation
```

This can help determine whether an indicator is:

```text
Known malicious
Suspicious
Unknown
Benign
```

---

# 15. Alert Correlation

One event may not be meaningful.

Multiple related events can reveal an attack.

Example:

```text
Failed Login
     +
Successful Login
     +
New Device
     +
PowerShell
     +
Suspicious DNS
     +
Outbound Connection
```

Together they provide much stronger evidence than any individual event.

This is known as **event correlation**.

---

# 16. Security Incident vs Security Event

A useful mental model:

```text
Security Event
      │
      ├── Normal
      │
      ├── Suspicious
      │
      └── Malicious
             │
             ▼
         Incident
```

However, organizations define and classify incidents differently.

Always follow the organization's:

* Incident response policy
* Severity matrix
* Escalation procedure
* Detection standards
* Regulatory requirements

---

# 17. SOC L1 Decision Process

When an alert arrives, L1 should think:

```text
             ALERT
               ↓
        What triggered it?
               ↓
        Is the detection valid?
               ↓
        What actually happened?
               ↓
        Is the activity expected?
               ↓
        What is the context?
               ↓
       Any malicious indicators?
               ↓
        Is there related activity?
               ↓
       ┌───────┴────────┐
       ↓                ↓
     Benign          Suspicious
       ↓                ↓
     Close           Escalate
                        ↓
                     L2 / IR
```

---

# 18. Example SOC Investigation

### Alert

```text
Rule:
Multiple Failed Authentication Attempts

Severity:
Medium

Source:
192.168.1.50

Target:
Administrator

Time:
14:05
```

### L1 Investigation

Check:

```text
1. Number of attempts
2. Source IP reputation
3. Target account
4. Successful authentication
5. Source device
6. Historical behavior
7. Related endpoint events
8. Other targeted accounts
```

### Findings

```text
30 failed attempts
        ↓
Successful login
        ↓
Administrator account
        ↓
New source device
        ↓
PowerShell execution
```

### Conclusion

```text
Potential Account Compromise
```

### Action

```text
Escalate to L2
```

---

# 19. Incident Documentation

A basic SOC case should record:

```text
Incident ID:
Date/Time:
Analyst:
Alert:
Affected Asset:
Affected User:
Source:
Destination:
Indicators:
Evidence:
Timeline:
Investigation:
Assessment:
Severity:
MITRE ATT&CK:
Actions Taken:
Escalation:
Final Disposition:
Recommendations:
```

This creates an auditable investigation trail.

---

# 20. Key SOC Terms

| Term           | Meaning                                          |
| -------------- | ------------------------------------------------ |
| Event          | Observable activity                              |
| Telemetry      | Data generated by systems/security tools         |
| Log            | Recorded system activity                         |
| Alert          | Notification generated by detection              |
| Detection      | Logic used to identify suspicious activity       |
| IOC            | Indicator of compromise                          |
| IOA            | Indicator of attack                              |
| TTP            | Tactics, techniques and procedures               |
| Incident       | Security event requiring response                |
| False Positive | Alert that is not actually malicious             |
| True Positive  | Detection correctly identifies relevant activity |
| Enrichment     | Adding external/contextual information           |
| Correlation    | Connecting related events                        |
| Escalation     | Passing an investigation to a higher level       |

---

# 21. Interview Questions

You should be able to answer these confidently:

### Beginner

1. What is a security event?
2. What is an alert?
3. What is an incident?
4. What is the difference between an event and an alert?
5. Is every alert an incident?
6. What is a false positive?
7. What is a true positive?

### SOC L1

8. How do you investigate an alert?
9. What information should an alert contain?
10. How do you prioritize an alert?
11. When should an alert be escalated?
12. How do you determine whether an alert is benign?
13. What is alert enrichment?
14. What is event correlation?

### Practical

15. How would you investigate a brute-force alert?
16. How would you investigate suspicious PowerShell?
17. What logs would you check for account compromise?
18. How would you determine whether an IP is malicious?
19. How would you document your investigation?

---

# 22. Practical Lab

Create a simple SOC investigation in your home lab.

### Environment

```text
Windows VM
     +
Sysmon
     +
Wazuh
     +
Kali Linux
```

### Generate Activity

For example:

```text
Failed Login Attempts
        ↓
PowerShell Execution
        ↓
Suspicious Process
        ↓
Network Connection
```

### Collect

```text
Windows Event Logs
Sysmon Logs
Wazuh Alerts
Network Telemetry
```

### Investigate

Create:

```text
Timeline
IOC List
MITRE ATT&CK Mapping
Alert Classification
Investigation Report
```

---

# 23. Portfolio Evidence

For your GitHub portfolio, this document should eventually connect to practical evidence:

```text
SOC Fundamentals
       ↓
Home Lab
       ↓
Telemetry
       ↓
Detection
       ↓
Alert
       ↓
Investigation
       ↓
Incident Report
```

Your strongest evidence is not simply knowing the definitions.

It is demonstrating:

> **"I can take raw security telemetry, understand what happened, investigate the resulting alert, determine whether it represents a threat, document the evidence, and escalate appropriately."**

---

# 24. Key Takeaway

```text
EVENT
Something happened
      ↓
ALERT
Detection says:
"This may be suspicious."
      ↓
TRIAGE
Analyst investigates
      ↓
INCIDENT
Confirmed/suspected security issue
      ↓
RESPONSE
Contain → Eradicate → Recover
```

### Remember:

> **Events are data. Alerts are signals. Incidents are security situations that require response.**

This distinction is fundamental to becoming an effective SOC analyst.
