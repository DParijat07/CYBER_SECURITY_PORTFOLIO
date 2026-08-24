# 09 - STIX and TAXII

## 1. Introduction

STIX and TAXII are important standards used in cyber threat intelligence.

- **STIX** describes and represents cyber threat intelligence.
- **TAXII** provides a standardized way to exchange that intelligence.

Together, they help organizations share structured threat intelligence between:

- Threat Intelligence Platforms
- SOC platforms
- Security vendors
- CERT organizations
- Government agencies
- Threat intelligence providers
- Security research organizations

Basic relationship:

Threat Intelligence
        ↓
      STIX
        ↓
Structured CTI
        ↓
      TAXII
        ↓
Intelligence Exchange
        ↓
TIP / SIEM / Security Tools


---

## 2. What Is STIX?

STIX stands for:

**Structured Threat Information Expression**

STIX is a standardized language and format for representing cyber threat intelligence.

STIX can represent:

- Indicators
- Malware
- Threat Actors
- Campaigns
- Attack Patterns
- Vulnerabilities
- Infrastructure
- Relationships
- Observed Data
- Reports

STIX helps different security systems understand threat intelligence in a consistent structure.


---

## 3. What Is TAXII?

TAXII stands for:

**Trusted Automated Exchange of Intelligence Information**

TAXII is a protocol designed for exchanging cyber threat intelligence.

Simplified model:

Threat Intelligence Provider
            ↓
          TAXII
            ↓
Threat Intelligence Platform
            ↓
       Security Team

TAXII focuses primarily on the transportation and exchange of threat intelligence.


---

## 4. STIX vs TAXII

The easiest way to understand the difference is:

**STIX = What the intelligence looks like**

**TAXII = How the intelligence is exchanged**

Example:

STIX:

    Indicator:
    Malicious IP
    203.0.113.10

TAXII:

    Provider
       ↓
    TAXII Server
       ↓
    Consumer

Therefore:

    STIX → Representation
    TAXII → Exchange


---

## 5. Why STIX and TAXII Matter

Without standardized formats:

    Vendor A
       ↓
    Format A

    Vendor B
       ↓
    Format B

    Vendor C
       ↓
    Format C

This makes integration difficult.

With standards:

    Provider A ─┐
    Provider B ─┤
    Provider C ─┤
                ↓
             STIX/TAXII
                ↓
             Consumer

This improves interoperability.


---

## 6. STIX Objects

STIX represents threat intelligence using structured objects.

Important STIX objects include:

- Indicator
- Malware
- Threat Actor
- Campaign
- Attack Pattern
- Vulnerability
- Infrastructure
- Intrusion Set
- Tool
- Identity
- Location
- Observed Data
- Report
- Relationship
- Sighting
- Note
- Opinion


---

## 7. STIX Indicator

An Indicator represents a pattern that can be used to detect potentially malicious activity.

Examples:

- Malicious IP
- Malicious domain
- Malicious URL
- File hash

Example:

    Indicator
       |
       +-- Type: IPv4
       +-- Value: 203.0.113.10
       +-- Confidence: High
       +-- Created: Date
       +-- Valid Until: Date

An indicator becomes useful when combined with context.


---

## 8. STIX Malware Object

A Malware object represents malicious software.

Example:

    Malware
       |
       +-- Name
       +-- Malware Type
       +-- Description
       +-- Version
       +-- Capabilities

It can be connected to:

- Indicators
- Threat actors
- Campaigns
- Infrastructure
- Attack techniques


---

## 9. STIX Threat Actor

A Threat Actor object represents an entity responsible for or associated with malicious activity.

Information may include:

- Name
- Description
- Aliases
- Motivation
- Goals
- Associated campaigns

Example:

Threat Actor
      ↓
Uses
      ↓
Malware
      ↓
Communicates With
      ↓
Infrastructure


---

## 10. STIX Campaign

A Campaign represents a coordinated malicious activity over a period of time.

Example:

Campaign
   ├── Threat Actor
   ├── Malware
   ├── Infrastructure
   ├── Victims
   └── Attack Patterns

Campaign-level intelligence helps analysts understand attacks as connected operations.


---

## 11. STIX Attack Pattern

An Attack Pattern describes a technique or method used by an attacker.

These can be mapped to the:

**MITRE ATT&CK framework**

Examples:

- Phishing
- Credential Dumping
- PowerShell
- Command and Scripting Interpreter
- Valid Accounts
- Remote Services

Example:

Threat Actor
      ↓
Attack Pattern
      ↓
Observed Activity


---

## 12. STIX Vulnerability

A Vulnerability object can represent information about a vulnerability.

Example:

    Vulnerability
         |
         +-- CVE
         +-- Description
         +-- Affected Product
         +-- Severity
         +-- References

Example:

CVE
 ↓
Known Exploitation
 ↓
Threat Actor
 ↓
Campaign


---

## 13. STIX Infrastructure

Infrastructure represents technical resources used by threat actors.

Examples:

- Domains
- IP addresses
- Servers
- Botnet infrastructure
- C2 infrastructure

Example:

Threat Actor
      ↓
Uses
      ↓
C2 Infrastructure
      ↓
Domain
      ↓
IP Address


---

## 14. STIX Intrusion Set

An Intrusion Set represents a grouped set of malicious activities that may be associated with a particular threat actor or campaign.

It can include:

- Attack patterns
- Infrastructure
- Malware
- Victimology
- Threat actors

This allows analysts to group related activities.


---

## 15. STIX Tool

A Tool object represents legitimate or malicious software that may be used during an attack.

Examples:

- PowerShell
- PsExec
- Mimikatz
- Remote administration tools
- Network utilities

Example:

Threat Actor
      ↓
Uses
      ↓
Tool
      ↓
Attack Pattern


---

## 16. STIX Relationship

Relationships connect different STIX objects.

Example:

Threat Actor
      |
     uses
      ↓
   Malware

Another example:

Malware
      |
communicates-with
      ↓
Infrastructure

Relationships are important because threat intelligence is not just a collection of isolated indicators.


---

## 17. STIX Sighting

A Sighting indicates that an object was observed.

Example:

Threat Intelligence:

    Malicious IP:
    203.0.113.10

Internal telemetry:

    Firewall observed:
    203.0.113.10

This can create a sighting.

Workflow:

Threat Indicator
      ↓
Internal Observation
      ↓
Sighting
      ↓
SOC Investigation


---

## 18. STIX Observed Data

Observed Data represents information actually observed in an environment.

Examples:

- Network connection
- DNS request
- File hash
- Process execution
- Email address

Example:

Endpoint
   ↓
Process Execution
   ↓
Observed Data
   ↓
Correlation with Indicator


---

## 19. STIX Report

A Report object can group intelligence related to a topic.

Example:

Threat Report
     ↓
Campaign
     ↓
Threat Actor
     ↓
Malware
     ↓
Indicators
     ↓
Attack Patterns


---

## 20. STIX Identity

An Identity object can represent organizations or individuals associated with intelligence.

Examples:

- Security vendor
- Government organization
- Research organization
- Threat intelligence provider

Identity helps identify the source or owner of information.


---

## 21. STIX Bundle

Multiple STIX objects can be grouped into a bundle.

Example:

Bundle
  ├── Threat Actor
  ├── Malware
  ├── Indicator
  ├── Infrastructure
  ├── Attack Pattern
  └── Relationships

This allows multiple related objects to be exchanged together.


---

## 22. STIX Object Relationships

Example:

    Threat Actor
          |
         uses
          ↓
       Malware
          |
    communicates
          ↓
    Infrastructure
          |
       contains
          ↓
       Domain
          |
       resolves
          ↓
         IP

This structure creates an intelligence graph.


---

## 23. STIX Data Model

A simplified model:

    STIX Objects
          ↓
    Properties
          ↓
    Relationships
          ↓
    Intelligence Graph

Each object contains structured information that can be processed by security systems.


---

## 24. STIX Patterning

STIX supports patterns for identifying observable data.

A simplified example:

    [file:hashes.'SHA-256' = 'HASH_VALUE']

This can represent a condition for identifying a file based on its SHA-256 hash.

Other observable properties can include:

- IP address
- Domain
- URL
- File hash
- Network connection


---

## 25. Indicator Pattern

Example concept:

    Indicator
       ↓
    Pattern
       ↓
    Observable
       ↓
    Detection

For example:

    Malicious IP
         ↓
    Indicator Pattern
         ↓
    Firewall / SIEM
         ↓
    Detection


---

## 26. Indicator Validity

Indicators should have lifecycle information.

Important fields include:

- Created
- Modified
- Valid From
- Valid Until

Example:

Indicator Created
      ↓
Valid From
      ↓
Active
      ↓
Valid Until
      ↓
Expired


---

## 27. Confidence

STIX intelligence may include confidence information.

Confidence represents how reliable an intelligence object or assessment is.

Example:

    Indicator
       ↓
    Confidence: High

Confidence should not be confused with severity.

---

## 28. Labels and Markings

Threat intelligence may contain sensitive information.

STIX supports mechanisms for marking and controlling how information should be handled.

Examples:

- Classification
- Sharing restrictions
- Handling instructions

Organizations should respect the distribution requirements associated with intelligence.


---

## 29. TAXII Architecture

A simplified TAXII architecture:

+----------------------+
| Threat Intelligence  |
| Provider             |
+----------------------+
          |
          ↓
      TAXII Server
          |
          ↓
    TAXII Collection
          |
          ↓
      TAXII Client
          |
          ↓
+----------------------+
| Intelligence Consumer|
+----------------------+


---

## 30. TAXII Server

A TAXII server provides threat intelligence to authorized clients.

It may expose:

- Collections
- Objects
- Metadata
- Discovery information

Example:

Threat Provider
      ↓
TAXII Server
      ↓
Collection
      ↓
TAXII Client


---

## 31. TAXII Client

A TAXII client connects to a TAXII server to retrieve or exchange intelligence.

Example:

    TIP
     ↓
TAXII Client
     ↓
TAXII Server
     ↓
Threat Intelligence


---

## 32. TAXII Collections

A TAXII server can organize intelligence into collections.

Example:

    TAXII Server
       |
       +-- Malware Collection
       |
       +-- Phishing Collection
       |
       +-- Vulnerability Collection
       |
       +-- IOC Collection


---

## 33. TAXII Discovery

A TAXII client can discover available TAXII services and collections.

Simplified workflow:

Client
  ↓
Discovery
  ↓
Available Services
  ↓
Available Collections
  ↓
Select Collection
  ↓
Retrieve Intelligence


---

## 34. TAXII Exchange Workflow

A typical workflow:

    Threat Intelligence Provider
              ↓
        Create STIX Objects
              ↓
          TAXII Server
              ↓
          Collection
              ↓
          TAXII Client
              ↓
          TIP / Consumer
              ↓
          Intelligence


---

## 35. STIX + TAXII Architecture

Combined architecture:

Threat Intelligence Provider
          ↓
      STIX Objects
          ↓
      TAXII Server
          ↓
      TAXII Collection
          ↓
      TAXII Client
          ↓
Threat Intelligence Platform
          ↓
    SIEM / SOAR / EDR


---

## 36. STIX + TAXII + TIP

A TIP can act as both a producer and consumer.

Example:

External Provider
      ↓
     TAXII
      ↓
     STIX
      ↓
     TIP
      ↓
Normalization
      ↓
Enrichment
      ↓
Correlation
      ↓
Internal Intelligence
      ↓
SIEM / SOAR / EDR


---

## 37. Threat Intelligence Sharing

Organizations can share intelligence through standardized systems.

Example:

Organization A
      ↓
STIX/TAXII
      ↓
Organization B

This improves interoperability between different security environments.


---

## 38. Information Sharing Communities

Threat intelligence may be shared among:

- CERTs
- ISACs
- Government agencies
- Security vendors
- Research organizations
- Private organizations

STIX/TAXII can help standardize this exchange.


---

## 39. STIX/TAXII and SOC Operations

SOC analysts can benefit from structured intelligence.

Example:

Threat Feed
    ↓
STIX/TAXII
    ↓
TIP
    ↓
SIEM
    ↓
IOC Match
    ↓
SOC Alert
    ↓
Investigation


---

## 40. STIX/TAXII and Threat Hunting

Threat hunters can consume structured intelligence.

Example:

STIX Indicator
      ↓
TIP
      ↓
Threat Hunting Query
      ↓
SIEM / EDR
      ↓
Internal Match
      ↓
Investigation


---

## 41. STIX/TAXII and Incident Response

During an incident:

Suspicious Indicator
       ↓
TIP
       ↓
STIX Relationship Search
       ↓
Related Malware
       ↓
Related Infrastructure
       ↓
Related Threat Actor
       ↓
Expanded Investigation


---

## 42. STIX/TAXII and SIEM

A SIEM can receive intelligence from a TIP that consumes STIX/TAXII data.

Example:

Threat Intelligence Provider
          ↓
        TAXII
          ↓
         STIX
          ↓
         TIP
          ↓
        SIEM
          ↓
     Correlation
          ↓
        Alert


---

## 43. STIX/TAXII and SOAR

SOAR can use structured intelligence for automation.

Example:

SIEM Alert
     ↓
IOC Extraction
     ↓
TIP
     ↓
STIX Intelligence
     ↓
SOAR
     ↓
Enrichment
     ↓
Response


---

## 44. STIX/TAXII and EDR

Example:

Malicious Hash
      ↓
STIX Indicator
      ↓
TIP
      ↓
EDR
      ↓
Endpoint Search
      ↓
Match
      ↓
Investigation


---

## 45. STIX/TAXII and Firewall

Example:

Malicious IP
      ↓
STIX Indicator
      ↓
TIP
      ↓
Firewall Integration
      ↓
Block / Alert


---

## 46. STIX/TAXII Data Flow

A complete enterprise workflow:

    Intelligence Provider
            ↓
         STIX Data
            ↓
       TAXII Server
            ↓
       TAXII Client
            ↓
            TIP
            ↓
    Normalization
            ↓
    Enrichment
            ↓
    Correlation
            ↓
    Threat Scoring
            ↓
      +-----+-----+
      ↓     ↓     ↓
     SIEM  SOAR   EDR
      ↓     ↓     ↓
      +-----+-----+
            ↓
           SOC


---

## 47. Open-Source Intelligence and STIX

Open-source intelligence can be converted into structured STIX objects.

Example:

Security Report
      ↓
IOC Extraction
      ↓
STIX Objects
      ↓
TIP
      ↓
SOC


---

## 48. AI-Assisted STIX Creation

AI can help transform unstructured reports into structured intelligence.

Example:

Threat Report
      ↓
AI Extraction
      ↓
Identify:
- IPs
- Domains
- Hashes
- Malware
- Threat Actors
- TTPs
      ↓
STIX Objects
      ↓
Analyst Validation
      ↓
TIP


---

## 49. AI-Assisted Intelligence Sharing

AI can assist with:

- IOC extraction
- Entity recognition
- TTP extraction
- Relationship identification
- Report summarization
- STIX object generation
- Intelligence classification

Recommended workflow:

AI
 ↓
Structured Intelligence
 ↓
Human Validation
 ↓
STIX
 ↓
TAXII
 ↓
Intelligence Consumer


---

## 50. Human Validation

AI-generated intelligence should be reviewed before distribution.

Recommended:

AI Extraction
     ↓
Analyst Review
     ↓
Validation
     ↓
STIX Object
     ↓
TAXII Distribution

Avoid blindly publishing AI-generated intelligence.


---

## 51. STIX/TAXII Security

Threat intelligence exchange infrastructure should be protected.

Important controls:

- TLS
- Authentication
- Authorization
- API security
- Access control
- Network segmentation
- Audit logging
- Secret management
- Rate limiting
- Monitoring

---

## 52. TAXII Authentication

TAXII services should restrict access to authorized clients.

Security controls may include:

- API credentials
- Certificates
- Tokens
- Mutual TLS
- Identity-based access

The exact mechanism depends on the implementation.


---

## 53. TAXII Rate Limiting

Threat intelligence services may need rate limiting to prevent:

- Abuse
- Excessive requests
- Resource exhaustion
- Denial-of-service conditions

Example:

TAXII Client
     ↓
Request Rate
     ↓
Rate Limiter
     ↓
Allowed / Rejected


---

## 54. Intelligence Sharing Governance

Before sharing intelligence, organizations should consider:

- Data sensitivity
- Legal requirements
- Privacy
- Sharing restrictions
- Source reliability
- Confidence
- Attribution
- Business impact

Technical standards do not replace governance.


---

## 55. Common STIX/TAXII Challenges

Organizations may face:

- Complex implementations
- Version differences
- Schema inconsistencies
- Poor-quality intelligence
- Integration issues
- Large data volumes
- Authentication problems
- Duplicate objects
- Expired indicators
- Incorrect relationships


---

## 56. Common Mistakes

Avoid:

- Treating STIX as the transport protocol
- Treating TAXII as the intelligence format
- Sharing unvalidated intelligence
- Ignoring data markings
- Ignoring indicator expiration
- Publishing sensitive information without authorization
- Using weak authentication
- Hardcoding credentials
- Creating unnecessary duplicate objects


---

## 57. STIX/TAXII Best Practices

1. Use standardized schemas.
2. Validate intelligence before sharing.
3. Track indicator lifecycle.
4. Maintain source information.
5. Maintain confidence values.
6. Use appropriate access controls.
7. Secure TAXII endpoints.
8. Monitor exchange infrastructure.
9. Deduplicate intelligence.
10. Maintain relationships between objects.
11. Respect sharing restrictions.
12. Review intelligence quality.
13. Use human validation for AI-generated intelligence.


---

## 58. Practical Lab — STIX Indicator Creation

### Objective

Create structured STIX indicators.

Create indicators for:

- IP address
- Domain
- URL
- SHA-256 hash

Document:

- Indicator type
- Value
- Confidence
- Description
- Created time
- Validity


---

## 59. Practical Lab — STIX Relationship Mapping

Create a simple intelligence graph.

Example:

Threat Actor
      ↓
Uses
      ↓
Malware
      ↓
Communicates With
      ↓
Domain
      ↓
Resolves To
      ↓
IP


---

## 60. Practical Lab — TAXII Collection

### Objective

Build or use an authorized TAXII environment to understand intelligence exchange.

Workflow:

TAXII Server
      ↓
Collection
      ↓
TAXII Client
      ↓
Retrieve STIX Objects
      ↓
TIP
      ↓
Analyze


---

## 61. Practical Lab — STIX/TAXII + SIEM

### Objective

Create a pipeline that consumes structured intelligence and uses it for detection.

Workflow:

TAXII
  ↓
STIX
  ↓
TIP
  ↓
IOC Extraction
  ↓
SIEM
  ↓
Log Correlation
  ↓
SOC Alert


---

## 62. Portfolio Project

### Project: STIX/TAXII Threat Intelligence Exchange Lab

### Objective

Build a professional lab demonstrating how structured threat intelligence can be exchanged between a threat intelligence provider, TIP, and SOC security systems.

### Architecture

Threat Intelligence Source
        ↓
      STIX
        ↓
    TAXII Server
        ↓
    TAXII Client
        ↓
       TIP
        ↓
Normalization
        ↓
Enrichment
        ↓
Correlation
        ↓
SIEM / SOAR / EDR


---

## 63. Project Components

Implement:

- STIX indicator creation
- STIX object relationships
- TAXII collection
- TAXII client
- Intelligence ingestion
- Normalization
- Deduplication
- Enrichment
- Threat scoring
- TIP integration
- SIEM integration
- Detection use cases
- Documentation


---

## 64. AI Automation Project

### Project: AI-Assisted STIX Intelligence Generator

### Objective

Create a workflow that extracts structured threat intelligence from security reports and prepares STIX objects for analyst validation.

Workflow:

Threat Report
      ↓
AI Processing
      ↓
IOC Extraction
      ↓
Entity Extraction
      ↓
TTP Extraction
      ↓
Relationship Discovery
      ↓
STIX Object Generation
      ↓
Analyst Validation
      ↓
TAXII
      ↓
TIP
      ↓
SOC Systems


---

## 65. AI Features

Possible features:

- Automatic IOC extraction
- Malware identification
- Threat actor identification
- TTP extraction
- Relationship discovery
- STIX object generation
- Report summarization
- Threat scoring
- Intelligence classification

AI should assist the analyst rather than replace validation.


---

## 66. Professional Work Sample

Create:

**STIX/TAXII Threat Intelligence Exchange Architecture Report**

Include:

### Executive Summary

Explain the purpose of the implementation.

### Architecture

Document the STIX/TAXII architecture.

### Intelligence Sources

Document intelligence providers.

### STIX Objects

Document the objects used.

### Relationships

Document intelligence relationships.

### TAXII Exchange

Document the exchange workflow.

### Security Controls

Document authentication and access controls.

### SIEM Integration

Document how intelligence reaches the SIEM.

### Detection Use Cases

Document detection scenarios.

### AI Automation

Document AI-assisted intelligence processing.

### Testing

Document test cases and results.

### Lessons Learned

Document implementation challenges.

### Recommendations

Document future improvements.


---

## 67. SOC Analyst Workflow

When structured intelligence reaches the SOC:

STIX/TAXII
     ↓
TIP
     ↓
SIEM
     ↓
IOC Match
     ↓
Alert
     ↓
L1 Analyst
     ↓
TIP Investigation
     ↓
Related Intelligence
     ↓
Internal Telemetry
     ↓
Assessment
     ↓
Escalation


---

## 68. L1 SOC Interview Example

### Question

What is the difference between STIX and TAXII?

### Answer

STIX is a standardized format used to represent cyber threat intelligence, such as indicators, malware, threat actors, campaigns, and relationships.

TAXII is a protocol used to exchange that structured threat intelligence between systems.

Simple explanation:

**STIX describes the intelligence; TAXII transports or exchanges it.**


---

## 69. Interview Questions

### Basic

1. What is STIX?
2. What is TAXII?
3. What does STIX stand for?
4. What does TAXII stand for?
5. What is the difference between STIX and TAXII?
6. Why are STIX and TAXII useful?
7. What is a STIX Indicator?
8. What is a STIX Relationship?

### Intermediate

9. What are common STIX objects?
10. What is a STIX Malware object?
11. What is a Threat Actor object?
12. What is a Campaign object?
13. What is an Attack Pattern?
14. What is a Sighting?
15. What is a STIX Bundle?
16. How does TAXII exchange intelligence?
17. What is a TAXII Collection?
18. How does a TIP use STIX/TAXII?

### Advanced

19. Design a STIX/TAXII architecture for a SOC.
20. How would you integrate TAXII with a TIP?
21. How would you send intelligence from a TIP to a SIEM?
22. How would you handle duplicate STIX objects?
23. How would you validate intelligence before sharing?
24. How would you secure a TAXII server?
25. How would you manage sensitive threat intelligence?
26. How could AI generate STIX intelligence?
27. How would you validate AI-generated STIX objects?
28. How would you design a scalable threat intelligence exchange platform?


---

## 70. Key Takeaways

STIX provides a structured way to represent cyber threat intelligence.

TAXII provides a standardized mechanism for exchanging that intelligence.

The relationship is:

STIX
 ↓
Threat Intelligence Representation
 ↓
TAXII
 ↓
Threat Intelligence Exchange
 ↓
TIP
 ↓
SIEM / SOAR / EDR
 ↓
SOC


---

## 71. Final Principle

> STIX provides the language for describing cyber threat intelligence, while TAXII provides a standardized mechanism for exchanging that intelligence.

A mature threat intelligence architecture combines:

    Quality Intelligence
          +
        STIX
          +
        TAXII
          +
          TIP
          +
      Correlation
          +
       Automation
          +
      Human Analysis
          +
      AI Assistance
          ↓
    Actionable Threat Intelligence
          ↓
    Better Detection
          ↓
    Faster Investigation
          ↓
    Improved Security Operations
