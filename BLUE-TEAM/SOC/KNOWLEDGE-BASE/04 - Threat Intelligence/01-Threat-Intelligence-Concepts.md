# Threat Intelligence Concepts

## 1. Introduction

Threat Intelligence is the process of collecting, processing, analyzing, and applying information about cyber threats to support better security decisions.

Threat Intelligence helps an organization understand:

- What threats exist
- Who may be behind the threats
- How attackers operate
- Which systems may be targeted
- Which indicators are associated with malicious activity
- Which vulnerabilities are actively exploited
- How defensive controls should be improved

The fundamental idea is:

    Threat Data
        ↓
    Processing
        ↓
    Analysis
        ↓
    Threat Intelligence
        ↓
    Security Decision
        ↓
    Defensive Action


---

## 2. Threat Data vs Threat Intelligence

These terms are related but different.

### Threat Data

Threat data is raw information collected from different sources.

Examples:

- IP addresses
- Domains
- URLs
- File hashes
- Malware samples
- Log entries
- Vulnerability information
- Security reports


Example:

    185.x.x.x
    malicious.example.com
    SHA256: abc123...


This information by itself may have limited context.


### Threat Intelligence

Threat Intelligence is analyzed and contextualized information that can support a security decision.

Example:

    IP:
    185.x.x.x

    Reputation:
    Malicious

    Associated Activity:
    Command and Control

    Malware:
    Example RAT

    ATT&CK:
    Command and Control

    Confidence:
    High

    Recommended Action:
    Block and investigate internal connections


The key difference is:

    Data = Raw Information

    Intelligence = Context + Analysis + Action


---

## 3. Core Objective

The objective of Threat Intelligence is not simply to collect as much information as possible.

The objective is to answer questions such as:

- What is happening?
- Why is it happening?
- Who is responsible?
- How does the attacker operate?
- What systems are at risk?
- What should we do?


A mature intelligence program converts:

    Information
        ↓
    Understanding
        ↓
    Decision
        ↓
    Action


---

## 4. Threat Intelligence in Cybersecurity

Threat Intelligence connects multiple cybersecurity functions.

    Threat Intelligence
            │
    ┌───────┼────────┐
    ↓       ↓        ↓
   SOC   Threat     IR
         Hunting
    ↓       ↓        ↓
 Monitoring Detection Response


It can also support:

- Vulnerability Management
- Risk Management
- Security Architecture
- Fraud Detection
- Cloud Security
- Identity Security
- Malware Analysis
- Executive Risk Management


---

## 5. Why Threat Intelligence Matters

Modern organizations face:

- Increasing attack volume
- Sophisticated attackers
- Ransomware
- Phishing
- Credential attacks
- Supply-chain attacks
- Cloud attacks
- Exploitation of vulnerabilities
- Insider threats


Threat Intelligence helps organizations become more proactive.

Without intelligence:

    Alert
      ↓
    Investigate
      ↓
    React


With intelligence:

    External Threat Information
              ↓
       Internal Monitoring
              ↓
        Early Detection
              ↓
          Response


---

## 6. Threat Intelligence Characteristics

Useful Threat Intelligence should be:

### Relevant

It should relate to the organization's environment and threat model.

### Accurate

The information should be reliable and validated.

### Timely

Threat intelligence should arrive while it is still useful.

### Actionable

The intelligence should support a security decision.

### Contextual

Indicators should include meaningful information about their purpose and relevance.

### Specific

The intelligence should answer a defined intelligence requirement.


---

## 7. Intelligence Requirements

An Intelligence Requirement (IR) defines what the organization needs to know.

Example:

> Which ransomware groups are currently targeting organizations in our industry?

Another example:

> Are any of our externally exposed systems associated with actively exploited vulnerabilities?


Intelligence requirements help prevent unnecessary data collection.


---

## 8. Priority Intelligence Requirements

A Priority Intelligence Requirement (PIR) is a high-priority question that requires intelligence support.

Example:

    PIR:
    Are our public-facing systems
    being targeted by a known threat actor?


The intelligence team then collects and analyzes information specifically related to that question.


---

## 9. Threat Intelligence Lifecycle

A typical lifecycle contains:

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


Each stage contributes to the final intelligence product.


---

## 10. Direction

Direction defines:

- What needs to be known
- Why it needs to be known
- Who needs the information
- How quickly it is needed
- What decisions it should support


Example:

    Business Concern:
    Ransomware Risk

          ↓

    Intelligence Requirement:
    Identify ransomware groups
    targeting our industry.


---

## 11. Collection

Collection gathers relevant information.

Sources may include:

- Open-source intelligence
- Security vendors
- Government advisories
- CERT organizations
- Threat feeds
- Internal security logs
- Incident reports
- Malware research
- Vulnerability databases


The collection process should be guided by intelligence requirements.


---

## 12. Processing

Raw information may contain:

- Duplicate indicators
- Different formats
- Missing context
- Inconsistent timestamps
- Invalid data
- Unstructured text


Processing converts raw information into a usable format.

Example:

    Raw Threat Feed
         ↓
    Remove Duplicates
         ↓
    Normalize Format
         ↓
    Validate Indicators
         ↓
    Enrich Data
         ↓
    Structured Dataset


---

## 13. Analysis

Analysis turns processed information into intelligence.

Analysts may determine:

- What happened
- Who may be involved
- What techniques were used
- What infrastructure was involved
- Which systems may be affected
- How likely the information is to be relevant


Example:

    Multiple Malicious IPs
          +
    Same Malware Family
          +
    Similar C2 Pattern
          ↓
    Possible Campaign


---

## 14. Dissemination

Dissemination means delivering intelligence to the correct audience.

Examples:

### SOC

Needs:

- IoCs
- TTPs
- Detection recommendations


### Incident Response

Needs:

- Threat actor information
- Infrastructure
- Malware information
- Attack techniques


### Vulnerability Management

Needs:

- Exploited vulnerabilities
- Threat activity
- Exploitation trends


### Executives

Need:

- Business risk
- Threat trends
- Strategic recommendations


---

## 15. Feedback

Feedback determines whether the intelligence was useful.

Questions include:

- Was the intelligence relevant?
- Was it timely?
- Was it accurate?
- Did it support a decision?
- Did the SOC use it?
- Did it improve detection?


Feedback improves future intelligence collection.


---

## 16. Types of Threat Intelligence

Threat Intelligence is commonly divided into:

1. Strategic Intelligence
2. Tactical Intelligence
3. Operational Intelligence
4. Technical Intelligence


Each type serves a different audience and purpose.


---

## 17. Strategic Threat Intelligence

Strategic intelligence focuses on high-level threats and business risk.

Audience:

- Executives
- CISOs
- Security leadership
- Risk managers
- Business leaders


Examples:

- Ransomware trends
- Geopolitical cyber risk
- Industry targeting
- Emerging threat landscape
- Business impact


Example:

    Threat:
    Ransomware targeting healthcare

    Business Impact:
    Operational disruption

    Strategic Decision:
    Increase ransomware resilience investment


---

## 18. Tactical Threat Intelligence

Tactical intelligence focuses on attacker behavior.

It commonly describes:

- Tactics
- Techniques
- Procedures
- Attack patterns


Audience:

- SOC analysts
- Threat hunters
- Detection engineers
- Incident responders


Example:

    Attack Technique:
    PowerShell

    Detection:
    Suspicious PowerShell execution


---

## 19. Operational Threat Intelligence

Operational intelligence focuses on active campaigns and attacker operations.

It may include:

- Campaign information
- Threat actor activity
- Attack timelines
- Targeting patterns
- Infrastructure
- Malware campaigns


Audience:

- Threat intelligence analysts
- Incident responders
- SOC teams


---

## 20. Technical Threat Intelligence

Technical intelligence focuses on technical indicators.

Examples:

- IP addresses
- Domains
- URLs
- File hashes
- Malware signatures
- Email addresses
- User agents
- Certificates


Technical intelligence is frequently integrated into security tools.


---

## 21. Indicators of Compromise

Indicators of Compromise are observable artifacts associated with potentially malicious activity.

Examples:

### Network

- IP address
- Domain
- URL
- DNS record


### Endpoint

- File hash
- File name
- Registry key
- Process name


### Email

- Sender address
- Malicious URL
- Attachment hash


### Cloud

- Suspicious IP
- Cloud account
- API activity
- Abnormal login location


IoCs require context before action.


---

## 22. Indicators of Attack

Indicators of Attack focus more on attacker behavior than static artifacts.

Examples:

- Credential dumping
- Suspicious PowerShell
- Lateral movement
- Privilege escalation
- Unusual process chains


Difference:

    IoC:
    What artifact was observed?

    IoA:
    What suspicious behavior occurred?


Behavior-based indicators can be more resilient against changing infrastructure.


---

## 23. Threat Actors

A threat actor is an individual or group responsible for malicious cyber activity.

Examples include:

- Cybercriminal groups
- Ransomware groups
- Nation-state groups
- Hacktivists
- Insider threats
- Initial access brokers


Threat intelligence may track:

- Motivation
- Capabilities
- Targets
- Infrastructure
- TTPs
- Campaigns


---

## 24. Threat Actor Motivation

Common motivations include:

### Financial

Examples:

- Ransomware
- Banking fraud
- Credential theft


### Espionage

Examples:

- Intelligence collection
- Sensitive information theft


### Ideological

Examples:

- Hacktivism
- Political messaging


### Disruption

Examples:

- Denial-of-service
- Destructive attacks


Understanding motivation can help predict attacker behavior.


---

## 25. Threat Actor Capability

Capability refers to what an attacker can realistically accomplish.

Factors include:

- Technical skills
- Resources
- Infrastructure
- Malware
- Exploit capabilities
- Operational maturity


Threat intelligence can use capability information to estimate risk.


---

## 26. Tactics, Techniques and Procedures

TTPs describe how attackers operate.

### Tactics

The attacker's objective.

Examples:

- Initial Access
- Persistence
- Credential Access
- Discovery
- Lateral Movement
- Exfiltration


### Techniques

Methods used to achieve the objective.

Example:

    Credential Access
          ↓
    OS Credential Dumping


### Procedures

Specific implementation details used by a threat actor.


---

## 27. MITRE ATT&CK

MITRE ATT&CK provides a structured knowledge base of adversary behavior.

Threat intelligence can be mapped to:

- Tactics
- Techniques
- Sub-techniques
- Groups
- Software
- Campaigns


Example:

    Threat Actor
         ↓
    Technique
         ↓
    Detection
         ↓
    Investigation


---

## 28. Threat Intelligence and Risk

Threat intelligence can improve risk assessment.

Example:

    Vulnerability
         +
    Internet Exposure
         +
    Active Exploitation
         +
    Critical Asset
         ↓
    High Risk


This is more useful than evaluating vulnerability severity alone.


---

## 29. Threat Intelligence and Vulnerability Management

Threat intelligence helps prioritize vulnerabilities based on real-world exploitation.

Example:

    CVE
      ↓
    Exploitation Observed
      ↓
    Threat Intelligence
      ↓
    Asset Check
      ↓
    Vulnerable System Found
      ↓
    Immediate Remediation


---

## 30. Threat Intelligence and SOC

SOC analysts can use intelligence to:

- Enrich alerts
- Identify malicious infrastructure
- Investigate suspicious activity
- Improve detections
- Hunt for threats
- Prioritize incidents


Example:

    SIEM Alert
        ↓
    Suspicious IP
        ↓
    Threat Intelligence Lookup
        ↓
    Malicious Reputation
        ↓
    High Priority Investigation


---

## 31. Threat Intelligence and Threat Hunting

Threat Intelligence can provide hunting hypotheses.

Example:

    Intelligence Report
          ↓
    Known C2 Domain
          ↓
    Search DNS Logs
          ↓
    Search Proxy Logs
          ↓
    Search Endpoint Logs
          ↓
    Internal Evidence


Threat intelligence therefore makes threat hunting more focused.


---

## 32. Threat Intelligence and Incident Response

During incident response, intelligence can help determine:

- Whether an IoC is malicious
- Related infrastructure
- Possible attacker identity
- Malware family
- TTPs
- Additional indicators
- Possible next attacker actions


Example:

    Compromised Host
          ↓
    Malware Hash
          ↓
    Intelligence Lookup
          ↓
    Malware Family Identified
          ↓
    Related IoCs
          ↓
    Environment-Wide Search


---

## 33. Threat Intelligence Enrichment

Enrichment adds additional context to an indicator.

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
    Related Malware
       ↓
    Threat Actor
       ↓
    Confidence


Enrichment helps analysts determine whether an indicator deserves investigation.


---

## 34. Confidence Levels

Threat intelligence can use confidence levels.

Example:

### High Confidence

Multiple trusted sources confirm the activity.


### Medium Confidence

Some evidence exists but additional validation is required.


### Low Confidence

Limited evidence or unverified reporting.


Confidence helps prevent overreaction to uncertain information.


---

## 35. Reliability vs Confidence

These concepts are related but different.

### Source Reliability

How trustworthy is the source?

### Intelligence Confidence

How confident are we that the specific assessment is correct?


Example:

    Reliable Source
         +
    Weak Evidence
         ↓
    Moderate Confidence


Both dimensions should be considered.


---

## 36. Threat Intelligence Feeds

Threat feeds provide machine-readable or human-readable threat information.

Examples:

- Malicious IP feeds
- Malware feeds
- Phishing feeds
- Domain feeds
- Vulnerability feeds
- Botnet feeds


A feed is only useful if the organization can:

- Validate it
- Process it
- Apply it
- Monitor it
- Measure its effectiveness


---

## 37. Threat Feed Challenges

Potential problems include:

- False positives
- Duplicate indicators
- Stale indicators
- Poor context
- Excessive volume
- Inconsistent formats


Therefore:

    More Threat Feeds
         ≠
    Better Security


Quality and relevance matter more than volume.


---

## 38. Threat Intelligence Platforms

Threat Intelligence Platforms help manage intelligence.

Common capabilities include:

- Feed collection
- IoC storage
- Enrichment
- Correlation
- Threat actor tracking
- Relationship mapping
- Sharing


Examples include:

- MISP
- OpenCTI


---

## 39. STIX

STIX stands for:

**Structured Threat Information Expression**

STIX provides a standardized way to represent threat intelligence.

It can represent:

- Indicators
- Malware
- Threat actors
- Campaigns
- Attack patterns
- Relationships


Example:

    Threat Actor
         ↓
    Uses
         ↓
    Malware
         ↓
    Connects To
         ↓
    Infrastructure


---

## 40. TAXII

TAXII stands for:

**Trusted Automated Exchange of Intelligence Information**

TAXII enables automated exchange of cyber threat intelligence.

Simplified:

    STIX
    ↓
    Intelligence Structure

    TAXII
    ↓
    Intelligence Exchange


Together they support structured intelligence sharing.


---

## 41. Threat Intelligence Correlation

Correlation connects related pieces of information.

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


Correlation can reveal relationships that individual indicators cannot show.


---

## 42. Threat Intelligence Analysis Example

Suppose the SOC receives:

    IP:
    203.x.x.x

Threat intelligence enrichment shows:

    Reputation:
    Malicious

    Malware:
    Example Malware

    First Seen:
    30 days ago

    Associated Domain:
    malicious-example.com

    ATT&CK:
    Command and Control


SOC workflow:

    Intelligence
        ↓
    Search SIEM
        ↓
    Internal Connection Found
        ↓
    Investigate Host
        ↓
    Identify Malware
        ↓
    Contain Host


This is where intelligence becomes operationally valuable.


---

## 43. Threat Intelligence Reporting

A professional intelligence report may contain:

1. Executive Summary
2. Intelligence Requirement
3. Threat Overview
4. Threat Actor
5. Targeting
6. TTPs
7. IoCs
8. MITRE ATT&CK Mapping
9. Confidence
10. Impact
11. Recommended Actions


Reports should be concise and actionable.


---

## 44. Actionable Intelligence

Good intelligence should answer:

> What should we do now?


Example:

    Intelligence:
    Active exploitation of vulnerability X

    Action:
    Identify affected assets

    Action:
    Apply vendor patch

    Action:
    Search logs for exploitation

    Action:
    Monitor related IoCs


This is actionable intelligence.


---

## 45. Intelligence-to-Action Workflow

    Intelligence
         ↓
    Validate
         ↓
    Enrich
         ↓
    Assess Relevance
         ↓
    Map to Environment
         ↓
    Identify Risk
         ↓
    Take Action
         ↓
    Measure Result


---

## 46. Threat Intelligence Automation

Automation can perform:

- Feed ingestion
- IoC normalization
- Deduplication
- Reputation checks
- Enrichment
- SIEM watchlist updates
- Ticket creation
- Notification


Example:

    Threat Feed
         ↓
    Python
         ↓
    Normalize
         ↓
    Enrich
         ↓
    Score
         ↓
    SIEM
         ↓
    Alert


---

## 47. AI-Assisted Threat Intelligence

AI can help analysts:

- Summarize reports
- Extract IoCs
- Extract TTPs
- Identify relationships
- Cluster similar threats
- Map behavior to ATT&CK
- Generate intelligence drafts
- Identify recurring patterns


Example:

    Threat Report
         ↓
    AI Extraction
         ↓
    IoCs + TTPs
         ↓
    ATT&CK Mapping
         ↓
    Analyst Validation
         ↓
    Intelligence Product


AI should assist analysts rather than make unvalidated high-impact security decisions.


---

## 48. Threat Intelligence Quality

Quality can be evaluated using:

- Accuracy
- Relevance
- Timeliness
- Completeness
- Confidence
- Actionability


Example:

    Intelligence:
    Accurate
    +
    Relevant
    +
    Timely
    +
    Actionable


This creates operational value.


---

## 49. Common Threat Intelligence Mistakes

### Mistake 1 — Collecting Everything

Large amounts of irrelevant data can overwhelm analysts.


### Mistake 2 — Trusting IoCs Blindly

An indicator may be:

- Shared infrastructure
- Compromised infrastructure
- Outdated
- Incorrect


### Mistake 3 — Ignoring Context

An IP address alone may not explain the threat.


### Mistake 4 — Ignoring Internal Data

Internal telemetry is critical for validating external intelligence.


### Mistake 5 — Failing to Measure Value

Threat intelligence should demonstrate operational impact.


---

## 50. Threat Intelligence Maturity

### Level 1 — Reactive

Intelligence is used only during incidents.


### Level 2 — Structured

Threat feeds and IoC management are introduced.


### Level 3 — Integrated

Intelligence is connected to SIEM, SOC and threat hunting.


### Level 4 — Proactive

Intelligence drives detection and vulnerability prioritization.


### Level 5 — Intelligence-Led

Threat intelligence continuously influences security strategy, detection, response and risk management.


---

## 51. Practical Lab

### Objective

Investigate a suspicious IP using threat intelligence.

### Workflow

    Suspicious IP
         ↓
    Reputation Lookup
         ↓
    Enrichment
         ↓
    Historical Activity
         ↓
    Related Indicators
         ↓
    MITRE ATT&CK Mapping
         ↓
    Internal SIEM Search
         ↓
    Risk Assessment
         ↓
    Recommendation


### Documentation

Record:

- Indicator
- Source
- Reputation
- First/last seen
- Related infrastructure
- Malware
- TTPs
- Confidence
- Internal matches
- Recommended action


---

## 52. Portfolio Evidence

For this topic, professional evidence can include:

- Threat intelligence investigation
- IoC analysis
- Threat actor profile
- MITRE ATT&CK mapping
- Threat intelligence report
- SIEM correlation
- Threat hunting query
- Automation script
- AI-assisted analysis


The evidence should demonstrate:

    Learn
      ↓
    Investigate
      ↓
    Analyze
      ↓
    Document
      ↓
    Automate
      ↓
    Validate


---

## 53. Professional Use Case

### Scenario

A SOC receives an alert showing outbound communication to a suspicious IP.

### Investigation

    SIEM Alert
        ↓
    IP Extraction
        ↓
    Threat Intelligence Lookup
        ↓
    Malicious Reputation
        ↓
    Related Malware Identified
        ↓
    Search Endpoint Logs
        ↓
    Malware Process Found
        ↓
    Host Isolation
        ↓
    IoC Sweep
        ↓
    Incident Response


Threat Intelligence accelerates the investigation by providing context.


---

## 54. Knowledge Base Structure

Future teaching documentation can organize Threat Intelligence into:

    Fundamentals
        ↓
    Lifecycle
        ↓
    Intelligence Types
        ↓
    IoCs
        ↓
    Threat Actors
        ↓
    TTPs
        ↓
    ATT&CK
        ↓
    Platforms
        ↓
    Automation
        ↓
    AI
        ↓
    Practical Projects


---

## 55. Interview Questions

### Basic

1. What is Threat Intelligence?
2. What is the difference between threat data and threat intelligence?
3. What are IoCs?
4. What are TTPs?
5. What is MITRE ATT&CK?


### Intermediate

6. What is the Threat Intelligence Lifecycle?
7. What is the difference between tactical and strategic intelligence?
8. How can Threat Intelligence support a SOC?
9. How can Threat Intelligence support threat hunting?
10. How do you validate an IoC?


### Advanced

11. How would you integrate Threat Intelligence with a SIEM?
12. How would you measure the quality of a threat feed?
13. How would you prioritize threat intelligence?
14. How can AI assist Threat Intelligence?
15. How would you prevent false positives from threat feeds?


---

## 56. Key Takeaways

Threat Intelligence is not simply a collection of malicious IPs and hashes.

It is a structured process of:

    Collecting
        ↓
    Processing
        ↓
    Analyzing
        ↓
    Contextualizing
        ↓
    Applying
        ↓
    Measuring


Important concepts include:

- Intelligence Requirements
- Threat Intelligence Lifecycle
- Strategic Intelligence
- Tactical Intelligence
- Operational Intelligence
- Technical Intelligence
- IoCs
- IoAs
- Threat Actors
- TTPs
- MITRE ATT&CK
- Threat Feeds
- Enrichment
- STIX
- TAXII
- Intelligence Platforms
- Automation
- AI-assisted analysis


---

## 57. Final Concept

The most important principle is:

> **Threat Intelligence is not valuable because it contains information. It is valuable because that information helps an organization make better security decisions and take better defensive action.**

Final model:

    Threat Data
         ↓
    Context
         ↓
    Analysis
         ↓
    Intelligence
         ↓
    Decision
         ↓
    Defensive Action
         ↓
    Measurement
         ↓
    Improvement
