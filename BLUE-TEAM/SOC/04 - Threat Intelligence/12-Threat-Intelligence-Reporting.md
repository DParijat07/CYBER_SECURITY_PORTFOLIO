# 12 - Threat Intelligence Reporting

## 1. Introduction

Threat Intelligence Reporting is the process of transforming analyzed threat information into clear, actionable intelligence products for different audiences.

A threat intelligence report should answer:

- What happened?
- Who is involved?
- What is the threat?
- How does it work?
- Who is targeted?
- Why does it matter?
- Are we affected?
- What should we do?

The goal is not to produce a large document.

The goal is to provide the **right information to the right audience at the right time**.

Basic workflow:

Threat Data
    ↓
Collection
    ↓
Processing
    ↓
Analysis
    ↓
Assessment
    ↓
Threat Intelligence Report
    ↓
Decision / Action


---

## 2. Why Threat Intelligence Reporting Matters

Raw intelligence is difficult to consume.

Example:

    IP: 203.0.113.10
    Domain: malicious-example.com
    Hash: HASH_VALUE
    CVE: CVE-XXXX-XXXXX

This provides data but limited context.

A useful report explains:

- What these indicators represent
- Which campaign they belong to
- Which threat actor may be involved
- Which TTPs are being used
- Whether the organization is exposed
- What actions should be taken

Therefore:

Raw Data
    ↓
Context
    ↓
Analysis
    ↓
Assessment
    ↓
Actionable Intelligence


---

## 3. Objectives of Threat Intelligence Reporting

A professional intelligence report should:

1. Communicate findings clearly.
2. Provide relevant context.
3. Explain risk.
4. Support security decisions.
5. Enable detection and hunting.
6. Support incident response.
7. Provide evidence.
8. Communicate confidence.
9. Recommend actions.
10. Create a historical intelligence record.


---

## 4. Audience Matters

Different audiences require different reports.

### Executive

Needs:

- Business impact
- Risk
- Strategic trends
- Major threats
- Recommendations

### SOC

Needs:

- Indicators
- TTPs
- Detection opportunities
- Threat context

### Threat Hunter

Needs:

- Attacker behavior
- TTPs
- Infrastructure
- Hunting hypotheses

### Incident Response

Needs:

- Timeline
- Infrastructure
- Malware
- Threat actor
- Attack chain

### Vulnerability Management

Needs:

- CVEs
- Exploitation status
- Affected products
- Risk
- Priority

### GRC

Needs:

- Risk
- Control implications
- Compliance impact
- Business exposure


---

## 5. Types of Threat Intelligence Reports

Common report types include:

1. Tactical Intelligence Report
2. Operational Intelligence Report
3. Strategic Intelligence Report
4. Technical Threat Report
5. Threat Actor Profile
6. Campaign Report
7. Malware Report
8. Vulnerability Intelligence Report
9. IOC Report
10. Executive Threat Brief
11. Incident Intelligence Report
12. Threat Hunting Report


---

## 6. Tactical Intelligence Report

Tactical intelligence focuses on technical indicators and attacker behavior.

Typical contents:

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses
- Malware
- TTPs
- Detection recommendations

Primary consumers:

- SOC
- Detection Engineering
- Threat Hunting
- Incident Response


---

## 7. Operational Intelligence Report

Operational intelligence focuses on campaigns and attack activity.

Typical contents:

- Threat actor
- Campaign
- Target
- Attack vector
- Infrastructure
- TTPs
- Timeline
- Objectives

Primary consumers:

- SOC
- Incident Response
- Threat Hunting
- Security Operations


---

## 8. Strategic Intelligence Report

Strategic reporting focuses on business-level implications.

Typical contents:

- Threat trends
- Industry targeting
- Business risk
- Threat landscape
- Strategic impact
- Security investment recommendations

Primary consumers:

- CISO
- CIO
- Executives
- Board
- Risk Management


---

## 9. Technical Threat Report

Technical reports provide detailed technical analysis.

Typical contents:

- Malware behavior
- Network indicators
- Host artifacts
- TTPs
- Exploitation
- Attack chain
- Detection logic
- Mitigation

Primary consumers:

- SOC
- Threat Researchers
- Detection Engineers
- Incident Responders


---

## 10. Threat Actor Profile

A threat actor profile provides structured information about a threat actor.

Example structure:

    Threat Actor
        ↓
    Aliases
        ↓
    Motivation
        ↓
    Targets
        ↓
    Malware
        ↓
    Infrastructure
        ↓
    TTPs
        ↓
    Campaigns
        ↓
    Recent Activity


---

## 11. Campaign Report

A campaign report explains a coordinated malicious operation.

Typical sections:

- Campaign overview
- Timeline
- Target
- Initial access
- Execution
- Persistence
- C2
- Malware
- TTPs
- Infrastructure
- Impact
- Detection
- Mitigation


---

## 12. Malware Report

A malware intelligence report can include:

- Malware name
- Family
- Type
- Capabilities
- Initial access
- Execution
- Persistence
- C2
- File artifacts
- Network indicators
- TTPs
- Detection
- Mitigation


---

## 13. Vulnerability Intelligence Report

A vulnerability report should explain:

- CVE
- Vulnerability description
- Severity
- Affected products
- Exploitation status
- Threat actor relevance
- Public exploit availability
- Internal exposure
- Business impact
- Recommended remediation


---

## 14. IOC Report

An IOC report focuses on indicators.

Example:

| Type | Indicator | Confidence | Source | First Seen | Valid Until |
|---|---|---|---|---|---|
| IPv4 | 203.0.113.10 | High | Threat Feed | Date | Date |
| Domain | malicious-example.com | High | Research | Date | Date |
| SHA-256 | HASH_VALUE | High | Malware Analysis | Date | Date |

Indicators should always include context when possible.


---

## 15. Executive Threat Brief

An executive brief should be short.

Recommended structure:

### Threat

What is happening?

### Business Impact

Why does it matter?

### Exposure

Are we affected?

### Risk

How serious is the threat?

### Recommendation

What should leadership do?

Example:

> A ransomware campaign is actively targeting organizations in our industry. Current intelligence indicates exploitation of a vulnerability affecting a product deployed in our environment. Immediate patch prioritization and threat hunting are recommended.


---

## 16. Report Structure

A professional threat intelligence report can use:

1. Title
2. Executive Summary
3. Threat Overview
4. Scope
5. Intelligence Requirements
6. Key Findings
7. Threat Actor
8. Campaign
9. TTPs
10. Infrastructure
11. Indicators
12. Timeline
13. Risk Assessment
14. Internal Exposure
15. Detection
16. Mitigation
17. Recommendations
18. Confidence
19. Sources
20. Appendix


---

## 17. Executive Summary

The executive summary should answer:

- What is the threat?
- Why is it relevant?
- What is the current risk?
- What action is required?

Keep it concise.

Avoid:

- Excessive technical details
- Long IOC lists
- Complex terminology

Focus on decisions.


---

## 18. Threat Overview

Explain:

- Threat name
- Threat type
- Threat actor
- Target
- Sector
- Geography
- Current activity
- Severity

Example:

    Threat:
    Ransomware Campaign

    Target:
    Financial Sector

    Activity:
    Active

    Severity:
    High


---

## 19. Scope

Define what the report covers.

Example:

### Scope

This report analyzes:

- Current ransomware activity
- Associated threat actors
- Known infrastructure
- Relevant vulnerabilities
- TTPs
- Internal exposure
- Detection opportunities


---

## 20. Intelligence Requirements

Reports should connect findings to intelligence requirements.

Example:

### Requirement 1

Is the threat relevant to our industry?

### Requirement 2

Are our assets exposed?

### Requirement 3

Are related indicators present internally?

### Requirement 4

What defensive actions should be prioritized?


---

## 21. Key Findings

Key findings should summarize the most important discoveries.

Example:

1. The campaign is actively targeting organizations in the financial sector.
2. The threat actor uses phishing for initial access.
3. Multiple malicious domains are associated with the campaign.
4. A relevant vulnerability affects systems in the organization's environment.
5. No confirmed compromise was identified during the initial search.


---

## 22. Evidence

Intelligence assessments should be supported by evidence.

Evidence can include:

- Threat reports
- Malware analysis
- SIEM logs
- EDR telemetry
- DNS logs
- Firewall logs
- Vulnerability scans
- Security advisories
- Internal incident records

Avoid unsupported conclusions.


---

## 23. Threat Actor Analysis

Document:

- Name
- Aliases
- Motivation
- Target sectors
- Geographic focus
- Known campaigns
- Malware
- Infrastructure
- TTPs
- Confidence

Example:

    Threat Actor
        ↓
    Motivation
        ↓
    Target
        ↓
    Campaign
        ↓
    Malware
        ↓
    TTPs
        ↓
    Infrastructure


---

## 24. TTP Analysis

Map observed attacker behavior to a recognized framework such as MITRE ATT&CK.

Example:

| Tactic | Technique | Observation |
|---|---|---|
| Initial Access | Phishing | Malicious email |
| Execution | PowerShell | Script execution |
| Credential Access | Credential Dumping | Credential theft |
| Discovery | System Discovery | Host enumeration |
| Command and Control | Application Layer Protocol | C2 traffic |

TTPs often remain useful even when individual IOCs change.


---

## 25. Attack Chain

A report should explain how the attack works.

Example:

Phishing
   ↓
Malicious Link
   ↓
Credential Theft
   ↓
Valid Account
   ↓
PowerShell
   ↓
Payload
   ↓
C2
   ↓
Lateral Movement
   ↓
Impact


---

## 26. Infrastructure Analysis

Document relevant infrastructure:

- IP addresses
- Domains
- URLs
- Hosting
- Certificates
- DNS
- Autonomous Systems
- C2 infrastructure

Example:

Threat Actor
      ↓
C2 Domain
      ↓
IP Address
      ↓
Hosting Provider


---

## 27. Indicator Context

Do not publish indicators without context.

Instead of:

    IP: 203.0.113.10

Use:

    Indicator:
    203.0.113.10

    Type:
    IPv4

    Associated Activity:
    C2 infrastructure

    Confidence:
    High

    First Seen:
    Date

    Last Seen:
    Date

    Source:
    Threat Research


---

## 28. Timeline

A timeline helps explain the evolution of an incident or campaign.

Example:

| Date | Event |
|---|---|
| Day 1 | Phishing infrastructure registered |
| Day 3 | Malicious emails distributed |
| Day 4 | Credentials harvested |
| Day 5 | C2 activity observed |
| Day 6 | Malware deployed |
| Day 7 | Campaign publicly reported |

Use UTC or clearly state the timezone when precise timing matters.


---

## 29. Internal Exposure Assessment

External intelligence should be compared with internal data.

Example:

External Threat
      ↓
IOC Collection
      ↓
Internal Search
      ↓
SIEM
      ↓
EDR
      ↓
DNS
      ↓
Firewall
      ↓
Result


Possible outcomes:

### Confirmed Exposure

Internal evidence matches.

### Potential Exposure

Affected systems exist but no malicious activity confirmed.

### No Evidence

No relevant internal evidence identified.

### Unknown

Insufficient telemetry.


---

## 30. Risk Assessment

Risk should consider:

- Threat likelihood
- Impact
- Asset criticality
- Exploitation activity
- Exposure
- Confidence

Example:

    Likelihood: High
    Impact: High
    Exposure: Medium
    Confidence: High

    Overall Risk:
    High


---

## 31. Risk Matrix

Example:

| Likelihood | Impact | Risk |
|---|---|---|
| Low | Low | Low |
| Low | High | Medium |
| Medium | Medium | Medium |
| High | Medium | High |
| High | High | Critical |

The exact scoring methodology should be documented by the organization.


---

## 32. Confidence Assessment

Every major assessment should communicate confidence.

Example:

### High Confidence

Multiple reliable sources and internal evidence support the assessment.

### Medium Confidence

Evidence supports the assessment but additional validation is required.

### Low Confidence

Limited or conflicting evidence exists.


---

## 33. Sources

Document intelligence sources.

Example:

| Source | Type | Reliability | Used For |
|---|---|---|---|
| Security Vendor | External | High | Threat Actor |
| CERT Advisory | Government | High | Vulnerability |
| Internal SIEM | Internal | High | Exposure |
| Threat Feed | External | Medium/High | IOC |

Do not use a source without evaluating its reliability.


---

## 34. Recommendations

Recommendations should be actionable.

Weak:

"Improve security."

Better:

- Patch affected systems.
- Search SIEM for associated indicators.
- Hunt for related TTPs.
- Block confirmed malicious infrastructure.
- Reset compromised credentials if required.
- Update detection rules.
- Monitor related infrastructure.


---

## 35. Detection Recommendations

Translate intelligence into detections.

Example:

Threat Intelligence
      ↓
IOC
      ↓
Detection Rule
      ↓
SIEM
      ↓
Alert

Also consider behavioral detections:

TTP
 ↓
Detection Logic
 ↓
SIEM / EDR
 ↓
Alert


---

## 36. Threat Hunting Recommendations

Example:

Threat Intelligence identifies PowerShell-based execution.

Hunting hypothesis:

"An attacker may be using PowerShell to execute a downloaded payload."

Search:

- PowerShell logs
- Process creation
- Parent-child relationships
- Network connections
- File creation
- EDR telemetry


---

## 37. Mitigation Recommendations

Mitigation can include:

- Patching
- Credential resets
- Network segmentation
- EDR rules
- Email filtering
- Firewall controls
- DNS filtering
- Application controls
- User awareness
- Monitoring


---

## 38. Report Quality

A high-quality report should be:

- Accurate
- Relevant
- Timely
- Concise
- Evidence-based
- Actionable
- Audience-specific
- Traceable

Avoid unnecessary technical information.


---

## 39. Intelligence vs Information

Information:

"An IP address was observed."

Intelligence:

"An IP address associated with a known C2 infrastructure was observed communicating with an internal endpoint, creating a potential compromise requiring investigation."

The second statement provides:

- Context
- Assessment
- Risk
- Action


---

## 40. Writing Style

Professional intelligence writing should be:

- Clear
- Direct
- Objective
- Evidence-based
- Neutral
- Precise

Avoid:

- Emotional language
- Unsupported claims
- Excessive jargon
- Speculation presented as fact


---

## 41. Assessment Language

Use appropriate language:

### Confirmed

Evidence directly supports the conclusion.

### Likely

Evidence strongly supports the conclusion.

### Possible

Evidence supports the possibility but is insufficient for a strong assessment.

### Unknown

Insufficient information exists.

This prevents analysts from overstating confidence.


---

## 42. Report Classification

Organizations may classify reports based on sensitivity.

Examples:

- Public
- Internal
- Confidential
- Restricted

The exact classification system depends on organizational policy.

Always follow information handling requirements.


---

## 43. Traffic Light Protocol

Threat intelligence communities may use the Traffic Light Protocol to communicate sharing restrictions.

Common concepts include:

- RED
- AMBER
- GREEN
- CLEAR

Always follow the current TLP specification and the organization's sharing policy.


---

## 44. STIX/TAXII Reporting Integration

Threat intelligence reports can be represented using structured intelligence.

Example:

Report
 ↓
STIX Objects
 ↓
Indicators
 ↓
Threat Actor
 ↓
Malware
 ↓
Campaign
 ↓
Relationships
 ↓
TAXII
 ↓
Threat Intelligence Platform


---

## 45. Automated Report Generation

Automation can generate initial report components.

Example:

Threat Feed
      ↓
Data Collection
      ↓
IOC Extraction
      ↓
Enrichment
      ↓
Threat Scoring
      ↓
Report Template
      ↓
Draft Intelligence Report
      ↓
Analyst Review
      ↓
Final Report


---

## 46. AI-Assisted Reporting

AI can assist with:

- Report summarization
- IOC extraction
- TTP extraction
- Timeline creation
- Threat actor profiling
- Relationship mapping
- Executive summary generation
- Technical summary generation
- Recommendation drafting

AI-generated reports must be validated before distribution.


---

## 47. AI Report Generation Workflow

Threat Intelligence
      ↓
AI Processing
      ↓
Extract Findings
      ↓
Generate Draft
      ↓
Analyst Validation
      ↓
Evidence Verification
      ↓
Final Report
      ↓
Dissemination


---

## 48. AI Hallucination Risk in Reporting

AI may:

- Invent sources
- Invent relationships
- Misinterpret technical information
- Incorrectly attribute threat actors
- Generate unsupported conclusions
- Misrepresent confidence

Controls:

- Source verification
- Evidence checking
- Analyst review
- Structured templates
- Citation validation
- Human approval


---

## 49. Executive Report Automation

A technical report can be transformed into an executive brief.

Technical Intelligence
      ↓
AI / Automation
      ↓
Business Impact
      ↓
Risk Summary
      ↓
Recommended Actions
      ↓
Executive Brief


---

## 50. Multi-Level Reporting

One intelligence event can produce multiple outputs.

Example:

Threat Event
      ↓
Technical Report
      ↓
SOC Detection
      ↓
Threat Hunting Brief
      ↓
Incident Response Brief
      ↓
Executive Summary


---

## 51. Intelligence Reporting Pipeline

A mature reporting architecture:

Collection
   ↓
Processing
   ↓
Enrichment
   ↓
Analysis
   ↓
Assessment
   ↓
Report Generation
   ↓
Analyst Validation
   ↓
Classification
   ↓
Dissemination
   ↓
Feedback


---

## 52. Reporting Automation Architecture

Example:

             Threat Sources
                   ↓
              CTI Pipeline
                   ↓
              TIP / Database
                   ↓
             Analysis Engine
                   ↓
             Scoring Engine
                   ↓
           Report Generator
              ↙    ↓    ↘
          SOC   Management   IR
           ↓        ↓         ↓
        Technical Executive Operational


---

## 53. Report Version Control

Reports may change as new intelligence becomes available.

Example:

Version 1.0
    ↓
Initial Assessment

Version 1.1
    ↓
New IOC Added

Version 1.2
    ↓
Threat Actor Attribution Updated

Version 2.0
    ↓
Major New Evidence


Maintain:

- Version
- Date
- Author
- Reviewer
- Changes
- Confidence


---

## 54. Report Review Process

Recommended workflow:

Analyst Draft
      ↓
Peer Review
      ↓
Technical Validation
      ↓
Classification Review
      ↓
Approval
      ↓
Dissemination


For high-impact intelligence, multiple levels of review may be appropriate.


---

## 55. Report Feedback

After dissemination, collect feedback.

Questions:

- Was the report useful?
- Was it timely?
- Was the information accurate?
- Did it support a decision?
- Did it improve detection?
- Did analysts need additional information?


---

## 56. Reporting Metrics

Useful metrics include:

### Timeliness

Time from intelligence discovery to report publication.

### Accuracy

Percentage of assessments later confirmed.

### Relevance

Percentage of reports useful to intended consumers.

### Actionability

Percentage resulting in a security action.

### Engagement

Number of consumers using the report.

### Detection Impact

Number of detections created from intelligence.


---

## 57. Mean Time to Report

Example:

Threat Identified:
09:00

Analysis Completed:
09:30

Report Published:
09:40

Mean Time to Report:

40 minutes


Automation can reduce report preparation time.


---

## 58. Report Templates

A standardized template improves consistency.

Recommended template:

```text
Title
Date
Classification
Author
Reviewer

Executive Summary

Threat Overview

Key Findings

Threat Actor

Campaign

TTPs

Infrastructure

Indicators

Timeline

Internal Exposure

Risk Assessment

Confidence

Detection

Mitigation

Recommendations

Sources

Appendix
