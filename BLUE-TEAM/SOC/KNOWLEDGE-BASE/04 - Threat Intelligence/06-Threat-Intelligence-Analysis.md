# Threat Intelligence Analysis

## 1. Introduction

Threat Intelligence Analysis is the process of examining collected security information, identifying meaningful patterns and relationships, assessing risk, and converting raw data into actionable intelligence.

The objective is not simply to identify Indicators of Compromise (IoCs).

The objective is to understand:

- What is happening?
- Who is behind it?
- How is the attack being conducted?
- Why is it happening?
- Who or what is being targeted?
- What is the potential impact?
- What should the organization do?

### Threat Intelligence Analysis Flow

    Raw Data
        ↓
    Collection
        ↓
    Validation
        ↓
    Enrichment
        ↓
    Analysis
        ↓
    Context
        ↓
    Intelligence
        ↓
    Decision
        ↓
    Security Action


---

# 2. Data vs Information vs Intelligence

These concepts should not be confused.

## Data

Raw observations.

Example:

    IP: 203.0.113.10

## Information

Data with basic context.

Example:

    203.0.113.10 was observed communicating
    with an internal workstation.

## Intelligence

Analyzed information that supports a decision.

Example:

    The destination IP is associated with
    known malicious infrastructure and the
    workstation should be investigated.

### Transformation

    Data
      ↓
    Information
      ↓
    Analysis
      ↓
    Intelligence


---

# 3. Purpose of Threat Intelligence Analysis

Threat intelligence analysis helps organizations:

- Understand threats
- Identify threat actors
- Identify attack campaigns
- Discover attacker infrastructure
- Understand TTPs
- Prioritize vulnerabilities
- Improve detections
- Support threat hunting
- Support incident response
- Improve security strategy
- Support executive decision-making


---

# 4. Intelligence Analysis Lifecycle

A practical analysis lifecycle is:

    Define Requirement
           ↓
       Collect Information
           ↓
       Validate
           ↓
       Normalize
           ↓
       Enrich
           ↓
       Correlate
           ↓
       Analyze
           ↓
       Assess Confidence
           ↓
       Develop Intelligence
           ↓
       Disseminate
           ↓
       Feedback

Analysis is therefore part of a larger intelligence lifecycle.


---

# 5. Intelligence Requirements

Analysis should always begin with a question.

Examples:

- Are attackers targeting our organization?
- Which vulnerabilities are actively exploited?
- Which threat actors target our industry?
- Is this IP address malicious?
- Is this activity related to a known campaign?

Without a defined question, analysts may spend time investigating information that has little operational value.


---

# 6. Analysis Questions

A useful analyst framework is:

### What?

What happened?

### Who?

Who is responsible?

### When?

When did the activity occur?

### Where?

Where did the activity originate and where was it targeted?

### How?

What techniques were used?

### Why?

What is the likely motivation?

### What Next?

What could happen next?

This framework helps structure investigations.


---

# 7. IoC Analysis

Indicators of Compromise include:

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses
- File paths
- Registry keys

IoCs should not be treated as isolated values.

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

This provides greater context.


---

# 8. IP Address Analysis

When analyzing an IP address, examine:

- Reputation
- ASN
- Hosting provider
- Geolocation
- Historical activity
- Associated domains
- Related malware
- Threat actor associations
- First seen
- Last seen

Example:

    Suspicious IP
         ↓
    Reputation
         ↓
    Infrastructure
         ↓
    Historical Activity
         ↓
    Related Domains
         ↓
    Threat Actor


---

# 9. Domain Analysis

Domain analysis may include:

- Registration information
- Creation date
- DNS records
- Nameservers
- Hosting provider
- Associated IPs
- TLS certificates
- Historical resolution
- Similar domains

Example:

    Domain
      ↓
    DNS
      ↓
    IP
      ↓
    Certificate
      ↓
    Related Domains
      ↓
    Infrastructure Cluster


---

# 10. URL Analysis

URL analysis can help identify:

- Phishing
- Malware delivery
- Exploit attempts
- Credential harvesting
- Redirect chains

Analysts may examine:

- Domain
- Path
- Parameters
- Redirects
- Reputation
- Hosting infrastructure
- Certificate


---

# 11. File Hash Analysis

Hashes are commonly used to identify files.

Examples:

- MD5
- SHA-1
- SHA-256

A hash can be searched against authorized threat intelligence sources.

Example:

    SHA-256
       ↓
    Reputation
       ↓
    Malware Family
       ↓
    First Seen
       ↓
    Related Infrastructure
       ↓
    Threat Actor

A hash alone does not explain the entire attack.


---

# 12. Malware Analysis Correlation

Malware intelligence becomes more useful when combined with other indicators.

Example:

    Malware
       ↓
    Hash
       ↓
    C2 Domain
       ↓
    C2 IP
       ↓
    Campaign
       ↓
    Threat Actor

This helps analysts understand the broader attack infrastructure.


---

# 13. TTP Analysis

TTP stands for:

**Tactics, Techniques, and Procedures**

TTP analysis focuses on attacker behavior.

Examples:

- Phishing
- PowerShell
- Credential dumping
- Persistence
- Lateral movement
- Remote services
- Data exfiltration

TTPs are often more valuable for long-term detection than individual IoCs.


---

# 14. MITRE ATT&CK Mapping

MITRE ATT&CK provides a structured framework for describing adversary behavior.

Example:

    Observed Activity
          ↓
    PowerShell
          ↓
    ATT&CK Technique
          ↓
    T1059.001

ATT&CK mapping helps analysts:

- Understand attacker behavior
- Build detections
- Develop hunting hypotheses
- Identify defensive gaps
- Communicate findings


---

# 15. Attack Chain Analysis

Threat intelligence can be mapped to an attack lifecycle.

Example:

    Reconnaissance
          ↓
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
    Command & Control
          ↓
    Exfiltration
          ↓
    Impact

This helps analysts understand where defensive controls can interrupt an attack.


---

# 16. Timeline Analysis

Timeline analysis reconstructs events in chronological order.

Example:

    09:00  Phishing email received
    09:05  User clicked URL
    09:06  Payload downloaded
    09:07  PowerShell executed
    09:08  C2 connection established
    09:15  Credential access detected
    09:20  Lateral movement observed

Timeline analysis is particularly useful during incident response.


---

# 17. Campaign Analysis

A campaign represents a coordinated set of malicious activities.

Analysts may correlate:

- Infrastructure
- Malware
- Victims
- TTPs
- Time periods
- Threat actors

Example:

    Campaign
       ├── Domain A
       ├── Domain B
       ├── IP A
       ├── Malware X
       ├── TTP Y
       └── Target Industry

Campaign analysis helps identify relationships that may not be visible when individual indicators are examined separately.


---

# 18. Threat Actor Analysis

Threat actor analysis attempts to understand:

- Identity
- Motivation
- Capabilities
- Targets
- Infrastructure
- Malware
- TTPs
- Historical campaigns

Possible motivations include:

- Financial gain
- Espionage
- Disruption
- Intelligence gathering
- Ideological objectives

Attribution should be handled carefully because available evidence may be incomplete.


---

# 19. Threat Actor Attribution

Attribution means determining who may be responsible for an activity.

Possible evidence includes:

- Infrastructure
- Malware
- TTPs
- Language
- Targeting
- Operational patterns
- Historical relationships

However:

    Indicator
       ≠
    Proof of Attribution

Attribution should be expressed using confidence levels rather than unsupported certainty.


---

# 20. Infrastructure Analysis

Infrastructure analysis examines relationships between attacker-controlled systems.

Example:

    Domain A
       ↓
    IP A
       ↓
    Certificate A
       ↓
    Domain B
       ↓
    IP B
       ↓
    Malware

This can help identify additional infrastructure that may not yet appear in standard threat feeds.


---

# 21. Infrastructure Clustering

Related infrastructure can be grouped into clusters.

Possible relationships:

- Shared IP
- Shared certificate
- Shared nameserver
- Shared registration pattern
- Shared malware
- Shared domain patterns
- Shared hosting

Example:

                 Threat Infrastructure
                         |
            ┌────────────┼────────────┐
            ↓            ↓            ↓
         Domain A      Domain B      Domain C
            ↓            ↓            ↓
           IP A         IP B         IP C
            └────────────┼────────────┘
                         ↓
                   Common Pattern


---

# 22. Relationship Analysis

Threat intelligence can be represented as relationships.

Example:

    Threat Actor
         ↓ uses
      Malware
         ↓ communicates with
       Domain
         ↓ resolves to
         IP
         ↓ hosted by
      Provider

Relationship analysis is particularly useful in graph-based intelligence platforms.


---

# 23. Threat Intelligence Graphs

A threat intelligence graph represents entities and relationships.

Example:

    [Threat Actor]
          |
          | uses
          ↓
       [Malware]
          |
          | communicates with
          ↓
       [Domain]
          |
          | resolves to
          ↓
         [IP]

Graph analysis can reveal hidden relationships.


---

# 24. Temporal Analysis

Threat activity changes over time.

Analysts should consider:

- First seen
- Last seen
- Campaign duration
- Infrastructure changes
- Malware evolution
- TTP changes

Example:

    January
    Domain A

    February
    Domain A + Domain B

    March
    New IP infrastructure

    April
    New malware version

This can reveal campaign evolution.


---

# 25. Trend Analysis

Trend analysis looks for changes over longer periods.

Examples:

- Increase in ransomware
- Increase in phishing
- Growth of credential attacks
- Increase in exploitation of a vulnerability
- Changes in attacker techniques

Example:

    Month 1 → 20 incidents
    Month 2 → 35 incidents
    Month 3 → 60 incidents

This may indicate an increasing threat trend.


---

# 26. Geographical Analysis

Threat intelligence may include geographic information.

Analysts may examine:

- Source location
- Target location
- Hosting location
- Campaign geography

Geolocation alone should not be treated as proof of attacker identity because infrastructure may be proxied or compromised.


---

# 27. Industry Targeting Analysis

Analysts can identify which sectors are being targeted.

Example:

    Healthcare
        ↓
    Ransomware

    Financial
        ↓
    Credential Theft

    Manufacturing
        ↓
    OT / ICS Attacks

Industry context helps prioritize intelligence.


---

# 28. Vulnerability Intelligence Analysis

Vulnerability analysis should consider:

- Severity
- Exploit availability
- Active exploitation
- Asset exposure
- Business criticality
- Patch availability

Example:

    Critical CVE
        +
    Public Exploit
        +
    Internet-Facing Asset
        +
    Active Exploitation
        ↓
    Very High Priority


---

# 29. Risk-Based Intelligence Analysis

Threat intelligence should be connected to risk.

A simplified model:

    Threat
       +
    Likelihood
       +
    Asset Exposure
       +
    Potential Impact
       ↓
    Risk

This helps organizations prioritize actions.


---

# 30. Confidence Assessment

Intelligence analysis should include confidence.

### High Confidence

Multiple independent sources plus internal evidence.

### Medium Confidence

Reliable source plus partial evidence.

### Low Confidence

Single source with limited supporting evidence.

Confidence should be based on evidence quality rather than intuition.


---

# 31. Source Reliability

Source reliability and intelligence confidence are separate.

### Source Reliability

How trustworthy is the source generally?

### Confidence

How confident are we about this particular finding?

Example:

    Reliable Source
          +
    Weak Evidence
          =
    Moderate Confidence


---

# 32. Hypothesis-Driven Analysis

Analysts can create hypotheses and test them.

Example:

### Hypothesis

    The workstation may be communicating
    with attacker-controlled infrastructure.

### Evidence

- DNS logs
- Firewall logs
- EDR
- Threat intelligence

### Analysis

    Evidence supports hypothesis.

### Conclusion

    High-confidence suspicious communication.

Hypothesis-driven analysis reduces unfocused investigation.


---

# 33. Competing Hypotheses

Sometimes multiple explanations are possible.

Example:

    Hypothesis A:
    Malware communication

    Hypothesis B:
    Legitimate software

    Hypothesis C:
    Security testing

Analysts compare evidence against each hypothesis.

This reduces confirmation bias.


---

# 34. Diamond Model

The Diamond Model describes four major elements:

```text
        Adversary
           /\
          /  \
         /    \
        /      \
Infrastructure — Capability
        \      /
         \    /
          \  /
          Victim
