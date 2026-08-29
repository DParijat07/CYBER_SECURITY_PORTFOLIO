# Threat Intelligence Types

## 1. Introduction

Threat Intelligence can be classified into different types based on its purpose, audience, level of detail, and operational use.

The four primary types are:

1. Strategic Threat Intelligence
2. Tactical Threat Intelligence
3. Operational Threat Intelligence
4. Technical Threat Intelligence

Each type answers different security questions.

    Strategic
        ↓
    Business Risk

    Tactical
        ↓
    Attacker Behavior

    Operational
        ↓
    Campaign Activity

    Technical
        ↓
    Indicators and Technical Evidence


---

# 2. Why Classify Threat Intelligence?

Different teams require different types of intelligence.

For example:

### Executive

Needs to understand:

- Business risk
- Threat trends
- Strategic priorities


### SOC Analyst

Needs:

- IoCs
- TTPs
- Detection information


### Threat Hunter

Needs:

- Attacker behavior
- TTPs
- Hunting hypotheses


### Incident Responder

Needs:

- Malware
- Infrastructure
- Threat actor information
- Related indicators


Therefore:

    One Threat
         ↓
    Multiple Intelligence Products
         ↓
    Different Audiences


---

# 3. Primary Types of Threat Intelligence

The four major categories are:

| Type | Primary Focus | Typical Audience |
|---|---|---|
| Strategic | Business risk and trends | Executives, CISOs |
| Tactical | Attacker behavior and TTPs | SOC, Threat Hunters |
| Operational | Campaigns and attacker operations | CTI, IR, SOC |
| Technical | Indicators and technical artifacts | SOC, IR, Detection Engineers |

These categories can overlap.


---

# 4. Strategic Threat Intelligence

Strategic Threat Intelligence focuses on the broader threat landscape and its potential impact on the organization.

It answers questions such as:

- What threats should leadership worry about?
- Which threat trends affect our industry?
- Which threat actors target our organization?
- What is the potential business impact?
- Where should security resources be invested?


---

# 5. Strategic Intelligence Audience

Typical users include:

- CEO
- CIO
- CISO
- Security leadership
- Risk management
- Board members
- Business leadership


Strategic intelligence should generally avoid unnecessary technical details.


---

# 6. Strategic Intelligence Examples

Examples include:

- Ransomware trends
- Nation-state cyber activity
- Industry targeting
- Geopolitical cyber risks
- Supply-chain threats
- Emerging attack trends
- Cybercrime trends
- Strategic vulnerability risks


Example:

    Threat:
    Ransomware

    Target:
    Financial organizations

    Business Risk:
    Operational disruption

    Strategic Recommendation:
    Improve backup and recovery
    capabilities.


---

# 7. Strategic Intelligence Characteristics

Strategic intelligence is generally:

- High-level
- Business-focused
- Long-term
- Risk-oriented
- Decision-oriented


It should answer:

> "What does this threat mean for the organization?"


---

# 8. Strategic Intelligence Workflow

    Threat Landscape
          ↓
    Trend Analysis
          ↓
    Business Impact
          ↓
    Risk Assessment
          ↓
    Strategic Recommendation
          ↓
    Leadership Decision


---

# 9. Strategic Intelligence Example

### Scenario

A company operates in the healthcare industry.

Threat intelligence identifies an increase in ransomware campaigns targeting healthcare organizations.

Strategic analysis:

    Ransomware
        ↓
    Healthcare Targeting
        ↓
    Increased Probability
        ↓
    Operational Risk
        ↓
    Business Impact


Possible recommendations:

- Improve backup strategy
- Test disaster recovery
- Improve endpoint protection
- Increase employee awareness
- Prioritize exposed vulnerabilities


---

# 10. Tactical Threat Intelligence

Tactical Threat Intelligence focuses on how attackers operate.

It commonly describes:

- Tactics
- Techniques
- Procedures
- Attack patterns
- Behavioral indicators


It answers:

> "How does the attacker perform the attack?"


---

# 11. Tactical Intelligence Audience

Typical users include:

- SOC analysts
- Threat hunters
- Detection engineers
- Incident responders
- Security engineers


---

# 12. Tactical Intelligence Examples

Examples:

- PowerShell execution
- Credential dumping
- Phishing
- Lateral movement
- Pass-the-Hash
- Remote Services
- Command and Control techniques
- Data exfiltration methods


---

# 13. Tactical Intelligence and MITRE ATT&CK

Tactical intelligence frequently uses MITRE ATT&CK.

Example:

    Tactic:
    Credential Access

          ↓

    Technique:
    OS Credential Dumping

          ↓

    Detection:
    Suspicious LSASS Access


Another example:

    Tactic:
    Execution

          ↓

    Technique:
    PowerShell

          ↓

    Detection:
    Suspicious PowerShell Activity


---

# 14. Tactical Intelligence Workflow

    Threat Report
         ↓
    Identify TTPs
         ↓
    Map to ATT&CK
         ↓
    Create Detection
         ↓
    Threat Hunting
         ↓
    Improve Defensive Controls


---

# 15. Tactical Intelligence Example

Suppose a threat actor commonly uses:

    Phishing
       ↓
    Malicious Attachment
       ↓
    PowerShell
       ↓
    Credential Theft
       ↓
    Lateral Movement


The SOC can use this information to:

- Build detection rules
- Create hunting queries
- Monitor suspicious PowerShell
- Monitor credential access
- Investigate lateral movement


---

# 16. Operational Threat Intelligence

Operational Threat Intelligence focuses on specific threat activity, campaigns, and attacker operations.

It answers:

> "What is the attacker doing, and what operation or campaign is currently occurring?"


---

# 17. Operational Intelligence Audience

Typical users include:

- Threat intelligence analysts
- SOC analysts
- Incident responders
- Threat hunters
- Security operations teams


---

# 18. Operational Intelligence Examples

Examples include:

- Active ransomware campaigns
- Phishing campaigns
- Malware campaigns
- Threat actor operations
- Targeting patterns
- Attack timelines
- Command-and-control infrastructure
- Campaign infrastructure changes


---

# 19. Operational Intelligence Example

Consider a phishing campaign.

    Threat Actor
         ↓
    Phishing Infrastructure
         ↓
    Malicious Emails
         ↓
    Credential Harvesting
         ↓
    Compromised Accounts
         ↓
    Internal Access


Operational intelligence can help determine:

- When the campaign started
- Who is targeted
- What infrastructure is used
- Which malware is involved
- What techniques are used
- What the attacker may do next


---

# 20. Operational Intelligence Workflow

    Campaign Identified
          ↓
    Infrastructure Analysis
          ↓
    Target Analysis
          ↓
    TTP Analysis
          ↓
    Timeline Creation
          ↓
    Internal Environment Search
          ↓
    Defensive Action


---

# 21. Technical Threat Intelligence

Technical Threat Intelligence focuses on specific technical indicators and artifacts.

Examples:

- IP addresses
- Domains
- URLs
- File hashes
- Malware signatures
- Email addresses
- File names
- Registry keys
- User agents
- Certificate fingerprints


It answers:

> "What technical artifacts can we detect or block?"


---

# 22. Technical Intelligence Audience

Typical users include:

- SOC analysts
- Incident responders
- Detection engineers
- Network security teams
- Endpoint security teams
- Security engineers


---

# 23. Technical Intelligence Example

Example indicator:

    IP Address:
    203.x.x.x

Enrichment:

    Type:
    IPv4

    Reputation:
    Malicious

    Associated Malware:
    Example RAT

    Function:
    Command and Control

    Confidence:
    High


This can be used to:

- Search SIEM
- Update firewall rules
- Update EDR indicators
- Create detection rules
- Investigate affected hosts


---

# 24. Technical Intelligence Workflow

    Technical Indicator
          ↓
    Validation
          ↓
    Enrichment
          ↓
    Correlation
          ↓
    Detection
          ↓
    Investigation
          ↓
    Response


---

# 25. Comparing the Four Types

## Strategic

Focus:

    "What does this mean for the business?"


## Tactical

Focus:

    "How does the attacker operate?"


## Operational

Focus:

    "What campaign or operation is happening?"


## Technical

Focus:

    "What technical indicators can we detect?"


Simplified:

    Strategic → Why should leadership care?

    Tactical → How does the attacker operate?

    Operational → What is happening now?

    Technical → What can we detect?


---

# 26. Strategic vs Tactical

| Strategic | Tactical |
|---|---|
| Business focused | Security operations focused |
| Long-term | More operational |
| Risk oriented | Behavior oriented |
| Executive audience | SOC / security audience |
| Threat trends | TTPs |
| Business impact | Attack techniques |


Example:

Strategic:

    Ransomware risk is increasing
    for organizations in our industry.


Tactical:

    Attackers commonly use
    PowerShell and credential dumping.


---

# 27. Tactical vs Operational

| Tactical | Operational |
|---|---|
| Focuses on TTPs | Focuses on campaigns |
| Behavior-oriented | Activity-oriented |
| General attacker methods | Specific operations |
| Supports detection | Supports active investigations |


Example:

Tactical:

    Threat actors use PowerShell
    for execution.


Operational:

    Threat Actor X is currently
    using PowerShell in Campaign Y.


---

# 28. Operational vs Technical

| Operational | Technical |
|---|---|
| Campaign focused | Indicator focused |
| Threat actor activity | IPs, domains, hashes |
| Timeline | Technical artifacts |
| Context-heavy | Machine-readable |
| Investigation support | Detection/blocking |


Example:

Operational:

    A phishing campaign is targeting
    employees in our industry.


Technical:

    phishing-example.com
    203.x.x.x
    SHA256: ...


---

# 29. Intelligence Types Working Together

The four intelligence types should not operate independently.

Example:

    Strategic
       ↓
    Ransomware Risk

       ↓

    Operational
       ↓
    Active Ransomware Campaign

       ↓

    Tactical
       ↓
    Attacker TTPs

       ↓

    Technical
       ↓
    IPs + Domains + Hashes

       ↓

    SOC
       ↓
    Detection + Investigation


This creates a complete intelligence-to-action workflow.


---

# 30. Intelligence Pyramid

A practical model is:

    ┌───────────────────────────────┐
    │         Strategic             │
    │     Business / Risk           │
    ├───────────────────────────────┤
    │         Operational           │
    │      Campaign / Activity      │
    ├───────────────────────────────┤
    │          Tactical             │
    │         TTP / Behavior        │
    ├───────────────────────────────┤
    │          Technical            │
    │       IoCs / Artifacts        │
    └───────────────────────────────┘


However, this should not be interpreted as a strict hierarchy.

The types complement each other.


---

# 31. Intelligence by Time Horizon

Another useful classification is based on time.

### Strategic

Long-term.

Examples:

- Threat trends
- Industry targeting
- Geopolitical risks


### Operational

Near-term.

Examples:

- Active campaigns
- Current threat actor activity


### Tactical

Persistent attacker behavior.

Examples:

- TTPs
- Attack patterns


### Technical

Immediate operational use.

Examples:

- IP
- Domain
- Hash
- URL


---

# 32. Intelligence by Audience

| Audience | Useful Intelligence |
|---|---|
| Board | Strategic |
| CISO | Strategic + Operational |
| SOC Manager | Operational + Tactical |
| SOC Analyst | Tactical + Technical |
| Threat Hunter | Tactical + Operational |
| Incident Responder | Operational + Technical |
| Detection Engineer | Tactical + Technical |
| Vulnerability Team | Strategic + Operational |
| Security Engineer | Tactical + Technical |


These are practical examples; organizations may structure teams differently.


---

# 33. Intelligence by Output

Different intelligence types can produce different outputs.

### Strategic Output

- Executive brief
- Risk report
- Threat landscape report


### Tactical Output

- TTP report
- ATT&CK mapping
- Detection recommendations


### Operational Output

- Campaign report
- Threat actor activity report
- Incident intelligence


### Technical Output

- IoC list
- Blocklist
- SIEM watchlist
- Detection signatures


---

# 34. Threat Intelligence and SOC Workflow

    External Threat
          ↓
    Strategic Assessment
          ↓
    Operational Campaign
          ↓
    Tactical TTPs
          ↓
    Technical IoCs
          ↓
    SIEM / EDR
          ↓
    SOC Alert
          ↓
    Investigation
          ↓
    Incident Response


This demonstrates how intelligence types can support the complete SOC process.


---

# 35. Threat Intelligence and Detection Engineering

Different intelligence types can contribute to detection.

### Strategic

Identifies important threat priorities.


### Operational

Identifies active campaigns.


### Tactical

Identifies attacker behavior.


### Technical

Provides concrete indicators.


Combined:

    Threat Landscape
          ↓
    Campaign
          ↓
    TTP
          ↓
    IoC
          ↓
    Detection


---

# 36. Threat Intelligence and Threat Hunting

Threat hunting often relies heavily on tactical and operational intelligence.

Example:

    Operational Intelligence
          ↓
    Active Campaign
          ↓
    Tactical Intelligence
          ↓
    TTP
          ↓
    Hunting Hypothesis
          ↓
    SIEM Search


Technical indicators can then help validate the hunt.


---

# 37. Threat Intelligence and Incident Response

During an incident:

    Operational
        ↓
    Identify Campaign

    Tactical
        ↓
    Understand TTPs

    Technical
        ↓
    Find IoCs

    Strategic
        ↓
    Understand Business Impact


This gives incident responders a broader understanding of the incident.


---

# 38. Threat Intelligence and Vulnerability Management

Strategic intelligence can identify important threat trends.

Operational intelligence can identify active exploitation.

Tactical intelligence can reveal exploitation techniques.

Technical intelligence can identify:

- Exploit indicators
- Malicious IPs
- Payload hashes
- Exploit URLs


Complete workflow:

    Threat Trend
         ↓
    Active Exploitation
         ↓
    Exploit Technique
         ↓
    Technical Indicators
         ↓
    Vulnerability Prioritization


---

# 39. Intelligence Fusion

Intelligence Fusion means combining multiple intelligence sources and intelligence types to create a more complete understanding.

Example:

    Threat Report
         +
    Threat Feed
         +
    Internal Logs
         +
    Incident Data
         +
    Vulnerability Data
         ↓
    Intelligence Fusion
         ↓
    Complete Threat Picture


---

# 40. Internal + External Intelligence

External intelligence provides information about the broader threat landscape.

Internal intelligence provides information about what is happening inside the organization.

Combining both is powerful.

    External Intelligence
            +
    Internal Telemetry
            ↓
        Correlation
            ↓
    Organization-Specific Intelligence


Example:

    External:
    Malicious C2 IP

            +

    Internal:
    Endpoint connected to IP

            ↓

    Confirmed Investigation Lead


---

# 41. Threat Intelligence Context

An indicator without context can produce false positives.

Example:

    IP:
    1.2.3.4


This alone does not tell us:

- Why it is malicious
- When it was observed
- Who used it
- What malware it is associated with
- Whether it is still active


Context should include:

- Source
- Timestamp
- Reputation
- Related infrastructure
- Malware
- TTPs
- Threat actor
- Confidence


---

# 42. Intelligence Confidence

Different intelligence types may have different confidence levels.

Example:

    Strategic Assessment:
    Medium Confidence

    Operational Campaign:
    High Confidence

    Tactical TTP:
    High Confidence

    Technical IoC:
    High Confidence


Confidence should be based on evidence.


---

# 43. Intelligence Reliability

Source reliability should also be considered.

Example:

    Source A:
    Highly trusted

    Source B:
    Unknown

    Source C:
    Community report


Analysts should evaluate the reliability of each source before making decisions.


---

# 44. Intelligence Freshness

Threat information becomes less useful over time.

Example:

    Malicious IP
        ↓
    Active today
        ↓
    Useful

    Malicious IP
        ↓
    Last seen 5 years ago
        ↓
    Requires validation


Technical intelligence often requires frequent freshness checks.


---

# 45. Common Mistakes

### Mistake 1 — Treating Every Intelligence Type the Same

Strategic intelligence should not be presented like a raw IoC list.


### Mistake 2 — Giving Executives Excessive Technical Detail

Executives generally need business impact and recommendations.


### Mistake 3 — Giving SOC Analysts Only High-Level Reports

SOC analysts need actionable technical information.


### Mistake 4 — Using IoCs Without Context

This increases false positives.


### Mistake 5 — Ignoring TTPs

Attackers can change infrastructure while keeping similar behavior.


### Mistake 6 — Ignoring Business Context

Not every threat has equal relevance to every organization.


---

# 46. Best Practices

- Match intelligence to the audience
- Match intelligence to the decision
- Combine multiple intelligence types
- Validate technical indicators
- Use TTP-based intelligence
- Map behavior to MITRE ATT&CK
- Add context
- Include confidence
- Consider freshness
- Connect intelligence with internal telemetry
- Automate repetitive enrichment
- Measure intelligence effectiveness


---

# 47. Automation by Intelligence Type

Automation opportunities differ by type.

### Strategic

AI can help:

- Summarize reports
- Identify trends
- Compare industries
- Generate executive briefs


### Tactical

Automation can:

- Extract TTPs
- Map to ATT&CK
- Generate detection ideas


### Operational

Automation can:

- Track campaigns
- Correlate infrastructure
- Monitor threat actor activity


### Technical

Automation can:

- Collect IoCs
- Enrich indicators
- Update watchlists
- Create alerts


---

# 48. AI-Assisted Intelligence Classification

AI can assist with classifying raw information.

Example:

    Threat Report
         ↓
    AI Processing
         ↓
    Strategic Information
         +
    Operational Information
         +
    Tactical Information
         +
    Technical Indicators
         ↓
    Analyst Validation


This can reduce manual analysis time.


---

# 49. AI-Assisted Threat Intelligence Workflow

    Threat Sources
         ↓
    AI Extraction
         ↓
    Classify Intelligence
         ↓
    IoC Extraction
         ↓
    TTP Extraction
         ↓
    ATT&CK Mapping
         ↓
    Threat Actor Identification
         ↓
    Analyst Validation
         ↓
    Intelligence Products


AI output should be treated as analyst assistance rather than automatically trusted intelligence.


---

# 50. Practical Lab

## Lab: Classify Threat Intelligence

### Objective

Take a threat report and classify information into:

- Strategic
- Tactical
- Operational
- Technical


### Example

Suppose a report states:

> A ransomware group is increasingly targeting financial institutions and is using phishing, PowerShell, and a known command-and-control domain.


Classify:

### Strategic

    Increasing targeting of
    financial institutions


### Operational

    Ransomware group campaign


### Tactical

    Phishing
    PowerShell


### Technical

    Known C2 domain


---

# 51. Practical IoC Classification

Given:

    malicious-example.com

Classification:

    Technical Intelligence


Then enrich it:

    Domain
      ↓
    Reputation
      ↓
    First Seen
      ↓
    Related IPs
      ↓
    Malware
      ↓
    Threat Actor
      ↓
    Campaign


The original technical indicator can now contribute to operational and tactical analysis.


---

# 52. Portfolio Project

## Project: Multi-Level Threat Intelligence Analysis

### Objective

Create a professional intelligence analysis showing how one threat can be represented at different intelligence levels.

### Workflow

    Raw Threat Data
          ↓
    Technical Intelligence
          ↓
    Tactical Analysis
          ↓
    Operational Analysis
          ↓
    Strategic Assessment
          ↓
    Security Recommendations


### Deliverables

- Raw threat information
- IoC analysis
- TTP analysis
- ATT&CK mapping
- Campaign analysis
- Business risk assessment
- Executive summary
- SOC recommendations


---

# 53. AI Automation Project

## Project: AI Threat Intelligence Classifier

Build an AI-assisted workflow that processes threat reports.

### Input

    Threat Report


### Processing

    AI
     ↓
    Extract:
    - Threat Actors
    - IoCs
    - Malware
    - TTPs
    - Campaigns
    - Target Industries


### Classification

    Strategic
    Tactical
    Operational
    Technical


### Validation

    AI Output
       ↓
    Human Review
       ↓
    Approved Intelligence


### Output

- Intelligence summary
- IoC list
- ATT&CK mapping
- Detection recommendations
- Executive summary


---

# 54. Professional Work Sample

Create a report structured as:

## Executive Summary

High-level strategic assessment.


## Threat Overview

Description of the threat.


## Operational Activity

Current campaign or activity.


## Tactical Analysis

Attacker TTPs.


## Technical Indicators

IoCs and technical artifacts.


## MITRE ATT&CK

Relevant techniques.


## Business Impact

Potential organizational impact.


## Recommendations

Defensive actions.


## Confidence

Assessment of intelligence quality.


---

# 55. Teaching Knowledge Base

This topic can be taught using the following progression:

    What is Threat Intelligence?
            ↓
    Why classify intelligence?
            ↓
    Strategic
            ↓
    Tactical
            ↓
    Operational
            ↓
    Technical
            ↓
    Intelligence Fusion
            ↓
    Practical Analysis
            ↓
    Automation
            ↓
    AI


---

# 56. Interview Questions

## Basic

1. What are the four major types of Threat Intelligence?
2. What is Strategic Threat Intelligence?
3. What is Tactical Threat Intelligence?
4. What is Operational Threat Intelligence?
5. What is Technical Threat Intelligence?


## Intermediate

6. What is the difference between strategic and tactical intelligence?
7. How does operational intelligence support incident response?
8. Why is technical intelligence useful to a SOC?
9. How does MITRE ATT&CK relate to tactical intelligence?
10. Why should intelligence be tailored to its audience?


## Advanced

11. How would you combine all four intelligence types during an incident?
12. How would you convert technical intelligence into strategic intelligence?
13. How can AI classify threat intelligence?
14. How would you measure the effectiveness of each intelligence type?
15. How would you integrate different intelligence types into a SIEM/SOC workflow?


---

# 57. Key Takeaways

The four major Threat Intelligence types are:

    Strategic
        ↓
    Business Risk

    Operational
        ↓
    Campaign Activity

    Tactical
        ↓
    Attacker Behavior

    Technical
        ↓
    Indicators


They should work together.

A complete intelligence workflow can be represented as:

    Strategic
       ↓
    Operational
       ↓
    Tactical
       ↓
    Technical
       ↓
    Detection
       ↓
    Investigation
       ↓
    Response


However, intelligence can flow in both directions depending on operational requirements.


---

# 58. Final Principle

> **Effective Threat Intelligence is not just about collecting indicators. It is about delivering the right level of intelligence to the right audience so that better security decisions can be made.**

Final model:

    Threat Data
         ↓
    Technical Intelligence
         ↓
    Tactical Understanding
         ↓
    Operational Context
         ↓
    Strategic Assessment
         ↓
    Security Decision
         ↓
    Defensive Action
