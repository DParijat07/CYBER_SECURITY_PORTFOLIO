# Threat Intelligence Sources

## 1. Introduction

Threat Intelligence Sources are the places, systems, organizations, feeds, platforms, and datasets from which cybersecurity threat information is collected.

Threat intelligence can come from both **external** and **internal** sources.

    Threat Intelligence Sources
             │
       ┌─────┴─────┐
       ↓           ↓
    External     Internal
       ↓           ↓
    OSINT        SIEM
    Feeds        EDR
    CERTs        Firewall
    Vendors      DNS
    Research     Incident Data
       │           │
       └─────┬─────┘
             ↓
        Correlation
             ↓
       Threat Intelligence
             ↓
       Security Action


---

# 2. Purpose of Threat Intelligence Sources

Threat intelligence sources help organizations:

- Discover emerging threats
- Identify malicious infrastructure
- Track threat actors
- Understand attacker techniques
- Identify exploited vulnerabilities
- Collect Indicators of Compromise (IoCs)
- Support threat hunting
- Improve security detections
- Support incident response
- Prioritize vulnerabilities
- Understand industry-specific threats


---

# 3. Source Categories

Threat intelligence sources can broadly be categorized as:

1. Internal Sources
2. Open-Source Intelligence (OSINT)
3. Commercial Intelligence
4. Government and CERT Sources
5. Threat Intelligence Feeds
6. Security Research
7. Community Intelligence
8. Industry Intelligence Sharing
9. Technical Infrastructure Sources
10. Dark Web / Underground Sources

Each source provides different levels of context, reliability, freshness, and operational value.


---

# 4. Internal Threat Intelligence Sources

Internal sources originate from within the organization.

Examples:

- SIEM
- EDR
- Firewall
- IDS/IPS
- DNS logs
- Proxy logs
- Email security
- Authentication logs
- Cloud logs
- Vulnerability scanners
- Incident reports
- Malware analysis
- Honeypots


Internal data is extremely valuable because it represents the organization's actual environment.


---

# 5. SIEM as an Intelligence Source

A SIEM collects and correlates security events.

Examples:

- Authentication failures
- Suspicious processes
- Network connections
- DNS queries
- Firewall events
- Endpoint alerts


Example:

    SIEM
      ↓
    Suspicious IP
      ↓
    Threat Intelligence Lookup
      ↓
    Malicious Reputation
      ↓
    Investigation


SIEM can therefore act as both a **consumer** and **producer** of threat intelligence.


---

# 6. EDR as an Intelligence Source

Endpoint Detection and Response systems provide endpoint telemetry.

Examples:

- Process execution
- Command-line activity
- File creation
- Registry changes
- Network connections
- Persistence mechanisms
- User activity


Example:

    EDR
     ↓
    Suspicious PowerShell
     ↓
    Process Tree
     ↓
    Related Domain
     ↓
    Threat Intelligence Enrichment


---

# 7. Firewall Intelligence

Firewalls provide network-level information.

Examples:

- Source IP
- Destination IP
- Ports
- Protocols
- Allowed connections
- Blocked connections


Example:

    Firewall Log
         ↓
    Outbound Connection
         ↓
    Destination IP
         ↓
    Threat Intelligence
         ↓
    Malicious C2
         ↓
    Alert


---

# 8. DNS Intelligence

DNS logs can reveal:

- Malicious domains
- C2 communication
- Newly registered domains
- DNS tunneling
- Suspicious lookups
- Domain generation activity


Example:

    DNS Query
       ↓
    Suspicious Domain
       ↓
    Reputation Check
       ↓
    Threat Intelligence
       ↓
    Investigation


DNS is particularly useful for detecting command-and-control activity.


---

# 9. Proxy and Web Gateway Sources

Proxy logs can provide:

- URLs
- Domains
- User agents
- Source hosts
- Destination IPs
- HTTP methods
- Web activity


They can help identify:

- Phishing
- Malware downloads
- C2 communication
- Suspicious browsing
- Data exfiltration


---

# 10. Email Security Sources

Email security systems provide intelligence about:

- Phishing emails
- Malicious attachments
- Sender addresses
- URLs
- Email headers
- Attachment hashes
- Spoofing attempts


Example:

    Phishing Email
         ↓
    URL Extraction
         ↓
    Domain Analysis
         ↓
    Threat Intelligence
         ↓
    Block / Investigate


---

# 11. Authentication Sources

Authentication logs can provide information about:

- Failed logins
- Successful logins
- Impossible travel
- Brute-force attempts
- Suspicious locations
- Privilege escalation
- Account misuse


Example:

    Multiple Failed Logins
            ↓
    Successful Login
            ↓
    Suspicious IP
            ↓
    Threat Intelligence
            ↓
    Account Investigation


---

# 12. Cloud Security Sources

Cloud environments provide intelligence from:

- CloudTrail
- Azure activity logs
- Microsoft Entra ID logs
- Cloud security platforms
- API activity
- IAM events
- Storage access logs


Example:

    Cloud API Activity
          ↓
    Suspicious Source IP
          ↓
    Threat Intelligence
          ↓
    Risk Assessment


---

# 13. Vulnerability Management Sources

Vulnerability scanners and vulnerability databases provide intelligence about:

- CVEs
- Affected software
- Severity
- Exploit availability
- Patch information
- Asset exposure


Threat intelligence can improve vulnerability prioritization.

    Vulnerability
         +
    Active Exploitation
         +
    Critical Asset
         ↓
    High Priority


---

# 14. Incident Response Sources

Previous incidents are valuable internal intelligence sources.

Incident reports may contain:

- IoCs
- TTPs
- Malware
- Attack timeline
- Compromised accounts
- Attacker infrastructure
- Root cause
- Lessons learned


This information can become future detection intelligence.


---

# 15. Malware Analysis as a Source

Malware analysis can produce:

- File hashes
- Domains
- IP addresses
- URLs
- File paths
- Registry keys
- Process behavior
- Persistence techniques
- C2 behavior
- ATT&CK mappings


Example:

    Malware Sample
         ↓
    Static Analysis
         ↓
    Dynamic Analysis
         ↓
    IoCs
         ↓
    TTPs
         ↓
    Threat Intelligence


---

# 16. Honeypots as Intelligence Sources

Honeypots are systems designed to attract or observe malicious activity.

They can reveal:

- Scanning activity
- Brute-force attempts
- Exploitation attempts
- Malware
- Attacker IPs
- Attack techniques


Example:

    Honeypot
       ↓
    Attack
       ↓
    Capture Activity
       ↓
    Analyze
       ↓
    Generate Intelligence


---

# 17. Open-Source Intelligence

Open-Source Intelligence (OSINT) refers to intelligence collected from publicly available information.

Examples:

- Security research
- Public reports
- Government advisories
- Security blogs
- Public databases
- Technical documentation
- Public vulnerability information
- Security conference presentations


OSINT can provide significant intelligence at relatively low cost.


---

# 18. OSINT Sources

Examples include:

- Security vendor blogs
- CERT advisories
- Public vulnerability databases
- Malware research
- Security researchers
- Public incident reports
- Threat actor research
- Public technical communities


OSINT should be validated before being used for high-impact decisions.


---

# 19. Government Sources

Government agencies often publish:

- Threat advisories
- Vulnerability alerts
- Incident guidance
- Malware reports
- Threat actor information
- Critical infrastructure warnings


Examples include:

- CISA
- CERT-In
- NCSC
- ENISA
- NSA cybersecurity guidance
- Government CERT organizations


Government sources are often valuable because they can provide authoritative information.


---

# 20. CERT and CSIRT Sources

CERT stands for:

**Computer Emergency Response Team**

CSIRT stands for:

**Computer Security Incident Response Team**

These organizations may publish:

- Vulnerability alerts
- Incident notifications
- Malware information
- Threat advisories
- IoCs
- Mitigation guidance


Organizations should prioritize relevant national and sector-specific advisories.


---

# 21. Security Vendor Sources

Security vendors continuously analyze global threats.

Vendor intelligence can include:

- Malware research
- Ransomware analysis
- Threat actor profiles
- Campaign tracking
- IoCs
- TTPs
- Vulnerability intelligence


Examples of vendor research ecosystems include:

- Microsoft Threat Intelligence
- Google Threat Intelligence
- Cisco Talos
- Palo Alto Networks Unit 42
- CrowdStrike
- Mandiant
- Fortinet FortiGuard Labs
- Sophos X-Ops


Vendor intelligence should still be evaluated for relevance to the organization's environment.


---

# 22. Threat Intelligence Platforms

Threat Intelligence Platforms can aggregate information from multiple sources.

Capabilities may include:

- Feed collection
- IoC management
- Enrichment
- Correlation
- Relationship mapping
- Threat actor tracking
- Intelligence sharing


Examples include:

- MISP
- OpenCTI


---

# 23. Threat Intelligence Feeds

Threat feeds provide machine-readable or semi-structured threat information.

Common feed types include:

### IP Feeds

Malicious IP addresses.


### Domain Feeds

Malicious or suspicious domains.


### URL Feeds

Malicious URLs.


### Hash Feeds

Malware file hashes.


### Phishing Feeds

Known phishing infrastructure.


### Malware Feeds

Malware samples and associated indicators.


### Vulnerability Feeds

Information about vulnerabilities and exploitation.


---

# 24. Commercial Threat Intelligence

Commercial intelligence services provide curated intelligence.

Advantages may include:

- High-quality research
- Dedicated analysts
- Threat actor tracking
- Industry-specific intelligence
- Faster reporting
- Structured feeds
- Customer support


Potential disadvantages:

- Cost
- Vendor dependency
- Licensing restrictions
- Different levels of transparency


Commercial intelligence should be evaluated based on operational value.


---

# 25. Community Threat Intelligence

Security communities share intelligence through:

- Research communities
- Security forums
- Open-source projects
- Conferences
- Professional groups
- Collaborative platforms


Community intelligence can provide early signals but may require additional validation.


---

# 26. Industry Information Sharing

Organizations in the same sector may share threat information.

Examples include:

- ISACs
- Industry groups
- Security consortiums
- Sector-specific intelligence communities


This can help identify sector-wide threats.


---

# 27. ISAC

ISAC stands for:

**Information Sharing and Analysis Center**

ISACs facilitate intelligence sharing among organizations within specific sectors.

Examples of sectors may include:

- Financial services
- Healthcare
- Energy
- Transportation
- Communications


ISAC participation can provide sector-specific threat context.


---

# 28. Vulnerability Databases

Vulnerability databases are important intelligence sources.

Examples:

- CVE
- NVD
- Vendor advisories
- CISA Known Exploited Vulnerabilities Catalog


They can provide:

- Vulnerability identifiers
- Severity
- Affected products
- References
- Exploitation information
- Remediation guidance


---

# 29. Exploit Intelligence

Exploit intelligence helps organizations determine whether vulnerabilities are actively being exploited.

Example:

    CVE
      ↓
    Public Exploit
      ↓
    Active Exploitation
      ↓
    Threat Intelligence
      ↓
    Emergency Remediation


This can significantly improve vulnerability prioritization.


---

# 30. Malware Intelligence Sources

Malware intelligence can come from:

- Malware research organizations
- Sandboxes
- Malware repositories
- Security vendors
- Internal malware analysis


Information may include:

- Hashes
- Families
- Behavior
- C2 infrastructure
- Persistence
- TTPs


---

# 31. Phishing Intelligence Sources

Phishing intelligence can include:

- Malicious URLs
- Domains
- Sender addresses
- Email templates
- Attachment hashes
- Credential harvesting infrastructure


Sources include:

- Email security platforms
- Phishing databases
- Security researchers
- Internal reports
- Threat feeds


---

# 32. Domain Intelligence

Domain intelligence may include:

- WHOIS information
- Registration date
- Nameservers
- DNS history
- IP relationships
- Certificate information
- Reputation


Example:

    Domain
       ↓
    WHOIS
       ↓
    DNS
       ↓
    Certificate
       ↓
    Related Infrastructure
       ↓
    Threat Actor


---

# 33. IP Intelligence

IP intelligence may include:

- Reputation
- ASN
- Geolocation
- Hosting provider
- Historical activity
- Related domains
- Malware association
- Threat actor association


IP intelligence is commonly used by SOC teams during alert investigation.


---

# 34. URL Intelligence

URL intelligence can identify:

- Phishing pages
- Malware downloads
- Exploit pages
- Redirect chains
- Credential harvesting


URL analysis may include:

- Domain reputation
- URL structure
- Redirect behavior
- Hosting infrastructure
- Certificate information


---

# 35. Certificate Intelligence

TLS certificates can reveal relationships between infrastructure.

Analysts may examine:

- Certificate fingerprints
- Subject
- Issuer
- Validity
- Associated domains


Certificate relationships can help identify related infrastructure.


---

# 36. Infrastructure Intelligence

Infrastructure intelligence focuses on systems used by attackers.

Examples:

- IP addresses
- Domains
- Servers
- VPS providers
- DNS infrastructure
- Certificates
- Hosting relationships


Example:

    Domain
       ↓
    IP
       ↓
    Certificate
       ↓
    Other Domains
       ↓
    Infrastructure Cluster


---

# 37. Threat Actor Intelligence Sources

Threat actor intelligence can be collected from:

- Security research
- Incident reports
- Malware analysis
- Threat feeds
- Government advisories
- Intelligence vendors
- Historical campaigns


Information may include:

- Motivation
- Targets
- TTPs
- Malware
- Infrastructure
- Campaigns


---

# 38. Threat Research Organizations

Security research organizations continuously investigate threats.

They may publish:

- Threat reports
- Malware research
- Vulnerability research
- Threat actor analysis
- Campaign tracking
- Detection guidance


These sources are valuable for understanding attacker behavior.


---

# 39. Academic Research

Academic research can provide deeper understanding of:

- Attack techniques
- Malware
- Network security
- Cryptography
- Detection methods
- Machine learning
- Threat intelligence methodologies


Academic sources are particularly useful for:

- Research
- Teaching
- Long-term understanding


They may not always provide real-time operational intelligence.


---

# 40. Security Conferences

Security conferences can provide:

- New attack techniques
- Research findings
- Vulnerability disclosures
- Defensive methods
- Threat research


Conference presentations can provide early awareness of emerging techniques.


---

# 41. Dark Web and Underground Sources

Threat intelligence teams may monitor legally accessible underground sources for:

- Stolen credentials
- Data leaks
- Ransomware activity
- Threat actor announcements
- Criminal services


This area requires:

- Legal authorization
- Strong operational controls
- Careful handling of sensitive information


Dark web information should be independently validated before action.


---

# 42. Social Media as a Source

Public social media can sometimes provide early threat signals.

Examples:

- Security researcher posts
- Vulnerability announcements
- Threat actor claims
- Incident reports
- Security community discussions


However:

    Social Media Claim
         ≠
    Confirmed Intelligence


Verification is required.


---

# 43. Threat Intelligence Source Reliability

Sources should be evaluated based on:

- Historical accuracy
- Transparency
- Expertise
- Evidence
- Update frequency
- Independence
- Relevance


A useful question is:

> Can this source's information be independently validated?


---

# 44. Source Reliability vs Information Confidence

These are different concepts.

### Source Reliability

How trustworthy is the source generally?


### Information Confidence

How confident are we about this specific intelligence?


Example:

    Highly Reliable Source
          +
    Limited Evidence
          ↓
    Moderate Confidence


Both should be recorded.


---

# 45. Source Evaluation Framework

A practical evaluation can consider:

| Factor | Question |
|---|---|
| Reliability | Is the source trustworthy? |
| Accuracy | Is the information correct? |
| Timeliness | Is it current? |
| Relevance | Does it apply to us? |
| Context | Does it explain the threat? |
| Coverage | Does it provide useful breadth? |
| Actionability | Can we act on it? |


---

# 46. Threat Feed Evaluation

Before integrating a feed, evaluate:

- False-positive rate
- Indicator freshness
- Duplicate rate
- Coverage
- Source reputation
- Update frequency
- Context availability
- API reliability


Example:

    Feed A
    10,000 IoCs
    80% stale

    Feed B
    2,000 IoCs
    95% relevant


Feed B may provide greater operational value.


---

# 47. Multiple Source Correlation

A single source may be wrong.

Multiple independent sources can increase confidence.

Example:

    Vendor Report
         +
    Government Advisory
         +
    Threat Feed
         +
    Internal Telemetry
         ↓
    Correlation
         ↓
    High Confidence


This is stronger than relying on one source alone.


---

# 48. Source Diversity

A mature intelligence program should use multiple source categories.

Example:

    Government
        +
    Vendor
        +
    OSINT
        +
    Internal Telemetry
        +
    Community
        ↓
    Intelligence Fusion


Source diversity reduces dependence on a single provider.


---

# 49. Source Prioritization

Not every source needs equal priority.

A practical priority model:

### Tier 1

Highly trusted and directly relevant.

### Tier 2

Useful but requires validation.

### Tier 3

Low-confidence or supplementary sources.


Example:

    Tier 1
    Government + Internal + Trusted Vendor

    Tier 2
    Community + OSINT

    Tier 3
    Unverified Reports


---

# 50. Threat Intelligence Source Lifecycle

Sources should themselves be managed.

    Identify Source
         ↓
    Evaluate
         ↓
    Integrate
         ↓
    Monitor Quality
         ↓
    Measure Value
         ↓
    Tune
         ↓
    Retire if Necessary


A source should not remain active simply because it has always been used.


---

# 51. Source Integration with SOC

    Threat Source
         ↓
    Collection
         ↓
    Normalization
         ↓
    Enrichment
         ↓
    SIEM / TIP
         ↓
    Correlation
         ↓
    Alert
         ↓
    SOC Investigation


---

# 52. Source Integration with Threat Hunting

    Threat Source
         ↓
    TTP / IoC
         ↓
    Hunting Hypothesis
         ↓
    SIEM Search
         ↓
    Evidence
         ↓
    Intelligence Update


---

# 53. Source Integration with Incident Response

    Incident
       ↓
    Internal IoC
       ↓
    External Intelligence
       ↓
    Correlation
       ↓
    Related Infrastructure
       ↓
    Expanded Investigation
       ↓
    Containment


---

# 54. Source Integration with Vulnerability Management

    Vulnerability Source
          ↓
    Exploitation Intelligence
          ↓
    Asset Inventory
          ↓
    Exposure Check
          ↓
    Risk Priority
          ↓
    Remediation


---

# 55. AI-Assisted Source Analysis

AI can help process information from multiple sources.

Example:

    Threat Reports
         +
    Advisories
         +
    Vendor Research
         +
    Threat Feeds
         ↓
    AI Processing
         ↓
    Extract IoCs
         ↓
    Extract TTPs
         ↓
    Identify Threat Actors
         ↓
    Detect Relationships
         ↓
    Analyst Validation


AI should not automatically treat every source as trustworthy.


---

# 56. Automated Source Collection

A practical automation pipeline:

    Source APIs
        ↓
    Python Collector
        ↓
    Data Normalization
        ↓
    Deduplication
        ↓
    Validation
        ↓
    Enrichment
        ↓
    Threat Intelligence Platform
        ↓
    SIEM


Possible technologies:

- Python
- REST APIs
- STIX/TAXII
- MISP
- OpenCTI
- SIEM
- SOAR


---

# 57. Source Quality Metrics

Useful metrics include:

- Number of indicators collected
- Percentage of valid indicators
- Duplicate rate
- Stale indicator rate
- False-positive rate
- Detection hits
- Investigation hits
- Feed uptime
- Processing time
- Intelligence usage rate


Example:

    Feed Indicators:
    10,000

    Valid:
    8,500

    Duplicates:
    1,000

    Useful Internal Matches:
    250


This helps determine actual feed value.


---

# 58. Common Source Management Problems

### Problem 1 — Too Many Feeds

Result:

    Alert / Data Overload


### Problem 2 — Poor Validation

Result:

    False Positives


### Problem 3 — Stale Indicators

Result:

    Ineffective Blocking


### Problem 4 — No Context

Result:

    Difficult Investigation


### Problem 5 — Vendor Dependency

Result:

    Limited intelligence diversity


### Problem 6 — No Measurement

Result:

    Unknown ROI


---

# 59. Best Practices

- Define intelligence requirements first
- Use multiple trusted sources
- Prioritize relevant sources
- Validate external intelligence
- Track source reliability
- Monitor indicator freshness
- Remove duplicates
- Enrich indicators
- Correlate external and internal data
- Measure source performance
- Regularly review feeds
- Retire low-value sources
- Automate repetitive processing
- Use AI carefully with human validation


---

# 60. Practical Lab

## Lab: Threat Intelligence Source Evaluation

### Objective

Evaluate three hypothetical threat intelligence sources.

Example:

    Source A
    Government Advisory

    Source B
    Commercial Feed

    Source C
    Community Feed


Evaluate:

- Reliability
- Accuracy
- Timeliness
- Relevance
- Context
- False positives
- Operational usefulness


Create a scoring table:

| Source | Reliability | Timeliness | Relevance | Context | Overall |
|---|---:|---:|---:|---:|---:|
| Source A | High | High | High | High | High |
| Source B | High | High | Medium | High | High |
| Source C | Medium | High | Medium | Medium | Medium |


---

# 61. Practical Lab — IoC Source Correlation

Take one suspicious IP.

Collect information from:

1. Threat feed
2. Reputation source
3. DNS information
4. Internal SIEM
5. Security research


Then compare:

    Source 1
       +
    Source 2
       +
    Source 3
       +
    Internal Data
       ↓
    Correlation
       ↓
    Confidence Assessment


Document the final conclusion.


---

# 62. Portfolio Project

## Project: Threat Intelligence Source Assessment

### Objective

Build a professional source evaluation framework.

### Workflow

    Identify Sources
         ↓
    Categorize
         ↓
    Evaluate Reliability
         ↓
    Measure Quality
         ↓
    Compare Sources
         ↓
    Select Sources
         ↓
    Integrate
         ↓
    Monitor


### Deliverables

- Source inventory
- Source classification
- Evaluation matrix
- Reliability assessment
- Feed comparison
- Integration architecture
- Metrics
- Recommendations


---

# 63. AI Automation Project

## Project: AI-Assisted Threat Source Aggregator

### Objective

Build an automated system that collects threat information from multiple sources and produces structured intelligence.

### Architecture

    Multiple Sources
          ↓
    API / Collection
          ↓
    Normalization
          ↓
    Deduplication
          ↓
    AI Extraction
          ↓
    Classification
          ↓
    Enrichment
          ↓
    Confidence
          ↓
    Human Validation
          ↓
    Threat Intelligence Database
          ↓
    SIEM / SOC


### AI Tasks

AI can assist with:

- Report summarization
- IoC extraction
- TTP extraction
- Threat actor identification
- Source classification
- Duplicate detection
- Relationship identification
- Intelligence summarization


---

# 64. Professional Work Sample

Create a **Threat Intelligence Source Assessment Report** containing:

## Executive Summary

Overview of the evaluated sources.


## Intelligence Requirements

What intelligence the organization needs.


## Source Inventory

List of sources.


## Source Classification

Internal / External / Commercial / Government / Community.


## Reliability Assessment

Source reliability.


## Quality Analysis

Accuracy, freshness and relevance.


## Operational Value

How the source supports:

- SOC
- Threat Hunting
- Incident Response
- Vulnerability Management


## Recommendations

Which sources should be:

- Integrated
- Monitored
- Reduced
- Removed


---

# 65. Teaching Knowledge Base

This topic can be taught in the following sequence:

    What is a Threat Intelligence Source?
          ↓
    Internal Sources
          ↓
    External Sources
          ↓
    OSINT
          ↓
    Government / CERT
          ↓
    Commercial
          ↓
    Threat Feeds
          ↓
    Community
          ↓
    Source Evaluation
          ↓
    Automation
          ↓
    AI


---

# 66. Interview Questions

## Basic

1. What are Threat Intelligence Sources?
2. What is OSINT?
3. What are internal intelligence sources?
4. What is a threat intelligence feed?
5. What is the difference between internal and external intelligence?


## Intermediate

6. How would you evaluate a threat intelligence feed?
7. Why is source reliability important?
8. What is the role of CERT organizations?
9. What is an ISAC?
10. Why should multiple sources be correlated?


## Advanced

11. How would you build a threat intelligence source strategy?
12. How would you measure the ROI of a threat intelligence feed?
13. How would you integrate multiple intelligence sources into a SIEM?
14. How can AI assist with threat intelligence source analysis?
15. How would you handle conflicting information from different sources?


---

# 67. Key Takeaways

Threat Intelligence can come from many sources:

    Internal Telemetry
          +
    Government
          +
    CERT
          +
    Security Vendors
          +
    OSINT
          +
    Threat Feeds
          +
    Research
          +
    Community
          ↓
    Intelligence Fusion


The best source is not necessarily the source with the largest amount of data.

A valuable source should be:

- Reliable
- Relevant
- Timely
- Accurate
- Contextual
- Actionable


---

# 68. Final Principle

> **A mature Threat Intelligence program does not simply collect information from many sources. It selects reliable and relevant sources, validates and correlates their information, measures their value, and converts the resulting intelligence into defensive action.**

Final model:

    Intelligence Requirements
             ↓
        Source Selection
             ↓
          Collection
             ↓
         Validation
             ↓
         Enrichment
             ↓
         Correlation
             ↓
          Analysis
             ↓
        Intelligence
             ↓
      Security Action
             ↓
          Feedback
