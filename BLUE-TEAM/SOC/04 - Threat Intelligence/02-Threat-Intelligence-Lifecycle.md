# Threat Intelligence Lifecycle

## 1. Introduction

The Threat Intelligence Lifecycle is a structured process used to transform raw threat information into actionable intelligence.

It ensures that threat intelligence is:

- Relevant
- Accurate
- Timely
- Actionable
- Contextual
- Continuously improved

The lifecycle is not a one-time process. It is a continuous feedback loop.

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
    Feedback
        ↓
    Direction


---

## 2. Purpose

The Threat Intelligence Lifecycle helps organizations:

- Identify relevant threats
- Collect appropriate information
- Process large amounts of data
- Analyze attacker activity
- Produce actionable intelligence
- Deliver intelligence to the right teams
- Improve security controls
- Measure intelligence effectiveness


---

## 3. Threat Intelligence Lifecycle Model

A practical lifecycle consists of six major stages:

1. Direction
2. Collection
3. Processing
4. Analysis
5. Dissemination
6. Feedback


Complete model:

    ┌───────────────┐
    │   Direction   │
    └───────┬───────┘
            ↓
    ┌───────────────┐
    │   Collection  │
    └───────┬───────┘
            ↓
    ┌───────────────┐
    │   Processing  │
    └───────┬───────┘
            ↓
    ┌───────────────┐
    │    Analysis   │
    └───────┬───────┘
            ↓
    ┌───────────────┐
    │ Dissemination │
    └───────┬───────┘
            ↓
    ┌───────────────┐
    │    Feedback   │
    └───────┬───────┘
            │
            └────────→ Direction


---

## 4. Stage 1 — Direction

Direction defines what the organization needs to know.

It answers:

- What information is required?
- Why is it required?
- Who needs it?
- How quickly is it required?
- What decision will it support?


Example:

    Business Concern:
    Ransomware

          ↓

    Intelligence Requirement:
    Which ransomware groups
    target our industry?

          ↓

    Collection Requirement:
    Gather current ransomware
    campaign intelligence.


---

## 5. Intelligence Requirements

An Intelligence Requirement (IR) is a question that intelligence should answer.

Example:

> Are any threat actors currently targeting our industry?

Another example:

> Are our externally exposed assets associated with actively exploited vulnerabilities?


Intelligence requirements prevent teams from collecting unnecessary information.


---

## 6. Priority Intelligence Requirements

A Priority Intelligence Requirement (PIR) is a high-priority intelligence question.

Example:

    PIR:
    Are our public-facing systems
    being targeted by active campaigns?


A PIR may receive:

- Higher collection priority
- Faster analysis
- More resources
- More frequent reporting


---

## 7. Direction and Business Objectives

Threat intelligence should support business objectives.

Example:

    Business Objective:
    Protect customer data

          ↓

    Security Concern:
    Credential theft

          ↓

    Intelligence Requirement:
    Which credential-stealing
    campaigns target our sector?


This ensures intelligence remains relevant to the organization.


---

## 8. Direction Questions

During direction, define:

### What?

What threat information is required?

### Why?

Why does the organization need it?

### Who?

Who will use the intelligence?

### When?

When is the intelligence required?

### Action?

What action should the intelligence enable?


---

# 9. Stage 2 — Collection

Collection is the process of gathering relevant threat information.

Sources may include:

- Open-source intelligence
- Threat intelligence feeds
- Security vendors
- Government advisories
- CERT organizations
- Security researchers
- Internal security logs
- Incident reports
- Malware analysis
- Vulnerability databases
- Dark web monitoring where legally and appropriately conducted


Collection should be guided by intelligence requirements.


---

## 10. Internal Collection

Internal data can provide valuable intelligence.

Sources include:

- SIEM
- EDR
- Firewall logs
- DNS logs
- Proxy logs
- Authentication logs
- Email security
- Cloud logs
- IDS/IPS
- Incident reports


Example:

    External Intelligence
            +
    Internal Telemetry
            ↓
       Correlation
            ↓
       Investigation


---

## 11. External Collection

External intelligence may include:

- Threat reports
- Malware research
- Vulnerability advisories
- Threat feeds
- Security blogs
- CERT advisories
- Industry reports
- Threat actor infrastructure
- Public security research


External intelligence provides broader visibility into the threat landscape.


---

## 12. Open Source Intelligence

OSINT refers to intelligence gathered from publicly available information.

Examples:

- Security publications
- Government websites
- Security research
- Public databases
- Public technical documentation
- Security communities


OSINT should still be validated before being used operationally.


---

## 13. Threat Feeds

Threat feeds provide structured or semi-structured threat information.

Examples:

- Malicious IP feeds
- Malware feeds
- Phishing feeds
- Botnet feeds
- Domain feeds
- Vulnerability feeds


Feed quality should be evaluated before integration.


---

## 14. Collection Challenges

Common collection challenges include:

- Excessive data volume
- Duplicate information
- Untrusted sources
- Outdated indicators
- Missing context
- Inconsistent formats
- Collection bias


The goal is:

    Relevant Data
        ≠
    Maximum Data


---

# 15. Stage 3 — Processing

Processing converts collected information into a usable format.

Raw intelligence may contain:

- Duplicate indicators
- Different formats
- Invalid values
- Missing fields
- Unstructured text
- Different timestamps
- Different naming conventions


Processing improves consistency.


---

## 16. Data Normalization

Normalization converts information into a common format.

Example:

    Raw Data:

    8.8.8.8
    8.8.8.8/32
    IPv4: 8.8.8.8


Normalized:

    Indicator Type:
    IPv4

    Indicator:
    8.8.8.8


This makes correlation easier.


---

## 17. Deduplication

The same indicator may appear in multiple sources.

Example:

    Feed A:
    192.x.x.x

    Feed B:
    192.x.x.x

    Feed C:
    192.x.x.x


Instead of storing three duplicate entries:

    192.x.x.x


Store one indicator with multiple sources.

Example:

    Indicator:
    192.x.x.x

    Sources:
    Feed A
    Feed B
    Feed C


---

## 18. Data Validation

Validation checks whether information is:

- Correctly formatted
- Current
- Relevant
- Supported by evidence
- From a reliable source


Example:

    Domain:
    malicious-example.com

    Check:
    Valid domain?

    Check:
    Current activity?

    Check:
    Multiple sources?

    Result:
    Validated


---

## 19. Enrichment

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
    Historical DNS
        ↓
    Malware Association
        ↓
    Threat Actor


Enrichment makes intelligence more useful to analysts.


---

## 20. Processing Automation

Processing can be automated using:

- Python
- APIs
- SIEM
- SOAR
- Threat intelligence platforms
- Data pipelines


Example:

    Threat Feed
        ↓
    Python
        ↓
    Normalize
        ↓
    Deduplicate
        ↓
    Validate
        ↓
    Enrich
        ↓
    Store


---

# 21. Stage 4 — Analysis

Analysis transforms processed information into intelligence.

Analysts determine:

- What happened?
- Who may be responsible?
- What techniques were used?
- Who is being targeted?
- What infrastructure is involved?
- What is the likely impact?
- How relevant is the threat to the organization?


---

## 22. Contextual Analysis

A raw indicator may have limited value.

Example:

    IP:
    192.x.x.x


After analysis:

    IP:
    192.x.x.x

    Associated Malware:
    Example RAT

    Infrastructure:
    C2 Server

    ATT&CK:
    Command and Control

    Target:
    Financial Sector

    Confidence:
    High


Now the indicator has meaningful context.


---

## 23. Correlation

Correlation connects related information.

Example:

    IP
     ↓
    Domain
     ↓
    Malware
     ↓
    Threat Actor
     ↓
    Campaign


Correlation can reveal relationships that individual indicators cannot.


---

## 24. Threat Actor Analysis

Analysts may evaluate:

- Threat actor identity
- Motivation
- Capabilities
- Targeting
- Infrastructure
- TTPs
- Historical activity


Example:

    Threat Actor
         ↓
    Motivation
         ↓
    Target
         ↓
    TTPs
         ↓
    Infrastructure
         ↓
    Campaign


Attribution should be based on evidence and confidence.


---

## 25. TTP Analysis

TTP analysis focuses on attacker behavior.

Example:

    Phishing
       ↓
    Credential Theft
       ↓
    Valid Account Use
       ↓
    Lateral Movement
       ↓
    Data Exfiltration


This behavioral understanding can support detection engineering.


---

## 26. MITRE ATT&CK Mapping

Threat intelligence can be mapped to MITRE ATT&CK.

Example:

    Phishing
       ↓
    T1566


    Valid Accounts
       ↓
    T1078


    PowerShell
       ↓
    T1059.001


ATT&CK mapping helps translate intelligence into defensive actions.


---

## 27. Relevance Assessment

Not every threat is equally important to an organization.

Evaluate:

- Industry
- Geography
- Technology
- Assets
- Exposure
- Threat actor targeting
- Vulnerability status
- Existing controls


Example:

    Threat:
    Active ransomware campaign

          ↓

    Organization:
    Healthcare

          ↓

    Relevance:
    High


---

## 28. Confidence Assessment

Intelligence should include confidence.

Example:

    Confidence:
    High


Possible levels:

- High
- Medium
- Low


Confidence should be based on evidence and source reliability.


---

## 29. Risk Assessment

Threat intelligence can contribute to risk analysis.

Example:

    Active Exploitation
          +
    Vulnerable Asset
          +
    Internet Exposure
          +
    Critical Business Function
          ↓
       High Risk


---

# 30. Stage 5 — Dissemination

Dissemination means delivering intelligence to the people or systems that need it.

The format should match the audience.


---

## 31. SOC Dissemination

SOC analysts may need:

- IoCs
- TTPs
- Detection rules
- Search queries
- Threat actor information
- Investigation recommendations


Example:

    Threat Intelligence
          ↓
    SIEM Watchlist
          ↓
    Alert
          ↓
    SOC Investigation


---

## 32. Threat Hunting Dissemination

Threat hunters may need:

- Hunting hypotheses
- TTPs
- IoCs
- Malware behavior
- Suspicious infrastructure


Example:

    Threat Report
         ↓
    Hunting Hypothesis
         ↓
    SIEM Query
         ↓
    Internal Search


---

## 33. Incident Response Dissemination

Incident responders may need:

- Related IoCs
- Malware information
- Threat actor details
- Attack techniques
- Infrastructure
- Containment recommendations


---

## 34. Vulnerability Management Dissemination

Vulnerability teams may need:

- Exploited CVEs
- Exploitation campaigns
- Threat actor targeting
- Vulnerable technology
- Recommended remediation priority


---

## 35. Executive Dissemination

Executives generally need:

- Threat overview
- Business impact
- Risk
- Trend
- Strategic recommendations


Example:

    Threat:
    Ransomware

    Business Risk:
    Operational disruption

    Recommendation:
    Improve backup resilience
    and recovery testing.


---

## 36. Intelligence Products

Common intelligence products include:

- Intelligence briefs
- Threat reports
- IoC lists
- Threat actor profiles
- Campaign reports
- Executive summaries
- Detection recommendations
- Threat hunting reports


---

# 37. Stage 6 — Feedback

Feedback determines whether intelligence was useful.

Questions include:

- Was the intelligence relevant?
- Was it timely?
- Was it accurate?
- Did analysts use it?
- Did it improve detection?
- Did it support a decision?
- Did it reduce risk?


---

## 38. Feedback Loop

    Intelligence
         ↓
    Dissemination
         ↓
    Operational Use
         ↓
    Analyst Feedback
         ↓
    Intelligence Improvement
         ↓
    Better Collection


This closes the lifecycle.


---

## 39. Example Feedback

Suppose a threat feed produces:

    1000 Indicators

SOC analysts discover:

    800 are irrelevant
    150 are outdated
     50 are useful


Feedback:

    Feed Quality = Poor


Action:

    Change feed source
    +
    Add filtering
    +
    Add validation


The lifecycle improves.


---

# 40. Complete Lifecycle Example

### Scenario

A company wants to understand ransomware threats targeting its industry.


### Direction

    Question:
    Which ransomware groups
    target our industry?


### Collection

Gather:

- Threat reports
- Ransomware intelligence
- IoCs
- TTPs
- Vulnerability information


### Processing

    Normalize
    ↓
    Deduplicate
    ↓
    Validate
    ↓
    Enrich


### Analysis

Identify:

- Threat actors
- TTPs
- Malware
- Infrastructure
- Targeting
- Exploited vulnerabilities


### Dissemination

Deliver:

- Executive report
- SOC detections
- Threat hunting queries
- Vulnerability priorities


### Feedback

Ask:

- Did the intelligence help?
- Were detections effective?
- Were the right assets protected?


Then restart the lifecycle.


---

# 41. Threat Intelligence Lifecycle and SOC

The lifecycle connects directly to SOC operations.

    Intelligence
        ↓
    Detection
        ↓
    Investigation
        ↓
    Incident Response
        ↓
    Lessons Learned
        ↓
    New Intelligence Requirement


This creates continuous improvement.


---

# 42. Threat Intelligence Lifecycle and Threat Hunting

    Threat Intelligence
          ↓
    TTP Identification
          ↓
    Hunting Hypothesis
          ↓
    Query Development
          ↓
    SIEM Search
          ↓
    Evidence
          ↓
    Intelligence Update


Threat hunting can therefore generate new intelligence.


---

# 43. Threat Intelligence Lifecycle and Detection Engineering

    Threat Intelligence
          ↓
    Attack Technique
          ↓
    Detection Requirement
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


This turns intelligence into defensive capability.


---

# 44. Threat Intelligence Lifecycle and Incident Response

    Incident
       ↓
    IoCs
       ↓
    Intelligence Enrichment
       ↓
    Threat Actor / Malware
       ↓
    Related IoCs
       ↓
    Environment-Wide Search
       ↓
    Containment
       ↓
    Lessons Learned
       ↓
    New Intelligence


---

# 45. Threat Intelligence Lifecycle and Vulnerability Management

    Threat Intelligence
         ↓
    Active Exploitation
         ↓
    Vulnerability Identified
         ↓
    Asset Inventory
         ↓
    Exposure Check
         ↓
    Risk Prioritization
         ↓
    Remediation
         ↓
    Validation


---

# 46. Automation Across the Lifecycle

Automation can support every stage.

### Direction

Automated collection of intelligence requirements.


### Collection

Automated feed ingestion.


### Processing

Automated:

- Normalization
- Deduplication
- Validation


### Analysis

Automated:

- Enrichment
- Correlation
- ATT&CK mapping


### Dissemination

Automated:

- SIEM updates
- Ticket creation
- Notifications


### Feedback

Automated:

- KPI collection
- Feed performance analysis


---

# 47. AI Across the Lifecycle

AI can assist with:

    Direction
       ↓
    Identify intelligence gaps

    Collection
       ↓
    Summarize sources

    Processing
       ↓
    Extract IoCs

    Analysis
       ↓
    Identify patterns

    Dissemination
       ↓
    Generate reports

    Feedback
       ↓
    Analyze intelligence effectiveness


Human validation should remain part of high-impact decisions.


---

# 48. AI-Assisted Lifecycle Workflow

    Threat Reports
         ↓
    AI Extraction
         ↓
    IoCs
         ↓
    TTPs
         ↓
    Threat Actors
         ↓
    ATT&CK Mapping
         ↓
    Analyst Validation
         ↓
    Intelligence Product
         ↓
    SOC / IR / Hunting
         ↓
    Feedback


---

# 49. Measuring Lifecycle Effectiveness

Useful metrics include:

- Intelligence production time
- Intelligence usage rate
- IoC validation rate
- Feed precision
- False-positive rate
- Intelligence timeliness
- Detection improvement
- Threat hunting discoveries
- Vulnerability prioritization impact
- Incident response improvement


---

# 50. Threat Intelligence Lifecycle Maturity

### Level 1 — Ad Hoc

Intelligence is collected reactively.


### Level 2 — Repeatable

Basic collection and reporting processes exist.


### Level 3 — Integrated

Intelligence is integrated with:

- SIEM
- SOC
- Threat hunting
- Incident response


### Level 4 — Proactive

Intelligence drives:

- Detection
- Vulnerability prioritization
- Threat hunting


### Level 5 — Intelligence-Led

Intelligence continuously influences:

- Security strategy
- Risk management
- Detection engineering
- Incident response
- Business decisions


---

# 51. Common Lifecycle Problems

### Problem 1 — No Clear Direction

Result:

    Large Data Volume
        ↓
    Little Actionable Intelligence


### Problem 2 — Poor Collection

Result:

    Missing Threat Information


### Problem 3 — Weak Processing

Result:

    Duplicate / Invalid Data


### Problem 4 — Poor Analysis

Result:

    Intelligence Without Context


### Problem 5 — Poor Dissemination

Result:

    Intelligence Not Used


### Problem 6 — No Feedback

Result:

    Same Problems Repeated


---

# 52. Best Practices

- Define intelligence requirements
- Prioritize relevant threats
- Use multiple trusted sources
- Validate indicators
- Remove duplicates
- Enrich indicators
- Map threats to ATT&CK
- Integrate intelligence with SOC tools
- Create actionable reports
- Measure intelligence effectiveness
- Collect analyst feedback
- Automate repetitive work
- Use AI with human validation
- Continuously improve the lifecycle


---

# 53. Practical Lab

## Threat Intelligence Lifecycle Lab

### Objective

Build a complete intelligence lifecycle using a suspicious IP.

### Step 1 — Direction

Define:

    Intelligence Requirement:

    Is this IP associated with
    malicious activity relevant
    to our environment?


### Step 2 — Collection

Collect:

- Reputation
- Threat feeds
- Historical data
- Related domains
- Malware information


### Step 3 — Processing

Perform:

- Normalization
- Deduplication
- Validation


### Step 4 — Analysis

Determine:

- Threat type
- Malware
- Threat actor
- TTPs
- ATT&CK techniques
- Confidence


### Step 5 — Dissemination

Create:

- Intelligence report
- IoC
- SIEM watchlist
- Hunting hypothesis


### Step 6 — Feedback

Record:

- Analyst feedback
- Detection result
- Investigation result
- Intelligence usefulness


---

# 54. Portfolio Project

## Project: Automated Threat Intelligence Lifecycle

### Objective

Build an automated workflow that transforms raw threat feeds into actionable intelligence.

### Architecture

    Threat Feeds
         ↓
    Python Collector
         ↓
    Normalization
         ↓
    Deduplication
         ↓
    Enrichment
         ↓
    Scoring
         ↓
    Threat Intelligence Platform
         ↓
    SIEM
         ↓
    SOC Alert
         ↓
    Analyst Investigation


### AI Component

Add:

    Threat Reports
         ↓
    AI Extraction
         ↓
    IoCs + TTPs
         ↓
    ATT&CK Mapping
         ↓
    Analyst Validation
         ↓
    Intelligence Report


### Evidence

Document:

- Architecture
- Data flow
- Python scripts
- API integrations
- Sample indicators
- Enrichment results
- ATT&CK mappings
- SIEM integration
- Screenshots
- Test results
- Lessons learned


---

# 55. Professional Work Sample

Create a sample report containing:

### Executive Summary

Short description of the threat.


### Intelligence Requirement

The question being answered.


### Collection

Sources used.


### Analysis

Threat actor, malware, infrastructure and TTP analysis.


### IoCs

Relevant indicators.


### ATT&CK Mapping

Associated techniques.


### Risk

Potential impact.


### Recommendations

Recommended defensive actions.


### Confidence

Assessment of intelligence reliability.


---

# 56. Teaching Knowledge Base

This document can be used to teach:

- Threat Intelligence fundamentals
- Intelligence requirements
- Intelligence lifecycle
- Threat feeds
- IoCs
- Threat actors
- TTPs
- Intelligence analysis
- Intelligence reporting
- Automation
- AI-assisted intelligence


Teaching structure:

    Concept
       ↓
    Example
       ↓
    Workflow
       ↓
    Lab
       ↓
    Project
       ↓
    Professional Use Case


---

# 57. Interview Questions

### Basic

1. What is the Threat Intelligence Lifecycle?
2. What are the stages of the lifecycle?
3. What is the purpose of the Direction phase?
4. What is an Intelligence Requirement?
5. What is the difference between collection and processing?


### Intermediate

6. Why is feedback important?
7. How does threat intelligence support a SOC?
8. How does threat intelligence support threat hunting?
9. What is the role of enrichment?
10. How can threat intelligence improve vulnerability prioritization?


### Advanced

11. How would you automate the Threat Intelligence Lifecycle?
12. How would you evaluate the quality of a threat feed?
13. How would you integrate threat intelligence into a SIEM?
14. How could AI assist the intelligence lifecycle?
15. How would you prevent poor-quality intelligence from affecting SOC decisions?


---

# 58. Key Takeaways

The Threat Intelligence Lifecycle transforms raw information into actionable intelligence.

The six major stages are:

    1. Direction
    2. Collection
    3. Processing
    4. Analysis
    5. Dissemination
    6. Feedback


The process is continuous:

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
    Feedback
       ↓
    Improved Direction


The lifecycle becomes more valuable when integrated with:

- SOC
- SIEM
- Threat Hunting
- Incident Response
- Detection Engineering
- Vulnerability Management
- Automation
- AI


---

# 59. Final Principle

> **The Threat Intelligence Lifecycle exists to ensure that the right threat information is collected, analyzed, delivered to the right people, converted into defensive action, and continuously improved through feedback.**

Final model:

    Question
       ↓
    Collect
       ↓
    Process
       ↓
    Analyze
       ↓
    Communicate
       ↓
    Act
       ↓
    Measure
       ↓
    Learn
       ↓
    Ask Better Questions
