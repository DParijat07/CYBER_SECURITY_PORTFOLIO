# Threat Intelligence Collection

## 1. Introduction

Threat Intelligence Collection is the process of gathering relevant threat information from internal and external sources based on defined intelligence requirements.

The objective is not to collect as much data as possible.

The objective is to collect **relevant, reliable, timely, and actionable information**.

    Intelligence Requirements
             ↓
       Source Selection
             ↓
          Collection
             ↓
        Normalization
             ↓
         Validation
             ↓
        Enrichment
             ↓
          Analysis
             ↓
       Intelligence
             ↓
      Security Action


---

# 2. Purpose of Threat Intelligence Collection

Threat intelligence collection helps organizations:

- Identify emerging threats
- Discover malicious infrastructure
- Track threat actors
- Identify attack techniques
- Monitor vulnerabilities
- Support threat hunting
- Improve detection
- Support incident response
- Prioritize security risks
- Improve defensive decision-making


---

# 3. Intelligence Collection vs Intelligence Analysis

These are different activities.

### Collection

Gather information.

### Analysis

Convert information into intelligence.

Example:

    Collection:
    Malicious IP = 203.x.x.x

             ↓

    Analysis:
    IP associated with a known
    malware campaign

             ↓

    Intelligence:
    The organization should
    investigate connections to
    this infrastructure.


---

# 4. Collection Lifecycle

A practical collection lifecycle is:

    Requirements
         ↓
    Planning
         ↓
    Source Identification
         ↓
    Collection
         ↓
    Normalization
         ↓
    Validation
         ↓
    Enrichment
         ↓
    Storage
         ↓
    Analysis
         ↓
    Dissemination
         ↓
    Feedback


This lifecycle should be continuous.


---

# 5. Intelligence Requirements

Collection should begin with intelligence requirements.

An intelligence requirement defines what information the organization needs.

Examples:

- Which threat actors target our industry?
- Which vulnerabilities are actively exploited?
- Which malicious domains target our organization?
- Which ransomware groups are active?
- What TTPs are being used against our technology stack?


Without requirements:

    Too Much Data
         ↓
    Data Overload
         ↓
    Analyst Fatigue
         ↓
    Low Intelligence Value


---

# 6. Priority Intelligence Requirements

Priority Intelligence Requirements are high-priority questions that require intelligence.

Examples:

### PIR 1

Are any critical vulnerabilities affecting our internet-facing systems being actively exploited?


### PIR 2

Are ransomware groups currently targeting our industry?


### PIR 3

Are any of our domains or credentials appearing in known compromise activity?


PIRs help focus collection efforts.


---

# 7. Collection Requirements

Collection requirements translate intelligence requirements into specific information to collect.

Example:

### Intelligence Requirement

Identify active threats targeting our organization.

### Collection Requirements

Collect:

- Threat actor names
- Campaigns
- Domains
- IP addresses
- Malware
- TTPs
- Vulnerabilities
- Industry targeting


---

# 8. Collection Planning

Before collecting data, define:

- What information is needed
- Why it is needed
- Which sources will be used
- How frequently data will be collected
- How data will be validated
- Where it will be stored
- Who will consume it


Example:

    Requirement:
    Monitor ransomware activity

    Sources:
    Government
    Vendors
    OSINT
    Threat Feeds

    Frequency:
    Continuous / Daily

    Output:
    Campaign intelligence


---

# 9. Collection Sources

Common collection sources include:

### Internal

- SIEM
- EDR
- Firewall
- IDS/IPS
- DNS
- Email security
- Cloud logs
- Authentication systems
- Vulnerability scanners
- Incident reports


### External

- Threat feeds
- Government advisories
- CERTs
- Security vendors
- OSINT
- Research reports
- Vulnerability databases
- Industry groups


---

# 10. Manual Collection

Manual collection involves analysts directly reviewing sources.

Examples:

- Reading threat reports
- Reviewing advisories
- Investigating security blogs
- Searching vulnerability databases
- Reviewing incident reports


Advantages:

- High context
- Human judgment
- Flexible investigation


Disadvantages:

- Time-consuming
- Difficult to scale
- Inconsistent
- Easy to miss information


---

# 11. Automated Collection

Automated collection uses software, APIs, feeds, and pipelines.

Example:

    Threat Feed
         ↓
        API
         ↓
    Collector
         ↓
    Normalize
         ↓
    Database
         ↓
    Enrichment
         ↓
    SIEM / TIP


Advantages:

- Scalable
- Fast
- Repeatable
- Continuous


Disadvantages:

- False positives
- Duplicate data
- Stale indicators
- Dependency on source quality


---

# 12. Hybrid Collection

Mature intelligence programs usually combine automation with human analysis.

    Automated Collection
            ↓
       Data Processing
            ↓
       AI Assistance
            ↓
      Analyst Validation
            ↓
        Intelligence


Automation handles volume.

Humans provide judgment.


---

# 13. API-Based Collection

APIs allow systems to collect structured intelligence automatically.

Example:

    Threat Intelligence API
             ↓
          Request
             ↓
          Response
             ↓
        Parse Data
             ↓
       Store Intelligence


Common API data may include:

- IP reputation
- Domain reputation
- Malware information
- Vulnerability information
- Threat actor information


---

# 14. Feed-Based Collection

Threat feeds provide continuously updated intelligence.

Example:

    Feed
      ↓
    Collector
      ↓
    Parser
      ↓
    Validation
      ↓
    Deduplication
      ↓
    Enrichment
      ↓
    Storage


Feeds may provide:

- IPs
- Domains
- URLs
- Hashes
- Malware
- Vulnerabilities


---

# 15. Web-Based Collection

Analysts may collect intelligence from publicly available web sources.

Examples:

- Security research
- Advisories
- Vendor reports
- Vulnerability disclosures
- Security blogs


A web collection workflow:

    Public Source
         ↓
    Relevant Information
         ↓
    Extract
         ↓
    Validate
         ↓
    Store
         ↓
    Analyze


Automated web collection must respect applicable legal and technical restrictions.


---

# 16. OSINT Collection

OSINT collection gathers publicly available information.

Examples:

- Public reports
- Research papers
- Security blogs
- Public advisories
- Vulnerability databases
- Security conference material


OSINT is useful for:

- Early threat awareness
- Research
- Threat actor tracking
- Vulnerability monitoring


---

# 17. Internal Telemetry Collection

Internal telemetry provides visibility into the organization's environment.

Examples:

- Process events
- Authentication events
- Network connections
- DNS requests
- File activity
- Cloud activity
- Endpoint alerts


Example:

    Endpoint
       ↓
    Process Event
       ↓
    Network Connection
       ↓
    Suspicious IP
       ↓
    Threat Intelligence
       ↓
    Investigation


---

# 18. IoC Collection

Indicators of Compromise can be collected from:

- Threat feeds
- Incident investigations
- Malware analysis
- Security reports
- Internal telemetry


Common IoCs:

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses
- File paths
- Registry keys


---

# 19. TTP Collection

Modern threat intelligence should also collect attacker behaviors.

Examples:

- PowerShell execution
- Credential dumping
- Lateral movement
- Persistence
- Phishing
- Remote services
- Command execution


TTPs are often more durable than individual IoCs.


---

# 20. Vulnerability Intelligence Collection

Vulnerability collection focuses on:

- CVEs
- Severity
- Affected software
- Exploit availability
- Active exploitation
- Vendor patches
- Mitigation guidance


Example:

    CVE
     ↓
    Exploit Available
     ↓
    Active Exploitation
     ↓
    Organization Exposure
     ↓
    Priority Remediation


---

# 21. Threat Actor Collection

Threat actor collection may include:

- Actor name
- Aliases
- Motivation
- Target industries
- Geography
- Malware
- Infrastructure
- TTPs
- Campaigns


Example:

    Threat Actor
         ↓
    Campaigns
         ↓
    Malware
         ↓
    Infrastructure
         ↓
    TTPs


---

# 22. Malware Intelligence Collection

Malware-related collection may include:

- Hashes
- Malware families
- File names
- C2 domains
- IPs
- URLs
- Persistence
- Behavioral characteristics


Example:

    Malware Sample
         ↓
    Analysis
         ↓
    IoCs
         ↓
    TTPs
         ↓
    Intelligence


---

# 23. Infrastructure Collection

Attackers use infrastructure such as:

- Domains
- IP addresses
- VPS servers
- Hosting providers
- DNS infrastructure
- Certificates


Collection can help discover relationships.

    Domain A
       ↓
      IP A
       ↓
    Certificate
       ↓
    Domain B
       ↓
      IP B


This can reveal infrastructure clusters.


---

# 24. Collection Frequency

Different intelligence requires different collection frequencies.

### Real-Time

Useful for:

- Critical IoCs
- Active campaigns
- Security alerts


### Hourly

Useful for:

- High-priority feeds
- Operational monitoring


### Daily

Useful for:

- Threat reports
- Vulnerability intelligence
- Industry monitoring


### Weekly

Useful for:

- Strategic trends
- Long-term research


Collection frequency should match operational requirements.


---

# 25. Collection Prioritization

Not all data deserves equal priority.

A simple prioritization model:

    Relevance
       +
    Threat Severity
       +
    Asset Exposure
       +
    Confidence
       +
    Freshness
       ↓
    Collection Priority


Example:

### High Priority

Critical vulnerability actively exploited against exposed assets.


### Medium Priority

Relevant vulnerability without known exploitation.


### Low Priority

Threat unrelated to the organization's environment.


---

# 26. Collection Filtering

Filtering reduces unnecessary data.

Example:

    Global Threat Feed
        ↓
    Millions of Indicators
        ↓
    Filter by:
    - Industry
    - Geography
    - Technology
    - Threat Type
        ↓
    Relevant Intelligence


This improves analyst efficiency.


---

# 27. Collection and Asset Context

Threat intelligence becomes more valuable when matched against the organization's assets.

Example:

    External IoC
         +
    Asset Inventory
         ↓
    Relevance Check
         ↓
    Internal Match
         ↓
    High Priority Investigation


Without asset context:

    IoC
     ↓
    Unknown Relevance


---

# 28. Collection and Technology Stack

Organizations should prioritize intelligence relevant to their technologies.

Example:

If an organization uses:

- Windows
- Active Directory
- Microsoft 365
- AWS
- Apache
- Cisco devices


Then intelligence collection should prioritize threats targeting these technologies.


---

# 29. Collection and Industry

Threat intelligence should also consider industry.

Examples:

### Banking

- Financial malware
- Fraud
- Credential theft
- Ransomware


### Healthcare

- Ransomware
- Data theft
- Medical system attacks


### Manufacturing

- OT/ICS threats
- Ransomware
- Supply-chain threats


Industry context helps prioritize collection.


---

# 30. Data Normalization

Different sources use different formats.

Example:

    Source A:
    IP = 1.2.3.4

    Source B:
    indicator: 1.2.3.4

    Source C:
    value: 1.2.3.4


Normalization converts these into a common structure.

    Raw Sources
         ↓
    Normalization
         ↓
    Standard Data Model


---

# 31. STIX

STIX stands for:

**Structured Threat Information Expression**

STIX provides a standardized way to represent threat intelligence.

It can represent objects such as:

- Indicators
- Malware
- Threat Actors
- Campaigns
- Attack Patterns
- Relationships


Example:

    Threat Actor
         ↓
    Uses Malware
         ↓
    Communicates with Domain
         ↓
    Uses TTP


---

# 32. TAXII

TAXII stands for:

**Trusted Automated Exchange of Intelligence Information**

TAXII is used to exchange threat intelligence between systems.

Simplified:

    Intelligence Provider
             ↓
           TAXII
             ↓
    Intelligence Platform
             ↓
           SIEM


STIX defines intelligence objects.

TAXII helps transport them.


---

# 33. MISP Collection

MISP can be used to collect and share threat intelligence.

Example workflow:

    Threat Sources
         ↓
        MISP
         ↓
    Normalize
         ↓
    Enrich
         ↓
    Correlate
         ↓
    Share / Export
         ↓
    SOC


MISP is widely used for collaborative threat intelligence management.


---

# 34. OpenCTI Collection

OpenCTI can help organize intelligence relationships.

Example:

    Threat Actor
         ↓
    Campaign
         ↓
    Malware
         ↓
    Infrastructure
         ↓
    IoC


This graph-based approach helps analysts understand relationships between entities.


---

# 35. Collection Storage

Collected intelligence may be stored in:

- Databases
- Threat Intelligence Platforms
- Data lakes
- SIEM
- Case management systems
- Structured files


Storage should preserve:

- Source
- Timestamp
- Indicator
- Type
- Confidence
- Context
- Relationships


---

# 36. Data Deduplication

Multiple sources may provide the same indicator.

Example:

    Feed A → 1.2.3.4

    Feed B → 1.2.3.4

    Feed C → 1.2.3.4


Without deduplication:

    3 records


With deduplication:

    1 indicator
    + multiple sources


This improves efficiency.


---

# 37. Indicator Enrichment

Collected indicators should be enriched.

Example:

    IP
     ↓
    Reputation
     ↓
    ASN
     ↓
    Geolocation
     ↓
    Related Domains
     ↓
    Malware
     ↓
    Threat Actor
     ↓
    Campaign


Enrichment adds context.


---

# 38. Indicator Validation

Not every collected indicator is malicious.

Validation may include:

- Source reputation
- Multiple-source confirmation
- Internal evidence
- Historical behavior
- Current activity
- False-positive checks


Example:

    IoC
     ↓
    Validate
     ↓
    Confirmed
     ↓
    Action


---

# 39. Freshness

Threat information can become outdated.

Example:

    Malicious Domain
         ↓
    Active
         ↓
    Infrastructure Removed
         ↓
    Indicator Becomes Less Useful


Collection systems should track:

- First seen
- Last seen
- Expiration
- Last updated


---

# 40. Collection Confidence

Each collected item should ideally have a confidence assessment.

Example:

    Indicator:
    malicious-example.com

    Source:
    Trusted Vendor

    Confidence:
    High

    First Seen:
    Recent

    Related Malware:
    Example Family


Confidence helps analysts prioritize investigations.


---

# 41. Source Attribution

Every collected intelligence item should maintain source information.

Example:

    Indicator:
    1.2.3.4

    Source:
    Government Advisory

    Collected:
    2026-08-23

    Confidence:
    High


Source attribution improves:

- Validation
- Auditing
- Investigation
- Intelligence sharing


---

# 42. Legal and Ethical Considerations

Threat intelligence collection must comply with:

- Applicable laws
- Organizational policies
- Privacy requirements
- Terms of service
- Data protection requirements
- Authorization boundaries


Organizations should avoid collecting information they are not legally or operationally authorized to access.


---

# 43. Collection Automation

A mature collection pipeline may look like:

    Sources
       ↓
    Collectors
       ↓
    Parsing
       ↓
    Normalization
       ↓
    Deduplication
       ↓
    Validation
       ↓
    Enrichment
       ↓
    Storage
       ↓
    Analysis
       ↓
    Dissemination


---

# 44. Python-Based Collection

Python is commonly useful for intelligence automation.

Possible tasks:

- API requests
- Feed parsing
- JSON processing
- CSV processing
- Indicator extraction
- Deduplication
- Database insertion
- Enrichment


Example architecture:

    Python Script
         ↓
    Threat API
         ↓
    JSON
         ↓
    Parse
         ↓
    Validate
         ↓
    Store


---

# 45. AI-Assisted Collection

AI can help analysts process unstructured sources.

Example:

    Threat Report
         ↓
        AI
         ↓
    Extract:
    - IoCs
    - TTPs
    - Malware
    - Threat Actors
    - Campaigns
         ↓
    Analyst Validation


AI can accelerate extraction but should not replace verification.


---

# 46. AI Collection Pipeline

A practical AI-assisted pipeline:

    Threat Reports
         +
    Advisories
         +
    Feeds
         ↓
    Collection
         ↓
    AI Extraction
         ↓
    Classification
         ↓
    Enrichment
         ↓
    Confidence Scoring
         ↓
    Human Validation
         ↓
    Intelligence Database


---

# 47. AI-Based Information Extraction

Given a report:

    "The threat actor used PowerShell
     to execute a malicious payload and
     communicated with example-domain.com."


AI can extract:

### Threat Actor

    Threat Actor X


### TTP

    PowerShell


### Domain

    example-domain.com


### Activity

    Command and Control


The extracted information should then be validated.


---

# 48. Collection Quality Metrics

Useful metrics include:

- Number of sources
- Number of indicators
- Valid indicator percentage
- Duplicate percentage
- Stale indicator percentage
- False-positive rate
- Collection latency
- Source uptime
- Internal detection matches
- Analyst time saved


Example:

    100,000 Indicators
          ↓
    20,000 Relevant
          ↓
    5,000 Internal Matches


The important metric is not simply the number collected.

It is the number that creates useful security outcomes.


---

# 49. Collection-to-Detection Workflow

    Threat Source
         ↓
    Collection
         ↓
    Validation
         ↓
    Enrichment
         ↓
    SIEM
         ↓
    Correlation
         ↓
    Detection
         ↓
    SOC Alert
         ↓
    Investigation


---

# 50. Collection-to-Threat-Hunting Workflow

    Threat Source
         ↓
    TTP / IoC
         ↓
    Hunting Hypothesis
         ↓
    Query SIEM / EDR
         ↓
    Identify Activity
         ↓
    Investigate
         ↓
    Generate New Intelligence


This creates a feedback loop.


---

# 51. Intelligence Feedback Loop

A mature program continuously learns.

    External Intelligence
            ↓
        Collection
            ↓
          Analysis
            ↓
       Detection / Hunt
            ↓
        Investigation
            ↓
       New Findings
            ↓
    Intelligence Update
            ↓
       Future Collection


---

# 52. Common Collection Problems

### Problem 1 — Collecting Everything

Creates data overload.


### Problem 2 — No Intelligence Requirements

Creates irrelevant collection.


### Problem 3 — Poor Source Quality

Creates unreliable intelligence.


### Problem 4 — No Deduplication

Creates unnecessary data.


### Problem 5 — No Freshness Management

Creates stale indicators.


### Problem 6 — No Internal Correlation

External intelligence may remain irrelevant.


### Problem 7 — Blind Automation

Bad source data can become automated bad decisions.


---

# 53. Best Practices

- Start with intelligence requirements
- Define PIRs
- Select relevant sources
- Automate repetitive collection
- Normalize data
- Deduplicate indicators
- Validate intelligence
- Enrich indicators
- Track freshness
- Maintain source attribution
- Use internal telemetry
- Correlate multiple sources
- Measure collection quality
- Apply human validation
- Continuously improve requirements


---

# 54. Practical Lab

## Lab: Build a Threat Intelligence Collection Pipeline

### Objective

Build a basic collection pipeline using publicly available and authorized sources.

### Architecture

    Threat Source
         ↓
       Python
         ↓
       Parser
         ↓
     Normalize
         ↓
     Deduplicate
         ↓
      Enrich
         ↓
      Store
         ↓
      Analyze


### Collect

- IPs
- Domains
- URLs
- Hashes


### Store

Use a structured format such as:

```text
indicator
type
source
first_seen
last_seen
confidence
context
