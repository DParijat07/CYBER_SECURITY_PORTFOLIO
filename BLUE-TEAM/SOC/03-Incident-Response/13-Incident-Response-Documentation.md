# Incident Response Documentation

## 1. Introduction

Incident Response Documentation is the structured recording of everything related to a cybersecurity incident, from initial detection and investigation through containment, recovery, and lessons learned.

Good documentation provides:

- A complete incident history
- Evidence of actions taken
- Investigation timelines
- Communication records
- Root cause analysis
- Recovery details
- Compliance evidence
- Knowledge for future incidents
- Input for security improvements

The basic model is:

    Detection
       ↓
    Investigation
       ↓
    Documentation
       ↓
    Containment
       ↓
    Recovery
       ↓
    Closure
       ↓
    Lessons Learned


---

## 2. Objectives

Incident documentation should:

- Preserve an accurate incident record
- Support investigation
- Improve collaboration
- Enable escalation
- Support management decisions
- Maintain accountability
- Support legal and compliance requirements
- Improve future response
- Provide evidence of security operations


---

## 3. Why Documentation Matters

Without documentation:

    Incident
       ↓
    Investigation
       ↓
    Memory-Based Reporting
       ↓
    Missing Details
       ↓
    Poor Lessons Learned


With proper documentation:

    Incident
       ↓
    Evidence
       ↓
    Timeline
       ↓
    Actions
       ↓
    Analysis
       ↓
    Final Report
       ↓
    Improvement


---

## 4. Incident Documentation Lifecycle

A complete documentation lifecycle is:

    Alert Created
         ↓
    Case Opened
         ↓
    Initial Triage
         ↓
    Investigation Notes
         ↓
    Evidence Collection
         ↓
    Containment Actions
         ↓
    Eradication
         ↓
    Recovery
         ↓
    Final Report
         ↓
    Lessons Learned
         ↓
    Case Closed


---

## 5. Incident Record

Every incident should have a unique identifier.

Example:

    Incident ID:
    INC-2026-001

    Title:
    Suspicious PowerShell Activity

    Severity:
    High

    Status:
    Investigating

    Assigned To:
    SOC L2

    Date Detected:
    2026-08-20

    Affected Asset:
    WIN-CLIENT-01


---

## 6. Core Incident Fields

A standard incident record may contain:

- Incident ID
- Title
- Description
- Date/time detected
- Date/time occurred
- Severity
- Priority
- Status
- Affected users
- Affected assets
- Source
- Detection method
- Assigned analyst
- Incident category
- IoCs
- Investigation notes
- Actions
- Escalation
- Resolution
- Root cause
- Lessons learned


---

## 7. Incident Status

Common statuses include:

    New
      ↓
    Assigned
      ↓
    Investigating
      ↓
    Contained
      ↓
    Eradicated
      ↓
    Recovering
      ↓
    Resolved
      ↓
    Closed


Other states may include:

- Pending
- Escalated
- Monitoring
- False Positive
- Duplicate


---

## 8. Incident Classification

Incidents should be categorized.

Example categories:

- Phishing
- Malware
- Ransomware
- Account Compromise
- Brute Force
- Data Exfiltration
- Privilege Escalation
- Vulnerability Exploitation
- Web Attack
- Insider Threat
- Cloud Security
- Network Security


---

## 9. Incident Severity

A simple model:

### Critical

Major business disruption, widespread compromise, or significant data exposure.

### High

Confirmed compromise with significant risk.

### Medium

Confirmed or strongly suspected malicious activity with limited impact.

### Low

Minor security event with limited risk.


Severity should be based on risk and impact, not just alert severity.


---

## 10. Incident Description

The description should be concise but informative.

Example:

    The SOC detected suspicious PowerShell
    activity on WIN-CLIENT-01. The command
    contained an encoded payload and initiated
    an outbound connection to an external IP.
    Investigation identified unauthorized
    execution by the affected user account.


Avoid unnecessary speculation.


---

## 11. Five Ws Documentation

Every incident should answer:

### Who?

Who was involved?

### What?

What happened?

### When?

When did it happen?

### Where?

Where did it occur?

### Why?

Why is it considered suspicious or malicious?


Example:

    Who:
    user01

    What:
    Suspicious PowerShell execution

    When:
    10:15 UTC

    Where:
    WIN-CLIENT-01

    Why:
    Encoded command downloaded an executable


---

## 12. Incident Timeline

A timeline is one of the most important components.

Example:

| Time | Event |
|---|---|
| 10:00 | Phishing email received |
| 10:05 | User clicked link |
| 10:07 | Authentication attempt detected |
| 10:10 | SIEM generated alert |
| 10:15 | Analyst acknowledged alert |
| 10:25 | Account disabled |
| 10:40 | Endpoint isolated |
| 11:30 | Investigation completed |


The timeline should distinguish confirmed facts from assumptions.


---

## 13. Timestamp Standardization

Use a consistent time zone.

Example:

    UTC


Or clearly document the local time zone.

When investigating distributed environments:

    Endpoint Time
         ↓
    SIEM Time
         ↓
    Cloud Time
         ↓
    Normalize to UTC


Incorrect timestamps can create misleading timelines.


---

## 14. Investigation Notes

Analysts should document:

- What was checked
- What was discovered
- Which tools were used
- Which queries were executed
- Which evidence was collected
- Why decisions were made
- What remains unknown


Example:

    Checked Windows Security Event Logs
    for authentication activity.

    Found successful login from an unusual
    external IP at 10:07 UTC.

    Compared the IP against previous
    authentication activity.

    No previous legitimate activity found.


---

## 15. Analyst Notes vs Final Report

### Analyst Notes

Detailed working information.

May include:

- Queries
- Hypotheses
- Intermediate findings
- Screenshots
- Technical observations


### Final Report

A concise summary of:

- What happened
- Impact
- Root cause
- Response
- Resolution
- Recommendations


Both are important.


---

## 16. Evidence Documentation

Record:

- Evidence ID
- Evidence type
- Source
- Collection time
- Analyst
- Hash where applicable
- Storage location
- Description


Example:

    Evidence ID:
    EV-001

    Type:
    Windows Event Log

    Source:
    WIN-CLIENT-01

    Collected:
    10:30 UTC

    Analyst:
    SOC-L2


---

## 17. Evidence Integrity

Evidence should be handled carefully.

Possible controls:

- Access restrictions
- Secure storage
- Hashing
- Timestamping
- Chain of custody
- Audit logging


Example:

    Evidence
       ↓
    Hash
       ↓
    Secure Storage
       ↓
    Access Control
       ↓
    Investigation


---

## 18. Chain of Custody

Chain of custody records who handled evidence and when.

Example:

| Time | Person | Action |
|---|---|---|
| 10:30 | Analyst A | Collected |
| 10:45 | Analyst A | Stored |
| 11:20 | Analyst B | Analyzed |
| 12:00 | IR Lead | Reviewed |


This becomes especially important for investigations that may have legal implications.


---

## 19. IoC Documentation

Document Indicators of Compromise such as:

- IP addresses
- Domains
- URLs
- File hashes
- Email addresses
- Filenames
- Registry keys
- User accounts
- Processes


Example:

    IoC Type: SHA256
    Value: <hash>

    IoC Type: Domain
    Value: malicious-example.com

    IoC Type: IP
    Value: 203.0.113.10


Use appropriate handling controls for sensitive indicators.


---

## 20. IoC Table

Example:

| Type | Indicator | Source | Confidence |
|---|---|---|---|
| IP | 203.0.113.10 | Firewall | High |
| Domain | example.com | DNS | High |
| Hash | SHA256... | EDR | High |
| User | user01 | IAM | Medium |


---

## 21. Investigation Hypothesis

Analysts may document working hypotheses.

Example:

    Hypothesis:

    The attacker obtained credentials
    through phishing and used them to
    access the cloud account.


Then test the hypothesis against evidence.

    Hypothesis
        ↓
    Evidence
        ↓
    Validation
        ↓
    Confirmed / Rejected


Avoid presenting an unverified hypothesis as fact.


---

## 22. Root Cause Documentation

Root cause explains why the incident occurred.

Example:

    Root Cause:
    User credentials were compromised
    through a phishing campaign.

Possible contributing factors:

- Missing MFA
- Weak password
- Outdated software
- Misconfiguration
- Excessive privileges
- Poor monitoring


---

## 23. Contributing Factors

Root cause and contributing factors are different.

Example:

    Root Cause:
    Credential theft

    Contributing Factors:
    - No MFA
    - Excessive privileges
    - Weak email filtering
    - Insufficient user awareness


This provides better improvement opportunities.


---

## 24. Attack Path Documentation

Document how the attacker moved through the environment.

Example:

    Phishing Email
         ↓
    Credential Theft
         ↓
    Account Access
         ↓
    Privilege Escalation
         ↓
    Internal Discovery
         ↓
    Data Access


This can be mapped to MITRE ATT&CK techniques.


---

## 25. MITRE ATT&CK Mapping

Document relevant techniques.

Example:

| Activity | Technique |
|---|---|
| Phishing | T1566 |
| PowerShell | T1059.001 |
| Account Discovery | T1087 |
| Valid Accounts | T1078 |
| Remote Services | T1021 |


Mapping helps improve detection coverage.


---

## 26. Response Actions

Document every significant action.

Example:

    10:25 UTC
    Disabled compromised account.

    10:30 UTC
    Revoked active sessions.

    10:40 UTC
    Isolated endpoint.

    11:00 UTC
    Blocked malicious domain.

    11:30 UTC
    Reset credentials.


Actions should include timestamps where practical.


---

## 27. Containment Documentation

Document:

- What was contained
- Why containment was required
- Who approved it
- When it happened
- What impact containment caused


Example:

    Endpoint WIN-CLIENT-01 was isolated
    to prevent potential lateral movement.


---

## 28. Eradication Documentation

Record actions such as:

- Malware removal
- Persistence removal
- Credential reset
- Patch deployment
- Configuration correction
- Unauthorized account removal


Example:

    Malicious scheduled task was removed
    after confirming it was responsible
    for persistence.


---

## 29. Recovery Documentation

Record:

- Systems restored
- Backup used
- Validation performed
- Monitoring period
- Service restoration time


Example:

    Endpoint rebuilt from trusted image.

    Security controls validated.

    Endpoint monitored for 24 hours.

    No further malicious activity observed.


---

## 30. Communication Log

Maintain a communication record.

Example:

| Time | Recipient | Method | Summary |
|---|---|---|---|
| 10:20 | IR Lead | Ticket | Incident escalated |
| 10:30 | IT | Email | Endpoint isolation requested |
| 11:00 | Management | Report | Initial impact shared |


Avoid including unnecessary sensitive information.


---

## 31. Stakeholder Documentation

Possible stakeholders:

- SOC
- Incident Response
- IT
- Network Team
- Cloud Team
- IAM Team
- Management
- Legal
- Privacy
- Compliance
- System Owner


The exact stakeholders depend on the incident.


---

## 32. Incident Report

A final incident report generally contains:

    Executive Summary
    Incident Overview
    Timeline
    Impact
    Investigation
    IoCs
    Root Cause
    Response Actions
    Recovery
    Lessons Learned
    Recommendations


---

## 33. Executive Summary

The executive summary should avoid unnecessary technical details.

Example:

    A phishing campaign resulted in the
    compromise of one employee account.
    The account was disabled and active
    sessions were revoked. No evidence of
    data exfiltration was identified.

    The organization has implemented
    additional email filtering and MFA
    enforcement.


---

## 34. Technical Summary

The technical summary should explain:

- Initial access
- Attack activity
- Affected systems
- Detection
- Investigation
- Containment
- Eradication
- Recovery


Example:

    Initial access occurred through a
    phishing link.

    Authentication logs identified
    suspicious login activity.

    The account was disabled and sessions
    revoked.

    Endpoint telemetry showed no evidence
    of persistent malware.


---

## 35. Impact Assessment

Document:

- Systems affected
- Users affected
- Data affected
- Service disruption
- Business impact
- Financial impact if known
- Regulatory impact if applicable


Example:

    Systems Affected:
    1

    Users Affected:
    1

    Confirmed Data Loss:
    None

    Service Disruption:
    None


---

## 36. Business Impact

Technical impact should be translated into business language.

Example:

    Technical:
    One endpoint was isolated.

    Business:
    One employee experienced temporary
    service disruption for approximately
    30 minutes.


---

## 37. Incident Closure Criteria

An incident should not be closed simply because the alert disappears.

Closure may require:

    [ ] Threat contained
    [ ] Root cause identified
    [ ] IoCs documented
    [ ] Affected systems validated
    [ ] Credentials secured
    [ ] Recovery completed
    [ ] Monitoring completed
    [ ] Required stakeholders notified
    [ ] Final report completed
    [ ] Lessons learned documented


---

## 38. Lessons Learned

After the incident, ask:

- What worked well?
- What failed?
- What took too long?
- Was detection effective?
- Was containment effective?
- Were playbooks useful?
- Were logs available?
- Was communication effective?
- What should change?


---

## 39. Corrective Actions

Corrective actions should be specific.

Example:

    Problem:
    Delayed detection

    Action:
    Improve authentication monitoring

    Owner:
    SOC

    Deadline:
    30 days

    Status:
    In Progress


---

## 40. Preventive Actions

Preventive actions reduce future risk.

Examples:

- Enable MFA
- Improve email filtering
- Patch vulnerable systems
- Reduce privileges
- Improve logging
- Update detection rules
- Improve endpoint controls
- Conduct security awareness training


---

## 41. Action Tracking

Use a structured table.

| Action | Owner | Priority | Due Date | Status |
|---|---|---|---|---|
| Enable MFA | IAM | High | 30 days | Open |
| Update detection | SOC | Medium | 14 days | In Progress |
| Patch endpoint | IT | High | 7 days | Complete |


---

## 42. Documentation Quality

Good incident documentation should be:

- Accurate
- Objective
- Clear
- Chronological
- Evidence-based
- Reproducible
- Concise where appropriate
- Technically detailed where required


Avoid:

- Unsupported assumptions
- Emotional language
- Blame
- Unverified conclusions
- Missing timestamps


---

## 43. Facts vs Assumptions

Clearly distinguish between:

### Confirmed Fact

    EDR detected PowerShell execution.


### Evidence-Based Finding

    The PowerShell process downloaded
    an executable from an external domain.


### Hypothesis

    The activity may have been initiated
    through a phishing email.


This distinction improves report quality.


---

## 44. Documentation and Compliance

Incident records may support:

- Internal audits
- Security assessments
- Regulatory requirements
- Customer reporting
- Legal investigations
- Insurance requirements


Retention requirements depend on organizational policy and applicable regulations.


---

## 45. Sensitive Information

Incident documentation may contain:

- User information
- Internal IP addresses
- System information
- Security configurations
- Vulnerability details
- Evidence
- Business-sensitive information


Access should follow least privilege and organizational data-handling requirements.


---

## 46. Documentation Access Control

Recommended controls:

- Role-based access
- Authentication
- Audit logging
- Encryption
- Secure storage
- Retention policies


Example:

    Analyst
       ↓
    Incident Record
       ↓
    Role-Based Access
       ↓
    Audit Log


---

## 47. Incident Documentation Tools

Possible platforms include:

- SIEM
- SOAR
- Ticketing systems
- Case management platforms
- Knowledge bases
- Secure document repositories
- Collaboration platforms


Examples of data sources:

    Wazuh
    Splunk
    Microsoft Sentinel
    Elastic
    EDR
    Firewall
    IAM
    Cloud Audit Logs


---

## 48. Automated Documentation

SOAR platforms can automatically populate:

- Incident ID
- Detection time
- Source IP
- Destination IP
- Hostname
- Username
- IoCs
- Alert details
- Enrichment results


Example:

    SIEM
      ↓
    Alert
      ↓
    SOAR
      ↓
    Case Creation
      ↓
    Automatic Enrichment
      ↓
    Analyst Review


---

## 49. AI-Assisted Documentation

AI can assist with:

- Incident summarization
- Timeline generation
- Alert correlation
- IoC extraction
- Investigation note organization
- Executive summary drafting
- Report formatting
- Recommendation generation


Example:

    Raw Security Events
          ↓
    AI Processing
          ↓
    Draft Timeline
          ↓
    Analyst Validation
          ↓
    Final Report


AI-generated conclusions should always be reviewed by a qualified analyst.


---

## 50. Documentation Quality Control

Before finalizing a report:

    [ ] Facts verified
    [ ] Timeline verified
    [ ] IoCs verified
    [ ] Severity verified
    [ ] Impact verified
    [ ] Actions documented
    [ ] Root cause reviewed
    [ ] Recommendations defined
    [ ] Sensitive information handled
    [ ] Stakeholders identified
    [ ] Report reviewed


---

## 51. Incident Documentation Metrics

Useful metrics include:

- Documentation completion rate
- Average report completion time
- Missing-field rate
- Investigation note quality
- Evidence completeness
- Closure SLA compliance
- Lessons-learned completion rate


Example:

    Documentation Completion:
    98%

    Evidence Completeness:
    95%

    Closure SLA:
    96%


---

## 52. Professional Incident Report Template

Use this structure for portfolio projects:

    # Incident Report

    ## 1. Incident Information

    Incident ID:
    Date:
    Severity:
    Status:
    Analyst:

    ## 2. Executive Summary

    ## 3. Incident Description

    ## 4. Five Ws

    ## 5. Affected Assets

    ## 6. Timeline

    ## 7. Investigation

    ## 8. Evidence

    ## 9. IoCs

    ## 10. Attack Path

    ## 11. MITRE ATT&CK Mapping

    ## 12. Containment

    ## 13. Eradication

    ## 14. Recovery

    ## 15. Impact

    ## 16. Root Cause

    ## 17. Lessons Learned

    ## 18. Corrective Actions

    ## 19. Preventive Actions

    ## 20. Final Conclusion


---

## 53. Example Incident Documentation

### Incident

    INC-2026-001

### Title

    Suspicious PowerShell Execution

### Severity

    High

### Detection

    Wazuh generated an alert for suspicious
    PowerShell execution.

### Affected Host

    WIN-CLIENT-01

### User

    user01

### Timeline

    10:00 - Suspicious process created
    10:02 - Wazuh generated alert
    10:05 - Analyst acknowledged alert
    10:15 - Investigation started
    10:25 - Endpoint isolated
    10:45 - Malicious file identified
    11:00 - File removed
    11:30 - Endpoint validated


### Findings

    PowerShell executed an encoded command
    and attempted to download an executable.

### Containment

    Endpoint isolated from the network.

### Eradication

    Malicious file and persistence mechanism
    removed.

### Recovery

    Endpoint restored and monitored.

### Conclusion

    Malicious activity was contained and
    no additional affected endpoints were
    identified.


---

## 54. Incident Documentation Workflow

    Alert
      ↓
    Case Creation
      ↓
    Initial Notes
      ↓
    Evidence Collection
      ↓
    Timeline Creation
      ↓
    Investigation
      ↓
    Response Actions
      ↓
    Impact Assessment
      ↓
    Root Cause
      ↓
    Final Report
      ↓
    Lessons Learned
      ↓
    Action Tracking
      ↓
    Closure


---

## 55. Portfolio Project

A strong portfolio project can demonstrate:

### Project

**SOC Incident Documentation & Reporting System**

### Environment

- Wazuh
- Windows
- Sysmon
- Linux
- Python
- Markdown
- GitHub

### Workflow

    Wazuh Alert
       ↓
    Incident Ticket
       ↓
    Evidence Collection
       ↓
    Timeline
       ↓
    IoC Analysis
       ↓
    MITRE Mapping
       ↓
    Incident Report
       ↓
    Lessons Learned


### AI Automation

Use AI to assist with:

- Alert summarization
- Timeline drafting
- IoC extraction
- Report generation
- Executive summary generation


Human validation remains mandatory.


---

## 56. Professional Repository Structure

Example:

    03-Incident-Response/
    │
    ├── README.md
    │
    ├── Playbooks/
    │
    ├── Incident-Reports/
    │
    ├── Evidence/
    │
    ├── Templates/
    │
    ├── Lessons-Learned/
    │
    └── Automation/


---

## 57. Documentation Checklist

    [ ] Incident ID created
    [ ] Severity assigned
    [ ] Incident classified
    [ ] Description written
    [ ] Five Ws completed
    [ ] Timeline created
    [ ] Evidence documented
    [ ] IoCs documented
    [ ] Investigation notes recorded
    [ ] Response actions recorded
    [ ] Containment documented
    [ ] Eradication documented
    [ ] Recovery documented
    [ ] Impact assessed
    [ ] Root cause identified
    [ ] Lessons learned recorded
    [ ] Corrective actions assigned
    [ ] Final report completed
    [ ] Stakeholders notified
    [ ] Incident closed


---

## 58. Key Takeaways

Professional incident documentation should:

- Record facts
- Preserve evidence
- Maintain timelines
- Document decisions
- Track response actions
- Explain business impact
- Identify root causes
- Track corrective actions
- Support future investigations
- Enable continuous improvement


The key principle is:

> **If an important incident response action is not documented, it becomes difficult to prove, reproduce, review, or improve that action.**


---

## 59. Final Incident Documentation Model

    Detect
      ↓
    Record
      ↓
    Investigate
      ↓
    Preserve Evidence
      ↓
    Document Actions
      ↓
    Contain
      ↓
    Eradicate
      ↓
    Recover
      ↓
    Report
      ↓
    Learn
      ↓
    Improve


---

## 60. Conclusion

Incident Response Documentation is a critical component of a mature SOC.

It connects:

    Detection
        +
    Investigation
        +
    Evidence
        +
    Response
        +
    Recovery
        +
    Lessons Learned

into a single auditable record.

A professional security team should not only respond to incidents but also create reliable documentation that explains what happened, why it happened, how it was handled, what impact occurred, and what will be done to prevent recurrence.

The ultimate objective is:

    Document
       ↓
    Understand
       ↓
    Improve
       ↓
    Prevent
       ↓
    Repeat
