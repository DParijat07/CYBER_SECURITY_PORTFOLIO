# 🛡️ What is a Security Operations Center (SOC)?

> A **Security Operations Center (SOC)** is a centralized security function responsible for continuously monitoring an organization's digital environment, detecting suspicious activity, investigating security events, responding to incidents, and improving the organization's defensive capabilities.

A SOC combines:

```text
People
   +
Processes
   +
Technology
   ↓
Security Operations
```

Its primary purpose is to reduce the organization's exposure to cyber threats by providing continuous visibility and coordinated security response.

---

# 1. Why Does an Organization Need a SOC?

Modern organizations operate large and complex technology environments.

An organization may have:

* Employee laptops
* Servers
* Databases
* Network devices
* Firewalls
* Cloud infrastructure
* Web applications
* APIs
* Email systems
* Identity platforms
* Security appliances
* IoT devices

Every one of these systems can generate security-relevant activity.

For example:

```text
User Login
File Access
Process Execution
Network Connection
DNS Request
Email Received
Cloud API Call
Firewall Connection
```

Individually, these activities may look normal.

However, when correlated together, they may reveal an attack.

Example:

```text
Failed Login Attempts
        ↓
Successful Login
        ↓
New Process
        ↓
PowerShell Execution
        ↓
External Network Connection
        ↓
Credential Access
```

A SOC provides the capability to identify and investigate such patterns.

---

# 2. Core Mission of a SOC

The core mission can be summarized as:

> **Detect threats early, investigate them accurately, respond effectively, and continuously improve security.**

A simplified lifecycle is:

```text
Monitor
   ↓
Detect
   ↓
Triage
   ↓
Investigate
   ↓
Respond
   ↓
Recover
   ↓
Learn
   ↓
Improve
```

---

# 3. What Does a SOC Actually Monitor?

A SOC can monitor multiple layers of an organization's environment.

## Endpoint

Examples:

* Windows
* Linux
* macOS
* Servers
* Workstations

Telemetry may include:

* Process creation
* File activity
* Authentication
* Registry changes
* Network connections
* Security events

---

## Network

Examples:

* Routers
* Switches
* Firewalls
* IDS/IPS
* Proxies
* DNS infrastructure

Telemetry may include:

* Source IP
* Destination IP
* Ports
* Protocols
* DNS queries
* Network sessions
* Suspicious traffic

---

## Identity

Examples:

* Active Directory
* Microsoft Entra ID
* IAM platforms
* Authentication systems

Monitoring may include:

* Login attempts
* Failed authentication
* MFA activity
* Privilege changes
* New accounts
* Password changes

---

## Applications

Examples:

* Web applications
* APIs
* Databases
* Business applications

Monitoring may include:

* Authentication
* Application errors
* API requests
* Suspicious input
* Administrative activity

---

## Cloud

Examples:

* AWS
* Microsoft Azure
* Google Cloud

Monitoring may include:

* API calls
* IAM activity
* Resource creation
* Configuration changes
* Storage access
* Administrative actions

---

# 4. SOC Architecture

A simplified SOC architecture looks like:

```text
                  ORGANIZATION
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     Endpoints       Network       Identity
        │              │              │
        └──────────────┼──────────────┘
                       ↓
                  Log Sources
                       ↓
                Collection Layer
                       ↓
                     SIEM
                       ↓
               Detection Rules
                       ↓
                    Alerts
                       ↓
                  SOC Analyst
                       ↓
              Investigation
                       ↓
             Incident Response
```

In a mature environment, additional systems may provide:

```text
SIEM
EDR/XDR
SOAR
TIP
NDR
Vulnerability Management
Case Management
```

---

# 5. People in a SOC

A SOC is not just a technology platform.

People are responsible for interpreting security information and making decisions.

Typical roles include:

```text
SOC Analyst L1
      ↓
SOC Analyst L2
      ↓
SOC Analyst L3
      ↓
Detection Engineer
Threat Hunter
Incident Responder
Threat Intelligence Analyst
SOC Manager
```

Different organizations use different titles and structures.

---

# 6. SOC Analyst L1

L1 is generally the first operational layer.

Typical responsibilities include:

* Monitor alerts
* Review security events
* Perform initial triage
* Validate alerts
* Identify basic IOCs
* Determine severity
* Document findings
* Escalate suspicious activity

The L1 analyst generally asks:

> **"Is this alert legitimate, and does it require escalation?"**

---

# 7. SOC Analyst L2

L2 performs deeper investigations.

Responsibilities may include:

* Correlating multiple events
* Investigating suspicious hosts
* Investigating compromised accounts
* Performing threat analysis
* Conducting threat hunting
* Tuning detections
* Performing root-cause analysis
* Supporting incident response

The L2 analyst asks:

> **"What happened, how did it happen, and what is the scope?"**

---

# 8. SOC Analyst L3

L3 typically handles highly complex security problems.

Responsibilities can include:

* Advanced threat hunting
* Detection engineering
* Advanced incident response
* Malware analysis
* Advanced forensics
* Adversary analysis
* Security engineering
* Complex investigations

The L3 analyst asks:

> **"How did the adversary operate, and how can we detect and prevent this behavior in the future?"**

---

# 9. SOC vs SIEM

These terms are often confused.

## SOC

A **security operation/function** involving:

* People
* Processes
* Technology
* Monitoring
* Investigation
* Response

## SIEM

A **technology platform** used to:

* Collect logs
* Normalize data
* Search events
* Correlate activity
* Generate detections
* Produce alerts

Therefore:

```text
SIEM ≠ SOC
```

Instead:

```text
SOC
 │
 ├── People
 ├── Processes
 └── Technology
       │
       └── SIEM
```

A SIEM is one component of a SOC.

---

# 10. SOC vs NOC

A **Network Operations Center (NOC)** primarily focuses on availability and performance.

A **Security Operations Center (SOC)** primarily focuses on security.

| NOC                   | SOC                 |
| --------------------- | ------------------- |
| Availability          | Security            |
| Performance           | Threat detection    |
| Network health        | Security monitoring |
| Outages               | Security incidents  |
| Infrastructure uptime | Risk reduction      |

There can be collaboration between both functions.

For example:

```text
Network Outage
     ↓
NOC

Suspicious Network Traffic
     ↓
SOC
```

---

# 11. SOC vs CERT/CSIRT

A SOC and an incident-response team can overlap but are not necessarily identical.

### SOC

Usually focuses on:

* Continuous monitoring
* Detection
* Alert triage
* Investigation
* Escalation

### CSIRT / CERT

Usually focuses more heavily on:

* Incident coordination
* Containment
* Eradication
* Recovery
* Major incident management

A mature organization may have both.

```text
SOC
 ↓
Detect
 ↓
Investigate
 ↓
Escalate
 ↓
CSIRT / IR
 ↓
Contain
 ↓
Eradicate
 ↓
Recover
```

---

# 12. SOC Workflow

A typical workflow is:

```text
1. Collect Telemetry
        ↓
2. Detect Suspicious Activity
        ↓
3. Generate Alert
        ↓
4. Triage
        ↓
5. Investigate
        ↓
6. Classify
        ↓
7. Escalate if Required
        ↓
8. Respond
        ↓
9. Recover
        ↓
10. Document
        ↓
11. Improve Detection
```

This is the operational cycle that will be explored throughout the SOC portfolio.

---

# 13. Security Telemetry

A SOC cannot detect what it cannot observe.

Therefore, visibility is fundamental.

Common telemetry sources include:

```text
Windows Event Logs
Sysmon
Linux Logs
Firewall Logs
DNS Logs
Proxy Logs
EDR
IDS/IPS
Cloud Logs
Authentication Logs
Application Logs
```

These sources provide evidence about what is happening in the environment.

---

# 14. Event → Alert → Incident

One of the most important concepts for a beginner SOC analyst is understanding the difference between these three.

## Event

Something happened.

Example:

```text
User authentication failed.
```

---

## Alert

A detection mechanism determines that an event or event pattern may require investigation.

Example:

```text
25 failed authentication attempts
from the same source within 5 minutes.
```

---

## Incident

Investigation determines that the activity represents a security event requiring response.

Example:

```text
Password spraying successfully compromised
a privileged account.
```

Therefore:

```text
Event
  ↓
Detection
  ↓
Alert
  ↓
Investigation
  ↓
Incident
```

Not every event becomes an alert.

Not every alert becomes an incident.

---

# 15. Example SOC Investigation

Consider this scenario.

An organization receives an alert:

```text
ALERT:
Multiple failed logins detected.
```

The analyst begins investigation.

### Step 1 — Identify Source

```text
Source IP: 185.x.x.x
```

### Step 2 — Identify Target

```text
Target:
Multiple employee accounts
```

### Step 3 — Analyze Timing

```text
50 attempts
15 accounts
10 minutes
```

### Step 4 — Check Authentication

One account successfully authenticated.

```text
Failed attempts
      ↓
Successful login
```

### Step 5 — Investigate the Account

The account is a normal employee account.

Immediately afterward:

```text
New login location
        ↓
PowerShell execution
        ↓
External connection
```

The alert is now significantly more suspicious.

### Step 6 — Correlate Evidence

```text
Password Spraying
       +
Successful Authentication
       +
Suspicious PowerShell
       +
External Connection
```

This may indicate account compromise.

---

# 16. Why Correlation Matters

A single event may not be malicious.

Consider:

```text
PowerShell executed
```

This could be completely legitimate.

But:

```text
PowerShell
+
Encoded command
+
Unusual parent process
+
External connection
+
Newly created account
```

provides much stronger evidence.

Therefore SOC analysts should think in terms of:

> **Context + Correlation + Evidence**

rather than isolated alerts.

---

# 17. Detection vs Prevention

A SOC primarily provides detection and response capabilities, but prevention is also part of the broader security ecosystem.

Example:

```text
Firewall
   ↓
Prevention

EDR
   ↓
Detection + Prevention

SIEM
   ↓
Detection + Investigation

SOC
   ↓
Monitoring + Investigation + Response
```

A SOC does not replace preventive security controls.

It operates as part of a broader defense-in-depth strategy.

---

# 18. SOC and Defense-in-Depth

A mature security architecture uses multiple layers.

```text
Identity Security
       ↓
Network Security
       ↓
Endpoint Security
       ↓
Application Security
       ↓
Data Security
       ↓
Monitoring
       ↓
SOC
       ↓
Incident Response
```

If one security control fails, another layer may still detect or limit the attack.

---

# 19. SOC Metrics

SOC performance can be measured using metrics such as:

### Mean Time to Detect — MTTD

How quickly a threat is detected.

### Mean Time to Respond — MTTR

How quickly the organization responds.

Other metrics may include:

* Alert volume
* False-positive rate
* Detection coverage
* Escalation rate
* Incident count
* Investigation time
* SLA compliance
* Detection effectiveness

Metrics should be interpreted in context rather than treated as isolated performance scores.

---

# 20. SOC Maturity

SOC capabilities can develop progressively.

```text
Reactive
   ↓
Basic Monitoring
   ↓
Structured Detection
   ↓
Proactive Hunting
   ↓
Advanced Detection Engineering
   ↓
Automated Security Operations
```

A mature SOC typically has:

* Strong telemetry
* Reliable detections
* Defined processes
* Skilled analysts
* Threat intelligence
* Threat hunting
* Automation
* Continuous improvement

---

# 21. SOC and AI

Artificial intelligence can augment SOC operations.

Potential applications include:

* Alert summarization
* Log analysis
* IOC enrichment
* Threat-intelligence summarization
* Investigation assistance
* Detection-rule suggestions
* Incident timeline generation
* Report drafting
* Security knowledge retrieval

However:

```text
AI Recommendation
       ↓
Human Verification
       ↓
Security Decision
```

AI should assist analysts rather than blindly replace analyst judgment.

---

# 22. SOC Analyst Mindset

A SOC analyst should be:

### Curious

Ask:

> "Why did this happen?"

### Analytical

Look for relationships between events.

### Evidence-driven

Base conclusions on observable evidence.

### Skeptical

Do not automatically trust an alert or dismiss it.

### Methodical

Follow a consistent investigation process.

### Documentation-oriented

Record what was observed and why a conclusion was reached.

---

# 23. What a Beginner Should Be Able to Explain

After studying this document, I should be able to answer:

1. What is a SOC?
2. Why do organizations need a SOC?
3. What are the three pillars of a SOC?
4. What does a SOC L1 analyst do?
5. What does L2 do?
6. What does L3 do?
7. What is a SIEM?
8. How is a SIEM different from a SOC?
9. What is security telemetry?
10. What is an event?
11. What is an alert?
12. What is an incident?
13. What is an IOC?
14. What is an IOA?
15. What are TTPs?
16. What is alert triage?
17. Why is correlation important?
18. What is escalation?
19. What is incident response?
20. What are MTTD and MTTR?

---

# 24. Practical Exercise

## Scenario

You receive:

```text
20 failed login attempts
from one IP address
against 8 user accounts
within 3 minutes.
```

### Questions

1. Is this automatically an incident?
2. What additional information should you collect?
3. Which accounts were targeted?
4. Was any login successful?
5. Is the source IP internal or external?
6. What is the source IP reputation?
7. What happened after successful authentication?
8. Are there related events?
9. What severity would you assign?
10. Should the alert be escalated?

### Investigation Principle

Do not immediately conclude:

> "This is brute force."

Instead:

> **Collect evidence → establish context → correlate activity → determine confidence → classify → respond.**

---

# 25. Key Takeaways

The most important concepts from this document are:

```text
SOC
 ↓
People + Process + Technology
```

```text
Telemetry
 ↓
Events
 ↓
Detection
 ↓
Alerts
 ↓
Triage
 ↓
Investigation
 ↓
Incident
 ↓
Response
```

```text
L1
 ↓
Monitor + Triage

L2
 ↓
Investigate + Hunt

L3
 ↓
Advanced Investigation + Engineering
```

And the fundamental SOC mindset is:

> **Don't just ask what the alert says. Ask what the evidence tells you.**

---

# 📚 Related Documentation

This document provides the foundation for the remaining SOC learning path.

Next:

```text
02-SOC-People-Process-Technology.md
03-SOC-Roles-and-Responsibilities.md
04-SOC-Tiers-L1-L2-L3.md
05-SOC-Workflow.md
06-Security-Telemetry.md
07-Logs-and-Events.md
```

Later practical implementation:

```text
02-SOC-L1/
05-SIEM/
06-Detection-Rules/
07-Alert-Triage/
08-Investigation/
09-Incident-Response/
```

---

# ⭐ Core Principle

> **A SOC is not simply a room full of security tools. It is an operational capability that turns security telemetry into timely, evidence-based security decisions.**
