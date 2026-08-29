# Threat Intelligence

> **SOC L1 Fundamental**

Threat Intelligence (TI) is the process of collecting, analyzing, contextualizing, and applying information about threats to improve an organization's ability to detect, investigate, respond to, and prevent cyber attacks.

For a SOC analyst, threat intelligence helps answer:

```text
Who or what is threatening us?
        ↓
What indicators are associated with the threat?
        ↓
How does the attacker operate?
        ↓
Are we seeing the same activity?
        ↓
What should we do about it?
```

The important principle is:

> **Threat intelligence turns raw security data into actionable context.**

---

# 1. Threat Data vs Threat Intelligence

These terms are often confused.

### Threat Data

Raw information:

```text
IP:
198.51.100.10

Domain:
example-malicious.com

Hash:
abc123...
```

By itself, this has limited meaning.

### Threat Intelligence

Contextualized information:

```text
198.51.100.10
        ↓
Known malicious infrastructure
        ↓
Associated with a malware campaign
        ↓
Observed communicating with infected endpoints
        ↓
Relevant to our environment
```

Therefore:

```text
Raw Data
   ↓
Analysis
   ↓
Context
   ↓
Intelligence
```

---

# 2. Why Threat Intelligence Matters to a SOC

Threat intelligence can help SOC teams:

```text
Detect Threats
Investigate Alerts
Prioritize Incidents
Identify IOCs
Understand TTPs
Improve Detection Rules
Support Threat Hunting
Block Malicious Infrastructure
Understand Threat Actors
```

Example:

```text
Firewall Alert
      ↓
Destination IP
      ↓
Threat Intelligence Lookup
      ↓
Known C2 Infrastructure
      ↓
Alert Priority Increases
```

---

# 3. Types of Threat Intelligence

A common classification is:

```text
Strategic
    ↓
Operational
    ↓
Tactical
    ↓
Technical
```

Each serves a different purpose.

---

# 4. Strategic Threat Intelligence

Strategic intelligence is high-level and business-focused.

Audience:

```text
CISO
Security Leadership
Executives
Risk Management
Board
```

It answers:

```text
What threats are relevant to our organization?
What risks are increasing?
Which sectors are being targeted?
What should leadership prioritize?
```

Example:

```text
Healthcare organizations
        ↓
Increasing ransomware activity
        ↓
Leadership decision
        ↓
Increase backup and recovery investment
```

---

# 5. Operational Threat Intelligence

Operational intelligence focuses on campaigns and attacker operations.

It answers:

```text
Who is conducting attacks?
Why?
Which organizations are targeted?
What campaigns are active?
What techniques are being used?
```

Useful for:

```text
Threat Hunting
Incident Response
Security Operations
```

---

# 6. Tactical Threat Intelligence

Tactical intelligence focuses on attacker techniques and procedures.

Examples:

```text
PowerShell
Credential Dumping
Scheduled Tasks
Phishing
Remote Services
Living-off-the-Land
```

It helps defenders understand:

```text
How does the attacker operate?
```

This is strongly connected with:

```text
MITRE ATT&CK
Detection Engineering
Threat Hunting
```

---

# 7. Technical Threat Intelligence

Technical intelligence focuses on technical indicators.

Examples:

```text
IP Addresses
Domains
URLs
File Hashes
Email Addresses
Malware Samples
File Names
Registry Keys
```

This is particularly useful for SOC L1 alert enrichment.

---

# 8. Threat Intelligence Lifecycle

A typical intelligence lifecycle:

```text
       REQUIREMENTS
            ↓
         COLLECTION
            ↓
         PROCESSING
            ↓
          ANALYSIS
            ↓
       DISSEMINATION
            ↓
          FEEDBACK
            ↓
       REQUIREMENTS
```

This is a continuous cycle.

---

# 9. Phase 1 — Requirements

First determine:

> **What intelligence does the organization actually need?**

Examples:

```text
Are our employees being targeted by phishing?
Are our public IPs associated with malicious activity?
Which ransomware groups target our industry?
Which vulnerabilities are actively exploited?
Are our endpoints communicating with known C2 infrastructure?
```

Intelligence should answer a business or security question.

---

# 10. Phase 2 — Collection

Collect relevant information from appropriate sources.

Examples:

```text
Security Logs
SIEM
EDR
Firewall
Threat Intelligence Platforms
Security Advisories
Vendor Reports
CERT Advisories
Open-Source Intelligence
Internal Incident Reports
```

Collection should be driven by requirements.

---

# 11. Phase 3 — Processing

Raw information often needs processing.

Examples:

```text
Remove Duplicates
Normalize Indicators
Extract IOCs
Validate Data
Convert Formats
Remove Noise
Organize Metadata
```

Example:

```text
Raw Feed
   ↓
Duplicate IPs
   ↓
Normalize
   ↓
Validated IOC
   ↓
Threat Intelligence Platform
```

---

# 12. Phase 4 — Analysis

Analysis determines:

```text
Is it malicious?
How reliable is the source?
What is it associated with?
Is it relevant to our organization?
What behavior is associated with it?
```

Example:

```text
IP
 ↓
Threat Feed
 ↓
Malware Association
 ↓
C2 Infrastructure
 ↓
Observed in recent campaign
```

The analyst now has meaningful context.

---

# 13. Phase 5 — Dissemination

Intelligence must reach the people who can act on it.

Examples:

```text
SOC
Threat Hunters
Incident Response
Detection Engineers
Security Engineering
Management
```

Different audiences require different formats.

---

# 14. Phase 6 — Feedback

After intelligence is used, determine:

```text
Was it useful?
Was it accurate?
Did it generate false positives?
Was the information timely?
Should collection change?
```

Then update requirements.

---

# 15. Indicators of Compromise

An **IOC** is an observable artifact that may indicate malicious activity.

Examples:

```text
IP Address
Domain
URL
File Hash
Malicious File
Email Address
Registry Key
File Path
```

Example:

```text
Malware
   ↓
SHA-256 Hash
   ↓
Search Environment
   ↓
Identify Infected Hosts
```

---

# 16. Indicators of Attack

An **IOA** focuses on suspicious behavior rather than a static artifact.

Examples:

```text
Office → PowerShell
PowerShell → Download
Credential Dumping
Mass File Encryption
Suspicious Remote Login
New Service Creation
Scheduled Task Creation
```

IOAs can remain useful even when attackers change their:

```text
IP
Domain
Hash
Filename
```

---

# 17. IOC vs IOA

| IOC                 | IOA                      |
| ------------------- | ------------------------ |
| Observable artifact | Observable behavior      |
| IP                  | PowerShell execution     |
| Domain              | Credential dumping       |
| Hash                | Suspicious process chain |
| URL                 | Lateral movement         |
| File                | Persistence behavior     |

A mature SOC uses both.

---

# 18. Indicator Enrichment

Suppose an alert contains:

```text
Destination IP:
198.51.100.10
```

Enrich it with:

```text
Reputation
WHOIS
ASN
Geolocation
Passive DNS
Threat Reports
Malware Associations
Historical Observations
```

Then:

```text
Raw IOC
   ↓
Context
   ↓
Risk Assessment
```

---

# 19. Indicator Reputation

An IOC may be classified as:

```text
Malicious
Suspicious
Unknown
Benign
```

But reputation should not automatically determine the final verdict.

For example:

```text
Known Malicious IP
+
Connection from Critical Server
+
Known Malware Process
```

is much stronger evidence than:

```text
IP Reputation = Suspicious
```

alone.

---

# 20. Threat Intelligence Confidence

Threat intelligence sources have different reliability.

Consider:

```text
Source Reliability
+
Indicator Confidence
+
Freshness
+
Corroborating Evidence
```

Example:

```text
Source A:
High-confidence vendor intelligence

Source B:
Unknown community feed
```

Do not treat both as equally authoritative.

---

# 21. False Positives in Threat Intelligence

Threat feeds can contain inaccurate or outdated information.

Example:

```text
IP previously used by attacker
        ↓
Infrastructure changed
        ↓
IP reassigned
        ↓
Now legitimate
```

Therefore:

> **Threat intelligence must be validated and contextualized.**

---

# 22. Threat Intelligence Sources

Useful categories include:

### Government / CERT

```text
CERT advisories
Government security alerts
National vulnerability advisories
```

### Security Vendors

```text
Malware research
Threat reports
Campaign analysis
Security advisories
```

### Open Source

```text
OSINT
Security blogs
Research papers
Community feeds
```

### Internal

```text
SOC incidents
Previous investigations
Internal telemetry
Previous phishing campaigns
```

Internal intelligence is particularly valuable because it reflects your own environment.

---

# 23. Threat Intelligence Platforms

A TIP can help organizations manage:

```text
Indicators
Threat Actors
Campaigns
Malware
Relationships
Sources
Confidence
Tags
Observations
```

A TIP may integrate with:

```text
SIEM
SOAR
EDR
Firewalls
Email Security
Detection Platforms
```

---

# 24. Threat Intelligence and SIEM

Example workflow:

```text
SIEM Alert
    ↓
Extract IOC
    ↓
Threat Intelligence Lookup
    ↓
Enrichment
    ↓
Correlation
    ↓
Risk Assessment
    ↓
SOC Investigation
```

This reduces the amount of manual context gathering.

---

# 25. Threat Intelligence and EDR

Example:

```text
EDR
 ↓
Suspicious Process
 ↓
Network Connection
 ↓
Destination IP
 ↓
Threat Intelligence
 ↓
Known C2
 ↓
High-confidence Investigation
```

The SOC can then investigate the endpoint more deeply.

---

# 26. Threat Intelligence and Detection Engineering

Threat intelligence can become detection logic.

Example:

```text
Threat Report
      ↓
Malicious Domain
      ↓
Add to Detection
      ↓
SIEM Query
      ↓
Alert
```

Or:

```text
Threat Report
      ↓
Known Attack Behavior
      ↓
MITRE ATT&CK Technique
      ↓
Detection Rule
```

This creates a feedback loop:

```text
Threat Intelligence
        ↓
Detection
        ↓
Incident
        ↓
New Intelligence
        ↓
Improved Detection
```

---

# 27. Threat Intelligence and Threat Hunting

Threat hunters can use intelligence to search proactively.

Example:

```text
Threat Intelligence
        ↓
Known C2 Domain
        ↓
Search SIEM
        ↓
No Alert?
        ↓
Search Historical Logs
        ↓
Potential Hidden Activity
```

This is an important difference:

> **Detection waits for a rule to trigger; hunting proactively searches for evidence.**

---

# 28. Threat Intelligence and Incident Response

During an incident:

```text
Known IOC
   ↓
Search Environment
   ↓
Identify Additional Hosts
   ↓
Determine Scope
   ↓
Contain
```

Threat intelligence can accelerate investigation.

---

# 29. Threat Intelligence and MITRE ATT&CK

Threat intelligence often describes attacker TTPs.

Example:

```text
Threat Report
      ↓
PowerShell
      ↓
MITRE ATT&CK
      ↓
T1059.001
      ↓
Detection Opportunity
```

This lets SOC teams move from:

```text
Threat Report
```

to:

```text
Actionable Detection
```

---

# 30. Threat Actors

A threat actor is an individual or group conducting malicious activity.

Examples of broad categories:

```text
Cybercriminal Groups
Nation-State Actors
Hacktivists
Insiders
Initial Access Brokers
Threat Groups
```

Threat intelligence may track:

```text
Motivation
Targets
Techniques
Infrastructure
Malware
Campaigns
```

Do not assume attribution is always certain.

---

# 31. Threat Actor Attribution

Attribution can be difficult.

Evidence may include:

```text
Infrastructure
TTPs
Malware
Target Selection
Language
Operational Patterns
Historical Activity
```

However:

> **Attribution should be treated with appropriate confidence rather than assumed from a single indicator.**

---

# 32. Malware Intelligence

Threat intelligence may provide information about:

```text
Malware Family
Hashes
C2 Domains
C2 IPs
Behavior
Persistence
Execution
Payload
Associated Campaigns
```

Example:

```text
Malware Sample
      ↓
Hash
      ↓
Known Family
      ↓
C2 Infrastructure
      ↓
Associated TTPs
```

---

# 33. Vulnerability Intelligence

A SOC should also pay attention to vulnerabilities being actively exploited.

Important questions:

```text
Which vulnerability?
Is it actively exploited?
Do we have affected systems?
Is public exploit code available?
Is the asset internet-facing?
Is a patch available?
```

Example:

```text
Critical Vulnerability
        ↓
Known Active Exploitation
        ↓
Internet-Facing Asset
        ↓
High Priority
```

This is where vulnerability management and SOC operations overlap.

---

# 34. Threat Intelligence vs Vulnerability Management

Threat intelligence asks:

```text
What threats are targeting us?
```

Vulnerability management asks:

```text
Where are we vulnerable?
```

Together:

```text
Threat
  +
Vulnerability
  +
Exposure
  =
Risk
```

---

# 35. Threat Intelligence and Risk

Example:

```text
Vulnerability:
Critical

Asset:
Internet-facing

Threat:
Active exploitation

Exploit:
Publicly available
```

This should receive significant attention.

Threat intelligence therefore helps prioritize vulnerabilities based on real-world threat activity.

---

# 36. Threat Intelligence Formats

Common formats include:

```text
STIX
TAXII
CSV
JSON
API
Plain Text
```

### STIX

Structured format for representing threat intelligence.

### TAXII

Protocol used to exchange cyber threat intelligence.

You do not need to master these immediately at SOC L1, but understanding their purpose is valuable.

---

# 37. Practical Threat Intelligence Workflow

For a SOC analyst:

```text
Alert
 ↓
Extract IOC
 ↓
Validate IOC
 ↓
Enrich IOC
 ↓
Check Reputation
 ↓
Check Historical Activity
 ↓
Search Internal Environment
 ↓
Correlate
 ↓
Assess Risk
 ↓
Document
```

---

# 38. Example — Malicious IP Investigation

Alert:

```text
Outbound Connection
```

IOC:

```text
203.0.113.10
```

Investigation:

```text
1. Identify source host
2. Identify destination
3. Identify process
4. Check DNS
5. Check reputation
6. Check threat reports
7. Search historical logs
8. Check other hosts
9. Determine whether connection is expected
10. Document findings
```

---

# 39. Example — Malicious Domain Investigation

Alert:

```text
Endpoint contacted suspicious-domain.example
```

Check:

```text
Domain Age
DNS Records
Reputation
Related IPs
Historical DNS
Threat Reports
Endpoint Process
URL Path
User
```

Then determine:

```text
Benign
Suspicious
Malicious
```

based on combined evidence.

---

# 40. Practical Home Lab

Your existing lab can become a basic threat-intelligence workflow:

```text
Windows VM
     ↓
Sysmon
     ↓
Wazuh
     ↓
Suspicious Network Alert
     ↓
Extract IOC
     ↓
Threat Intelligence Lookup
     ↓
Enrich Alert
     ↓
Investigate
     ↓
Document
```

For every investigation, record:

```text
IOC
Source
Reputation
Confidence
Context
Related TTP
Internal Observations
Final Verdict
```

---

# 41. Portfolio Project

Create:

```text
Threat-Intelligence-Lab/
│
├── README.md
├── IOC-Analysis/
│   ├── IP/
│   ├── Domains/
│   ├── Hashes/
│   └── URLs/
│
├── Threat-Reports/
├── MITRE-Mapping/
├── Threat-Actor-Profiles/
├── Malware-Analysis/
├── Vulnerability-Intelligence/
├── Detection-Rules/
├── Investigation-Reports/
└── Screenshots/
```

Create at least:

```text
10 IOC investigations
5 threat reports
5 detection rules
5 MITRE ATT&CK mappings
3 complete case studies
```

---

# 42. Threat Intelligence Case Study Structure

For each case:

```text
# Threat Intelligence Case Study

## 1. Objective

## 2. Intelligence Question

## 3. IOC

## 4. Source

## 5. Source Reliability

## 6. Indicator Context

## 7. Reputation

## 8. Related Malware / Campaign

## 9. Associated TTPs

## 10. Internal Search

## 11. Findings

## 12. Risk Assessment

## 13. Detection Opportunity

## 14. MITRE ATT&CK Mapping

## 15. Recommended Action

## 16. Conclusion
```

---

# 43. Interview Questions

### Fundamentals

1. What is threat intelligence?
2. What is the difference between threat data and intelligence?
3. What are the types of threat intelligence?
4. What is an IOC?
5. What is an IOA?
6. What is STIX?
7. What is TAXII?

### SOC L1

8. How do you enrich an alert?
9. How do you investigate a suspicious IP?
10. How do you investigate a malicious domain?
11. How do you determine whether an IOC is reliable?
12. How does threat intelligence help incident response?
13. How does threat intelligence improve detection rules?

### Scenario

14. A SIEM alert contains a suspicious destination IP. What do you do?

Strong answer:

```text
Identify source host
      ↓
Identify process/user
      ↓
Validate destination
      ↓
Threat intelligence lookup
      ↓
Check reputation
      ↓
Check historical internal activity
      ↓
Correlate related events
      ↓
Determine whether communication is expected
      ↓
Assess risk
      ↓
Escalate / contain if required
      ↓
Document
```

---

# 44. Common Mistakes

Avoid:

```text
Treating every threat-feed IOC as malicious
Ignoring IOC age
Ignoring source reliability
Relying only on reputation
Ignoring internal context
Confusing IOC with IOA
Making unsupported attribution claims
Copying threat reports without analysis
```

The strongest SOC analysts combine:

```text
External Intelligence
+
Internal Telemetry
+
Business Context
```

---

# 45. Key Takeaway

Threat intelligence should not become a collection of random malicious IPs and hashes.

The real value is:

```text
Threat Data
      ↓
Context
      ↓
Analysis
      ↓
Intelligence
      ↓
Detection
      ↓
Investigation
      ↓
Response
```

For your SOC portfolio, demonstrate this complete workflow:

```text
Threat Report
      ↓
Extract IOC / IOA
      ↓
Validate
      ↓
Enrich
      ↓
Search Wazuh / SIEM
      ↓
Correlate
      ↓
Map MITRE ATT&CK
      ↓
Create Detection
      ↓
Investigate
      ↓
Document
```

That demonstrates that you can use threat intelligence **operationally**, rather than simply knowing its definition.
