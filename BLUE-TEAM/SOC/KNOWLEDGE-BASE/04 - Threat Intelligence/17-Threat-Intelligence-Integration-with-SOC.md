# 17 - Threat Intelligence Integration with SOC

## 1. Introduction

Threat Intelligence (TI) becomes significantly more valuable when it is integrated directly into Security Operations Center (SOC) workflows.

A SOC continuously collects security telemetry, generates alerts, investigates suspicious activity, and responds to incidents.

Threat Intelligence adds external and internal context that helps analysts understand:

- What an indicator represents
- Whether an indicator is malicious
- Who may be behind an attack
- Which malware or campaign is involved
- Which TTPs are being used
- How serious the activity may be
- What actions should be taken

Basic model:

Threat Intelligence
        ↓
   Enrichment
        ↓
       SIEM
        ↓
      Alert
        ↓
   SOC Analyst
        ↓
 Investigation
        ↓
 Response


---

## 2. Objectives

The main objectives of CTI-SOC integration are:

1. Improve alert enrichment.
2. Improve detection accuracy.
3. Reduce investigation time.
4. Prioritize threats.
5. Support threat hunting.
6. Improve incident response.
7. Identify related indicators.
8. Improve detection engineering.
9. Automate repetitive enrichment.
10. Create a continuous intelligence feedback loop.


---

## 3. Why SOC Needs Threat Intelligence

A raw alert may contain limited information.

Example:

    Source IP:
    185.x.x.x

    Destination:
    Internal Server

    Port:
    443

    Event:
    Suspicious connection


Without intelligence:

    "Suspicious IP detected."

With intelligence:

    "The IP is associated with previously
    reported malicious infrastructure and
    appears in multiple threat intelligence
    sources."


The second result provides much more investigation context.


---

## 4. CTI-SOC Integration Model

A basic architecture:

                    Threat Sources
                         ↓
                  Threat Intelligence
                         ↓
                 IOC Processing
                         ↓
                    Enrichment
                         ↓
              +----------+----------+
              ↓                     ↓
             SIEM                  TIP
              ↓                     ↓
            Alerts              Intelligence
              ↓                     ↓
              +----------+----------+
                         ↓
                    SOC Analyst
                         ↓
                Investigation
                         ↓
                Incident Response
                         ↓
                     Feedback
                         ↓
                Threat Intelligence


---

## 5. SOC Data Sources

CTI can be correlated with:

- Firewall logs
- DNS logs
- Proxy logs
- VPN logs
- Windows Event Logs
- Sysmon
- Linux logs
- EDR
- IDS/IPS
- Email security
- Cloud logs
- Authentication logs
- Application logs
- Network traffic


---

## 6. Threat Intelligence Data Types

SOC integration commonly uses:

### Indicators

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses

### Behavioral Intelligence

- TTPs
- Attack patterns
- Malware behavior
- Command execution

### Context

- Threat actor
- Campaign
- Malware family
- Vulnerability
- Confidence
- Source


---

## 7. Indicator Enrichment

Enrichment adds additional information to an indicator.

Example:

    Input:
    203.x.x.x

    Enrichment:
    Reputation
    ASN
    Country
    Hosting Provider
    Threat Actor
    Malware
    Campaign
    First Seen
    Last Seen
    Confidence


Enrichment helps analysts make better decisions.


---

## 8. IOC Lifecycle

The SOC should manage indicators through a lifecycle:

    Collect
      ↓
    Validate
      ↓
    Enrich
      ↓
    Prioritize
      ↓
    Search
      ↓
    Detect
      ↓
    Investigate
      ↓
    Respond
      ↓
    Review
      ↓
    Expire / Retire


---

## 9. IOC Validation

Not every indicator should automatically be trusted.

Validation should consider:

- Source reliability
- Confidence
- Age
- Context
- Reputation
- Internal observations
- Multiple-source confirmation


---

## 10. IOC Confidence

A simple classification:

    Low
    Medium
    High
    Critical


Example:

### Low

Single unverified source.

### Medium

Multiple supporting signals.

### High

Multiple reliable sources and technical evidence.

### Critical

Strong evidence of active compromise.


---

## 11. SIEM Integration

A SIEM can correlate CTI with security logs.

Example:

    Threat Intelligence
           ↓
      Malicious IP
           ↓
          SIEM
           ↓
      Firewall Logs
           ↓
      IOC Match
           ↓
          Alert
           ↓
      SOC Analyst


---

## 12. Wazuh Integration

Wazuh can be used in a home lab to demonstrate CTI-driven SOC monitoring.

Example architecture:

    Kali Linux
         ↓
    Threat Simulation
         ↓
    Windows VM
         ↓
       Sysmon
         ↓
       Wazuh
         ↓
    CTI Enrichment
         ↓
       Alert
         ↓
    Investigation


---

## 13. SIEM Correlation

Example:

    Event 1:
    DNS request to suspicious domain

    Event 2:
    Endpoint connection to same domain

    Event 3:
    PowerShell execution

    Event 4:
    Known malicious hash detected


Together these events may provide stronger evidence than any single event.


---

## 14. Threat Intelligence Matching

Basic matching workflow:

    Event
      ↓
    Extract Indicator
      ↓
    Normalize
      ↓
    Compare with CTI
      ↓
    Match?
      ↓
    Yes → Enrich → Alert
      ↓
    No → Continue Monitoring


---

## 15. Types of IOC Matching

SOC systems may match:

- Exact IP
- Domain
- URL
- Hash
- Email
- Certificate
- User-Agent
- File path
- Registry value


---

## 16. Exact Matching

Example:

    Event IP:
    192.0.2.50

    CTI IP:
    192.0.2.50

    Result:
    MATCH


Exact matching is simple but can generate false positives if indicators are outdated.


---

## 17. Contextual Matching

Instead of checking only the indicator, analysts consider:

- Indicator
- Time
- User
- Host
- Process
- Network behavior
- Threat intelligence confidence


Example:

    Known malicious domain
          +
    PowerShell execution
          +
    Suspicious process
          +
    Recent user login


This provides stronger evidence.


---

## 18. Threat Intelligence Alert Enrichment

A CTI-enriched alert may contain:

    Alert ID
    Timestamp
    Host
    User
    Source IP
    Destination
    IOC
    IOC Type
    Threat Actor
    Malware
    Campaign
    TTP
    Confidence
    Recommended Action


This reduces the analyst's need to perform manual lookups.


---

## 19. SOC Analyst Workflow

A typical workflow:

    Alert Received
         ↓
    Review Context
         ↓
    Check CTI
         ↓
    Validate Indicator
         ↓
    Investigate Endpoint
         ↓
    Search Related Events
         ↓
    Determine Severity
         ↓
    Escalate / Contain
         ↓
    Document
         ↓
    Feedback to CTI


---

## 20. L1 SOC Workflow

For an L1 analyst:

### Step 1

Receive alert.

### Step 2

Identify indicator.

### Step 3

Check threat intelligence.

### Step 4

Review event context.

### Step 5

Determine whether the alert is likely benign or suspicious.

### Step 6

Follow escalation procedure.

### Step 7

Document findings.


---

## 21. L2 SOC Workflow

L2 analysts may:

- Perform deeper correlation
- Search historical logs
- Analyze TTPs
- Investigate endpoint behavior
- Identify related indicators
- Conduct threat hunting
- Recommend containment


---

## 22. L3 SOC Workflow

L3 analysts may:

- Develop detections
- Perform advanced threat hunting
- Conduct malware analysis
- Develop intelligence assessments
- Investigate complex campaigns
- Improve security architecture


---

## 23. CTI and Alert Prioritization

Threat intelligence can help prioritize alerts.

Example:

    Alert A
    Known malicious IP
    High confidence
    Critical asset
    → Critical

    Alert B
    Unknown IP
    Low confidence
    Non-critical system
    → Low


Threat intelligence should be combined with asset and business context.


---

## 24. Risk-Based Alert Prioritization

A simplified model:

    Risk =
    Threat Severity
    × Asset Criticality
    × Confidence
    × Exposure


Example:

    High Threat
        ×
    Critical Asset
        ×
    High Confidence

    = High Priority


---

## 25. Threat Intelligence and Threat Hunting

CTI can generate hunting hypotheses.

Example:

CTI reports:

    Threat actor uses:
    PowerShell
    Scheduled Tasks
    Credential Dumping


Threat Hunter creates hypothesis:

    "The threat actor may be using
    PowerShell and scheduled tasks
    on internal Windows endpoints."


Then searches telemetry.


---

## 26. CTI-Driven Threat Hunting

Workflow:

    CTI Report
       ↓
    Extract TTP
       ↓
    Create Hypothesis
       ↓
    Identify Telemetry
       ↓
    Search SIEM
       ↓
    Analyze Results
       ↓
    Validate
       ↓
    Update Detection
       ↓
    Update CTI


---

## 27. MITRE ATT&CK Integration

CTI can be mapped to MITRE ATT&CK.

Example:

    Threat Actor
         ↓
    T1059.001
    PowerShell
         ↓
    Detection
         ↓
    Windows Event Logs
         ↓
    SIEM Rule


This connects intelligence with technical detection.


---

## 28. TTP-Based Detection

Instead of relying only on IOCs, detect attacker behavior.

Example:

IOC:

    Malicious IP

TTP:

    PowerShell
    encoded command
    suspicious parent process


TTP-based detection is generally more resilient to changing infrastructure.


---

## 29. IOC Expiration

Indicators have lifetimes.

Example:

    Malicious IP
    First Seen:
    January

    Last Seen:
    February

    Current Status:
    Inactive


Old indicators should be reviewed and expired according to defined policy.


---

## 30. Indicator Aging

Track:

- First seen
- Last seen
- Confidence
- Source
- Current activity
- Expiration date


This prevents outdated intelligence from continuously generating alerts.


---

## 31. False Positives

CTI can generate false positives.

Causes include:

- Shared hosting
- CDN infrastructure
- Compromised websites
- Dynamic IPs
- Expired indicators
- Poor-quality feeds


Therefore:

**IOC Match ≠ Confirmed Compromise**


---

## 32. False Positive Investigation

When an IOC matches:

1. Validate source.
2. Check confidence.
3. Check indicator age.
4. Review endpoint context.
5. Review network behavior.
6. Search historical activity.
7. Determine maliciousness.
8. Document the result.


---

## 33. Threat Intelligence and Incident Response

During an incident:

    Detection
       ↓
    CTI Enrichment
       ↓
    Threat Actor Identification
       ↓
    Related IOC Discovery
       ↓
    Scope Investigation
       ↓
    Containment
       ↓
    Eradication
       ↓
    Recovery
       ↓
    Lessons Learned
       ↓
    CTI Update


---

## 34. Scope Expansion

If one malicious IOC is discovered, search for related:

- IPs
- Domains
- URLs
- Hashes
- User accounts
- Hosts
- TTPs
- Malware
- Infrastructure


This helps determine the full scope of an incident.


---

## 35. CTI Feedback Loop

SOC findings should feed back into CTI.

Example:

    SOC detects malware
          ↓
    Extract IOC
          ↓
    Research IOC
          ↓
    Identify Campaign
          ↓
    Identify TTP
          ↓
    Update CTI
          ↓
    Update Detection
          ↓
    Search Environment


This creates a closed-loop intelligence capability.


---

## 36. CTI and Detection Engineering

Threat intelligence can help detection engineers identify:

- New IOCs
- New TTPs
- New malware
- New attack patterns
- New vulnerabilities


Workflow:

    Intelligence
        ↓
    Detection Hypothesis
        ↓
    Detection Rule
        ↓
    Testing
        ↓
    Deployment
        ↓
    Monitoring
        ↓
    Tuning


---

## 37. Detection Rule Example

Example conceptual rule:

    IF
        Process = powershell.exe
        AND
        CommandLine contains suspicious encoded content
        AND
        Destination matches known malicious infrastructure

    THEN

        Generate High Severity Alert


The exact implementation depends on the SIEM and telemetry available.


---

## 38. CTI and EDR

EDR can provide:

- Process activity
- Network connections
- File activity
- Registry changes
- User activity
- Persistence behavior


CTI enriches this information with external threat context.


---

## 39. CTI and Network Security

CTI can be integrated with:

- Firewalls
- IDS
- IPS
- DNS security
- Proxies
- Network detection tools


Example:

    Known malicious domain
            ↓
          DNS
            ↓
        IOC Match
            ↓
          Alert
            ↓
           SOC


---

## 40. CTI and Email Security

Threat intelligence can help analyze:

- Sender addresses
- Domains
- URLs
- Attachments
- File hashes
- IP addresses


Example:

    Phishing Email
          ↓
    Extract URL
          ↓
    CTI Reputation
          ↓
    Malicious
          ↓
    Alert / Block


---

## 41. CTI and Vulnerability Management

SOC and vulnerability teams can use CTI together.

Example:

    CVE
     ↓
    Active Exploitation
     ↓
    Threat Actor Usage
     ↓
    Internal Asset Exposure
     ↓
    High Priority Patch


This is more useful than prioritizing vulnerabilities only by CVSS score.


---

## 42. CTI and Cloud Security

Cloud CTI integration can monitor:

- Malicious IPs
- Suspicious domains
- Cloud abuse
- Credential attacks
- API abuse
- Compromised infrastructure


Cloud logs can be correlated with threat intelligence in the SIEM.


---

## 43. CTI and Identity Security

Threat intelligence can help investigate:

- Credential attacks
- Brute-force sources
- Impossible travel
- Suspicious authentication infrastructure
- Compromised accounts


Example:

    Login Attempt
        ↓
    Source IP
        ↓
    CTI Check
        ↓
    Known Malicious
        ↓
    Authentication Alert


---

## 44. SOAR Integration

SOAR can automate CTI enrichment.

Example:

    Alert
      ↓
    Extract IOC
      ↓
    Threat Intelligence Lookup
      ↓
    Reputation Check
      ↓
    Add Context
      ↓
    Update Ticket
      ↓
    Notify Analyst


---

## 45. Automated Response

Possible automated actions:

- Block malicious IP
- Block domain
- Disable account
- Isolate endpoint
- Create ticket
- Notify analyst


High-impact actions should follow organizational authorization and validation procedures.


---

## 46. Human-in-the-Loop

A safer model:

    Automated Detection
          ↓
    Automated Enrichment
          ↓
    Risk Assessment
          ↓
    Human Review
          ↓
    Authorized Response


Automation should not eliminate appropriate human oversight.


---

## 47. CTI Data Quality

Good integration depends on good data.

Important attributes:

- Indicator type
- Value
- Source
- Confidence
- First seen
- Last seen
- Expiration
- Context
- Related threat
- TTP


---

## 48. Data Normalization

Different sources may use different formats.

Example:

    Source A:
    malicious-domain.com

    Source B:
    Domain = malicious-domain.com

    Source C:
    indicator_type = domain
    value = malicious-domain.com


Normalize these records before correlation.


---

## 49. Deduplication

Multiple feeds may contain the same indicator.

Without deduplication:

    Feed A → IOC
    Feed B → Same IOC
    Feed C → Same IOC

This can create unnecessary processing and duplicate alerts.


---

## 50. Threat Intelligence Prioritization

Prioritize intelligence using:

- Confidence
- Relevance
- Severity
- Recency
- Asset criticality
- Threat actor relevance
- Internal evidence


Example:

    High Confidence
    +
    Active Threat
    +
    Critical Asset
    =
    Highest Priority


---

## 51. CTI Alert Enrichment Example

### Raw Alert

    Source IP:
    203.x.x.x

    Destination:
    Internal Web Server

    Port:
    443


### Enriched Alert

    IOC:
    203.x.x.x

    Type:
    IPv4

    Reputation:
    Malicious

    Confidence:
    High

    Associated Activity:
    Scanning

    Related Campaign:
    Known Campaign

    Recommended Action:
    Investigate source and review
    historical connections.


---

## 52. Investigation Questions

When a CTI match occurs, ask:

1. Is the indicator trustworthy?
2. Is it still active?
3. What source reported it?
4. What is the confidence?
5. Which internal system interacted with it?
6. Which user was involved?
7. What process generated the connection?
8. What happened before and after?
9. Are related indicators present?
10. Does the activity indicate compromise?


---

## 53. Evidence Collection

During investigation collect:

- Timestamp
- Hostname
- Username
- Source IP
- Destination IP
- Domain
- URL
- Hash
- Process
- Command line
- Network connection
- Relevant logs


Maintain evidence according to organizational incident-response procedures.


---

## 54. CTI Case Management

A CTI/SOC case may contain:

    Case ID
    Alert ID
    Indicator
    Source
    Confidence
    Threat Actor
    Campaign
    TTP
    Evidence
    Analyst Notes
    Actions
    Final Verdict


---

## 55. Verdict Classification

Example:

    True Positive
    False Positive
    Benign
    Suspicious
    Inconclusive


The organization should define consistent criteria for each verdict.


---

## 56. CTI Metrics for SOC

Important metrics:

- IOC match rate
- Alert enrichment rate
- CTI-driven alert count
- CTI-driven incidents
- CTI-driven hunts
- False positive rate
- MTTD
- MTTR
- Investigation time
- Analyst time saved


---

## 57. Measuring CTI-SOC Value

A useful model:

    CTI
     ↓
    Better Context
     ↓
    Faster Investigation
     ↓
    Better Detection
     ↓
    Faster Response
     ↓
    Reduced Risk


The objective is measurable security improvement.


---

## 58. Home Lab Project

# Project: CTI-Integrated SOC Monitoring Lab

## Objective

Build a practical SOC environment where threat intelligence is used to enrich and investigate security events.


---

## 59. Lab Environment

Use:

- Windows 11 Host
- Kali Linux VM
- Second Kali VM
- Windows 7 VM
- Metasploitable 2
- Wazuh
- Sysmon
- Wireshark
- Nmap
- Python
- GitHub


---

## 60. Lab Architecture

    Kali Attacker
         ↓
    Controlled Activity
         ↓
    Windows Victim
         ↓
       Sysmon
         ↓
       Wazuh
         ↓
    CTI Enrichment
         ↓
       SIEM Alert
         ↓
    SOC Investigation
         ↓
      Response
         ↓
     Documentation


---

## 61. Lab Task 1 — Install Telemetry

Configure:

- Wazuh
- Sysmon
- Windows logging
- Network visibility


Verify that events are being collected.


---

## 62. Lab Task 2 — Generate Controlled Activity

Use authorized lab systems to generate activity such as:

- Port scanning
- Authentication failures
- Suspicious PowerShell activity
- File creation
- Network connections


Do not perform testing against systems you do not own or have authorization to test.


---

## 63. Lab Task 3 — Extract Indicators

From the generated events identify:

- Source IP
- Destination IP
- Domain
- URL
- Hash
- Username
- Hostname


---

## 64. Lab Task 4 — Enrich Indicators

For each indicator record:

    Indicator
    Type
    Source
    Reputation
    Confidence
    First Seen
    Last Seen
    Context
    Analyst Verdict


---

## 65. Lab Task 5 — Correlate with Wazuh

Search Wazuh for the relevant indicators.

Example:

    IOC
     ↓
    Wazuh Search
     ↓
    Historical Events
     ↓
    Related Host
     ↓
    Related User
     ↓
    Related Process


---

## 66. Lab Task 6 — Investigate

Determine:

- What happened?
- Which system was affected?
- Which user was involved?
- What process was executed?
- Was network communication established?
- Does the activity indicate compromise?


---

## 67. Lab Task 7 — Create Detection

Create a detection based on the intelligence.

Example:

    Known malicious domain
           +
    DNS request
           +
    Endpoint activity
           ↓
        Alert


Test the rule using controlled lab activity.


---

## 68. Lab Task 8 — Map to MITRE ATT&CK

Document:

    Technique
    ↓
    Evidence
    ↓
    Detection
    ↓
    Intelligence
    ↓
    Response


This demonstrates the connection between CTI and SOC detection.


---

## 69. Lab Task 9 — Document the Incident

Create an incident report containing:

- Summary
- Timeline
- Indicators
- Evidence
- Threat intelligence
- TTPs
- Impact
- Detection
- Response
- Lessons learned


---

## 70. Lab Task 10 — Create Feedback

After the investigation:

    New IOC
       ↓
    Intelligence Record
       ↓
    Detection Update
       ↓
    Threat Hunt
       ↓
    SOC Knowledge Base


This demonstrates the CTI feedback loop.


---

## 71. Portfolio Evidence

Include:

- Architecture diagram
- Wazuh screenshots
- Sysmon events
- CTI enrichment results
- IOC table
- Detection rule
- MITRE ATT&CK mapping
- Investigation report
- KPI dashboard
- Lessons learned


---

## 72. Recommended Repository Structure

    17-Threat-Intelligence-Integration-with-SOC/
    │
    ├── README.md
    │
    ├── architecture/
    │   └── cti-soc-architecture.md
    │
    ├── enrichment/
    │   └── indicator-enrichment.md
    │
    ├── detection/
    │   ├── ioc-detection.md
    │   └── ttp-detection.md
    │
    ├── hunting/
    │   └── cti-driven-hunting.md
    │
    ├── incident-response/
    │   └── cti-incident-workflow.md
    │
    ├── automation/
    │   └── soar-enrichment.md
    │
    ├── metrics/
    │   └── soc-cti-metrics.md
    │
    ├── evidence/
    │   └── screenshots/
    │
    └── lessons-learned.md


---

## 73. Interview Question

### How does threat intelligence help a SOC?

Threat intelligence gives the SOC additional context about indicators, threat actors, malware, campaigns, and attacker behavior.

It helps analysts:

- Prioritize alerts
- Enrich investigations
- Detect known threats
- Build hunting hypotheses
- Improve detections
- Respond faster


---

## 74. Interview Question

### Does an IOC match mean the organization is compromised?

No.

An IOC match is an indicator that requires investigation.

The analyst should validate:

- Indicator confidence
- Indicator age
- Source reliability
- Internal context
- Endpoint activity
- Network behavior
- Related events


---

## 75. Interview Question

### Why are TTPs important when IOCs change?

Attack infrastructure can change quickly.

IP addresses, domains, and hashes can change.

Attacker behavior and techniques may remain more consistent.

Therefore:

**IOC-based detection + TTP-based detection**

provides stronger defensive coverage.


---

## 76. Interview Question

### How would you integrate CTI with a SIEM?

I would:

1. Collect relevant intelligence.
2. Validate and normalize indicators.
3. Store them in an appropriate intelligence system.
4. Integrate the intelligence with the SIEM.
5. Correlate indicators with security telemetry.
6. Enrich alerts.
7. Prioritize relevant matches.
8. Investigate and respond.
9. Feed confirmed findings back into CTI.


---

## 77. Learning Outcome

After completing this topic, you should be able to:

- Explain CTI-SOC integration.
- Enrich SOC alerts.
- Understand IOC matching.
- Investigate CTI-driven alerts.
- Use CTI for threat hunting.
- Map intelligence to MITRE ATT&CK.
- Integrate CTI with SIEM concepts.
- Explain SOAR-based enrichment.
- Build a CTI feedback loop.
- Measure CTI operational value.


---

## 78. Professional Skill Mapping

This topic demonstrates:

### Blue Team

- Security monitoring
- Alert investigation
- Threat detection
- Incident response

### CTI

- IOC analysis
- Threat actor analysis
- TTP analysis
- Intelligence enrichment

### SOC

- L1 alert triage
- L2 investigation concepts
- Threat hunting

### Automation

- Enrichment
- Correlation
- SOAR workflows

### AI Security

- AI-assisted intelligence analysis
- Human validation
- AI governance


---

## 79. Complete CTI-SOC Workflow

The complete workflow is:

    Threat Intelligence
          ↓
       Collection
          ↓
       Validation
          ↓
       Enrichment
          ↓
       Prioritization
          ↓
       SIEM / TIP
          ↓
     Security Telemetry
          ↓
        Correlation
          ↓
          Alert
          ↓
      SOC Investigation
          ↓
      Threat Hunting
          ↓
    Incident Response
          ↓
      New Intelligence
          ↓
    Detection Improvement
          ↓
      Program Metrics
          ↓
     Continuous Improvement


---

## 80. Final Principle

Threat intelligence should not remain inside reports or dashboards.

Its real value comes when intelligence is operationalized inside the SOC.

The strongest CTI-SOC model is:

**Intelligence → Context → Detection → Investigation → Response → Feedback**

A mature SOC does not simply ask:

**"Is this indicator malicious?"**

It asks:

**"What does this activity mean, how does it relate to the threat landscape, what is the risk to our environment, and what action should we take?"**

That is the foundation of effective CTI-driven Security Operations.
