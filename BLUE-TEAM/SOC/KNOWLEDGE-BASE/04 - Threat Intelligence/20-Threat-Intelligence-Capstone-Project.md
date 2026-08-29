# 20 - Threat Intelligence Capstone Project

## 1. Introduction

The Threat Intelligence Capstone Project combines the concepts learned throughout the Threat Intelligence directory into one practical SOC-focused project.

The objective is to demonstrate the complete Threat Intelligence lifecycle:

Threat Collection
        ↓
IOC Processing
        ↓
Validation
        ↓
Enrichment
        ↓
Analysis
        ↓
Threat Mapping
        ↓
Risk Assessment
        ↓
Operationalization
        ↓
Detection
        ↓
Investigation
        ↓
Response
        ↓
Reporting
        ↓
Metrics
        ↓
Continuous Improvement


---

## 2. Project Objective

Build a practical Threat Intelligence workflow that demonstrates how a SOC analyst can:

1. Collect threat intelligence.
2. Process indicators.
3. Validate intelligence.
4. Enrich indicators.
5. Analyze threats.
6. Map activity to MITRE ATT&CK.
7. Prioritize threats.
8. Integrate intelligence with SOC monitoring.
9. Investigate alerts.
10. Support incident response.
11. Automate repetitive tasks.
12. Measure intelligence effectiveness.
13. Produce a professional intelligence report.


---

## 3. Project Scenario

### Scenario

A fictional organization operates:

- Windows endpoints
- Linux servers
- Network infrastructure
- Web applications
- Cloud services
- Employee email systems

The SOC receives intelligence about a suspected malicious campaign.

The objective is to determine:

- What is the threat?
- Which indicators are associated with it?
- Which systems may be affected?
- Which techniques are being used?
- How relevant is the threat?
- What detections should be created?
- What response actions should be considered?


---

## 4. Project Architecture

    External Threat Intelligence
              ↓
        Collection Layer
              ↓
       Processing Layer
              ↓
       Validation Layer
              ↓
       Enrichment Layer
              ↓
        Analysis Layer
              ↓
        Risk Scoring
              ↓
    ┌─────────┴──────────┐
    ↓                    ↓
   SIEM                 TIP
    ↓                    ↓
Detection             Intelligence
    ↓                    ↓
Threat Hunting      Investigation
    └─────────┬──────────┘
              ↓
        SOC Analyst
              ↓
       Incident Response
              ↓
          Reporting
              ↓
           Metrics


---

## 5. Project Components

The capstone should contain:

- Intelligence collection
- IOC management
- Threat analysis
- IOC enrichment
- MITRE ATT&CK mapping
- Threat actor analysis
- Malware analysis
- Vulnerability intelligence
- Detection engineering
- Threat hunting
- Incident investigation
- Automation
- Reporting
- Metrics


---

## 6. Tools

Suggested lab tools:

### Operating Systems

- Kali Linux
- Windows 11
- Windows 7
- Ubuntu

### Security Monitoring

- Wazuh
- Sysmon
- Wireshark

### Threat Intelligence

- STIX/TAXII concepts
- Approved CTI APIs
- MITRE ATT&CK
- Public threat intelligence sources

### Automation

- Python
- JSON
- SQLite
- REST APIs

### Documentation

- Markdown
- GitHub


---

## 7. Lab Safety

Use only:

- Your own systems
- Authorized virtual machines
- Simulated indicators
- Publicly available intelligence
- Approved APIs

Do not perform unauthorized scanning, exploitation, credential attacks, or blocking actions against external systems.


---

## 8. Phase 1 — Intelligence Collection

Collect intelligence from approved sources.

Potential intelligence types:

- IP addresses
- Domains
- URLs
- File hashes
- Malware names
- Threat actors
- CVEs
- TTPs
- Campaign information


Workflow:

    Source
      ↓
    Collect
      ↓
    Record
      ↓
    Classify


---

## 9. Phase 2 — IOC Extraction

Extract:

- IPv4 addresses
- Domains
- URLs
- Hashes
- Email addresses

Example:

    Threat Report
        ↓
    IOC Extraction
        ↓
    IP
    Domain
    URL
    Hash


Each IOC should be stored in a structured format.


---

## 10. Phase 3 — IOC Validation

Validate every indicator.

Check:

- Syntax
- Indicator type
- Completeness
- Duplicate status
- Source
- Confidence


Example:

    IOC
     ↓
    Valid?
    /   \
   No    Yes
   ↓      ↓
 Reject  Enrich


---

## 11. Phase 4 — IOC Normalization

Create a standard schema.

Example:

    {
        "type": "ip",
        "value": "203.0.113.10",
        "source": "Lab Dataset",
        "confidence": "high",
        "first_seen": "2026-08-01",
        "last_seen": "2026-08-25"
    }


Use safe documentation/test indicators where appropriate.


---

## 12. Phase 5 — Deduplication

Identify repeated indicators.

Example:

    Feed A → IOC-001
    Feed B → IOC-001
    Feed C → IOC-001


Store:

    IOC-001
      ├── Source A
      ├── Source B
      └── Source C


This prevents unnecessary duplication.


---

## 13. Phase 6 — IOC Enrichment

Enrich indicators using approved sources.

Possible enrichment:

- Reputation
- ASN
- DNS
- WHOIS
- Malware associations
- Threat actor associations
- Historical observations
- Confidence


Workflow:

    IOC
     ↓
    Source 1
     ↓
    Source 2
     ↓
    Source 3
     ↓
    Internal Telemetry
     ↓
    Combined Context


---

## 14. Phase 7 — Threat Analysis

Analyze the collected intelligence.

Questions:

1. What threat is being described?
2. Who may be responsible?
3. What malware is involved?
4. What infrastructure is used?
5. What TTPs are involved?
6. What sectors are targeted?
7. How recent is the activity?
8. Is the threat relevant to the organization?


---

## 15. Phase 8 — Threat Actor Analysis

Document:

- Threat actor name
- Aliases
- Motivation
- Target sectors
- Geographic targeting
- Known malware
- Infrastructure
- TTPs
- Historical campaigns


Avoid treating attribution as certain when evidence is weak.


---

## 16. Phase 9 — Malware Analysis

Document relevant malware information:

- Malware family
- Capabilities
- Initial access
- Execution
- Persistence
- Command and control
- Discovery
- Exfiltration


Use public research and authorized malware-analysis environments.


---

## 17. Phase 10 — MITRE ATT&CK Mapping

Map observed behavior to ATT&CK techniques.

Example:

    PowerShell
       ↓
    Command and Scripting Interpreter
       ↓
    T1059.001


Another example:

    Scheduled Task
       ↓
    Scheduled Task/Job
       ↓
    Relevant ATT&CK Technique


Only map techniques supported by evidence.


---

## 18. Phase 11 — Threat Relevance Assessment

Determine whether the intelligence applies to the organization.

Consider:

- Industry
- Geography
- Technology
- Exposed services
- Existing vulnerabilities
- Threat actor targeting
- Internal telemetry


Example:

    Threat
      ↓
    Relevant Industry?
      ↓
    Relevant Technology?
      ↓
    Relevant Geography?
      ↓
    Internal Exposure?
      ↓
    Overall Relevance


---

## 19. Phase 12 — Risk Assessment

Evaluate:

- Likelihood
- Impact
- Confidence
- Asset criticality
- Threat recency
- Internal evidence


Example:

    Likelihood = High
    Impact = High
    Confidence = High

    Overall Risk = High


The scoring model should be documented clearly.


---

## 20. Phase 13 — Intelligence Prioritization

Classify intelligence:

### Critical

Immediate security action may be required.

### High

Requires prompt investigation.

### Medium

Requires monitoring or additional analysis.

### Low

Useful for background or future correlation.


Example:

    High Confidence
    + Recent Activity
    + Critical Asset
    + Internal Match

    → Critical Priority


---

## 21. Phase 14 — Intelligence Operationalization

Convert intelligence into security operations.

Possible actions:

- Create SIEM rules
- Update detection logic
- Add hunting queries
- Enrich alerts
- Update blocklists where authorized
- Patch vulnerable systems
- Create SOC tickets
- Update security controls


The objective is:

**Intelligence → Action**


---

## 22. Phase 15 — SIEM Integration

Integrate relevant intelligence with Wazuh.

Example:

    IOC
     ↓
    Intelligence Database
     ↓
    Wazuh
     ↓
    Event Match
     ↓
    Alert
     ↓
    SOC Investigation


The implementation can be simulated if full production integration is unavailable.


---

## 23. Phase 16 — Detection Engineering

Develop detection logic based on:

- IOC
- TTP
- Malware behavior
- Network behavior
- Endpoint activity


Example:

    Threat Intelligence
          ↓
       TTP
          ↓
    Detection Logic
          ↓
        SIEM
          ↓
        Alert


Detection rules should be tested before deployment.


---

## 24. Phase 17 — Threat Hunting

Create a hunting hypothesis.

Example:

> If the threat actor is targeting our environment, suspicious PowerShell execution combined with unusual outbound network communication may be observable on endpoints.

Then:

    Hypothesis
       ↓
    Data Sources
       ↓
    Search
       ↓
    Findings
       ↓
    Conclusion


---

## 25. Phase 18 — Internal Telemetry Correlation

Search:

- Windows logs
- Sysmon
- Linux logs
- Firewall logs
- DNS logs
- Proxy logs
- Authentication logs
- Wazuh alerts


Example:

    External IOC
        ↓
    SIEM Search
        ↓
    Historical Events
        ↓
    Related Endpoint
        ↓
    Investigation


---

## 26. Phase 19 — Alert Investigation

For each relevant alert:

1. Identify the affected asset.
2. Identify the user.
3. Identify the IOC.
4. Determine first observed activity.
5. Review related events.
6. Search for additional IOCs.
7. Map behavior to TTPs.
8. Determine severity.
9. Escalate if required.
10. Document findings.


---

## 27. Phase 20 — Incident Response Support

If malicious activity is confirmed:

    Detection
       ↓
    Investigation
       ↓
    Confirmation
       ↓
    Containment
       ↓
    Eradication
       ↓
    Recovery
       ↓
    Lessons Learned


CTI should support each relevant phase.


---

## 28. Phase 21 — IOC Expansion

When one malicious IOC is discovered, search for related indicators.

Example:

    Malicious Domain
          ↓
    Related IP
          ↓
    Related URL
          ↓
    Related Hash
          ↓
    Related Malware
          ↓
    Related TTP


This expands the investigation scope.


---

## 29. Phase 22 — Attack Infrastructure Analysis

Analyze relationships between:

- Domains
- IP addresses
- Certificates
- DNS records
- Malware
- URLs
- Threat actors


Example:

    Domain
      ↓
    IP
      ↓
    Certificate
      ↓
    Related Domain
      ↓
    Campaign


Document relationships carefully and distinguish facts from assumptions.


---

## 30. Phase 23 — Vulnerability Intelligence

Check whether the campaign uses known vulnerabilities.

For each relevant CVE:

- CVE ID
- Affected product
- Severity
- Exploitation status
- Internal exposure
- Patch status
- Recommended action


Prioritize vulnerabilities based on organizational risk.


---

## 31. Phase 24 — Automated Enrichment

Implement a Python workflow:

    IOC
     ↓
    Validate
     ↓
    Normalize
     ↓
    API Lookup
     ↓
    Enrich
     ↓
    Score
     ↓
    Store
     ↓
    Report


Include:

- Error handling
- Logging
- Rate-limit handling
- Secure API-key management


---

## 32. Phase 25 — AI-Assisted Analysis

AI may assist with:

- Report summarization
- IOC extraction
- TTP extraction
- Threat relationship analysis
- Drafting intelligence reports
- Generating investigation questions
- Creating preliminary hunting hypotheses


AI output must be validated against trusted sources and security telemetry.


---

## 33. Phase 26 — Human Validation

Use:

    AI / Automation
          ↓
    Preliminary Result
          ↓
    Source Verification
          ↓
    Analyst Review
          ↓
    Approved Intelligence
          ↓
    Security Action


High-impact actions should not rely solely on automated or AI-generated conclusions.


---

## 34. Phase 27 — Intelligence Report

Create a professional report containing:

### Executive Summary

Short description of the threat and organizational relevance.

### Threat Overview

Describe the campaign or activity.

### Indicators

List relevant IOCs.

### TTPs

Document observed techniques.

### Risk Assessment

Explain likelihood and impact.

### Internal Findings

Document relevant telemetry.

### Recommendations

Provide prioritized actions.


---

## 35. Phase 28 — Executive Summary Example

Example structure:

    A recently identified threat campaign
    presents a potential risk to the organization's
    technology environment.

    Intelligence analysis identified relevant
    infrastructure, indicators, and attack techniques.

    Internal telemetry was reviewed to determine
    whether related activity was observed.

    Recommended actions include detection updates,
    targeted threat hunting, vulnerability remediation,
    and continued monitoring.


Use actual project findings rather than fabricated conclusions.


---

## 36. Phase 29 — Intelligence Confidence

Every major conclusion should include confidence.

Example:

    High Confidence
    → Supported by multiple reliable sources.

    Medium Confidence
    → Supported by credible but incomplete evidence.

    Low Confidence
    → Limited evidence or preliminary assessment.


Confidence is separate from severity.


---

## 37. Phase 30 — Intelligence Lifecycle

Complete lifecycle:

    Direction
       ↓
    Collection
       ↓
    Processing
       ↓
    Analysis
       ↓
    Dissemination
       ↓
    Operationalization
       ↓
    Feedback


The capstone should demonstrate this entire lifecycle.


---

## 38. Phase 31 — Metrics

Measure:

- Number of indicators collected
- Valid indicators
- Duplicate indicators
- Relevant indicators
- Enriched indicators
- CTI-driven detections
- CTI-driven hunts
- Investigation time
- Enrichment time
- Automation success
- Analyst time saved


---

## 39. Phase 32 — KPI Dashboard

Example:

    +--------------------------------------+
    | THREAT INTELLIGENCE DASHBOARD        |
    +--------------------------------------+
    | Indicators Collected          10,000 |
    | Valid Indicators               9,500 |
    | Relevant Indicators             2,100 |
    | High Confidence                 1,200 |
    | CTI Detections                     35 |
    | CTI Hunts                          12 |
    | Automation Success                98% |
    | Avg Enrichment Time             1.7s |
    +--------------------------------------+


Use actual project data in the final implementation.


---

## 40. Phase 33 — Lessons Learned

Document:

- What worked?
- What failed?
- Which feeds were useful?
- Which indicators were irrelevant?
- What detection gaps were identified?
- What automation failures occurred?
- What could be improved?
- What would be changed in production?


---

## 41. Project Deliverables

The final project should contain:

1. Architecture diagram.
2. Intelligence collection documentation.
3. IOC dataset.
4. Enrichment workflow.
5. Threat analysis.
6. MITRE ATT&CK mapping.
7. Detection rules.
8. Threat hunting queries.
9. Investigation notes.
10. Incident response workflow.
11. Automation script.
12. KPI dashboard.
13. Threat intelligence report.
14. Lessons learned.


---

## 42. Recommended Repository Structure

    20-Threat-Intelligence-Capstone-Project/
    │
    ├── README.md
    │
    ├── architecture/
    │   └── architecture.md
    │
    ├── collection/
    │   └── intelligence-collection.md
    │
    ├── iocs/
    │   ├── sample-iocs.json
    │   └── ioc-analysis.md
    │
    ├── enrichment/
    │   └── enrichment-workflow.md
    │
    ├── analysis/
    │   ├── threat-analysis.md
    │   ├── threat-actor-analysis.md
    │   └── malware-analysis.md
    │
    ├── mitre/
    │   └── attack-mapping.md
    │
    ├── detection/
    │   └── detection-engineering.md
    │
    ├── threat-hunting/
    │   └── hunting-hypotheses.md
    │
    ├── investigation/
    │   └── investigation-report.md
    │
    ├── incident-response/
    │   └── response-workflow.md
    │
    ├── automation/
    │   └── ti-automation.md
    │
    ├── ai/
    │   └── ai-assisted-analysis.md
    │
    ├── metrics/
    │   └── kpi-dashboard.md
    │
    ├── reports/
    │   └── threat-intelligence-report.md
    │
    ├── evidence/
    │   └── screenshots/
    │
    └── lessons-learned.md


---

## 43. Portfolio Evidence

Capture screenshots showing:

- Intelligence dataset
- IOC enrichment
- Wazuh alerts
- SIEM searches
- Detection rules
- Threat hunting
- Investigation
- Automation
- KPI dashboard
- Final report


Remove sensitive information before publishing.


---

## 44. GitHub Documentation

The project README should explain:

### Problem

What security problem is being addressed?

### Objective

What is the project designed to achieve?

### Architecture

How does intelligence move through the system?

### Tools

Which technologies were used?

### Implementation

How was the workflow built?

### Findings

What did the investigation discover?

### Detection

What security detections were developed?

### Automation

Which tasks were automated?

### Results

What measurable improvement was achieved?

### Lessons Learned

What was learned from the project?


---

## 45. Skills Demonstrated

This capstone demonstrates:

### Threat Intelligence

- Intelligence lifecycle
- IOC analysis
- Threat actor analysis
- Malware intelligence
- Threat assessment
- Intelligence reporting

### SOC

- SIEM monitoring
- Alert investigation
- Threat hunting
- Detection engineering
- Incident response

### Technical

- Python
- APIs
- JSON
- Log analysis
- Security monitoring

### Automation

- IOC enrichment
- Workflow automation
- Risk scoring
- KPI generation

### AI

- AI-assisted analysis
- AI output validation
- Prompt injection awareness
- Human-in-the-loop workflows


---

## 46. Interview Explanation

### "Tell me about your Threat Intelligence project."

A strong answer:

> I built a Threat Intelligence capstone project that simulates a SOC workflow from intelligence collection to operationalization. I collected and normalized IOCs, enriched them using approved intelligence sources, analyzed threat actors and TTPs, mapped activity to MITRE ATT&CK, and correlated the intelligence with SIEM telemetry. I then created detection and threat-hunting workflows, automated repetitive enrichment tasks using Python, and measured the process using CTI and SOC metrics. Finally, I documented the findings in a professional threat intelligence report.


---

## 47. Interview Question

### How does CTI help a SOC?

CTI gives the SOC additional context about threats.

It can help analysts:

- Identify malicious indicators.
- Understand attacker behavior.
- Prioritize alerts.
- Create detections.
- Develop hunting hypotheses.
- Investigate incidents.
- Improve response.


---

## 48. Interview Question

### What is the difference between an IOC and TTP?

An IOC is an observable indicator associated with potentially malicious activity.

Examples:

- IP address
- Domain
- URL
- File hash

A TTP describes attacker behavior.

Examples:

- PowerShell execution
- Credential dumping
- Scheduled task persistence
- Data exfiltration

IOCs can change quickly, while attacker techniques may remain useful for longer-term detection.


---

## 49. Interview Question

### How do you determine whether intelligence is useful?

I evaluate:

- Relevance
- Reliability
- Confidence
- Recency
- Actionability
- Internal applicability
- Detection value


Useful intelligence should help the organization make a better security decision.


---

## 50. Interview Question

### What would you automate?

I would automate repetitive, low-risk activities such as:

- IOC extraction
- Validation
- Normalization
- Deduplication
- Enrichment
- Scoring
- Ticket creation
- Reporting


I would keep human approval for high-impact response actions.


---

## 51. Interview Question

### How can AI help Threat Intelligence?

AI can assist with:

- Processing large reports
- Extracting IOCs
- Summarizing intelligence
- Identifying TTPs
- Generating investigation questions
- Clustering related information
- Drafting reports


However, analysts should validate AI-generated conclusions before using them for important security decisions.


---

## 52. Project Success Criteria

The capstone is successful when it demonstrates:

    Intelligence
        ↓
    Processing
        ↓
    Analysis
        ↓
    Operationalization
        ↓
    Detection
        ↓
    Investigation
        ↓
    Response
        ↓
    Measurement


Every stage should have documented evidence.


---

## 53. Project Maturity

### Level 1

Manual IOC collection and analysis.

### Level 2

Automated enrichment.

### Level 3

SIEM integration and CTI-driven detection.

### Level 4

Threat hunting and SOAR workflows.

### Level 5

AI-assisted intelligence analysis with human oversight and measurable business impact.


---

## 54. Final Project Workflow

    External Intelligence
             ↓
        Collection
             ↓
        IOC Extraction
             ↓
          Validation
             ↓
         Normalization
             ↓
         Deduplication
             ↓
          Enrichment
             ↓
        Threat Analysis
             ↓
       MITRE ATT&CK
             ↓
        Risk Scoring
             ↓
       Prioritization
             ↓
    ┌────────┴────────┐
    ↓                 ↓
   SIEM              TIP
    ↓                 ↓
 Detection        Intelligence
    ↓                 ↓
 Threat Hunting  Investigation
    └────────┬────────┘
             ↓
        SOC Analyst
             ↓
      Incident Response
             ↓
         Reporting
             ↓
           KPIs
             ↓
    Continuous Improvement


---

## 55. Key Takeaways

Remember:

1. Intelligence must be relevant.
2. Intelligence must be validated.
3. IOC volume is not intelligence quality.
4. Intelligence should be operationalized.
5. CTI should support detection.
6. CTI should support threat hunting.
7. CTI should support incident response.
8. Automation should reduce repetitive work.
9. AI output requires validation.
10. High-impact actions require appropriate human oversight.
11. Metrics should demonstrate operational value.
12. Intelligence should ultimately support better security decisions.


---

## 56. Final Principle

A mature Threat Intelligence capability is not simply a collection of threat feeds.

It is a complete operational process:

**Collect → Process → Analyze → Prioritize → Operationalize → Detect → Investigate → Respond → Measure → Improve**

The most valuable intelligence is intelligence that changes a security decision.

The ultimate objective of this capstone is to demonstrate that a SOC analyst can transform raw threat information into:

**Actionable Intelligence → Better Detection → Faster Investigation → Better Response → Reduced Risk**


---

## 57. Career Value

This project can demonstrate practical capability for entry-level roles such as:

- SOC Analyst
- Cybersecurity Analyst
- Threat Intelligence Analyst
- Security Operations Intern
- Junior Threat Hunter
- Vulnerability Management Analyst
- Security Monitoring Analyst


It can also provide a foundation for future specialization in:

- Threat Hunting
- Detection Engineering
- DFIR
- GRC
- Security Automation
- AI Security


---

## 58. Final Portfolio Statement

> This Threat Intelligence Capstone demonstrates an end-to-end SOC-oriented intelligence workflow, combining threat intelligence analysis, IOC enrichment, MITRE ATT&CK mapping, SIEM monitoring, threat hunting, incident investigation, automation, AI-assisted analysis, and KPI measurement.

The project demonstrates the ability to transform raw threat information into actionable security intelligence while maintaining validation, documentation, and human oversight.


---

## 59. Final Checklist

Before marking the project complete:

- [ ] Architecture documented
- [ ] Intelligence sources documented
- [ ] IOC dataset created
- [ ] IOC validation completed
- [ ] IOC normalization completed
- [ ] Deduplication implemented
- [ ] Enrichment workflow implemented
- [ ] Threat analysis completed
- [ ] Threat actor analysis completed
- [ ] Malware analysis completed
- [ ] MITRE ATT&CK mapping completed
- [ ] Risk assessment completed
- [ ] Detection logic created
- [ ] Threat hunting performed
- [ ] SIEM correlation completed
- [ ] Investigation documented
- [ ] Incident response workflow documented
- [ ] Automation implemented
- [ ] AI assistance documented
- [ ] Human validation documented
- [ ] Metrics calculated
- [ ] KPI dashboard created
- [ ] Final intelligence report completed
- [ ] Screenshots collected
- [ ] Sensitive information removed
- [ ] GitHub documentation completed
- [ ] Lessons learned documented


---

## 60. Conclusion

The Threat Intelligence Capstone Project brings together the complete knowledge developed throughout this directory.

It demonstrates how a modern SOC can combine:

**Threat Intelligence + SIEM + Threat Hunting + Detection Engineering + Incident Response + Automation + AI + Metrics**

The goal is not simply to know what a threat is.

The goal is to determine:

**What does this threat mean for our organization?**

**What evidence do we have?**

**What should we detect?**

**What should we investigate?**

**What action should we take?**

**How effective was our response?**

That is the practical value of Threat Intelligence in a modern Security Operations Center.
