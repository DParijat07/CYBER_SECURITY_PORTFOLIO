# 04 - Threat Intelligence

## Overview

Threat Intelligence is the process of collecting, analyzing, validating, and applying information about cyber threats to improve an organization's security decisions and defensive capabilities.

Threat Intelligence helps security teams understand:

- Who may be targeting the organization
- What threats are relevant
- How attackers operate
- Which Indicators of Compromise (IoCs) are associated with threats
- Which vulnerabilities are being exploited
- Which MITRE ATT&CK techniques are being used
- How existing security controls can be improved
- What actions the SOC should take

The fundamental objective is:

    Raw Threat Data
          ↓
    Analysis
          ↓
    Threat Intelligence
          ↓
    Security Decision
          ↓
    Defensive Action


---

## Purpose of This Directory

This directory documents the practical implementation of Threat Intelligence within a SOC environment.

It combines:

- Threat Intelligence concepts
- Threat intelligence lifecycle
- Intelligence sources
- IoCs
- Threat actors
- Tactics, Techniques and Procedures
- MITRE ATT&CK
- Threat feeds
- IoC enrichment
- Threat intelligence platforms
- Intelligence analysis
- Threat hunting
- Detection engineering
- Incident response
- Intelligence reporting
- Automation
- AI-assisted threat intelligence


---

## Learning Objectives

After completing this section, the learner should be able to:

- Understand Threat Intelligence fundamentals
- Differentiate threat data from threat intelligence
- Understand the Threat Intelligence Lifecycle
- Identify different types of intelligence
- Work with Indicators of Compromise
- Analyze malicious IPs, domains, URLs and hashes
- Understand threat actors and campaigns
- Use MITRE ATT&CK for intelligence analysis
- Evaluate threat intelligence feeds
- Enrich security alerts using intelligence
- Apply intelligence to SIEM detections
- Support threat hunting with intelligence
- Produce professional intelligence reports
- Automate repetitive intelligence tasks
- Understand AI-assisted threat intelligence workflows


---

# Threat Intelligence in a SOC

Threat Intelligence acts as a bridge between external threat information and internal security operations.

Example:

    External Threat Intelligence
              ↓
       Malicious IP
              ↓
        SIEM Search
              ↓
       Internal Match
              ↓
       SOC Investigation
              ↓
       Incident Response


Threat Intelligence therefore supports multiple SOC functions.


---

# Threat Intelligence Functions

Threat Intelligence can support:

- Security Monitoring
- Detection Engineering
- Threat Hunting
- Incident Response
- Vulnerability Management
- Risk Management
- Security Architecture
- Executive Decision-Making


---

# Types of Threat Intelligence

## 1. Strategic Intelligence

Focuses on high-level threats and business risk.

Audience:

- Executives
- Security leadership
- Risk teams
- Business leaders


## 2. Tactical Intelligence

Focuses on attacker tactics, techniques and procedures.

Audience:

- SOC
- Threat hunters
- Detection engineers
- Security analysts


## 3. Operational Intelligence

Focuses on active campaigns and attacker operations.

Audience:

- SOC
- Incident responders
- Threat intelligence analysts


## 4. Technical Intelligence

Focuses on technical indicators.

Examples:

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses
- Malware signatures


---

# Threat Intelligence Lifecycle

The Threat Intelligence Lifecycle generally follows:

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


The lifecycle is continuous.


---

# Intelligence Sources

Threat intelligence can come from:

- Security vendors
- Government agencies
- CERT organizations
- Open-source intelligence
- Security researchers
- Threat intelligence platforms
- ISACs
- Internal incident data
- Malware analysis
- Honeypots
- Security communities


Sources must be evaluated for:

- Reliability
- Accuracy
- Timeliness
- Relevance
- Context


---

# Indicators of Compromise

Common IoCs include:

- IPv4 addresses
- IPv6 addresses
- Domains
- URLs
- File hashes
- Email addresses
- Malware names
- File names
- Registry keys
- User agents
- Certificate fingerprints


IoCs should not be treated as automatically malicious.

Context and validation are required.


---

# IoC Lifecycle

    IoC Collected
         ↓
    Validate
         ↓
    Enrich
         ↓
    Score
         ↓
    Correlate
         ↓
    Detect
         ↓
    Investigate
         ↓
    Respond
         ↓
    Retire


---

# Threat Actors

Threat intelligence can help identify:

- Threat actors
- Cybercriminal groups
- Nation-state groups
- Hacktivist groups
- Insider threats
- Initial access brokers
- Ransomware groups


Threat actor attribution should be handled carefully.

Attribution should be based on evidence and confidence rather than assumptions.


---

# Tactics, Techniques and Procedures

TTPs describe how attackers operate.

Example:

    Initial Access
          ↓
    Execution
          ↓
    Persistence
          ↓
    Privilege Escalation
          ↓
    Defense Evasion
          ↓
    Credential Access
          ↓
    Discovery
          ↓
    Lateral Movement
          ↓
    Collection
          ↓
    Command and Control
          ↓
    Exfiltration
          ↓
    Impact


TTP-based intelligence is generally more durable than relying only on individual IoCs.


---

# MITRE ATT&CK

MITRE ATT&CK provides a knowledge base of adversary behavior.

Threat intelligence can be mapped to:

- Tactics
- Techniques
- Sub-techniques
- Procedures
- Groups
- Software


Example:

    Threat Actor
         ↓
    Technique
         ↓
    Detection
         ↓
    Investigation
         ↓
    Response


---

# Threat Intelligence and SIEM

Threat intelligence can enrich SIEM monitoring.

Example:

    Threat Feed
         ↓
    Malicious IP
         ↓
    SIEM
         ↓
    Internal Log Match
         ↓
    Alert
         ↓
    SOC Investigation


This creates a practical connection between external intelligence and internal telemetry.


---

# Threat Intelligence and Threat Hunting

Threat intelligence provides hypotheses for threat hunting.

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
    Internal Match?
          ↓
       Yes / No


---

# Threat Intelligence and Incident Response

During an incident, intelligence can help:

- Identify malicious infrastructure
- Enrich IoCs
- Identify malware
- Understand attacker behavior
- Identify related campaigns
- Identify additional compromised systems
- Improve containment decisions


---

# Threat Intelligence and Vulnerability Management

Threat intelligence can help prioritize vulnerabilities.

Example:

    Vulnerability
         +
    Active Exploitation
         +
    Critical Asset
         ↓
    High Priority


This is more useful than prioritizing vulnerabilities based only on severity scores.


---

# Threat Intelligence and Detection Engineering

Threat intelligence can produce:

- New detection rules
- New SIEM queries
- New YARA rules
- New Sigma rules
- New correlation logic
- New hunting hypotheses


Workflow:

    Threat Intelligence
          ↓
    Attack Behavior
          ↓
    Detection Logic
          ↓
    Testing
          ↓
    Production


---

# Threat Intelligence Enrichment

Enrichment adds context to raw indicators.

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
    Historical Activity
       ↓
    Related Domains
       ↓
    Threat Actor
       ↓
    Confidence Score


Enrichment helps analysts make better decisions.


---

# Threat Intelligence Platforms

A Threat Intelligence Platform (TIP) can help organizations:

- Collect intelligence
- Normalize data
- Enrich IoCs
- Correlate indicators
- Manage threat feeds
- Share intelligence
- Track relationships


Possible platforms and technologies include:

- MISP
- OpenCTI
- STIX/TAXII
- VirusTotal
- AlienVault OTX
- Abuse.ch
- Threat intelligence APIs


These should be evaluated according to organizational requirements.


---

# STIX and TAXII

## STIX

Structured Threat Information Expression (STIX) is a standardized language for representing cyber threat intelligence.

It can represent:

- Indicators
- Malware
- Threat actors
- Campaigns
- Attack patterns
- Relationships


## TAXII

Trusted Automated Exchange of Intelligence Information (TAXII) provides a protocol for exchanging cyber threat intelligence.

Simplified model:

    STIX
    ↓
    Intelligence Format

    TAXII
    ↓
    Intelligence Transport


---

# Threat Intelligence Automation

Automation can help:

- Collect threat feeds
- Normalize indicators
- Enrich IoCs
- Deduplicate indicators
- Score indicators
- Update SIEM watchlists
- Create tickets
- Trigger alerts


Example:

    Threat Feed
         ↓
    Automation
         ↓
    Normalize
         ↓
    Enrich
         ↓
    Validate
         ↓
    SIEM
         ↓
    Detection


---

# AI and Threat Intelligence

AI can assist with:

- Threat report summarization
- Indicator classification
- Threat clustering
- Campaign correlation
- TTP extraction
- Threat actor analysis
- Intelligence prioritization
- Natural-language search
- Report generation


Example:

    Threat Reports
         ↓
    AI Processing
         ↓
    Extract IoCs
         ↓
    Extract TTPs
         ↓
    Map to ATT&CK
         ↓
    Analyst Validation
         ↓
    Intelligence Report


AI-generated intelligence should always be validated against trusted evidence.


---

# Professional Threat Intelligence Workflow

    Intelligence Requirement
             ↓
         Collection
             ↓
         Processing
             ↓
          Analysis
             ↓
        Enrichment
             ↓
       Correlation
             ↓
       Intelligence
             ↓
       Dissemination
             ↓
      Security Action
             ↓
         Feedback


---

# Portfolio Projects

This directory will contain practical, project-based Threat Intelligence work.

Potential projects include:

### Project 1 — IoC Analysis Lab

Analyze:

- IPs
- Domains
- URLs
- Hashes

Produce:

- Enrichment
- Risk assessment
- Confidence score
- Investigation recommendations


### Project 2 — Threat Intelligence Feed Integration

Build a workflow:

    Threat Feed
       ↓
    Normalization
       ↓
    Enrichment
       ↓
    SIEM
       ↓
    Alert


### Project 3 — MISP Threat Intelligence Lab

Build a small threat intelligence environment using MISP.

Document:

- Feed ingestion
- IoC management
- Event creation
- Correlation
- Sharing


### Project 4 — MITRE ATT&CK Intelligence Mapping

Map:

    Threat Actor
       ↓
    Campaign
       ↓
    TTPs
       ↓
    ATT&CK Techniques
       ↓
    Detection Coverage


### Project 5 — AI-Assisted Threat Intelligence

Build an AI-assisted workflow for:

    Threat Reports
       ↓
    Extraction
       ↓
    IoCs
       ↓
    TTPs
       ↓
    ATT&CK Mapping
       ↓
    Analyst Validation
       ↓
    Intelligence Report


---

# Professional Work Samples

This directory should demonstrate practical cybersecurity capability through:

- Threat intelligence reports
- IoC analysis
- Threat actor profiles
- Threat campaign analysis
- Intelligence briefs
- Detection mappings
- Threat hunting hypotheses
- Intelligence dashboards
- Automation workflows
- AI-assisted intelligence workflows


The objective is to demonstrate **how intelligence is transformed into security action**.


---

# Teaching Knowledge Base

This directory also functions as a knowledge base for future cybersecurity teaching.

Documentation should explain concepts from:

    Beginner
       ↓
    Intermediate
       ↓
    Practical
       ↓
    Professional


Topics should include:

- Definitions
- Concepts
- Examples
- Workflows
- Tools
- Labs
- Case studies
- Practical exercises
- Interview questions


---

# Freelance / Client Demonstration

The Threat Intelligence portfolio can demonstrate services such as:

- IoC investigation
- Threat feed setup
- Threat intelligence reporting
- Security monitoring enrichment
- Threat hunting support
- Intelligence automation
- SIEM threat intelligence integration
- Security intelligence dashboards


Client-facing work should avoid exposing confidential information.


---

# Hiring Manager Value

This directory demonstrates understanding of:

- SOC operations
- Threat intelligence
- Security monitoring
- IoC analysis
- MITRE ATT&CK
- Detection engineering
- Threat hunting
- Incident response
- Automation
- AI-assisted cybersecurity


It shows that the learner can move from:

    Threat Data
         ↓
    Intelligence
         ↓
    Analysis
         ↓
    Detection
         ↓
    Investigation
         ↓
    Response


---

# AI Automation Strategy

AI automation should be incorporated throughout this domain.

Potential workflow:

    Threat Sources
         ↓
    Automated Collection
         ↓
    Data Normalization
         ↓
    AI Extraction
         ↓
    IoC Extraction
         ↓
    TTP Extraction
         ↓
    ATT&CK Mapping
         ↓
    Correlation
         ↓
    Analyst Validation
         ↓
    Intelligence Report
         ↓
    SIEM / Threat Hunting


Human validation remains mandatory for high-impact security decisions.


---

# Directory Structure

The directory will contain a maximum of **20 core documentation files**, followed by project sections.

Recommended structure:

    04-Threat-Intelligence/
    │
    ├── README.md
    │
    ├── 01-Threat-Intelligence-Concepts.md
    ├── 02-Threat-Intelligence-Lifecycle.md
    ├── 03-Threat-Intelligence-Types.md
    ├── 04-Threat-Intelligence-Sources.md
    ├── 05-Indicators-of-Compromise.md
    ├── 06-Threat-Actors-and-Campaigns.md
    ├── 07-TTPs-and-MITRE-ATTACK.md
    ├── 08-Threat-Intelligence-Feeds.md
    ├── 09-Threat-Intelligence-Enrichment.md
    ├── 10-STIX-and-TAXII.md
    ├── 11-Threat-Intelligence-Platforms.md
    ├── 12-IoC-Analysis.md
    ├── 13-Threat-Intelligence-and-SIEM.md
    ├── 14-Threat-Intelligence-and-Threat-Hunting.md
    ├── 15-Threat-Intelligence-and-Incident-Response.md
    ├── 16-Threat-Intelligence-and-Detection-Engineering.md
    ├── 17-Threat-Intelligence-Reporting.md
    ├── 18-Threat-Intelligence-Automation.md
    ├── 19-AI-Assisted-Threat-Intelligence.md
    ├── 20-Threat-Intelligence-Metrics.md
    │
    └── Projects/
        ├── 01-IoC-Analysis-Lab/
        ├── 02-Threat-Feed-Integration/
        ├── 03-MISP-Threat-Intelligence-Lab/
        ├── 04-MITRE-ATTACK-Intelligence-Mapping/
        └── 05-AI-Threat-Intelligence-Automation/


---

# Documentation Standard

Every documentation file should preferably contain:

1. Definition
2. Purpose
3. Core concepts
4. Architecture / workflow
5. Practical examples
6. Tools
7. SOC relevance
8. Detection relevance
9. Incident response relevance
10. Automation opportunities
11. AI opportunities
12. Practical lab
13. Professional use case
14. Key takeaways


---

# Evidence of Learning

Evidence should include:

- GitHub documentation
- Screenshots
- Lab results
- Threat intelligence reports
- IoC investigations
- Detection rules
- SIEM queries
- MITRE ATT&CK mappings
- Automation scripts
- Dashboards
- Project reports


---

# Portfolio Philosophy

This directory follows the overall portfolio philosophy:

    LEARN
      ↓
    PRACTICE
      ↓
    DOCUMENT
      ↓
    BUILD
      ↓
    AUTOMATE
      ↓
    VALIDATE
      ↓
    SHOWCASE
      ↓
    TEACH


The goal is not to collect theoretical notes.

The goal is to demonstrate **practical cybersecurity capability through professional work samples**.


---

# Final Goal

The Threat Intelligence section should demonstrate the ability to transform external and internal threat information into actionable cybersecurity intelligence.

The complete capability is:

    Threat Data
         ↓
    Collection
         ↓
    Processing
         ↓
    Enrichment
         ↓
    Analysis
         ↓
    Intelligence
         ↓
    Detection
         ↓
    Threat Hunting
         ↓
    Incident Response
         ↓
    Continuous Improvement


## Core Principle

> **Threat Intelligence is valuable when it leads to better security decisions and measurable defensive action.**
