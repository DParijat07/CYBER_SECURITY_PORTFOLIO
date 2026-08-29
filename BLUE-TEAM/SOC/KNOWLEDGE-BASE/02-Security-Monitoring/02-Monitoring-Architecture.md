# Monitoring Architecture

> **Blue Team → SOC → Security Monitoring**

Security monitoring architecture defines how security data moves from organizational assets to monitoring platforms, detection systems, SOC analysts, and ultimately incident response.

A good architecture provides:

* Visibility
* Centralized telemetry
* Reliable data collection
* Detection capability
* Investigation capability
* Scalability
* Retention
* Security context

The fundamental model is:

```text
Assets
   ↓
Telemetry
   ↓
Collection
   ↓
Processing
   ↓
Storage
   ↓
Detection
   ↓
Alerting
   ↓
SOC
   ↓
Investigation
   ↓
Response
```

---

# 1. Objectives

After completing this section, you should understand:

* Security monitoring architecture
* Data sources
* Sensors and agents
* Log collectors
* Log pipelines
* Data normalization
* Data enrichment
* Centralized logging
* SIEM architecture
* Detection engines
* Alerting
* SOC analyst workflow
* Network monitoring architecture
* Endpoint monitoring architecture
* Cloud monitoring architecture
* Home-lab architecture
* Monitoring architecture weaknesses

---

# 2. High-Level Security Monitoring Architecture

A modern monitoring environment can be represented as:

```text
                    ORGANIZATIONAL ENVIRONMENT
                              │
       ┌──────────────────────┼──────────────────────┐
       ↓                      ↓                      ↓
   Endpoints               Network                Identity
       │                      │                      │
 Windows / Linux        Firewall / IDS          AD / IAM / VPN
 EDR / Sysmon            DNS / Proxy             SSO / MFA
       │                      │                      │
       └──────────────────────┼──────────────────────┘
                              ↓
                       DATA COLLECTION
                              ↓
                     PROCESSING / PARSING
                              ↓
                       NORMALIZATION
                              ↓
                         ENRICHMENT
                              ↓
                           STORAGE
                              ↓
                           SIEM
                              ↓
                    CORRELATION / DETECTION
                              ↓
                           ALERTING
                              ↓
                       SOC ANALYST
                              ↓
                    INVESTIGATION / RESPONSE
```

---

# 3. Architecture Layers

A useful way to understand the architecture is through layers:

```text
Layer 1  Assets
Layer 2  Telemetry
Layer 3  Collection
Layer 4  Processing
Layer 5  Storage
Layer 6  Detection
Layer 7  Alerting
Layer 8  Investigation
Layer 9  Response
```

Each layer has a different purpose.

---

# 4. Layer 1 — Assets

Assets generate the activity that must be monitored.

Examples:

```text
Workstations
Servers
Laptops
Mobile Devices
Network Devices
Firewalls
Applications
Databases
Cloud Resources
Identity Systems
Email Systems
```

Example:

```text
Windows Server
       ↓
Process Event
       ↓
Security Telemetry
```

---

# 5. Layer 2 — Telemetry

Telemetry describes what is happening inside the environment.

Examples:

```text
Windows Events
Sysmon
Linux Logs
Firewall Logs
DNS Queries
Network Flows
EDR Events
Authentication Events
Cloud Audit Logs
Application Logs
```

Telemetry is the raw input for the monitoring architecture.

---

# 6. Layer 3 — Data Collection

Telemetry must be collected from the source.

Common approaches:

```text
Agent-Based Collection
Agentless Collection
Network Sensors
API Collection
Log Forwarding
Cloud Connectors
```

Examples:

```text
Wazuh Agent
Windows Event Forwarding
Syslog
Cloud APIs
Network Sensors
```

---

# 7. Agent-Based Collection

An agent runs on the monitored endpoint.

Example:

```text
Windows Endpoint
      │
 Wazuh Agent
      │
      ↓
Wazuh Manager
```

Advantages:

* Detailed endpoint visibility
* Real-time collection
* Local processing
* Endpoint-specific telemetry

Potential challenges:

* Agent deployment
* Resource consumption
* Configuration management
* Agent tampering

---

# 8. Agentless Collection

Some systems can forward logs without installing an endpoint agent.

Example:

```text
Firewall
   │
   ↓
Syslog
   │
   ↓
Log Collector
   │
   ↓
SIEM
```

Useful for:

```text
Network Devices
Firewalls
Some Applications
Infrastructure Appliances
```

---

# 9. Network Sensors

Network sensors observe traffic and network behavior.

Examples:

```text
IDS
IPS
Zeek
Suricata
NetFlow
Packet Capture
```

Architecture:

```text
Network Traffic
      ↓
Network Sensor
      ↓
Metadata / Alerts
      ↓
SIEM
```

Network monitoring complements endpoint telemetry.

---

# 10. Log Collection

A centralized collector receives logs from multiple sources.

Example:

```text
Windows ───────┐
Linux ─────────┤
Firewall ──────┤
DNS ───────────┤
Application ───┤
Cloud ─────────┘
        ↓
 Log Collector
        ↓
      SIEM
```

The collector acts as a bridge between data sources and the monitoring platform.

---

# 11. Log Processing

Raw logs often need processing before analysis.

Typical steps:

```text
Raw Log
   ↓
Parsing
   ↓
Field Extraction
   ↓
Normalization
   ↓
Enrichment
   ↓
Indexing
```

Example:

```text
Raw:
"Failed password for admin from 10.0.0.5"

Parsed:
Event = Authentication Failure
User = admin
Source IP = 10.0.0.5
```

---

# 12. Log Parsing

Parsing converts unstructured or semi-structured logs into usable fields.

Example:

```text
Raw Event
    ↓
Timestamp
User
Source IP
Action
Status
```

Without effective parsing:

```text
Searchability ↓
Correlation ↓
Detection Quality ↓
```

---

# 13. Normalization

Different systems may represent similar activity differently.

Example:

```text
Windows:
4625

Linux:
Failed password

Cloud:
Authentication failure
```

A monitoring platform can normalize them conceptually as:

```text
Authentication Failure
```

This allows cross-platform correlation.

---

# 14. Data Enrichment

Enrichment adds additional context.

Example:

```text
Source IP
    ↓
Threat Intelligence
    ↓
IP Reputation
    ↓
GeoIP
    ↓
Asset Information
    ↓
User Information
```

The original event becomes more useful to the analyst.

---

# 15. Storage

Security data must be stored for:

```text
Investigation
Threat Hunting
Compliance
Forensics
Historical Analysis
Detection Development
Incident Response
```

Important considerations:

```text
Retention
Capacity
Performance
Access Control
Integrity
Encryption
```

---

# 16. Hot vs Cold Data

Security platforms may maintain different storage tiers.

### Hot Data

Frequently accessed.

```text
Recent Events
Active Investigations
Current Alerts
```

### Cold Data

Older information retained for:

```text
Historical Investigation
Compliance
Forensics
Long-Term Analysis
```

This can reduce storage costs while maintaining historical visibility.

---

# 17. SIEM Layer

The SIEM is often the central monitoring platform.

Core functions include:

```text
Collection
Parsing
Normalization
Storage
Search
Correlation
Detection
Alerting
Dashboards
Investigation
Reporting
```

Examples:

```text
Wazuh
Splunk
Microsoft Sentinel
IBM QRadar
Elastic Security
```

---

# 18. Detection Engine

The detection layer evaluates telemetry against defined logic.

Example:

```text
Failed Login
+
Same Source
+
Multiple Accounts
+
Short Time Window
        ↓
Password Spraying Detection
```

Detection can be:

```text
Rule-Based
Threshold-Based
Correlation-Based
Behavior-Based
Anomaly-Based
```

---

# 19. Rule-Based Detection

A rule looks for a known pattern.

Example:

```text
IF
PowerShell executes
AND
command contains suspicious behavior
THEN
generate alert
```

Rule-based detection is highly useful for known behaviors.

---

# 20. Threshold Detection

Threshold detection looks for activity exceeding a defined limit.

Example:

```text
IF
Failed logins > 20
within 5 minutes
THEN
generate alert
```

This can be useful for:

```text
Brute Force
Scanning
Excessive Requests
Data Transfer
```

Thresholds must be tuned to the environment.

---

# 21. Correlation Detection

Correlation combines multiple events.

Example:

```text
Failed Login
      ↓
Successful Login
      ↓
Privileged Action
      ↓
Suspicious Network Connection
```

The combination may be more meaningful than any single event.

---

# 22. Alerting Layer

When detection logic identifies suspicious activity:

```text
Detection
   ↓
Alert
```

An alert should ideally contain:

```text
Alert Name
Severity
Timestamp
Host
User
Source
Destination
Evidence
Detection Rule
MITRE ATT&CK
Related Events
```

Good alerts provide enough context for efficient triage.

---

# 23. SOC Analyst Layer

The SOC analyst receives alerts and performs:

```text
Triage
Validation
Enrichment
Correlation
Investigation
Classification
Escalation
Documentation
```

Example:

```text
Alert
 ↓
Validate
 ↓
Investigate
 ↓
Determine Risk
 ↓
Escalate / Close
```

---

# 24. Response Layer

If malicious activity is confirmed, response actions may include:

```text
Endpoint Isolation
Account Disablement
Credential Reset
IP Blocking
Domain Blocking
Process Termination
File Quarantine
Firewall Changes
Incident Escalation
```

The exact action depends on organizational procedures and analyst authorization.

---

# 25. Endpoint Monitoring Architecture

A typical endpoint architecture:

```text
                 ENDPOINT
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
     Windows      Sysmon       EDR
     Events
        │           │           │
        └───────────┼───────────┘
                    ↓
                 Agent
                    ↓
                  SIEM
                    ↓
                Detection
                    ↓
                  Alert
```

---

# 26. Windows Home-Lab Architecture

For your lab:

```text
Windows VM
    │
    ├── Windows Event Logs
    │
    └── Sysmon
          │
          ↓
      Wazuh Agent
          │
          ↓
     Wazuh Manager
          │
          ↓
       Dashboard
```

This gives you practical experience with endpoint telemetry.

---

# 27. Linux Monitoring Architecture

Example:

```text
Linux VM
   │
   ├── auth.log
   ├── syslog
   ├── journalctl
   └── auditd
          │
          ↓
      Wazuh Agent
          │
          ↓
      Wazuh Manager
          │
          ↓
          SIEM
```

---

# 28. Network Monitoring Architecture

A basic network monitoring design:

```text
Network
   │
   ├──────────────→ Firewall
   │
   ├──────────────→ IDS/IPS
   │
   ├──────────────→ DNS
   │
   └──────────────→ Network Sensor
                          │
                          ↓
                         SIEM
                          │
                          ↓
                       SOC
```

---

# 29. Identity Monitoring Architecture

Identity monitoring:

```text
User
 ↓
Authentication
 ↓
AD / IAM / SSO / VPN
 ↓
Authentication Logs
 ↓
SIEM
 ↓
Correlation
 ↓
Detection
 ↓
Alert
```

This becomes particularly important for:

```text
Brute Force
Password Spraying
Account Compromise
Privilege Abuse
Impossible Travel
```

---

# 30. Cloud Monitoring Architecture

A simplified cloud model:

```text
Cloud Resources
      │
      ↓
Cloud Audit Logs
      │
      ↓
Cloud Monitoring
      │
      ↓
API / Connector
      │
      ↓
SIEM
      │
      ↓
Detection
      │
      ↓
SOC
```

Cloud monitoring should cover:

```text
IAM
API Activity
Storage
Network
Compute
Configuration
Security Controls
```

---

# 31. Distributed vs Centralized Monitoring

### Centralized

```text
All Sources
     ↓
One Central SIEM
     ↓
SOC
```

Advantages:

* Easier investigation
* Centralized visibility
* Easier correlation
* Centralized reporting

### Distributed

Multiple monitoring platforms or regional systems may exist.

Useful for:

```text
Large Enterprises
Multiple Regions
Different Business Units
Regulatory Requirements
```

A mature architecture may combine both approaches.

---

# 32. Security of the Monitoring Infrastructure

The monitoring platform itself must be protected.

Protect:

```text
SIEM
Log Collectors
Agents
Detection Rules
Dashboards
Credentials
API Keys
Stored Logs
```

Threats include:

```text
Log Tampering
Log Deletion
Agent Tampering
Credential Theft
Unauthorized Access
Detection Rule Manipulation
```

Security monitoring infrastructure is itself a critical asset.

---

# 33. Log Integrity

Logs may become evidence during an investigation.

Important controls:

```text
Access Control
Integrity Protection
Centralized Collection
Time Synchronization
Retention Policies
Audit Trails
```

Avoid relying solely on logs stored locally on a potentially compromised system.

---

# 34. Time Synchronization

Accurate timestamps are essential.

Architecture should ideally use:

```text
NTP
   ↓
Consistent System Time
   ↓
Accurate Event Correlation
   ↓
Reliable Timeline
```

Without synchronized clocks:

```text
Event A: 10:05
Event B: 09:58
```

may appear to occur in the wrong sequence.

---

# 35. Monitoring Architecture and Scalability

A small lab may have:

```text
3–5 endpoints
+
1 SIEM
```

An enterprise may have:

```text
Thousands of Endpoints
+
Hundreds of Network Devices
+
Cloud Infrastructure
+
Multiple Applications
+
Millions of Events
```

Architecture must therefore consider:

```text
Volume
Velocity
Storage
Network Bandwidth
Processing
High Availability
Retention
```

---

# 36. High Availability

Critical monitoring infrastructure should avoid a single point of failure.

Conceptually:

```text
Sources
   │
   ├────→ Collector A ────┐
   │                      │
   └────→ Collector B ────┤
                          ↓
                     SIEM Cluster
                          ↓
                         SOC
```

The exact implementation depends on the platform and organizational requirements.

---

# 37. Monitoring Architecture Failure Points

Potential failures include:

```text
Missing Telemetry
Agent Offline
Network Failure
Collector Failure
Parser Failure
Storage Failure
Detection Rule Failure
Alert Delivery Failure
Dashboard Failure
```

A good SOC monitors its own monitoring infrastructure.

---

# 38. Detection Pipeline Failure

Consider:

```text
Endpoint
  ↓
Telemetry Generated
  ↓
Collection Failed
  ↓
No SIEM Event
  ↓
No Detection
  ↓
No Alert
```

The attacker may remain invisible.

Therefore monitoring health should also be monitored.

---

# 39. Monitoring Health

Useful health checks include:

```text
Agent Status
Log Ingestion Rate
Collector Health
Parser Errors
Storage Capacity
Detection Rule Status
Alert Pipeline
Time Synchronization
```

Example:

```text
Expected:
1000 events/minute

Actual:
20 events/minute

        ↓

Potential Monitoring Failure
```

---

# 40. Your Home-Lab Architecture

Your portfolio can demonstrate a practical architecture like:

```text
                         HOME LAB
                            │
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
        Windows VM       Linux VM    Metasploitable
             │              │              │
          Sysmon          Logs         Vulnerable App
             │              │              │
             └──────────────┼──────────────┘
                            ↓
                       Wazuh Agents
                            ↓
                       Wazuh Manager
                            ↓
                         Wazuh SIEM
                            ↓
                     Detection Rules
                            ↓
                          Alerts
                            ↓
                       Investigation
                            ↓
                          Reports
```

You can later extend it with:

```text
Kali
Suricata
Zeek
Wireshark
Firewall
Cloud Lab
```

---

# 41. Architecture-to-Portfolio Mapping

Your GitHub should demonstrate each architectural layer.

| Layer         | Portfolio Evidence           |
| ------------- | ---------------------------- |
| Assets        | Home-lab topology            |
| Telemetry     | Sample logs                  |
| Collection    | Wazuh Agent configuration    |
| Processing    | Parsing/decoding examples    |
| Normalization | Normalized fields            |
| Enrichment    | Threat intelligence examples |
| Storage       | SIEM dashboards              |
| Detection     | Detection rules              |
| Alerting      | Alert screenshots            |
| Investigation | Case studies                 |
| Response      | Incident reports             |
| Improvement   | Detection tuning             |

This is much stronger than simply writing about SIEM architecture.

---

# 42. Architecture Documentation

For every major lab, document:

```text
Architecture Diagram
Components
Data Sources
Data Flow
Collection Method
Detection Method
Alert Flow
Investigation Process
Limitations
Security Controls
```

A simplified example:

```text
[Windows VM]
      │
      │ Sysmon
      ↓
[Wazuh Agent]
      │
      │ Secure Transmission
      ↓
[Wazuh Manager]
      │
      ↓
[Detection Engine]
      │
      ↓
[Alert]
      │
      ↓
[SOC Analyst]
```

---

# 43. Architecture Review Checklist

When designing monitoring architecture, ask:

```text
□ What assets need monitoring?
□ What telemetry is available?
□ What telemetry is missing?
□ How will data be collected?
□ How will logs be normalized?
□ How will data be enriched?
□ Where will logs be stored?
□ What detections are required?
□ How will alerts reach analysts?
□ How long will data be retained?
□ How will monitoring infrastructure be protected?
□ What happens if collection fails?
□ What happens if the SIEM fails?
□ How will coverage be measured?
```

---

# 44. Interview Questions

### Architecture

1. What is a security monitoring architecture?
2. What are the major components of a SOC monitoring architecture?
3. What is the role of a log collector?
4. What is the role of a SIEM?
5. What is the difference between an agent and an agentless collector?
6. Why is normalization important?
7. What is log enrichment?
8. How does a detection engine work?
9. Why is time synchronization important?
10. How would you design monitoring for a small organization?

### Scenario

**Question:**

> A Windows endpoint is generating security events, but nothing appears in the SIEM. How would you investigate?

Approach:

```text
Endpoint
   ↓
Check Event Generation
   ↓
Check Agent
   ↓
Check Agent Connectivity
   ↓
Check Collector
   ↓
Check Parsing
   ↓
Check Ingestion
   ↓
Check SIEM Index
   ↓
Check Detection
```

---

# 45. Key Takeaways

```text
1. Monitoring architecture connects assets to analysts.

2. Telemetry is the foundation of monitoring.

3. Collection brings telemetry into the monitoring platform.

4. Processing makes raw data usable.

5. Normalization enables correlation.

6. Enrichment adds context.

7. SIEM provides centralized visibility and detection.

8. Detection rules convert behavior into alerts.

9. Analysts convert alerts into investigations.

10. Monitoring infrastructure itself must be monitored.

11. Architecture must account for scalability and availability.

12. Good architecture reduces visibility gaps.
```

---

# 46. Final Mental Model

Remember the complete flow:

```text
                         ASSETS
                           ↓
                       TELEMETRY
                           ↓
                       COLLECTION
                           ↓
                       PROCESSING
                           ↓
                      NORMALIZATION
                           ↓
                       ENRICHMENT
                           ↓
                         STORAGE
                           ↓
                      CORRELATION
                           ↓
                       DETECTION
                           ↓
                        ALERTING
                           ↓
                     SOC ANALYST
                           ↓
                      INVESTIGATION
                           ↓
                       RESPONSE
                           ↓
                    LESSONS LEARNED
                           ↓
                  DETECTION IMPROVEMENT
```

> **A strong security monitoring architecture does not simply collect logs. It transforms distributed security activity into reliable, searchable, contextualized, and actionable security intelligence.**
