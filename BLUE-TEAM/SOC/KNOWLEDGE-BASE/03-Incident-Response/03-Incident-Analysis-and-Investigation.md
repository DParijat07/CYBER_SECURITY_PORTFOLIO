# Incident Analysis and Investigation

## 1. Introduction

Incident Analysis and Investigation is the process of examining a confirmed or suspected security incident to determine what happened, how it happened, which systems and users were affected, what evidence exists, and what actions are required.

It transforms initial triage findings into a structured understanding of the incident.

The core workflow is:

    Alert
      ↓
    Triage
      ↓
    Investigation
      ↓
    Evidence Collection
      ↓
    Correlation
      ↓
    Timeline
      ↓
    Attack Reconstruction
      ↓
    Scope Determination
      ↓
    Impact Assessment
      ↓
    Response


---

## 2. Objectives

The primary objectives of incident investigation are to:

- Determine whether malicious activity occurred
- Identify the initial attack vector
- Identify affected systems
- Identify affected users
- Identify Indicators of Compromise (IoCs)
- Reconstruct the attack timeline
- Determine attacker behavior
- Identify persistence mechanisms
- Determine lateral movement
- Identify compromised accounts
- Determine data access or exfiltration
- Assess business impact
- Identify root cause
- Provide evidence for containment and eradication
- Improve future detection and prevention


---

## 3. Investigation Principles

A professional investigation should be:

### Evidence-Based

Conclusions should be supported by available evidence.

### Repeatable

Another analyst should be able to understand and reproduce the investigation process.

### Objective

Analysts should distinguish facts from assumptions.

### Documented

Important observations, decisions, and actions should be recorded.

### Time-Aware

Timestamps should be correlated carefully across different systems.

### Scope-Aware

The investigation should determine whether the incident affects one system or a wider environment.


---

## 4. Investigation vs Triage

Triage answers:

> "Does this alert require further action?"

Investigation answers:

> "What exactly happened, how did it happen, and what was affected?"

Typical progression:

    Alert
      ↓
    L1 Triage
      ↓
    Suspicious
      ↓
    L2 Investigation
      ↓
    Confirmed Incident
      ↓
    Incident Response


---

## 5. Investigation Questions

During an investigation, the analyst should continuously ask:

### What?

What happened?

### When?

When did the activity occur?

### Where?

Which systems, applications, networks, or cloud resources were involved?

### Who?

Which users, accounts, processes, or external entities were involved?

### How?

How did the attacker gain access and move through the environment?

### Why?

What was the likely objective?

### Impact?

What systems, data, or business operations were affected?


---

## 6. Investigation Lifecycle

A structured investigation can follow:

    01. Confirm Incident
          ↓
    02. Define Scope
          ↓
    03. Preserve Evidence
          ↓
    04. Collect Evidence
          ↓
    05. Analyze Evidence
          ↓
    06. Correlate Events
          ↓
    07. Build Timeline
          ↓
    08. Reconstruct Attack
          ↓
    09. Identify IoCs
          ↓
    10. Determine Impact
          ↓
    11. Identify Root Cause
          ↓
    12. Recommend Response


---

## 7. Initial Investigation

Before collecting large amounts of data, establish the basic facts.

Record:

    Incident ID
    Detection Source
    Alert ID
    Date and Time
    Affected Host
    Affected User
    Source IP
    Destination IP
    Detection Rule
    Initial Severity
    Initial Analyst
    Initial Findings


---

## 8. Incident Scope

Scope determines the boundaries of the incident.

Investigate:

- Hosts
- Servers
- Users
- Accounts
- Applications
- Network segments
- Cloud resources
- Data repositories
- External destinations


Example:

    Initial Alert
         ↓
    Host A
         ↓
    Search IOC
         ↓
    Host B
         ↓
    Search IOC
         ↓
    Host C
         ↓
    Potential Multi-Host Incident


---

## 9. Evidence Sources

Evidence may come from:

### Endpoint

- Windows Event Logs
- Sysmon
- EDR
- File system
- Registry
- Process information
- Scheduled tasks
- Services

### Network

- Firewall
- IDS/IPS
- DNS
- Proxy
- VPN
- NetFlow
- Packet capture

### Identity

- Authentication logs
- Active Directory
- MFA logs
- Privileged access systems

### Application

- Web server logs
- Application logs
- Database logs
- API logs

### Cloud

- Cloud audit logs
- Identity logs
- API activity
- Object access logs
- Security services

### Email

- Email headers
- Mail gateway
- Attachments
- URLs
- Authentication results


---

## 10. Evidence Preservation

Evidence should be preserved before significant changes are made to affected systems whenever possible.

Important principles include:

- Avoid unnecessary modification of evidence
- Record collection time
- Record source system
- Record collector
- Preserve original evidence
- Maintain hashes where appropriate
- Document evidence handling


Example:

    Evidence
       ↓
    Collection
       ↓
    Hash
       ↓
    Secure Storage
       ↓
    Analysis Copy


---

## 11. Chain of Custody

For investigations requiring formal evidence handling, document:

    Evidence ID
    Description
    Source
    Collection Time
    Collector
    Transfer Time
    Recipient
    Storage Location
    Hash
    Purpose


Chain of custody helps demonstrate that evidence was handled consistently.


---

## 12. Log Analysis

Logs are one of the most important sources of investigation evidence.

Analysts should examine:

- Timestamp
- Event ID
- User
- Host
- Source
- Destination
- Process
- Action
- Result
- Status


Example:

    Authentication Failure
          ↓
    Same Source IP
          ↓
    Multiple Accounts
          ↓
    Successful Login
          ↓
    Suspicious Authentication


---

## 13. Windows Investigation

Important Windows evidence may include:

- Security Event Logs
- System Event Logs
- PowerShell logs
- Sysmon
- Task Scheduler
- Services
- Registry
- Prefetch
- Windows Defender logs
- User activity


Useful investigation areas include:

    Process Creation
    Network Connections
    Logon Events
    Account Changes
    Privilege Changes
    PowerShell Activity
    Persistence


---

## 14. Linux Investigation

Linux investigation may include:

- Authentication logs
- Syslog
- Audit logs
- Shell history
- Process list
- Network connections
- Cron jobs
- SSH activity
- Services
- File changes


Example:

    SSH Login
       ↓
    Shell Activity
       ↓
    Privilege Escalation
       ↓
    Persistence
       ↓
    Network Connection


---

## 15. Network Investigation

Network analysis can identify:

- Source
- Destination
- Protocol
- Port
- DNS activity
- Connection frequency
- Data volume
- Suspicious domains
- Command-and-control traffic


Example:

    Compromised Host
          ↓
    DNS Query
          ↓
    Suspicious Domain
          ↓
    External Connection
          ↓
    Repeated Beaconing


---

## 16. Process Investigation

Process analysis helps identify suspicious execution.

Review:

- Process name
- Parent process
- Command line
- User
- Path
- Hash
- Start time
- Network activity
- Child processes


Example:

    Office Application
          ↓
    PowerShell
          ↓
    Encoded Command
          ↓
    Network Connection


This may indicate malicious execution.


---

## 17. Parent-Child Process Analysis

Parent-child relationships are extremely useful.

Example:

    winword.exe
         ↓
    powershell.exe
         ↓
    cmd.exe
         ↓
    suspicious.exe


An unusual process chain can provide strong evidence of malicious activity.


---

## 18. Authentication Investigation

For suspicious authentication activity, examine:

- Username
- Source IP
- Destination
- Authentication type
- Login time
- Failed attempts
- Successful attempts
- MFA status
- Device
- Geographic location
- Privilege level


Example:

    30 Failed Attempts
          ↓
    Successful Login
          ↓
    New Device
          ↓
    Privileged Account
          ↓
    High-Risk Investigation


---

## 19. Account Compromise Investigation

Potential evidence includes:

- Password changes
- New MFA devices
- New sessions
- Unusual login locations
- Privilege changes
- New API keys
- Suspicious mailbox rules
- Unusual resource access


The objective is to determine:

    Was the account compromised?
           ↓
    How was access obtained?
           ↓
    What did the attacker access?
           ↓
    Did the attacker create persistence?


---

## 20. Persistence Investigation

Persistence allows an attacker to maintain access.

Investigate:

- Scheduled tasks
- Services
- Startup items
- Registry run keys
- Cron jobs
- SSH keys
- Web shells
- Account creation
- Cloud access keys


Example:

    Initial Compromise
          ↓
    Persistence
          ↓
    Reboot
          ↓
    Malicious Process
          ↓
    Continued Access


---

## 21. Privilege Escalation Investigation

Investigate:

- Administrative group changes
- Sudo usage
- UAC bypass indicators
- Exploited vulnerabilities
- Credential theft
- Service abuse
- Token manipulation


Example:

    Standard User
          ↓
    Exploitation
          ↓
    Elevated Privileges
          ↓
    Administrative Activity


---

## 22. Lateral Movement Investigation

Look for:

- RDP
- SMB
- SSH
- WinRM
- Remote services
- Remote administration tools
- Credential reuse
- Administrative shares


Example:

    Host A
      ↓
    Stolen Credentials
      ↓
    Host B
      ↓
    Remote Access
      ↓
    Host C


---

## 23. Data Collection Investigation

Determine whether the attacker accessed or collected sensitive information.

Investigate:

- Files accessed
- Database queries
- Archive creation
- Large file reads
- Sensitive directories
- Cloud object access
- Email access


Example:

    Sensitive Files
          ↓
    Archive Created
          ↓
    Archive Accessed
          ↓
    External Transfer


---

## 24. Data Exfiltration Investigation

Look for:

- Large outbound transfers
- Unusual destinations
- Cloud storage uploads
- DNS tunneling
- Web uploads
- Archive transfers
- Suspicious encrypted connections


Example:

    Data Collection
          ↓
    Compression
          ↓
    Staging
          ↓
    External Transfer


---

## 25. Malware Investigation

Malware investigation may include:

- File name
- File path
- Hash
- Parent process
- Child processes
- Persistence
- Network connections
- DNS
- C2 indicators
- File modifications


Example:

    Suspicious File
          ↓
    Hash Analysis
          ↓
    Threat Intelligence
          ↓
    Process Analysis
          ↓
    Network Analysis
          ↓
    Malware Classification


---

## 26. Phishing Investigation

A phishing investigation should examine:

- Sender
- Sender domain
- Recipient
- Email headers
- URLs
- Attachments
- Domain age/reputation
- Authentication results
- User interaction
- Endpoint activity


Workflow:

    Email
      ↓
    Header Analysis
      ↓
    URL / Attachment Analysis
      ↓
    User Interaction
      ↓
    Endpoint Investigation
      ↓
    Account Investigation


---

## 27. Web Application Investigation

Investigate:

- HTTP requests
- Source IP
- User agent
- URI
- Parameters
- Response codes
- Authentication
- Application errors
- Database activity


Example:

    Suspicious Request
          ↓
    Web Server Log
          ↓
    Application Log
          ↓
    Database Log
          ↓
    Possible Exploitation


---

## 28. Cloud Investigation

Cloud investigations may involve:

- Identity activity
- API calls
- Access keys
- Role changes
- Resource creation
- Resource deletion
- Network changes
- Object access
- Cloud audit logs


Example:

    Compromised Identity
          ↓
    API Access
          ↓
    Privilege Change
          ↓
    Resource Access
          ↓
    Data Access


---

## 29. IOC Identification

Indicators of Compromise can include:

### Network

- IP addresses
- Domains
- URLs
- Ports

### Host

- File hashes
- File names
- File paths
- Registry keys
- Mutexes

### Identity

- Compromised accounts
- Email addresses
- Access keys

### Behavioral

- Suspicious commands
- Process chains
- Unusual authentication
- Abnormal network behavior


---

## 30. IOC Validation

An IOC should be evaluated in context.

Example:

    IP Address
       ↓
    Threat Intelligence
       ↓
    Historical SIEM Search
       ↓
    DNS Search
       ↓
    Network Search
       ↓
    Endpoint Search
       ↓
    Confidence Assessment


A single IOC should not automatically be treated as proof of compromise.


---

## 31. Timeline Analysis

Timeline construction is one of the most important investigation activities.

Example:

    08:55 - Phishing email received
    09:02 - User opened attachment
    09:03 - Word process spawned PowerShell
    09:04 - Suspicious script executed
    09:05 - Malware file created
    09:06 - External connection established
    09:08 - Credential access observed
    09:10 - Lateral movement attempted
    09:12 - SOC alert generated
    09:15 - Analyst began investigation
    09:20 - Endpoint isolated


The timeline helps reconstruct the attack sequence.


---

## 32. Attack Chain Reconstruction

A mature investigation should attempt to reconstruct the attack.

Example:

    Initial Access
          ↓
    Execution
          ↓
    Persistence
          ↓
    Privilege Escalation
          ↓
    Credential Access
          ↓
    Discovery
          ↓
    Lateral Movement
          ↓
    Collection
          ↓
    Exfiltration


Not every incident will contain every stage.


---

## 33. MITRE ATT&CK Mapping

Observed activity can be mapped to MITRE ATT&CK.

Example:

    Phishing
       ↓
    Initial Access

    PowerShell
       ↓
    Execution

    Scheduled Task
       ↓
    Persistence

    Credential Dumping
       ↓
    Credential Access

    RDP
       ↓
    Lateral Movement


ATT&CK mapping helps analysts describe attacker behavior consistently.


---

## 34. Correlation Across Systems

Investigations should correlate evidence from multiple sources.

Example:

    SIEM
      +
    EDR
      +
    Firewall
      +
    DNS
      +
    Authentication
      +
    Email
      ↓
    Unified Timeline


No single data source is guaranteed to contain the complete attack story.


---

## 35. Hypothesis-Driven Investigation

A useful investigation technique is hypothesis-driven analysis.

Example:

### Hypothesis

The attacker compromised a user account through phishing.

### Evidence to Search

- Phishing email
- Login anomalies
- MFA events
- New sessions
- Password changes
- Mailbox rules
- Resource access

### Result

    Evidence Supports Hypothesis
             OR
    Evidence Contradicts Hypothesis


This prevents random investigation.


---

## 36. Root Cause Analysis

Root cause identifies the underlying reason the incident occurred.

Possible root causes:

- Phishing
- Weak credentials
- Unpatched vulnerability
- Misconfiguration
- Excessive privileges
- Exposed service
- Insecure application
- Poor access controls
- Lack of monitoring


Example:

    Incident
       ↓
    Compromised Account
       ↓
    Phishing
       ↓
    User Clicked Malicious Link
       ↓
    Lack of Email Filtering
       ↓
    Root Cause / Contributing Factors


---

## 37. Impact Assessment

Determine:

- Systems affected
- Users affected
- Data affected
- Business services affected
- Credentials compromised
- Downtime
- Financial impact
- Regulatory impact
- Reputation impact


Impact should be based on evidence where possible.


---

## 38. Confidence Assessment

Investigation findings can be categorized as:

### Confirmed

Strong evidence directly supports the conclusion.

### Highly Likely

Multiple independent evidence sources support the conclusion.

### Possible

Evidence exists but is incomplete.

### Unknown

Insufficient evidence to reach a conclusion.


Avoid presenting assumptions as confirmed facts.


---

## 39. Investigation Documentation

Document:

    Incident Summary
    Scope
    Evidence
    IoCs
    Timeline
    Findings
    Attack Chain
    Impact
    Root Cause
    Confidence
    Containment Recommendations
    Eradication Recommendations
    Recovery Recommendations
    Lessons Learned


---

## 40. Investigation Notebook

A practical analyst notebook can contain:

    Date / Time
    Observation
    Evidence Source
    Query / Command
    Result
    Interpretation
    Next Action


Example:

    10:15
    Observation:
    PowerShell spawned by Word.

    Source:
    Sysmon Event ID 1.

    Interpretation:
    Potential malicious document execution.

    Next Action:
    Investigate command line and network activity.


---

## 41. Evidence Quality

Evidence can be evaluated based on:

- Reliability
- Relevance
- Integrity
- Timeliness
- Corroboration


Strong investigations combine multiple independent evidence sources.


---

## 42. Investigation Queries

Typical SIEM searches may investigate:

- Same IP across multiple hosts
- Same hash across endpoints
- Same user across locations
- Same domain across DNS logs
- Same process across endpoints
- Events immediately before and after an alert


Example:

    IOC
      ↓
    Search ±24 Hours
      ↓
    Search All Hosts
      ↓
    Search All Users
      ↓
    Search Related Events


---

## 43. Investigation Toolset

Potential tools include:

### SIEM

- Wazuh
- Splunk
- Elastic Security

### Endpoint

- Sysmon
- Windows Event Viewer
- PowerShell
- Linux tools
- EDR platforms

### Network

- Wireshark
- tcpdump
- Zeek
- Firewall logs

### Threat Intelligence

- IOC reputation
- Malware intelligence
- ATT&CK
- Threat feeds

### Automation

- Python
- PowerShell
- Bash
- APIs


---

## 44. Practical Investigation Workflow

A complete investigation can follow:

    01. Receive Alert
          ↓
    02. Validate Alert
          ↓
    03. Confirm Suspicious Activity
          ↓
    04. Define Scope
          ↓
    05. Preserve Evidence
          ↓
    06. Collect Logs
          ↓
    07. Investigate Endpoint
          ↓
    08. Investigate Network
          ↓
    09. Investigate Identity
          ↓
    10. Correlate Evidence
          ↓
    11. Build Timeline
          ↓
    12. Reconstruct Attack
          ↓
    13. Identify IoCs
          ↓
    14. Determine Impact
          ↓
    15. Determine Root Cause
          ↓
    16. Document Findings
          ↓
    17. Recommend Response


---

## 45. Investigation Checklist

    [ ] Confirm alert
    [ ] Identify incident ID
    [ ] Identify affected host
    [ ] Identify affected user
    [ ] Record timestamps
    [ ] Determine scope
    [ ] Preserve important evidence
    [ ] Collect endpoint logs
    [ ] Collect network evidence
    [ ] Review authentication activity
    [ ] Review process activity
    [ ] Review persistence
    [ ] Identify IoCs
    [ ] Search historical activity
    [ ] Correlate related events
    [ ] Build timeline
    [ ] Map attack techniques
    [ ] Determine impact
    [ ] Determine root cause
    [ ] Assess confidence
    [ ] Document findings
    [ ] Recommend containment
    [ ] Recommend eradication
    [ ] Recommend recovery


---

## 46. Example Investigation

### Scenario

A Wazuh alert reports suspicious PowerShell activity on a Windows endpoint.

### Initial Alert

    Host: WIN-CLIENT01
    User: user01
    Process: powershell.exe
    Parent: winword.exe
    Severity: High


### Investigation

The analyst identifies:

    Word
      ↓
    PowerShell
      ↓
    Encoded Command
      ↓
    File Creation
      ↓
    External Network Connection


### Additional Evidence

- The user received a suspicious email.
- The email contained an attachment.
- The attachment was opened shortly before the PowerShell execution.
- The destination IP has a malicious reputation.
- The same IOC was found on another endpoint.


### Assessment

    Initial Access
        ↓
    Phishing

    Execution
        ↓
    PowerShell

    Command and Control
        ↓
    External Connection


### Scope

Two endpoints are potentially affected.

### Recommended Response

- Isolate affected endpoints
- Preserve evidence
- Investigate the user account
- Search for the same IoCs across the environment
- Begin containment
- Escalate to Incident Response


---

## 47. AI-Assisted Investigation

AI can assist analysts with:

- Large log summarization
- Timeline construction
- Event correlation
- Command interpretation
- Investigation hypothesis generation
- Report drafting
- ATT&CK mapping assistance


Example:

    Large Log Dataset
          ↓
    AI-Assisted Summarization
          ↓
    Potential Sequence
          ↓
    Analyst Validation
          ↓
    Confirmed Findings


AI should not replace evidence collection or human validation.

---

## 48. Automation-Assisted Investigation

Automation can reduce repetitive investigation tasks.

Example:

    Alert
      ↓
    Extract IoCs
      ↓
    Query SIEM
      ↓
    Query Threat Intelligence
      ↓
    Query Asset Inventory
      ↓
    Query EDR
      ↓
    Build Investigation Package
      ↓
    Analyst Review


This can significantly reduce investigation time.


---

## 49. Investigation Metrics

Useful metrics include:

### Mean Time to Investigate

Average time required to complete an investigation.

### Mean Time to Contain

Average time from incident identification to containment.

### Investigation Completion Rate

    Completed Investigations
    ------------------------ × 100
    Total Investigations


### Evidence Coverage

Percentage of required evidence sources successfully collected.

### IOC Coverage

Percentage of identified IoCs searched across available systems.


---

## 50. Lessons Learned

Every investigation should identify:

- What worked?
- What failed?
- What evidence was missing?
- Which detection worked?
- Which detection failed?
- What caused the incident?
- What controls should be improved?
- What automation can be added?
- What playbook should be updated?


---

## 51. Detection Improvement

Investigation findings should improve detection.

Example:

    Investigation
         ↓
    Unknown Behavior Identified
         ↓
    Detection Gap
         ↓
    New Detection Rule
         ↓
    Test
         ↓
    Deploy
         ↓
    Monitor


This creates a continuous defensive improvement cycle.


---

## 52. Professional Investigation Report

A professional report should contain:

    Executive Summary
    Incident Overview
    Detection
    Scope
    Evidence
    IoCs
    Timeline
    Technical Findings
    Attack Chain
    Impact
    Root Cause
    Confidence
    Containment Recommendations
    Eradication Recommendations
    Recovery Recommendations
    Lessons Learned
    Detection Improvements


---

## 53. Key Takeaways

Effective incident investigation requires more than finding suspicious logs.

A professional analyst should be able to:

- Collect evidence
- Analyze logs
- Investigate endpoints
- Analyze network activity
- Investigate identity events
- Correlate multiple data sources
- Identify IoCs
- Build timelines
- Reconstruct attack chains
- Determine scope
- Assess impact
- Identify root cause
- Document findings
- Support containment and recovery


The key principle is:

> **Build conclusions from correlated evidence rather than assumptions.**

---

## 54. Final Investigation Workflow

The complete investigation model is:

    Alert
      ↓
    Triage
      ↓
    Incident Confirmation
      ↓
    Scope
      ↓
    Evidence Preservation
      ↓
    Evidence Collection
      ↓
    Endpoint Analysis
      ↓
    Network Analysis
      ↓
    Identity Analysis
      ↓
    Correlation
      ↓
    Timeline
      ↓
    Attack Reconstruction
      ↓
    IOC Identification
      ↓
    Impact Assessment
      ↓
    Root Cause
      ↓
    Confidence Assessment
      ↓
    Response Recommendations
      ↓
    Documentation
      ↓
    Detection Improvement


---

## 55. Conclusion

Incident Analysis and Investigation transforms a suspicious alert into an evidence-based understanding of a security incident.

The analyst's role is to determine:

    What happened?
    When did it happen?
    How did it happen?
    Who was involved?
    What was affected?
    What evidence supports the findings?
    What was the impact?
    What caused the incident?
    What should happen next?

A mature investigation combines **SIEM data, endpoint telemetry, network evidence, identity logs, threat intelligence, automation, and human analytical judgment**.

The ultimate objective is to provide accurate evidence and actionable findings that enable effective **containment, eradication, recovery, and continuous security improvement**.
