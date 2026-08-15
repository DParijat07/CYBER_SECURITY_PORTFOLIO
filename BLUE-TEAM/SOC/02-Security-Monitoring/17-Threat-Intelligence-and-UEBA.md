# Threat Intelligence and UEBA

## 1. Introduction

Threat Intelligence and User and Entity Behavior Analytics (UEBA) are important capabilities in modern Security Operations Centers (SOCs).

Threat Intelligence provides information about known and emerging threats, while UEBA identifies suspicious behavior by comparing observed activity against normal behavioral baselines.

Together they help SOC analysts answer two important questions:

1. **Is this indicator associated with a known threat?**
2. **Is this behavior abnormal for this user, device, or entity?**

A simplified workflow is:

Threat Intelligence
        ↓
Indicators / Context
        ↓
SIEM
        ↓
Correlation
        ↓
UEBA
        ↓
Behavior Analysis
        ↓
SOC Alert
        ↓
Investigation
        ↓
Response


---

## 2. What Is Threat Intelligence?

Threat Intelligence is the collection, analysis, and application of information about cyber threats.

Threat intelligence can provide information about:

- Malicious IP addresses
- Malicious domains
- Malware hashes
- Phishing URLs
- Attack techniques
- Threat actors
- Campaigns
- Vulnerabilities
- Command-and-control infrastructure

The goal is not simply to collect indicators.

The goal is:

> Turn threat information into actionable security decisions.


---

## 3. Objectives of Threat Intelligence

Threat Intelligence helps organizations:

1. Identify known malicious infrastructure
2. Improve detection capabilities
3. Enrich security alerts
4. Understand attacker behavior
5. Prioritize threats
6. Identify emerging attack techniques
7. Support incident investigation
8. Improve security controls
9. Support proactive threat hunting
10. Improve incident response


---

## 4. Types of Threat Intelligence

Threat Intelligence can be divided into several categories.

### Strategic Intelligence

Focuses on high-level threats and business impact.

Audience:

- Executives
- Security leadership
- Risk teams
- GRC teams

Examples:

- Major threat trends
- Industry-specific threats
- Geopolitical cyber risks
- Business impact of ransomware


### Tactical Intelligence

Focuses on attacker techniques and procedures.

Examples:

- Attack techniques
- Tactics
- Procedures
- MITRE ATT&CK mappings


### Operational Intelligence

Focuses on specific campaigns and attacks.

Examples:

- Current attack campaigns
- Threat actor activity
- Malware campaigns
- Attack infrastructure


### Technical Intelligence

Focuses on technical indicators.

Examples:

- IP addresses
- Domains
- URLs
- Hashes
- File names
- Malware signatures


---

## 5. Indicators of Compromise

Indicators of Compromise (IoCs) are technical artifacts associated with potentially malicious activity.

Common IoCs include:

    IP Address
    Domain
    URL
    File Hash
    Email Address
    File Name
    Registry Key
    Mutex
    Malware Family


### Example

    Malicious IP:
    203.0.113.50

    SHA-256:
    <example-hash>

    Domain:
    suspicious-example.com

An IOC by itself does not always prove compromise.

Context is required.


---

## 6. Indicators of Attack

Indicators of Attack (IoAs) focus more on attacker behavior than static artifacts.

Examples:

- Credential dumping
- PowerShell execution
- Privilege escalation
- Lateral movement
- Suspicious process chains
- Persistence attempts
- Security control modification

Example:

    Office Application
          ↓
    PowerShell
          ↓
    External Connection

This behavior may be suspicious even if no known malicious hash is present.


---

## 7. IoC vs IoA

| Feature | IoC | IoA |
|---|---|---|
| Focus | Artifact | Behavior |
| Example | Malicious IP | Credential dumping |
| Static | Often | Usually behavioral |
| Useful For | Known threats | Attack detection |
| Limitation | Can become outdated | Requires behavioral analysis |

Modern security monitoring should use both.

---

## 8. Threat Intelligence Sources

Threat intelligence can come from:

- Internal incident investigations
- Security vendors
- Government agencies
- CERT organizations
- Open-source intelligence
- Commercial intelligence providers
- Industry information-sharing groups
- Malware research
- Security research communities

Internal intelligence is especially valuable because it reflects threats observed within the organization's own environment.


---

## 9. Threat Intelligence Lifecycle

A typical lifecycle is:

    Planning
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
    Improvement


### Planning

Determine:

- What threats matter?
- Which assets need protection?
- What intelligence is required?


### Collection

Collect information from:

- Logs
- Security tools
- External intelligence
- Incident investigations


### Processing

Normalize and organize collected information.


### Analysis

Determine:

- Is the indicator malicious?
- How relevant is it?
- What threat is associated with it?
- What systems may be affected?


### Dissemination

Share intelligence with:

- SOC
- Incident Response
- Threat Hunting
- Detection Engineering
- GRC
- Management


### Feedback

Determine whether the intelligence was useful and improve the process.


---

## 10. Threat Intelligence Enrichment

Threat intelligence can enrich SIEM alerts.

Example:

    Firewall Alert
         ↓
    Destination IP
         ↓
    Threat Intelligence Lookup
         ↓
    Known Malicious Infrastructure
         ↓
    Alert Enrichment
         ↓
    SOC Investigation


A useful enrichment may include:

    IP Reputation
    Malware Association
    Threat Actor
    Country
    ASN
    First Seen
    Last Seen
    Confidence
    Related Campaign


---

## 11. Threat Intelligence Confidence

Not every intelligence indicator has the same reliability.

A practical model can be:

### High Confidence

Multiple reliable sources confirm malicious activity.

### Medium Confidence

Some evidence indicates malicious activity but further validation is required.

### Low Confidence

Limited or uncertain evidence exists.

SOC analysts should avoid automatically blocking every low-confidence indicator.


---

## 12. False Positives in Threat Intelligence

An indicator can become misleading because:

- IP addresses are reassigned
- Domains are compromised
- Shared hosting is used
- Threat infrastructure changes
- Intelligence becomes outdated
- Security researchers interact with malicious infrastructure
- CDN infrastructure is shared

Therefore:

> Threat intelligence should be treated as evidence, not absolute truth.


---

# 13. UEBA

UEBA stands for User and Entity Behavior Analytics.

UEBA analyzes the behavior of:

- Users
- Endpoints
- Servers
- Applications
- Service accounts
- Network devices
- Cloud identities

The goal is to identify behavior that deviates significantly from normal activity.


---

## 14. Why UEBA Is Important

Traditional detection often depends on known signatures or rules.

UEBA adds behavioral analysis.

Example:

Traditional detection:

    Known malicious IP
          ↓
        Alert

UEBA:

    User normally logs in
    from one location
          ↓
    Suddenly logs in
    from multiple unusual locations
          ↓
    Accesses unusual systems
          ↓
    Downloads large amount of data
          ↓
    Behavioral anomaly


---

## 15. UEBA Entities

UEBA can monitor many types of entities.

### Users

Monitor:

- Login patterns
- Applications
- Resources
- Locations
- Data access
- Privileges


### Devices

Monitor:

- Network connections
- Processes
- Users
- Applications
- Traffic volume


### Service Accounts

Monitor:

- Authentication sources
- Applications
- Access patterns
- Privilege usage


### Applications

Monitor:

- Requests
- Users
- Resources
- Error rates
- Data access


---

## 16. Behavioral Baselines

UEBA establishes a baseline of normal activity.

Example:

User:

    analyst01

Normal behavior:

    Login: 09:00–18:00
    Device: Laptop01
    Location: Office
    Applications: SIEM, Email, Browser
    Data Access: Normal SOC datasets

Observed:

    Login: 03:15
    Device: Unknown
    Location: New Country
    Application: Database
    Data Download: 15 GB

This represents a significant behavioral deviation.


---

## 17. Behavioral Anomalies

Common anomalies include:

- Login at unusual time
- Login from unusual location
- New device
- New application
- Unusual data access
- Large downloads
- Unusual privilege usage
- Abnormal network traffic
- Access to previously unused systems
- Sudden increase in activity


---

## 18. Risk Scoring

UEBA systems often assign risk scores.

Example:

    Unusual Login
          +
    New Device
          +
    Sensitive Resource Access
          +
    Large Data Download
          ↓
    Risk Score: High


A simple conceptual model is:

    Risk Score =
    Authentication Anomaly
    +
    Device Anomaly
    +
    Access Anomaly
    +
    Data Anomaly


The exact scoring method depends on the platform.


---

## 19. User Behavior Monitoring

UEBA can establish normal behavior for each user.

Monitor:

    Login Frequency
    Login Location
    Device Usage
    Applications
    Resource Access
    Data Access
    Network Activity
    Privilege Usage


Example:

Normal:

    User accesses
    HR portal

Abnormal:

    Same user suddenly accesses
    database servers
    and administrative systems

This should be investigated.


---

## 20. Entity Behavior Monitoring

UEBA is not limited to humans.

An entity can be:

- Server
- Endpoint
- Application
- Service account
- Cloud resource
- Database
- Network device

Example:

    Database Server
          ↓
    Normal:
    100 queries/minute

    Observed:
    20,000 queries/minute

This may indicate:

- Application failure
- Automated process
- Attack
- Data extraction
- Misconfiguration


---

## 21. Impossible Travel

UEBA can identify geographically unusual authentication patterns.

Example:

    09:00
    India

    09:30
    United States

Possible explanations:

- Credential compromise
- VPN
- Proxy
- Cloud infrastructure
- Geolocation error

Therefore, the alert requires validation.


---

## 22. Insider Threat Detection

UEBA can help identify potential insider threats.

Potential indicators:

- Unusual data access
- Large file downloads
- Access outside normal role
- Access outside working hours
- Sudden privilege usage
- Unusual removable media activity
- Unusual cloud storage usage

Example:

    Employee
       ↓
    Accesses unusual database
       ↓
    Downloads large dataset
       ↓
    Compresses files
       ↓
    Uploads externally

This should be investigated.


---

## 23. Account Compromise Detection

UEBA can help detect compromised accounts.

Example:

    Normal User
        ↓
    New Device
        ↓
    New Location
        ↓
    Unusual Login Time
        ↓
    Sensitive Resource Access
        ↓
    Large Data Download

The combination is more significant than any single event.


---

## 24. Threat Intelligence + UEBA

Threat Intelligence and UEBA become more powerful when combined.

Example:

    User Login
        ↓
    Behavioral Anomaly
        ↓
    Connection to Suspicious IP
        ↓
    Threat Intelligence Match
        ↓
    High Risk
        ↓
    SOC Alert


This provides:

    Who?
    ↓
    What?
    ↓
    Where?
    ↓
    Why?
    ↓
    Risk?


---

## 25. UEBA + SIEM

SIEM provides centralized event collection.

UEBA adds behavioral analysis.

Example:

    Authentication Logs
           +
    Endpoint Logs
           +
    Network Logs
           +
    Cloud Logs
           +
    Application Logs
           ↓
          SIEM
           ↓
          UEBA
           ↓
    Behavioral Analysis
           ↓
       Risk Score
           ↓
       SOC Alert


---

## 26. Threat Hunting with Threat Intelligence

Threat intelligence can support proactive threat hunting.

Example:

    Threat Intelligence
          ↓
    Malicious Domain
          ↓
    Search DNS Logs
          ↓
    Identify Hosts
          ↓
    Investigate Endpoints
          ↓
    Determine Impact


Another example:

    Malware Hash
        ↓
    Search EDR
        ↓
    Identify Affected Hosts
        ↓
    Investigate Process Tree
        ↓
    Determine Compromise


---

## 27. Detection Engineering with Threat Intelligence

Threat intelligence can be converted into detection rules.

Example:

    Threat Intelligence
          ↓
    Malicious Domain
          ↓
    SIEM Rule
          ↓
    DNS Query
          ↓
    Match
          ↓
    Alert


Behavioral intelligence can also be converted into rules.

Example:

    Threat Research
          ↓
    Attack Behavior
          ↓
    Detection Logic
          ↓
    SIEM / EDR
          ↓
    Alert


---

## 28. MITRE ATT&CK Mapping

Threat intelligence and UEBA detections can be mapped to MITRE ATT&CK techniques.

Examples:

### Credential Access

    T1003
    OS Credential Dumping

### PowerShell

    T1059.001

### Remote Services

    T1021

### Account Manipulation

    T1098

Mapping detections to ATT&CK helps organizations understand detection coverage.


---

## 29. Detection Rule Examples

### Rule 1 — Threat Intelligence Match

    IF
    endpoint connects to
    known malicious IP

    THEN
    generate high-priority alert

Severity:

    High


### Rule 2 — Suspicious Domain + UEBA Anomaly

    IF
    user accesses suspicious domain

    AND

    behavior is significantly
    different from baseline

    THEN
    generate high-priority alert

Severity:

    High


### Rule 3 — Unusual Login + Sensitive Access

    IF
    login occurs from
    unusual location

    AND

    sensitive resource is accessed

    THEN
    generate investigation alert

Severity:

    High


### Rule 4 — Large Data Transfer

    IF
    user accesses unusual resource

    AND

    transfers significantly
    more data than baseline

    THEN
    generate data-exfiltration alert

Severity:

    High


### Rule 5 — Threat Intelligence + Endpoint Detection

    IF
    endpoint connects to
    known malicious infrastructure

    AND

    suspicious process exists

    THEN
    generate critical investigation alert

Severity:

    Critical


---

## 30. Example SOC Alert

Alert:

    Potential Compromised User Account

Severity:

    High

User:

    user01

Observed Activity:

    Login from unusual location
    New device detected
    Access to unusual server
    Large data download
    Connection to suspicious external IP

Threat Intelligence:

    Destination IP associated
    with malicious infrastructure

UEBA:

    High behavioral deviation

### Analyst Comment

The user's activity significantly deviates from the established behavioral baseline. A new device and unusual geographic login were followed by access to a previously unused server, a large data transfer, and communication with infrastructure associated with suspicious activity. The combination of behavioral anomalies and threat intelligence indicators suggests potential account compromise and requires immediate investigation.


---

## 31. SOC Triage Process

### Step 1 — Identify the User or Entity

Determine:

    Username
    Device
    Server
    Application
    Service Account


### Step 2 — Review Threat Intelligence

Check:

    IP Reputation
    Domain Reputation
    URL
    File Hash
    Malware Association
    Threat Actor
    Confidence


### Step 3 — Review Behavioral Baseline

Compare:

    Normal Login Time
    Normal Location
    Normal Device
    Normal Applications
    Normal Resource Access
    Normal Data Volume


### Step 4 — Analyze Anomalies

Identify:

    New Device
    New Location
    Unusual Application
    Unusual Resource
    Unusual Data Transfer
    Unusual Privilege Usage


### Step 5 — Correlate Events

Check:

    Authentication Logs
    Endpoint Logs
    DNS Logs
    Firewall Logs
    Proxy Logs
    Cloud Logs
    Application Logs


### Step 6 — Investigate Endpoint

Check:

    Processes
    Files
    Network Connections
    Persistence
    Malware Indicators


### Step 7 — Determine Account Status

Ask:

    Is the account compromised?
    Is the activity legitimate?
    Was MFA bypassed?
    Was privilege abused?


### Step 8 — Determine Impact

Check:

    Data Access
    Data Transfer
    Lateral Movement
    Persistence
    Additional Compromised Accounts


### Step 9 — Respond

Possible actions:

    Disable Account
    Reset Password
    Revoke Sessions
    Isolate Endpoint
    Block Malicious IP
    Block Malicious Domain
    Remove Persistence
    Escalate Incident


---

## 32. Threat Intelligence and UEBA Investigation Checklist

    [ ] Identify user/entity
    [ ] Identify affected device
    [ ] Check IP reputation
    [ ] Check domain reputation
    [ ] Check URL reputation
    [ ] Check file hash
    [ ] Validate intelligence confidence
    [ ] Review authentication history
    [ ] Review behavioral baseline
    [ ] Check login location
    [ ] Check login time
    [ ] Check device history
    [ ] Check application usage
    [ ] Check resource access
    [ ] Check data transfer
    [ ] Check privilege usage
    [ ] Review endpoint activity
    [ ] Review DNS activity
    [ ] Review network activity
    [ ] Review cloud activity
    [ ] Map relevant activity to MITRE ATT&CK
    [ ] Determine account compromise
    [ ] Determine impact
    [ ] Assign severity
    [ ] Document findings
    [ ] Contain if required
    [ ] Escalate if required


---

## 33. Best Practices

Organizations should:

- Maintain reliable threat intelligence sources
- Validate intelligence before automated blocking
- Track intelligence confidence
- Remove outdated indicators
- Integrate threat intelligence with SIEM
- Integrate threat intelligence with EDR
- Establish user and entity baselines
- Tune UEBA detection models
- Reduce false positives
- Correlate multiple telemetry sources
- Use behavioral context
- Map detections to MITRE ATT&CK
- Use threat intelligence for threat hunting
- Continuously improve detection rules
- Protect intelligence feeds
- Document investigation results


---

## 34. Key Takeaways

Threat Intelligence provides external and internal knowledge about threats.

UEBA provides behavioral context.

Threat Intelligence asks:

    "Is this indicator associated
     with a known threat?"

UEBA asks:

    "Is this activity abnormal
     for this user or entity?"

Together:

    Threat Intelligence
          +
    Behavioral Analysis
          +
    SIEM
          +
    Endpoint / Network Telemetry
          ↓
    High-Confidence Detection
          ↓
    SOC Investigation
          ↓
    Incident Response


The core investigation model is:

    Indicator
       ↓
    Intelligence Validation
       ↓
    User / Entity Context
       ↓
    Behavioral Baseline
       ↓
    Correlation
       ↓
    Risk Assessment
       ↓
    Threat Hunting
       ↓
    Impact Assessment
       ↓
    Response

**Threat Intelligence helps the SOC understand known threats, while UEBA helps identify abnormal behavior. Combining both capabilities improves detection of account compromise, insider threats, lateral movement, command-and-control activity, and other attacks that may not be detected by simple signature-based rules alone.**
