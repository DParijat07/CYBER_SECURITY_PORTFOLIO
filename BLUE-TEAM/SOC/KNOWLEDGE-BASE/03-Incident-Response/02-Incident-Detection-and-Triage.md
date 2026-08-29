# Incident Detection and Triage

## 1. Introduction

Incident Detection and Triage is the process of identifying potentially malicious activity, validating security alerts, determining their severity, and deciding whether an event should be escalated for further investigation.

In a SOC, detection and triage form the bridge between continuous security monitoring and formal Incident Response.

The basic workflow is:

    Security Event
          ↓
    Detection
          ↓
    Alert
          ↓
    Triage
          ↓
    Validation
          ↓
    Prioritization
          ↓
    Investigation / Escalation
          ↓
    Incident Response


---

## 2. Detection vs Triage

### Detection

Detection identifies potentially suspicious or malicious activity.

Examples:

- Multiple failed logins
- Suspicious PowerShell
- Malware detection
- Unusual network connection
- Privilege escalation
- Large outbound data transfer

### Triage

Triage determines:

- Is the alert legitimate?
- Is it malicious?
- How serious is it?
- What systems are affected?
- What user is involved?
- Does it require escalation?

Therefore:

> Detection finds potential problems; triage determines what deserves action.


---

## 3. Security Event

A security event is an observable activity that may be relevant to security.

Examples:

    User Login
    Process Creation
    File Creation
    Network Connection
    DNS Query
    Firewall Block
    Authentication Failure
    Privilege Change


Not every security event is malicious.

---

## 4. Security Alert

An alert is generated when a security monitoring system identifies activity that matches a detection condition.

Example:

    20 Failed Logins
          ↓
    Detection Rule
          ↓
    Security Alert


An alert is not automatically a confirmed incident.

The analyst must investigate the context.


---

## 5. Incident

An incident occurs when suspicious activity is confirmed or sufficiently suspected to represent a security compromise or policy violation requiring response.

Example:

    Suspicious Login
          +
    Impossible Travel
          +
    Successful Authentication
          +
    Sensitive Resource Access
          ↓
    Potential Account Compromise


---

## 6. Detection Sources

Incident detection can come from:

- SIEM
- EDR
- XDR
- IDS
- IPS
- Firewall
- Antivirus
- DLP
- Email security
- Cloud security
- Authentication systems
- Vulnerability scanners
- Threat intelligence
- User reports

---

## 7. Common Detection Categories

### Authentication

- Brute force
- Impossible travel
- Multiple failed logins
- Suspicious login
- Privileged account activity

### Endpoint

- Malware
- Suspicious process
- PowerShell abuse
- Persistence
- File modification

### Network

- Port scanning
- C2 traffic
- DNS tunneling
- Suspicious outbound traffic
- Lateral movement

### Data

- Large downloads
- Sensitive file access
- External uploads
- Data staging
- DLP violations

### Cloud

- Suspicious API calls
- New access keys
- Privilege changes
- Unusual login
- Public resource exposure


---

## 8. Detection Pipeline

A typical pipeline is:

    Endpoint / Network / Cloud
              ↓
        Telemetry
              ↓
       Log Collection
              ↓
       SIEM / XDR
              ↓
      Detection Rules
              ↓
           Alert
              ↓
          Triage


---

## 9. Detection Logic

Detection rules identify suspicious patterns.

Example:

    Failed Login
        +
    Failed Login
        +
    Failed Login
        +
    Successful Login
        ↓
    Suspicious Authentication Alert


Another example:

    Word Document
         ↓
    PowerShell
         ↓
    Suspicious Network Connection
         ↓
    Potential Malware Alert


---

## 10. Rule-Based Detection

Rule-based detection uses predefined conditions.

Example:

    IF failed_login_count > 10
    within 5 minutes

    THEN

    generate alert


Advantages:

- Easy to understand
- Easy to test
- Predictable
- Good for known behaviors

Limitations:

- Can generate false positives
- May miss unknown behavior
- Requires continuous tuning


---

## 11. Behavior-Based Detection

Behavior-based detection focuses on unusual activity.

Example:

    Normal User
        ↓
    10 Login Attempts
        ↓
    Unusual Location
        ↓
    New Device
        ↓
    Sensitive Resource Access
        ↓
    Suspicious Behavior


Behavior-based detection can identify activity that does not match known signatures.


---

## 12. Signature-Based Detection

Signature-based detection looks for known patterns.

Examples:

- Malware hash
- Known malicious IP
- Known domain
- Known exploit pattern
- Known file signature


Example:

    File Hash
       ↓
    Threat Intelligence
       ↓
    Known Malware
       ↓
    Detection


Advantages:

- Fast
- Efficient
- Good for known threats

Limitation:

- Weak against previously unknown threats


---

## 13. Anomaly Detection

Anomaly detection identifies deviations from normal behavior.

Example:

    Normal:
    User downloads 100 MB/day

    Today:
    User downloads 15 GB

          ↓

    Anomalous Activity


Anomaly detection should always be evaluated with context.


---

## 14. Alert Triage

Alert triage is the first analytical stage after an alert is generated.

The analyst should answer:

1. What happened?
2. When did it happen?
3. Where did it happen?
4. Who was involved?
5. Why did the system generate the alert?
6. Is the activity expected?
7. Is the activity malicious?
8. What is the potential impact?


---

## 15. First-Level Triage

An L1 SOC analyst should quickly establish:

    Alert Type
    Host
    User
    Timestamp
    Source
    Destination
    Severity
    Detection Rule


The objective is not to perform a full forensic investigation.

The objective is to determine whether escalation is necessary.


---

## 16. Alert Context

Context is critical.

Consider:

- Asset criticality
- User role
- Business function
- Time of activity
- Geographic location
- Previous behavior
- Related alerts
- Threat intelligence
- Current vulnerabilities


Example:

A failed login on a test account is different from repeated failed logins followed by successful authentication against a domain administrator account.


---

## 17. Alert Enrichment

Enrichment adds additional information to an alert.

Example:

    Alert
      ↓
    Source IP
      ↓
    Threat Intelligence
      ↓
    IP Reputation
      ↓
    GeoIP
      ↓
    ASN
      ↓
    Historical Activity
      ↓
    Enriched Alert


Other enrichment sources include:

- Asset inventory
- User directory
- Vulnerability management
- EDR
- DNS
- WHOIS information
- Threat intelligence


---

## 18. IOC Investigation

Indicators of Compromise may include:

- IP addresses
- Domains
- URLs
- File hashes
- File names
- Email addresses
- Registry keys


For each IOC, determine:

    Known Malicious?
    Known Benign?
    Suspicious?
    Previously Seen?
    Associated With Malware?
    Associated With C2?


---

## 19. False Positive

A false positive occurs when a security detection triggers but the activity is legitimate.

Example:

    Security Tool
        ↓
    Port Scan Alert
        ↓
    Investigation
        ↓
    Authorized Vulnerability Scan
        ↓
    False Positive


False positives should be documented and used to improve detection rules.


---

## 20. True Positive

A true positive occurs when the detection correctly identifies malicious or unauthorized activity.

Example:

    Suspicious PowerShell
          ↓
    Investigation
          ↓
    Malicious Script Confirmed
          ↓
    True Positive


---

## 21. Benign Positive

A benign positive is legitimate activity that matches a security detection condition but is not malicious.

Example:

    Administrator
        ↓
    PowerShell Script
        ↓
    Approved Maintenance
        ↓
    Alert Triggered
        ↓
    Benign Positive


This distinction is useful for detection tuning.


---

## 22. Alert Severity

A practical model is:

| Severity | Meaning |
|---|---|
| Informational | Useful security information |
| Low | Limited risk |
| Medium | Suspicious activity requiring investigation |
| High | Significant potential compromise |
| Critical | Confirmed or highly likely severe compromise |

Severity should be based on evidence and context.


---

## 23. Alert Prioritization

Prioritization should consider:

    Alert Severity
         +
    Asset Criticality
         +
    User Privilege
         +
    Threat Intelligence
         +
    Data Sensitivity
         +
    Exploitability
         +
    Business Impact
         ↓
    Investigation Priority


---

## 24. Triage Decision Tree

A simplified decision process:

    Alert
      ↓
    Is the alert valid?
      │
      ├── No → Close / Tune
      │
      └── Yes
            ↓
       Is activity expected?
            │
            ├── Yes → Document / Close
            │
            └── No
                  ↓
             Is it suspicious?
                  │
                  ├── No → Monitor
                  │
                  └── Yes
                        ↓
                   Investigate
                        ↓
                   Determine Impact
                        ↓
                    Escalate


---

## 25. Scope Determination

The analyst must determine whether the activity affects:

- One endpoint
- Multiple endpoints
- One user
- Multiple users
- One server
- Multiple servers
- Cloud resources
- Network infrastructure
- Sensitive data


Example:

    One Alert
       ↓
    Search Historical Events
       ↓
    Same IOC Found
       ↓
    10 Endpoints
       ↓
    Potential Widespread Incident


---

## 26. Timeline Construction

A timeline helps determine the attack sequence.

Example:

    09:00 - Phishing email received
    09:05 - User clicked link
    09:06 - PowerShell executed
    09:07 - Malware created
    09:08 - External connection
    09:10 - EDR alert
    09:12 - SOC triage
    09:15 - Endpoint isolated


Timeline analysis helps identify:

- Initial access
- Execution
- Persistence
- Discovery
- Lateral movement
- Collection
- Exfiltration


---

## 27. Correlation

A single alert may not reveal the complete attack.

Correlation combines multiple events.

Example:

    Failed Login
         +
    Successful Login
         +
    New Device
         +
    Privileged Access
         +
    Data Download
         ↓
    Potential Account Compromise


Correlation is one of the main strengths of SIEM platforms.


---

## 28. Alert Correlation

Useful correlation dimensions include:

- Same user
- Same host
- Same IP
- Same domain
- Same hash
- Same time window
- Same process
- Same attack technique


Example:

    IOC
      ↓
    Host A
      ↓
    Host B
      ↓
    Host C
      ↓
    Common Infrastructure


This can reveal lateral movement or coordinated activity.


---

## 29. MITRE ATT&CK During Triage

MITRE ATT&CK can help classify observed behavior.

Example:

    Suspicious PowerShell
          ↓
    Command and Scripting Interpreter
          ↓
    PowerShell


Another example:

    Multiple Remote Logins
          ↓
    Lateral Movement
          ↓
    Remote Services


Mapping behavior helps analysts understand attacker objectives.


---

## 30. Threat Intelligence During Triage

Threat intelligence can provide context about:

- IP reputation
- Domain reputation
- Malware
- Threat actors
- Campaigns
- C2 infrastructure
- Exploited vulnerabilities


Example:

    Suspicious IP
         ↓
    Threat Intelligence
         ↓
    Known C2 Infrastructure
         ↓
    High Confidence
         ↓
    Escalate


Threat intelligence should be treated as supporting evidence rather than the only basis for a decision.


---

## 31. Asset Criticality

Asset importance directly affects incident priority.

Example:

    Test Machine
        ↓
    Medium Risk

    Production Database
        ↓
    High Risk

    Domain Controller
        ↓
    Critical Risk


The same detection can therefore receive different priorities depending on the affected asset.


---

## 32. User Context

User context is also important.

Consider:

- Standard user
- Administrator
- Domain administrator
- Service account
- Privileged account
- External account


Example:

    PowerShell Execution

    Standard User
        → Medium Priority

    Domain Administrator
        → High / Critical Priority


---

## 33. Authentication Triage

For suspicious authentication events, investigate:

- Username
- Source IP
- Destination
- Device
- Location
- Timestamp
- Authentication method
- MFA status
- Failed attempts
- Successful attempts
- Previous login history


---

## 34. Endpoint Triage

For endpoint alerts, investigate:

- Hostname
- IP
- User
- Process
- Parent process
- Command line
- File path
- Hash
- Network connections
- Persistence
- Recent events


Example:

    Alert
      ↓
    Process Tree
      ↓
    Parent Process
      ↓
    Command Line
      ↓
    Network Connection
      ↓
    IOC Analysis


---

## 35. Network Triage

Investigate:

- Source IP
- Destination IP
- Destination domain
- Port
- Protocol
- Connection frequency
- Data volume
- DNS activity
- Historical communication


Example:

    Internal Host
         ↓
    Unusual Destination
         ↓
    Known Malicious IP
         ↓
    Large Outbound Transfer
         ↓
    High Priority


---

## 36. Cloud Triage

Cloud investigation may include:

- User identity
- API calls
- Source IP
- Geographic location
- Resource accessed
- Permission changes
- Access key usage
- MFA status
- Cloud audit logs


Example:

    New Access Key
          ↓
    Unusual Location
          ↓
    Privileged API Calls
          ↓
    Suspicious Cloud Activity


---

## 37. Email Triage

For suspicious email, investigate:

- Sender
- Recipient
- Subject
- Timestamp
- Headers
- URLs
- Attachments
- Domain
- Authentication results
- User interaction


Example:

    Suspicious Email
          ↓
    URL Analysis
          ↓
    Domain Reputation
          ↓
    User Click
          ↓
    Endpoint Investigation


---

## 38. Data Loss Triage

Investigate:

- User
- Host
- File
- File classification
- Destination
- Data volume
- Transfer method
- Authorization
- DLP alert


Example:

    Sensitive File
         ↓
    External Upload
         ↓
    Unauthorized Destination
         ↓
    Potential Data Exfiltration


---

## 39. Triage Documentation

Every triaged alert should contain:

    Alert Summary
    Analyst
    Timestamp
    Affected Host
    User
    Detection Source
    IoCs
    Investigation
    Evidence
    Verdict
    Severity
    Actions Taken
    Escalation Decision


---

## 40. Example Triage Note

### Alert

    Multiple Failed Login Attempts

### Host

    DC01

### User

    admin01

### Source

    10.10.20.45

### Investigation

    Multiple failed authentication attempts
    were observed within a short time window.

    A successful authentication followed the
    failed attempts.

    The source device is not normally used by
    the administrator.

    No approved maintenance activity was found.

### Verdict

    Suspicious / Potential Account Compromise

### Severity

    High

### Action

    Escalated for L2 investigation.


---

## 41. Example False Positive Note

### Alert

    Suspicious Port Scan

### Investigation

    Source IP belongs to the organization's
    authorized vulnerability scanning system.

    The activity occurred during the approved
    vulnerability assessment window.

### Verdict

    False Positive

### Action

    Documented and detection tuning recommended.


---

## 42. Example True Positive Note

### Alert

    Suspicious PowerShell Execution

### Investigation

    PowerShell was launched by an unusual
    parent process.

    The command line contained encoded content.

    The process established an external
    network connection.

    Threat intelligence identified the
    destination as malicious.

### Verdict

    True Positive

### Severity

    Critical

### Action

    Endpoint isolation recommended and
    incident escalated to Incident Response.


---

## 43. L1 Triage Checklist

    [ ] Read alert description
    [ ] Identify detection source
    [ ] Identify affected host
    [ ] Identify user
    [ ] Check timestamp
    [ ] Check source IP
    [ ] Check destination
    [ ] Check alert severity
    [ ] Review related alerts
    [ ] Enrich IoCs
    [ ] Check asset criticality
    [ ] Check user privilege
    [ ] Determine whether activity is expected
    [ ] Determine whether activity is suspicious
    [ ] Determine scope
    [ ] Assign verdict
    [ ] Update severity if required
    [ ] Document findings
    [ ] Escalate when necessary


---

## 44. L2 Investigation Handoff

When escalating an alert, provide:

    Alert ID
    Alert Summary
    Host
    User
    Timestamp
    IoCs
    Evidence
    Timeline
    Initial Findings
    Severity
    Scope
    Recommended Next Steps


Good escalation reduces duplicated investigation effort.


---

## 45. Common Triage Mistakes

### Mistake 1 — Trusting Alert Severity Blindly

A "Critical" alert may still be a false positive.

### Mistake 2 — Ignoring Context

The same event can have different risk levels depending on the asset and user.

### Mistake 3 — Investigating Only One Event

Attackers often generate multiple related events.

### Mistake 4 — Ignoring Historical Activity

Previous behavior may reveal whether the activity is normal.

### Mistake 5 — Failing to Document

Undocumented investigations are difficult to audit and improve.

### Mistake 6 — Closing Too Quickly

A suspicious event should be validated before closure.

### Mistake 7 — Escalating Without Evidence

Escalation should include enough context for the next analyst to continue the investigation.


---

## 46. Alert Tuning

Detection rules should be continuously improved.

Workflow:

    Alert
      ↓
    Investigation
      ↓
    False Positive?
      ↓
    Identify Cause
      ↓
    Tune Rule
      ↓
    Test
      ↓
    Deploy
      ↓
    Monitor


Possible tuning methods:

- Threshold adjustment
- Allowlisting
- Asset exclusions
- User exclusions
- Time-based exceptions
- Process exclusions
- Context-aware rules


---

## 47. Detection Engineering Feedback Loop

Triage should feed information back into detection engineering.

    Detection
       ↓
    Alert
       ↓
    Triage
       ↓
    Findings
       ↓
    False Positive / True Positive
       ↓
    Detection Improvement
       ↓
    New Detection
       ↓
    Better Alerts


This creates continuous improvement.


---

## 48. Automation in Triage

Automation can perform repetitive tasks.

Example:

    Alert
      ↓
    Extract IOC
      ↓
    Threat Intelligence
      ↓
    Asset Lookup
      ↓
    User Lookup
      ↓
    Historical Search
      ↓
    Enriched Alert
      ↓
    Analyst


Automation should reduce manual effort while preserving analyst oversight.


---

## 49. AI-Assisted Triage

AI can assist with:

- Alert summarization
- Log interpretation
- Timeline generation
- Related event identification
- Threat intelligence summarization
- Investigation recommendations
- Documentation


Example:

    Multiple Logs
         ↓
    AI-Assisted Analysis
         ↓
    Possible Attack Chain
         ↓
    Analyst Validation
         ↓
    Triage Decision


AI output should be treated as an investigative aid rather than authoritative evidence.


---

## 50. Triage Metrics

Important metrics include:

### Mean Time to Triage

Time from alert creation to initial analyst decision.

### False Positive Rate

    False Positives
    ---------------- × 100
    Total Alerts


### Escalation Rate

    Escalated Alerts
    ---------------- × 100
    Total Alerts


### True Positive Rate

    True Positives
    -------------- × 100
    Total Alerts


### Alert Closure Time

Time required to complete an alert investigation.


---

## 51. Practical Triage Project

Build a controlled SOC triage lab.

### Scenario

Generate:

- Failed logins
- Successful login
- Suspicious PowerShell
- Malware-like process activity
- Unusual network connection


### Workflow

    Generate Event
          ↓
    SIEM Detection
          ↓
    Alert
          ↓
    L1 Triage
          ↓
    IOC Enrichment
          ↓
    Correlation
          ↓
    Verdict
          ↓
    Escalation
          ↓
    Incident Response


### Documentation

Record:

    Detection
    Alert
    Evidence
    Investigation
    Verdict
    Severity
    Escalation
    Lessons Learned


---

## 52. Professional Triage Workflow

A mature SOC triage workflow is:

    Alert
      ↓
    Validate
      ↓
    Enrich
      ↓
    Correlate
      ↓
    Investigate
      ↓
    Scope
      ↓
    Prioritize
      ↓
    Verdict
      ↓
    Document
      ↓
    Escalate / Close
      ↓
    Detection Improvement


---

## 53. Key Takeaways

Incident Detection and Triage is the foundation of effective SOC operations.

A good analyst should be able to:

- Understand security alerts
- Validate detections
- Analyze context
- Investigate IoCs
- Correlate events
- Determine scope
- Assess severity
- Identify false positives
- Identify true positives
- Document findings
- Escalate appropriately

The most important principle is:

> **Never treat an alert as an incident without investigation, and never close a suspicious alert without sufficient evidence.**

---

## 54. Conclusion

Effective Incident Detection and Triage connects security monitoring with Incident Response.

The complete process is:

    Security Event
          ↓
    Detection
          ↓
    Alert
          ↓
    Triage
          ↓
    Enrichment
          ↓
    Correlation
          ↓
    Investigation
          ↓
    Scope
          ↓
    Verdict
          ↓
    Escalation
          ↓
    Incident Response
          ↓
    Continuous Improvement


A professional SOC analyst should combine technical evidence, business context, threat intelligence, automation, and analytical reasoning to determine which alerts require immediate action.

The ultimate goal is not to process the highest number of alerts.

The goal is to **identify the most important threats accurately, quickly, consistently, and with sufficient evidence to support the next stage of Incident Response.**
