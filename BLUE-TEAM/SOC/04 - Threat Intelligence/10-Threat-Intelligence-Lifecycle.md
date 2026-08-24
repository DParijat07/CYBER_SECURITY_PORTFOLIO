# 10 - Threat Intelligence Lifecycle

## 1. Introduction

The Threat Intelligence Lifecycle is the structured process used to transform raw information into actionable cyber threat intelligence.

A mature lifecycle helps security teams:

- Identify intelligence requirements
- Collect relevant information
- Process raw data
- Analyze threats
- Produce intelligence
- Distribute intelligence
- Measure results
- Improve future intelligence collection

Core lifecycle:

Planning
   ↓
Collection
   ↓
Processing
   ↓
Analysis
   ↓
Dissemination
   ↓
Feedback
   ↓
Planning


---

## 2. Why the Threat Intelligence Lifecycle Matters

Raw threat data alone does not provide enough value.

Example:

IP Address:
203.0.113.10

This is only an indicator.

After analysis:

IP:
203.0.113.10

Context:
- Malicious infrastructure
- Associated malware
- Related campaign
- Recent activity
- High confidence
- Internal connection observed

Now the information becomes actionable intelligence.

Therefore:

Raw Data
   ↓
Processing
   ↓
Context
   ↓
Analysis
   ↓
Actionable Intelligence


---

## 3. Threat Intelligence Lifecycle

A practical lifecycle contains six major stages:

1. Planning and Direction
2. Collection
3. Processing
4. Analysis
5. Dissemination
6. Feedback

The process is continuous rather than strictly linear.

Planning
   ↓
Collection
   ↓
Processing
   ↓
Analysis
   ↓
Dissemination
   ↓
Feedback
   └──────────────→ Planning


---

## 4. Stage 1 — Planning and Direction

Planning defines what intelligence the organization actually needs.

Key questions:

- What threats are relevant?
- Which assets need protection?
- Who will consume the intelligence?
- What decisions should intelligence support?
- What intelligence gaps exist?
- What timeframe is required?
- What level of confidence is acceptable?

---

## 5. Intelligence Requirements

Intelligence Requirements are questions that intelligence should answer.

Examples:

- Which threat actors target our industry?
- Which vulnerabilities are being actively exploited?
- Are our exposed assets being targeted?
- Which malware families are relevant?
- Which phishing campaigns are targeting employees?
- Which attacker infrastructure is associated with current campaigns?

Good intelligence requirements should be specific and actionable.


---

## 6. Priority Intelligence Requirements

Priority Intelligence Requirements, or PIRs, represent the most important intelligence questions.

Example:

### PIR 1

Are threat actors actively targeting our internet-facing infrastructure?

### PIR 2

Are vulnerabilities affecting our critical systems being actively exploited?

### PIR 3

Are current phishing campaigns targeting our employees?

PIRs help prioritize intelligence collection.


---

## 7. Intelligence Requirements by Audience

Different users need different intelligence.

### Executive

Needs:

- Business risk
- Major threats
- Strategic trends
- Financial impact
- Security priorities

### SOC

Needs:

- Indicators
- TTPs
- Malware
- Threat actors
- Detection opportunities

### Incident Response

Needs:

- Infrastructure
- Malware
- Campaigns
- Attack patterns
- Historical activity

### Threat Hunting

Needs:

- TTPs
- Indicators
- Behavioral patterns
- Threat actor techniques


---

## 8. Intelligence Requirement Example

Business question:

"Are we at risk from ransomware groups?"

Convert into intelligence requirements:

- Which ransomware groups target our sector?
- Which vulnerabilities do they exploit?
- What infrastructure do they use?
- Which malware families are associated?
- What TTPs do they use?
- Are any related indicators present internally?

This transforms a broad question into actionable collection requirements.


---

## 9. Stage 2 — Collection

Collection involves gathering relevant information.

Possible sources:

- Threat intelligence feeds
- Security vendors
- Government advisories
- CERTs
- Open-source intelligence
- Dark web monitoring
- Security reports
- SIEM
- EDR
- Firewall
- IDS/IPS
- DNS
- Incident response
- Vulnerability scanners
- Internal security teams


---

## 10. External Collection

External sources provide information about threats outside the organization.

Examples:

- Threat reports
- Malware research
- Vulnerability advisories
- IOC feeds
- Security blogs
- Government alerts
- Industry sharing groups
- Commercial intelligence feeds

External intelligence provides broader visibility.


---

## 11. Internal Collection

Internal sources show what is happening inside the organization.

Examples:

- Authentication logs
- DNS logs
- Proxy logs
- Firewall logs
- EDR telemetry
- SIEM alerts
- Email security logs
- Incident reports
- Vulnerability scans

Internal data is critical for determining whether external threats affect the organization.


---

## 12. Open-Source Intelligence

Open-source intelligence can include:

- Public reports
- Security research
- Vulnerability databases
- Vendor advisories
- Public infrastructure information
- Public malware research
- Public threat actor information

OSINT should be validated before being treated as reliable intelligence.


---

## 13. Collection Planning

Collection should be aligned with requirements.

Example:

Requirement:

"Identify ransomware threats targeting our sector."

Collection sources:

Threat Reports
      ↓
Ransomware Feeds
      ↓
Vendor Research
      ↓
Government Advisories
      ↓
Internal Incident Data

This is better than collecting every available threat feed.


---

## 14. Source Reliability

Not all sources have the same reliability.

A source evaluation can consider:

- Historical accuracy
- Expertise
- Transparency
- Technical evidence
- Consistency
- Corroboration

Example:

Source A:
High reliability

Source B:
Medium reliability

Source C:
Unknown reliability

Analysts should consider source reliability during analysis.


---

## 15. Information Credibility

Source reliability and information credibility are related but different.

### Source Reliability

How trustworthy is the source?

### Information Credibility

How believable is this specific information?

Example:

A highly reliable source can occasionally publish incorrect information.

Therefore both should be assessed.


---

## 16. Stage 3 — Processing

Raw information often requires processing before analysis.

Processing may include:

- Parsing
- Normalization
- Deduplication
- Translation
- Formatting
- Classification
- Validation
- Extraction
- Enrichment

Workflow:

Raw Information
      ↓
Processing
      ↓
Structured Information


---

## 17. Data Normalization

Different sources may use different formats.

Example:

Source A:

IP=203.0.113.10

Source B:

Address=203.0.113.10

Source C:

IOC=203.0.113.10

Normalize:

Type: IPv4
Value: 203.0.113.10


---

## 18. Deduplication

The same IOC may appear in multiple feeds.

Example:

Feed A → malicious-domain.example

Feed B → malicious-domain.example

Feed C → malicious-domain.example

Instead of storing three separate records:

Domain:
malicious-domain.example

Sources:
A, B, C

This reduces duplicate intelligence.


---

## 19. Data Enrichment

Enrichment adds context.

Example:

IP Address
     ↓
Reputation
     ↓
ASN
     ↓
Geolocation
     ↓
WHOIS
     ↓
Related Domains
     ↓
Malware
     ↓
Threat Actor

Enrichment helps analysts understand the significance of an indicator.


---

## 20. IOC Extraction

Threat reports may contain indicators inside unstructured text.

Example:

Report:

"Researchers observed connections to 203.0.113.10 and malicious-domain.example."

Extraction:

IP:
203.0.113.10

Domain:
malicious-domain.example

These indicators can then be enriched and analyzed.


---

## 21. TTP Extraction

Threat intelligence should not focus only on IOCs.

Analysts should also identify:

- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Command and Control
- Exfiltration
- Impact

This helps create behavioral intelligence.


---

## 22. Stage 4 — Analysis

Analysis transforms processed information into intelligence.

Analysts ask:

- What happened?
- Who is responsible?
- How did the attack occur?
- Why is it happening?
- What infrastructure is involved?
- What assets are at risk?
- What should the organization do?


---

## 23. Analysis Methods

Common approaches include:

- Technical analysis
- Contextual analysis
- Behavioral analysis
- Trend analysis
- Correlation
- Link analysis
- Timeline analysis
- Risk analysis
- Hypothesis-driven analysis


---

## 24. Technical Analysis

Technical analysis focuses on technical artifacts.

Examples:

- IP addresses
- Domains
- URLs
- Hashes
- Malware
- Processes
- Network traffic
- Exploit techniques

Example:

Malicious Hash
      ↓
Malware Family
      ↓
C2 Domain
      ↓
C2 IP
      ↓
Threat Actor


---

## 25. Contextual Analysis

Context answers:

"Why does this indicator matter?"

Example:

IP:
203.0.113.10

Context:

- Associated with malware
- Used by a known campaign
- Recently active
- Observed in the organization's logs

The context increases the value of the indicator.


---

## 26. Behavioral Analysis

Behavioral analysis focuses on attacker activity rather than individual indicators.

Example:

Phishing
  ↓
Credential Theft
  ↓
Valid Account
  ↓
Remote Access
  ↓
Privilege Escalation
  ↓
Lateral Movement

This helps defenders detect attacks even when specific IOCs change.


---

## 27. Correlation

Correlation connects multiple pieces of information.

Example:

IP
 ↓
Domain
 ↓
Certificate
 ↓
Malware
 ↓
Threat Actor
 ↓
Campaign

This can reveal relationships that are not visible from individual indicators.


---

## 28. Timeline Analysis

Timeline analysis determines the sequence of events.

Example:

09:00 — Phishing email received

09:05 — User clicked malicious link

09:06 — Credentials submitted

09:15 — Suspicious login

09:20 — PowerShell execution

09:30 — C2 connection

09:45 — Lateral movement

This helps reconstruct an attack.


---

## 29. Link Analysis

Link analysis identifies relationships between entities.

Example:

Threat Actor
      |
     uses
      ↓
Malware
      |
communicates
      ↓
Domain
      |
resolves
      ↓
IP
      |
hosted on
      ↓
Infrastructure

Link analysis is especially useful for campaign investigations.


---

## 30. Hypothesis-Driven Analysis

Analysts can create hypotheses.

Example:

Hypothesis:

"Threat Actor X may be targeting our organization."

Test:

1. Search known infrastructure.
2. Search known malware.
3. Search related domains.
4. Search TTPs.
5. Review SIEM.
6. Review EDR.
7. Review authentication logs.

Result:

Confirmed / Not Confirmed / Inconclusive


---

## 31. Threat Scoring

Threat intelligence can be prioritized using:

- Source reliability
- Confidence
- Recency
- Internal sightings
- Threat actor association
- Malware association
- Active exploitation
- Asset criticality

Example:

Risk Score =
Confidence
+
Severity
+
Recency
+
Internal Exposure


---

## 32. Confidence Assessment

Analysts should communicate confidence.

Example:

### High Confidence

Multiple reliable sources confirm the activity.

### Medium Confidence

Evidence supports the assessment but additional validation is required.

### Low Confidence

Limited evidence exists.

Confidence should be explicitly documented in intelligence products.


---

## 33. Stage 5 — Dissemination

Dissemination means delivering intelligence to the correct audience.

Possible consumers:

- SOC
- Incident Response
- Threat Hunting
- Security Engineering
- Vulnerability Management
- GRC
- Executives
- Management


---

## 34. Intelligence Dissemination Methods

Intelligence can be distributed through:

- TIP
- SIEM
- SOAR
- Email
- Dashboards
- Reports
- APIs
- STIX/TAXII
- Tickets
- Security advisories

The method should match the audience and urgency.


---

## 35. Tactical Dissemination

Tactical intelligence can be distributed to:

- SIEM
- EDR
- Firewall
- IDS/IPS
- Threat hunters

Example:

Malicious IP
      ↓
TIP
      ↓
SIEM / Firewall / EDR
      ↓
Detection


---

## 36. Operational Dissemination

Operational intelligence can support:

- Incident response
- Threat hunting
- SOC investigations
- Detection engineering

Example:

Campaign Intelligence
      ↓
SOC
      ↓
Threat Hunting
      ↓
Detection Development


---

## 37. Strategic Dissemination

Strategic intelligence is usually delivered to leadership.

Example:

Threat Trend
      ↓
Business Risk
      ↓
Potential Impact
      ↓
Executive Report
      ↓
Security Decision


---

## 38. Intelligence Product

An intelligence product should be designed for its audience.

Typical structure:

### Executive Summary

Short description of the threat.

### Threat Overview

What is happening?

### Impact

Why does it matter?

### Evidence

What supports the assessment?

### Indicators

Relevant technical indicators.

### TTPs

Relevant attacker behaviors.

### Assessment

Analyst conclusion.

### Recommendations

Recommended actions.


---

## 39. Stage 6 — Feedback

Feedback closes the intelligence lifecycle.

Consumers can provide:

- Was the intelligence useful?
- Was it accurate?
- Did it produce a detection?
- Was it relevant?
- Was it too broad?
- Was it too late?
- What additional information is required?

Feedback improves future intelligence collection.


---

## 40. Feedback Loop

Intelligence Product
       ↓
Consumer
       ↓
Operational Use
       ↓
Feedback
       ↓
Updated Requirements
       ↓
New Collection
       ↓
Improved Intelligence


---

## 41. Intelligence Lifecycle Is Continuous

The lifecycle is not:

Plan → Collect → Analyze → Done

Instead:

Plan
 ↓
Collect
 ↓
Process
 ↓
Analyze
 ↓
Disseminate
 ↓
Feedback
 ↓
Plan Again

Threat environments continuously change, so intelligence must continuously evolve.


---

## 42. Intelligence Lifecycle Example

Scenario:

A ransomware group starts targeting a specific industry.

### Planning

Question:

"Is this ransomware group targeting our organization?"

### Collection

Collect:

- Threat reports
- Malware information
- Infrastructure
- TTPs
- Vulnerabilities

### Processing

Normalize:

- IPs
- Domains
- Hashes
- TTPs

### Analysis

Determine:

- Threat actor
- Campaign
- Targeting
- Relevant vulnerabilities

### Dissemination

Send:

- IOCs to SIEM
- TTPs to threat hunters
- Risk assessment to management

### Feedback

SOC reports:

"One IOC matched internal DNS traffic."

The lifecycle starts again with deeper investigation.


---

## 43. Threat Intelligence Lifecycle and SOC

The lifecycle supports SOC operations.

Planning
   ↓
Threat Requirements
   ↓
Collection
   ↓
Processing
   ↓
TIP
   ↓
Analysis
   ↓
SIEM / EDR / SOAR
   ↓
SOC
   ↓
Investigation
   ↓
Feedback


---

## 44. Threat Intelligence Lifecycle and Incident Response

During an incident:

Incident
   ↓
Intelligence Requirement
   ↓
Collection
   ↓
Processing
   ↓
Analysis
   ↓
Threat Assessment
   ↓
Response
   ↓
Lessons Learned
   ↓
Updated Intelligence


---

## 45. Threat Intelligence Lifecycle and Vulnerability Management

Example:

New CVE
 ↓
Collection
 ↓
Threat Intelligence
 ↓
Active Exploitation?
 ↓
Affected Assets?
 ↓
Business Criticality
 ↓
Risk Assessment
 ↓
Patch Priority


---

## 46. Threat Intelligence Lifecycle and Threat Hunting

Example:

New Threat Actor Intelligence
        ↓
Collection
        ↓
Analysis
        ↓
TTP Identification
        ↓
Hunting Hypothesis
        ↓
SIEM / EDR Search
        ↓
Internal Evidence
        ↓
Feedback


---

## 47. Automation in the Lifecycle

Automation can support almost every stage.

### Planning

AI can help identify intelligence gaps.

### Collection

Automated feed ingestion.

### Processing

Automated parsing and normalization.

### Analysis

Automated enrichment and correlation.

### Dissemination

Automated distribution.

### Feedback

Automated metrics and reporting.


---

## 48. AI-Assisted Threat Intelligence Lifecycle

Example:

Threat Sources
      ↓
Automated Collection
      ↓
AI Extraction
      ↓
Normalization
      ↓
AI Enrichment
      ↓
Correlation
      ↓
AI-Assisted Analysis
      ↓
Human Validation
      ↓
Dissemination
      ↓
Feedback
      ↓
Continuous Improvement


---

## 49. AI-Assisted Report Analysis

Input:

Threat Research Report

AI extracts:

- Threat actors
- Malware
- IP addresses
- Domains
- URLs
- Hashes
- CVEs
- TTPs

Then:

AI
 ↓
Structured Intelligence
 ↓
Analyst Validation
 ↓
TIP


---

## 50. AI-Assisted Intelligence Summarization

A long technical report can be transformed into:

### Executive Summary

Short business-focused explanation.

### Technical Summary

Technical details for security teams.

### IOCs

Extracted indicators.

### TTPs

Mapped attacker behaviors.

### Recommendations

Recommended defensive actions.


---

## 51. AI-Assisted Intelligence Prioritization

AI can help rank intelligence based on:

- Threat severity
- Confidence
- Recency
- Internal exposure
- Asset criticality
- Threat actor relevance
- Active exploitation

Example:

1000 Indicators
      ↓
AI Prioritization
      ↓
Top 50 Relevant Indicators
      ↓
Analyst Validation
      ↓
SOC


---

## 52. Human-in-the-Loop

AI should assist analysts rather than blindly control security decisions.

Recommended:

AI Recommendation
      ↓
Analyst Review
      ↓
Validation
      ↓
Approved Intelligence
      ↓
Security Action


---

## 53. Intelligence Automation Pipeline

A practical automated pipeline:

Threat Feed
      ↓
API Collection
      ↓
Parser
      ↓
Normalizer
      ↓
Deduplication
      ↓
Enrichment
      ↓
Threat Scoring
      ↓
TIP
      ↓
SIEM / SOAR / EDR


---

## 54. Intelligence Quality

Quality should be measured continuously.

Important dimensions:

- Accuracy
- Relevance
- Timeliness
- Completeness
- Confidence
- Actionability

High-volume intelligence is not automatically high-quality intelligence.


---

## 55. Intelligence Timeliness

Threat intelligence loses value when it becomes outdated.

Example:

New C2 Domain
     ↓
High Value
     ↓
24 Hours Later
     ↓
Still Relevant

Months later:

Old C2 Domain
     ↓
Potentially Expired
     ↓
Requires Validation


---

## 56. Indicator Expiration

Indicators should have lifecycle controls.

Example:

New Indicator
      ↓
Active
      ↓
Monitor
      ↓
Expiration Date
      ↓
Review
      ↓
Renew / Expire


---

## 57. Intelligence Gaps

An intelligence gap exists when the organization does not have enough information to answer an important question.

Example:

Question:

"Which threat actors are targeting our industry?"

Current knowledge:

Only one actor identified.

Gap:

Unknown actors and campaigns.

Action:

Collect additional intelligence.


---

## 58. Intelligence Gap Workflow

Requirement
      ↓
Known Information
      ↓
Identify Gap
      ↓
Collection Plan
      ↓
Collect
      ↓
Analyze
      ↓
Close Gap


---

## 59. Intelligence Requirements Matrix

Example:

| Requirement | Consumer | Priority | Source | Output |
|---|---|---|---|---|
| Active ransomware threats | SOC | High | Threat Feeds | IOC/TTP |
| Exploited vulnerabilities | Vulnerability Team | High | CVE/Threat Reports | Risk |
| Industry threat actors | Management | Medium | Research | Strategic Report |
| Phishing campaigns | SOC | High | Email/Threat Feeds | Detection |

---

## 60. Intelligence Collection Matrix

Example:

| Source | Type | Frequency | Reliability | Use |
|---|---|---|---|---|
| Threat Feed | External | Continuous | High | IOC |
| Vendor Report | External | Periodic | High | TTP |
| SIEM | Internal | Continuous | High | Detection |
| EDR | Internal | Continuous | High | Endpoint |
| CERT Advisory | External | Event-based | High | Vulnerability |

---

## 61. Intelligence Lifecycle Metrics

Useful metrics include:

### Collection

- Feed availability
- Collection success rate
- Number of sources

### Processing

- Parsing success
- Deduplication rate
- Enrichment success

### Analysis

- Intelligence quality
- Confidence
- Internal matches

### Dissemination

- Distribution time
- Consumer coverage

### Outcome

- Detection improvement
- Investigation time reduction
- Incident response improvement


---

## 62. Measuring Intelligence Value

A useful model:

Intelligence Value =
Relevance
+
Accuracy
+
Timeliness
+
Actionability

The goal is not maximum data.

The goal is maximum useful intelligence.


---

## 63. Practical Lab — Build a Threat Intelligence Lifecycle

### Objective

Create an end-to-end threat intelligence workflow.

### Components

- Intelligence requirements
- Threat feeds
- Data collection
- Processing
- Enrichment
- Analysis
- Dissemination
- Feedback

Architecture:

Requirements
    ↓
Collection
    ↓
Processing
    ↓
Analysis
    ↓
TIP
    ↓
SIEM / SOAR
    ↓
SOC
    ↓
Feedback


---

## 64. Practical Lab — Intelligence Requirement

Create three PIRs.

Example:

PIR 1:
Are ransomware groups targeting our industry?

PIR 2:
Which vulnerabilities are being actively exploited against organizations like ours?

PIR 3:
Are any known malicious infrastructures present in our environment?


---

## 65. Practical Lab — Intelligence Collection

Collect intelligence from authorized sources.

Document:

- Source
- Type
- Reliability
- Collection method
- Frequency
- Data format
- Relevance


---

## 66. Practical Lab — Intelligence Processing

Process collected data.

Tasks:

- Extract indicators
- Normalize data
- Remove duplicates
- Add metadata
- Validate indicators
- Enrich indicators
- Assign confidence


---

## 67. Practical Lab — Intelligence Analysis

Select one threat actor or campaign.

Analyze:

- Motivation
- Target
- Malware
- Infrastructure
- TTPs
- Vulnerabilities
- Indicators
- Timeline
- Confidence


---

## 68. Practical Lab — Intelligence Dissemination

Create separate outputs for:

### SOC

IOC + TTP + Detection

### Threat Hunter

Behavior + Hunting Hypothesis

### Management

Risk + Business Impact + Recommendation


---

## 69. Practical Lab — Feedback

After dissemination, evaluate:

- Was the intelligence useful?
- Did it generate alerts?
- Did it improve investigation?
- Was it accurate?
- Was it timely?
- What additional information was needed?

Document the results.


---

## 70. Portfolio Project

# Project: End-to-End Threat Intelligence Lifecycle

## Objective

Build a complete threat intelligence workflow that demonstrates how an organization transforms raw threat information into actionable intelligence.

### Architecture

Threat Sources
      ↓
Collection
      ↓
Processing
      ↓
TIP
      ↓
Enrichment
      ↓
Analysis
      ↓
Threat Scoring
      ↓
Dissemination
      ↓
SIEM / SOAR / EDR
      ↓
SOC
      ↓
Feedback
      ↓
Improved Requirements


---

## 71. Project Deliverables

Create:

1. Intelligence Requirements Document
2. Collection Matrix
3. Threat Intelligence Processing Pipeline
4. TIP Configuration
5. Intelligence Analysis Report
6. Threat Actor Profile
7. IOC Database
8. Detection Use Cases
9. Threat Hunting Hypotheses
10. Executive Intelligence Report
11. Feedback Report
12. Architecture Diagram


---

## 72. AI Automation Portfolio Project

# Project: AI-Assisted Threat Intelligence Lifecycle

## Objective

Build an AI-assisted intelligence pipeline that reduces manual intelligence processing while keeping analysts responsible for validation and high-impact decisions.

### Workflow

Threat Report
      ↓
AI Extraction
      ↓
IOC / TTP / Entity Extraction
      ↓
Normalization
      ↓
Enrichment
      ↓
AI-Assisted Analysis
      ↓
Threat Scoring
      ↓
Human Validation
      ↓
TIP
      ↓
SIEM / SOAR
      ↓
SOC


---

## 73. AI Features

Implement or demonstrate:

- Threat report summarization
- IOC extraction
- Entity extraction
- TTP identification
- ATT&CK mapping
- Threat actor identification
- Campaign clustering
- Intelligence prioritization
- Automated enrichment
- Intelligence report generation


---

## 74. Professional Work Sample

Create:

**Threat Intelligence Lifecycle Assessment & Automation Report**

Include:

### 1. Executive Summary

Explain the threat intelligence problem.

### 2. Business Requirements

Define intelligence requirements.

### 3. Collection Architecture

Document sources.

### 4. Processing Pipeline

Explain normalization and enrichment.

### 5. Analysis Methodology

Explain how intelligence is evaluated.

### 6. Dissemination

Show how intelligence reaches security teams.

### 7. Automation

Document automated workflows.

### 8. AI Integration

Explain AI-assisted processing.

### 9. Human Validation

Explain analyst oversight.

### 10. Detection

Show how intelligence improves detection.

### 11. Metrics

Measure outcomes.

### 12. Lessons Learned

Document challenges.

### 13. Recommendations

Define future improvements.


---

## 75. Resume-Level Achievement Example

Instead of writing:

"Studied Threat Intelligence Lifecycle."

Write:

"Designed and documented an end-to-end threat intelligence lifecycle integrating collection, normalization, enrichment, analysis, threat scoring, and SIEM-driven dissemination, with AI-assisted IOC extraction and analyst validation."


---

## 76. Interview Scenario

### Scenario

A new threat intelligence report identifies a ransomware campaign targeting your industry.

### Step 1

Define intelligence requirements.

### Step 2

Collect:

- Malware
- Domains
- IPs
- Hashes
- TTPs
- Vulnerabilities

### Step 3

Process the information.

### Step 4

Enrich indicators.

### Step 5

Correlate the campaign.

### Step 6

Check internal telemetry.

### Step 7

Distribute relevant intelligence.

### Step 8

Create detections.

### Step 9

Provide executive risk assessment.

### Step 10

Collect feedback.

### Step 11

Update intelligence requirements.


---

## 77. L1 SOC Analyst Perspective

As an L1 SOC analyst, the lifecycle helps answer:

- Why did this alert trigger?
- Is the IOC known?
- Is the IOC related to a threat actor?
- Is the activity part of a known campaign?
- Has this IOC been seen internally?
- What TTP is involved?
- Should the alert be escalated?

Workflow:

Alert
 ↓
IOC
 ↓
TIP
 ↓
Context
 ↓
Internal Telemetry
 ↓
Assessment
 ↓
Escalation


---

## 78. Key Takeaways

The Threat Intelligence Lifecycle transforms information into intelligence.

The core process is:

Planning
   ↓
Collection
   ↓
Processing
   ↓
Analysis
   ↓
Dissemination
   ↓
Feedback
   ↓
Planning


The mature approach adds:

Automation
+
Threat Intelligence Platforms
+
STIX/TAXII
+
SIEM
+
SOAR
+
EDR
+
AI Assistance
+
Human Validation


---

## 79. Final Principle

> The purpose of the threat intelligence lifecycle is not to collect the maximum amount of threat data. Its purpose is to answer important security questions and convert reliable information into timely, relevant, and actionable intelligence.

A mature intelligence program therefore follows:

**Requirement → Collection → Processing → Analysis → Intelligence → Action → Feedback → Improvement**
