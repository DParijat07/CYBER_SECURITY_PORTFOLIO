# 👥 SOC — People, Process & Technology

> A Security Operations Center is effective only when **people, processes, and technology work together as one operational system**.

The three pillars of a SOC are:

```text id="q7b2k1"
              SOC
               │
      ┌────────┼────────┐
      │        │        │
    PEOPLE   PROCESS  TECHNOLOGY
      │        │        │
      └────────┼────────┘
               ↓
      Security Operations
               ↓
       Risk Reduction
```

A powerful security tool cannot compensate for poor processes or inexperienced analysts. Similarly, skilled analysts cannot operate effectively without the required telemetry, tools, and defined procedures.

---

# 1. The Three Pillars

## People

People provide:

* Analysis
* Decision-making
* Investigation
* Threat assessment
* Incident coordination
* Security expertise

## Process

Processes provide:

* Consistency
* Repeatability
* Escalation paths
* Incident handling
* Documentation
* Accountability

## Technology

Technology provides:

* Visibility
* Data collection
* Detection
* Investigation capabilities
* Automation
* Response capabilities

Therefore:

```text id="q8y0cb"
People
  ↓
Understand the threat

Process
  ↓
Define what to do

Technology
  ↓
Provide visibility and capability
```

---

# 2. Why All Three Matter

Consider an organization with an excellent SIEM.

The SIEM generates:

```text id="4n5p7z"
10,000 security alerts
```

But there are:

* No trained analysts
* No triage process
* No escalation procedure
* No incident-response plan

The organization still has a weak SOC.

Now consider the opposite.

There are highly skilled analysts but:

* Poor logging
* No centralized monitoring
* No detection rules
* No endpoint telemetry

The analysts cannot see enough of the environment.

This demonstrates:

> **SOC effectiveness depends on the interaction between People, Process and Technology.**

---

# 3. PEOPLE

People are responsible for interpreting security information and making decisions.

A SOC team may contain several specialized roles.

```text id="m4m2s7"
SOC Manager
     │
     ├── SOC L3
     │     ├── Detection Engineering
     │     └── Advanced Investigation
     │
     ├── SOC L2
     │     ├── Threat Hunting
     │     └── Incident Investigation
     │
     └── SOC L1
           ├── Monitoring
           ├── Triage
           └── Escalation
```

The exact structure differs between organizations.

---

# 4. SOC Manager

The SOC Manager is responsible for the overall operation of the SOC.

Typical responsibilities:

* Team management
* Operational planning
* Security metrics
* SLA management
* Incident coordination
* Resource planning
* Process improvement
* Stakeholder communication
* Reporting to management

The manager is generally focused more on:

> **Operational effectiveness and risk management**

than individual alert investigation.

---

# 5. SOC Analyst L1

L1 is usually the first line of operational analysis.

Typical responsibilities:

* Monitor alerts
* Review events
* Perform initial triage
* Validate suspicious activity
* Identify basic IOCs
* Determine severity
* Document findings
* Escalate suspicious cases

Typical workflow:

```text id="8mx7bq"
Alert
 ↓
Validate
 ↓
Collect Context
 ↓
Classify
 ↓
Document
 ↓
Close / Escalate
```

The L1 analyst's main objective is:

> **Quickly determine whether an alert requires further investigation.**

---

# 6. SOC Analyst L2

L2 performs deeper investigations.

Typical responsibilities:

* Correlate multiple events
* Investigate suspicious hosts
* Analyze user activity
* Investigate compromised accounts
* Perform threat analysis
* Conduct threat hunting
* Tune detections
* Perform root-cause analysis
* Support incident response

Typical workflow:

```text id="p1q2x6"
Escalated Alert
      ↓
Deep Investigation
      ↓
Correlation
      ↓
Root Cause
      ↓
Scope
      ↓
Response Recommendation
```

---

# 7. SOC Analyst L3

L3 handles complex or advanced security problems.

Typical responsibilities:

* Advanced threat hunting
* Detection engineering
* Advanced incident response
* Malware analysis
* Advanced forensics
* Adversary analysis
* Security engineering
* Complex incident investigation

The L3 analyst often asks:

> **How can we detect, contain and prevent this class of attack more effectively?**

---

# 8. Detection Engineer

A detection engineer converts threat knowledge into technical detections.

Typical responsibilities:

* Create detection rules
* Develop queries
* Map detections to adversary behavior
* Test detection logic
* Tune false positives
* Improve detection coverage
* Validate telemetry
* Measure detection effectiveness

Example:

```text id="h0c5qy"
Threat Behavior
      ↓
MITRE Technique
      ↓
Telemetry
      ↓
Detection Logic
      ↓
Alert
      ↓
Testing
      ↓
Tuning
```

---

# 9. Threat Hunter

Threat hunters proactively search for malicious activity.

Unlike traditional alert-driven monitoring:

```text id="w0x2q4"
SOC Monitoring
    ↓
Alert
    ↓
Investigation
```

Threat hunting often starts with:

```text id="q0x5cv"
Hypothesis
    ↓
Query
    ↓
Search
    ↓
Analysis
    ↓
Finding
```

Example hypothesis:

> "An attacker may be using PowerShell to establish persistence."

The hunter then searches telemetry for evidence.

---

# 10. Incident Responder

Incident responders focus on handling confirmed security incidents.

Responsibilities may include:

* Containment
* Eradication
* Recovery
* Evidence preservation
* Incident coordination
* Root-cause analysis
* Post-incident review

Example:

```text id="m5t9x2"
SOC Alert
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

Threat intelligence analysts provide context about threats.

They may research:

* Threat actors
* Malware
* Campaigns
* IOCs
* TTPs
* Vulnerabilities
* Infrastructure

Their intelligence can improve:

```text id="1qk0s8"
Detection
+
Threat Hunting
+
Investigation
+
Incident Response
```

---

# 12. PROCESS

Processes define **how the SOC operates**.

Without processes, analysts may respond differently to identical situations.

A good SOC process should be:

* Documented
* Repeatable
* Measurable
* Consistent
* Risk-based
* Continuously improved

---

# 13. Core SOC Processes

Important processes include:

```text id="2xj8sc"
Monitoring
Detection
Alert Triage
Investigation
Incident Response
Threat Hunting
Threat Intelligence
Detection Engineering
Escalation
Reporting
Lessons Learned
```

---

# 14. Alert Triage Process

A standard triage process may look like:

```text id="4x3q5s"
Receive Alert
      ↓
Validate Alert
      ↓
Identify Asset
      ↓
Identify User
      ↓
Analyze Event
      ↓
Check Related Events
      ↓
Analyze IOCs
      ↓
Determine Severity
      ↓
False Positive?
    /     \
  Yes      No
   ↓        ↓
Close    Escalate
```

Detailed triage procedures will be documented separately.

---

# 15. Escalation Process

Not every alert can be resolved by L1.

Example:

```text id="7z6x3b"
L1
 ↓
Initial Triage
 ↓
Insufficient Evidence / High Severity
 ↓
L2
 ↓
Deep Investigation
 ↓
Complex Incident
 ↓
L3 / Incident Response
```

Escalation criteria may include:

* High severity
* Privileged account
* Critical asset
* Confirmed compromise
* Lateral movement
* Malware
* Data exfiltration
* Multiple affected systems
* Insufficient L1 visibility

---

# 16. Incident Response Process

A typical incident-response lifecycle:

```text id="1v2x9k"
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

A SOC must know when monitoring ends and formal incident response begins.

---

# 17. Change Management

Security detections and SOC infrastructure require controlled changes.

Examples:

* New detection rule
* SIEM parser modification
* Log-source change
* New data source
* Alert-threshold change
* Playbook modification

A basic process:

```text id="8x0b5n"
Change Request
      ↓
Review
      ↓
Testing
      ↓
Approval
      ↓
Deployment
      ↓
Validation
      ↓
Documentation
```

This reduces accidental disruption.

---

# 18. Documentation Process

Every significant investigation should leave an audit trail.

Documentation may contain:

* Alert ID
* Timestamp
* Analyst
* Affected asset
* User
* Source IP
* Destination IP
* Process
* IOC
* Investigation steps
* Evidence
* Severity
* Conclusion
* Response
* Escalation
* Lessons learned

A strong rule is:

> **If it wasn't documented, it is difficult to prove what happened.**

---

# 19. TECHNOLOGY

Technology provides the SOC with visibility and operational capability.

A modern SOC may use:

```text id="n8h2m5"
SIEM
EDR/XDR
IDS/IPS
NDR
SOAR
TIP
Firewall
Email Security
Vulnerability Management
Case Management
Cloud Security
```

---

# 20. SIEM

A SIEM provides centralized collection and analysis of security data.

Core functions:

* Log collection
* Parsing
* Normalization
* Searching
* Correlation
* Detection
* Alerting
* Dashboards
* Investigation

Examples:

* Wazuh
* Splunk
* Microsoft Sentinel
* Elastic Security
* IBM QRadar

My initial practical SIEM focus:

> **Wazuh**

---

# 21. EDR / XDR

## EDR

Endpoint Detection and Response focuses on endpoint activity.

It can provide visibility into:

* Processes
* Files
* Network connections
* Persistence
* Authentication
* Endpoint threats

## XDR

Extended Detection and Response expands detection across multiple security domains.

Conceptually:

```text id="8u4d1q"
Endpoint
   +
Network
   +
Identity
   +
Email
   +
Cloud
   ↓
Cross-Domain Detection
```

---

# 22. IDS / IPS

## IDS

Intrusion Detection System:

> Detects suspicious network activity.

## IPS

Intrusion Prevention System:

> Detects and may actively block suspicious activity.

Example:

```text id="j5k2q8"
Network Traffic
      ↓
IDS
      ↓
Suspicious?
   /      \
 No       Yes
           ↓
         Alert
```

An IPS may additionally take preventive action.

---

# 23. SOAR

Security Orchestration, Automation and Response helps automate repetitive security workflows.

Example:

```text id="b9q1v3"
Alert
 ↓
SOAR
 ↓
Extract IOC
 ↓
Threat Intelligence Lookup
 ↓
Enrich Alert
 ↓
Create Ticket
 ↓
Notify Analyst
```

Automation should be carefully controlled because incorrect automation can amplify mistakes.

---

# 24. Threat Intelligence Platform

A TIP helps organize and operationalize threat intelligence.

Potential data:

* IPs
* Domains
* URLs
* Hashes
* Threat actors
* Campaigns
* TTPs

Threat intelligence can feed:

```text id="c2d7x4"
SIEM
EDR
Threat Hunting
Detection Engineering
Incident Response
```

---

# 25. Case Management

SOC investigations need structured case tracking.

A case may contain:

```text id="s0w5f4"
Case ID
Alert
Severity
Affected Assets
Analyst
Timeline
Evidence
IOC
Actions
Escalation
Resolution
Lessons Learned
```

This provides accountability and historical context.

---

# 26. Technology Without Process

A SOC can fail even with expensive security tools.

Example:

```text id="f7w3m1"
Excellent SIEM
       +
Poor Detection Rules
       +
Poor Triage Process
       +
No Escalation Procedure
```

Result:

> **Large amounts of security data but poor security outcomes.**

---

# 27. Process Without Technology

The opposite problem also exists.

```text id="h3x9s2"
Excellent Analysts
       +
Good Procedures
       +
Insufficient Telemetry
```

Analysts cannot investigate activity they cannot observe.

Therefore:

> **Visibility is a prerequisite for effective detection and investigation.**

---

# 28. Technology + Process Without People

Automation can improve efficiency, but security decisions still require appropriate expertise.

```text id="w1q5c8"
Tools
  +
Processes
  +
No Skilled Analysts
```

may result in:

* Poor investigation
* Incorrect classification
* Missed threats
* Excessive false positives
* Incorrect response

---

# 29. The Complete SOC System

A mature SOC connects all three pillars.

```text id="c4v8k0"
                    PEOPLE
                      │
        ┌─────────────┼─────────────┐
        │             │             │
      L1/L2          L3       Threat Hunters
        │             │             │
        └─────────────┼─────────────┘
                      ↓
                   PROCESS
                      │
       ┌──────────────┼──────────────┐
       │              │              │
     Triage      Investigation   Response
       │              │              │
       └──────────────┼──────────────┘
                      ↓
                  TECHNOLOGY
                      │
       ┌──────────────┼──────────────┐
       │              │              │
      SIEM           EDR           SOAR
       │              │              │
       └──────────────┼──────────────┘
                      ↓
              SECURITY OPERATIONS
                      ↓
                 RISK REDUCTION
```

---

# 30. SOC Continuous Improvement

A SOC should not remain static.

After every significant incident, the team should ask:

* What happened?
* Why wasn't it detected earlier?
* Was the telemetry sufficient?
* Was the detection effective?
* Was the alert too noisy?
* Did the analyst have enough context?
* Was escalation timely?
* Did the response work?
* What should change?

This creates a feedback loop:

```text id="v4h8x2"
Incident
   ↓
Investigation
   ↓
Lessons Learned
   ↓
Detection Improvement
   ↓
Process Improvement
   ↓
Training
   ↓
Better Detection
```

---

# 31. People–Process–Technology Example

Consider a phishing incident.

## People

L1 analyst:

* Receives alert
* Performs triage

L2 analyst:

* Investigates email and account activity

Incident responder:

* Contains compromised account

---

## Process

```text id="2p7m1c"
Phishing Alert
      ↓
Triage
      ↓
Investigation
      ↓
Account Compromise?
      ↓
Containment
      ↓
Recovery
      ↓
Lessons Learned
```

---

## Technology

Potential technologies:

```text id="n6v2q5"
Email Security
     ↓
SIEM
     ↓
EDR
     ↓
Threat Intelligence
     ↓
SOAR
```

Together:

```text id="r2f6v8"
People
 +
Process
 +
Technology
 ↓
Phishing Incident Response
```

---

# 32. AI and the Three Pillars

AI can augment all three pillars.

## People

AI can assist analysts with:

* Summarization
* Investigation assistance
* Knowledge retrieval
* Report drafting

## Process

AI can assist with:

* Workflow automation
* Case summarization
* Playbook generation
* Prioritization assistance

## Technology

AI can support:

* Anomaly detection
* Alert enrichment
* Threat classification
* Detection development

But:

```text id="f8k2p0"
AI
 ↓
Recommendation
 ↓
Human Validation
 ↓
Security Decision
```

AI should not be treated as an unquestioned authority.

---

# 33. Practical Exercise

## Scenario

Your organization deploys a SIEM.

It receives:

```text
20,000 alerts/day
```

However:

* Only two analysts are available
* There is no documented triage process
* No severity model exists
* No escalation criteria exist
* Detection rules have not been tuned

### Questions

1. Which SOC pillar is weak?
2. Is buying another SIEM the correct first solution?
3. What process improvements are required?
4. What people-related improvements are required?
5. How could automation help?
6. What metrics should management monitor?

### Expected Thinking

The problem is not simply:

> "We need a better SIEM."

It may be:

> **People + Process + Technology are not aligned.**

---

# 34. Key Takeaways

### People

> **People make security decisions.**

### Process

> **Processes make security operations consistent.**

### Technology

> **Technology provides visibility and operational capability.**

Together:

```text id="t5v1x9"
People
+
Process
+
Technology
↓
Effective SOC
```

None of the three pillars should be considered independently.

---

# 📚 Related Documents

Previous:

```text
01-What-is-SOC.md
```

Next:

```text
03-SOC-Roles-and-Responsibilities.md
```

Later:

```text
04-SOC-Tiers-L1-L2-L3.md
05-SOC-Workflow.md
06-Security-Telemetry.md
```

---

# ⭐ Core Principle

> **A SOC is strongest when skilled people follow well-defined processes using the right technology to make evidence-based security decisions.**
