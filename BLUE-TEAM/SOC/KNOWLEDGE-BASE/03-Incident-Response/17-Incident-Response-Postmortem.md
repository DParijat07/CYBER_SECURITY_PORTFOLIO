# Incident Response Postmortem

## 1. Introduction

An Incident Response Postmortem is a structured review performed after a cybersecurity incident has been resolved.

The purpose of a postmortem is to understand:

- What happened
- How the incident started
- How it was detected
- How the organization responded
- What worked
- What failed
- What caused the incident
- What impact occurred
- What improvements are required

A postmortem should be **blameless, evidence-based, and improvement-focused**.

The basic model is:

    Incident
       ↓
    Detection
       ↓
    Investigation
       ↓
    Response
       ↓
    Recovery
       ↓
    Postmortem
       ↓
    Root Cause
       ↓
    Improvement Actions
       ↓
    Validation


---

## 2. Objectives

The main objectives of a postmortem are to:

- Reconstruct the incident
- Identify root cause
- Identify contributing factors
- Evaluate security controls
- Evaluate incident response
- Identify detection gaps
- Identify process gaps
- Identify communication gaps
- Identify automation opportunities
- Create corrective actions
- Prevent recurrence


---

## 3. Postmortem vs Incident Report

These documents have different purposes.

### Incident Report

Focuses on:

- What happened
- Evidence
- Timeline
- Investigation
- Response
- Resolution


### Postmortem

Focuses on:

- Why it happened
- What worked
- What failed
- Root cause
- Process weaknesses
- Security control weaknesses
- Improvements


Therefore:

    Incident Report
         ↓
    Documents the Incident

    Postmortem
         ↓
    Learns From the Incident


---

## 4. Why Postmortems Matter

Without a postmortem:

    Incident
       ↓
    Resolved
       ↓
    Closed
       ↓
    Weakness Remains
       ↓
    Similar Incident


With a postmortem:

    Incident
       ↓
    Resolution
       ↓
    Analysis
       ↓
    Root Cause
       ↓
    Corrective Action
       ↓
    Validation
       ↓
    Reduced Recurrence


---

## 5. Blameless Postmortem

A professional postmortem should avoid personal blame.

Instead of:

    "The analyst failed to respond."

Use:

    "The escalation process did not
    provide sufficient notification
    for this alert category."


Instead of:

    "The administrator configured
    the system incorrectly."

Use:

    "The configuration control did not
    prevent the insecure setting."


The goal is to improve systems and processes.


---

## 6. Postmortem Lifecycle

    Incident Resolved
          ↓
    Evidence Consolidated
          ↓
    Timeline Finalized
          ↓
    Stakeholders Identified
          ↓
    Postmortem Meeting
          ↓
    Root Cause Analysis
          ↓
    Gap Analysis
          ↓
    Corrective Actions
          ↓
    Ownership
          ↓
    Validation
          ↓
    Closure


---

## 7. When to Conduct a Postmortem

A formal postmortem may be appropriate for:

- Critical incidents
- High-severity incidents
- Data breaches
- Ransomware
- Major account compromise
- Significant cloud incidents
- Major service disruption
- Repeated incidents
- Incidents that expose major control gaps
- Incidents requiring executive escalation


---

## 8. Postmortem Participants

Depending on the incident:

- SOC Analyst
- SOC Lead
- Incident Response Team
- IT
- Network Team
- Endpoint Team
- Cloud Team
- IAM Team
- Application Team
- System Owner
- Security Management
- Legal
- Compliance
- Privacy
- Business Owner


Only relevant stakeholders should participate.


---

## 9. Postmortem Information

A postmortem should begin with accurate incident information.

Example:

    Incident ID:
    INC-2026-001

    Title:
    Account Compromise

    Severity:
    High

    Date:
    2026-08-20

    Status:
    Resolved

    Affected Assets:
    3

    Business Impact:
    Limited


---

## 10. Executive Summary

The executive summary should be concise.

Example:

    A phishing campaign resulted in the
    compromise of one employee account.

    Security monitoring detected unusual
    authentication activity.

    The account was disabled and active
    sessions were revoked.

    No confirmed data exfiltration was
    identified.

    The primary improvement actions are
    MFA enforcement and enhanced email
    security controls.


---

## 11. Incident Description

Describe the incident in simple terms.

Example:

    The SOC detected suspicious login
    activity associated with a user account.

    Investigation identified authentication
    from an unusual external location.

    Further analysis indicated that the
    user's credentials had likely been
    compromised through phishing.


---

## 12. Incident Scope

Document:

- Affected users
- Affected endpoints
- Servers
- Applications
- Cloud resources
- Accounts
- Data
- Business services


Example:

    Users:
    1

    Endpoints:
    2

    Servers:
    0

    Cloud Accounts:
    1

    Confirmed Data Exposure:
    None


---

## 13. Timeline

A detailed timeline is essential.

Example:

| Time | Event |
|---|---|
| 09:45 | Phishing email received |
| 09:50 | User clicked link |
| 10:05 | Suspicious authentication |
| 10:10 | SIEM generated alert |
| 10:15 | SOC acknowledged |
| 10:25 | Account disabled |
| 10:40 | Sessions revoked |
| 11:00 | Investigation completed |
| 12:00 | Recovery completed |


The timeline should use a consistent time zone.


---

## 14. Detection

Document:

- Detection source
- Detection rule
- Detection time
- Alert severity
- Available telemetry


Example:

    Detection Source:
    Wazuh

    Detection:
    Unusual authentication activity

    Detection Time:
    10:10 UTC


---

## 15. Detection Effectiveness

Ask:

- Was the incident detected?
- How quickly?
- Was the correct alert generated?
- Was the alert severity correct?
- Were relevant logs available?
- Could the incident have been detected earlier?


Example:

    Detection:
    Successful

    Gap:
    Initial phishing email was not detected.


---

## 16. Investigation

Document:

- Investigation methodology
- Data sources
- Tools
- Queries
- Findings
- Evidence


Example:

    Data Sources:

    - Windows Security Logs
    - Sysmon
    - Wazuh
    - Firewall Logs
    - Authentication Logs


---

## 17. Investigation Findings

Example:

    Findings:

    1. User credentials were used from
       an unusual external IP.

    2. The account had no MFA enabled.

    3. No evidence of privilege escalation
       was identified.

    4. No confirmed data exfiltration
       was identified.


---

## 18. Root Cause

Root cause should explain why the incident occurred.

Example:

    Root Cause:

    User credentials were compromised
    through a phishing attack.


The root cause should be supported by evidence.


---

## 19. Contributing Factors

Possible contributing factors:

- MFA not enabled
- Weak email filtering
- Excessive privileges
- Missing detection
- Incomplete logging
- Poor segmentation
- Outdated software
- Lack of user awareness


Example:

    Root Cause:
    Credential theft

    Contributing Factors:
    - MFA not enforced
    - Email filtering gap
    - Excessive account privileges


---

## 20. Five Whys Analysis

Use the Five Whys method.

### Why was the account compromised?

Credentials were stolen.

### Why were credentials stolen?

The user interacted with a phishing page.

### Why did the phishing email reach the user?

Email filtering did not identify it.

### Why did filtering fail?

The domain was newly registered and had limited reputation data.

### Why was there no additional control?

Additional URL protection was not enabled.


This leads to actionable improvements.


---

## 21. Fishbone Analysis

Potential root-cause categories:

    People
       +
    Process
       +
    Technology
       +
    Configuration
       +
    Environment
       ↓
    Incident


Example:

    People:
    User interacted with phishing content

    Process:
    Delayed credential response

    Technology:
    Email filtering gap

    Configuration:
    MFA not enabled


---

## 22. What Went Well

Document successful elements.

Example:

- SIEM generated an alert
- Analyst responded quickly
- Account was disabled
- Sessions were revoked
- Logs were available
- Communication was effective


This identifies controls that should be preserved.


---

## 23. What Did Not Go Well

Document weaknesses.

Example:

- Phishing email bypassed filtering
- MFA was not enabled
- Initial escalation was delayed
- No automated account disablement existed
- Playbook lacked a cloud-account branch


---

## 24. Detection Gaps

Identify what was not detected.

Example:

| Activity | Detection |
|---|---|
| Suspicious Login | Yes |
| Phishing Email | No |
| Credential Theft | Partial |
| Session Hijacking | No |
| Data Exfiltration | Yes |


This provides a detection engineering roadmap.


---

## 25. Logging Gaps

Review telemetry.

Example:

    Available:
    - Authentication logs
    - Windows logs
    - Firewall logs

    Missing:
    - Detailed cloud session logs


Missing telemetry can significantly affect investigation quality.


---

## 26. Security Control Review

Review controls involved in the incident.

Example:

| Control | Result |
|---|---|
| MFA | Missing |
| EDR | Effective |
| SIEM | Effective |
| Email Filtering | Ineffective |
| IAM | Partially Effective |


---

## 27. Process Review

Review the response process.

Questions:

- Was the correct playbook used?
- Was escalation timely?
- Were responsibilities clear?
- Were approvals delayed?
- Were response procedures accurate?


---

## 28. Communication Review

Evaluate:

- Initial notification
- Escalation
- Stakeholder communication
- Management updates
- Technical coordination
- Final reporting


Example:

    Strength:
    SOC → IT escalation was fast.

    Gap:
    Management notification was delayed.


---

## 29. Response Review

Evaluate:

    Detection
       ↓
    Investigation
       ↓
    Containment
       ↓
    Eradication
       ↓
    Recovery


For each phase ask:

    What worked?
    What failed?
    Why?
    What should change?


---

## 30. Containment Review

Questions:

- How quickly was containment started?
- Was the correct system contained?
- Did containment prevent further activity?
- Was business impact minimized?


Example:

    Detection:
    10:10

    Containment:
    10:25

    Containment Time:
    15 minutes


---

## 31. Eradication Review

Evaluate:

- Malware removal
- Persistence removal
- Credential reset
- Vulnerability remediation
- Unauthorized account removal


Example:

    Compromised Account
          ↓
    Disable
          ↓
    Credential Reset
          ↓
    Session Revocation
          ↓
    Re-enable After Validation


---

## 32. Recovery Review

Evaluate:

- System restoration
- Service availability
- Backup quality
- Security validation
- Post-recovery monitoring


Example:

    System Restored
         ↓
    Security Validation
         ↓
    Monitoring
         ↓
    Return to Service


---

## 33. Metrics Review

Include relevant metrics.

Example:

    MTTD:
    5 minutes

    MTTA:
    3 minutes

    MTTC:
    15 minutes

    MTTR:
    90 minutes


Compare actual performance against organizational targets.


---

## 34. Business Impact

Document:

- Systems affected
- Users affected
- Downtime
- Data impact
- Service impact
- Financial impact where known


Example:

    Affected Users:
    1

    Downtime:
    30 minutes

    Confirmed Data Loss:
    None

    Business Impact:
    Low


---

## 35. Risk Impact

Assess whether the incident changed organizational risk.

Example:

    Before Incident:
    Medium Risk

    After Incident:
    High Risk

    Reason:
    Identity control weakness identified.


Risk should be reassessed after corrective actions.


---

## 36. Corrective Actions

Create specific actions.

Example:

| Action | Owner | Priority |
|---|---|---|
| Enable MFA | IAM | Critical |
| Improve email filtering | Security | High |
| Update playbook | IR | High |
| Add cloud logging | Cloud Team | High |
| Review privileges | IAM | Medium |


---

## 37. Preventive Actions

Preventive actions should reduce recurrence.

Examples:

- MFA enforcement
- Security awareness training
- Email filtering improvement
- Least privilege
- Network segmentation
- Better monitoring
- Improved patching
- Detection engineering


---

## 38. Action Ownership

Every action should have:

- Owner
- Priority
- Deadline
- Status
- Validation method


Example:

    Action:
    Enable MFA

    Owner:
    IAM

    Priority:
    Critical

    Deadline:
    14 days

    Status:
    In Progress


---

## 39. Action Validation

Do not close an action simply because it was implemented.

Use:

    Action
       ↓
    Implementation
       ↓
    Testing
       ↓
    Validation
       ↓
    Evidence
       ↓
    Closure


Example:

    MFA Enabled
       ↓
    Test Account
       ↓
    Authentication Test
       ↓
    MFA Challenge Confirmed
       ↓
    Action Validated


---

## 40. Detection Improvement

A postmortem may result in new detection rules.

Example:

    Detection Gap
         ↓
    New Detection Rule
         ↓
    Controlled Test
         ↓
    Alert
         ↓
    SOC Investigation
         ↓
    Detection Validated


---

## 41. Playbook Improvement

Example:

    Incident
       ↓
    Missing Response Step
       ↓
    Playbook Updated
       ↓
    Analyst Training
       ↓
    Tabletop Exercise
       ↓
    Validation


---

## 42. Automation Opportunities

Identify repetitive manual tasks.

Examples:

- Account disabling
- IoC enrichment
- Ticket creation
- Stakeholder notification
- Endpoint isolation
- Evidence collection
- Report generation


Example:

    Suspicious Account
          ↓
    Detection
          ↓
    SOAR
          ↓
    Enrichment
          ↓
    Approval
          ↓
    Account Disablement


---

## 43. AI-Assisted Postmortem

AI can assist with:

- Timeline summarization
- Incident comparison
- Root-cause hypothesis generation
- Pattern detection
- Gap identification
- Recommendation drafting
- Executive summary generation


Example:

    Historical Incidents
          ↓
    AI Analysis
          ↓
    Recurring Weaknesses
          ↓
    Analyst Validation
          ↓
    Improvement Plan


AI-generated findings should be validated against evidence.


---

## 44. Recurrence Analysis

Compare the incident with previous incidents.

Example:

    Incident 1:
    Phishing

    Incident 2:
    Phishing

    Incident 3:
    Phishing

    Pattern:
    Repeated Email Security Weakness


This suggests that previous corrective actions may have been insufficient.


---

## 45. Knowledge Base Updates

Update:

- Detection rules
- Playbooks
- IoC lists
- Investigation queries
- Threat intelligence
- Security documentation
- Training material


Lessons should become reusable organizational knowledge.


---

## 46. MITRE ATT&CK Mapping

Map observed techniques.

Example:

| Activity | ATT&CK |
|---|---|
| Phishing | T1566 |
| Valid Accounts | T1078 |
| PowerShell | T1059.001 |
| Account Discovery | T1087 |


Then evaluate detection coverage for each technique.


---

## 47. Postmortem Action Priority

A simple prioritization model:

### Critical

Immediate risk reduction.

### High

Significant security improvement.

### Medium

Important improvement.

### Low

Long-term optimization.


Prioritization should consider:

    Risk
      +
    Impact
      +
    Likelihood
      +
    Cost
      +
    Effort


---

## 48. Postmortem Report Structure

A professional postmortem can use:

    # Incident Response Postmortem

    ## 1. Executive Summary

    ## 2. Incident Overview

    ## 3. Scope

    ## 4. Timeline

    ## 5. Detection

    ## 6. Investigation

    ## 7. Findings

    ## 8. Root Cause

    ## 9. Contributing Factors

    ## 10. What Went Well

    ## 11. What Did Not Go Well

    ## 12. Detection Gaps

    ## 13. Control Gaps

    ## 14. Communication Review

    ## 15. Metrics

    ## 16. Business Impact

    ## 17. Corrective Actions

    ## 18. Preventive Actions

    ## 19. Validation Plan

    ## 20. Lessons Learned

    ## 21. Final Conclusion


---

## 49. Example Postmortem

### Incident

    INC-2026-001

### Title

    Phishing-Based Account Compromise

### Severity

    High


### Summary

    An employee account was compromised
    following a phishing attack.

    Suspicious authentication activity
    was detected by the SIEM.

    The account was disabled and active
    sessions were revoked.


### Root Cause

    Credential theft through phishing.


### Contributing Factors

    - MFA not enabled
    - Email filtering gap
    - Excessive privileges


### What Went Well

    - SIEM detected suspicious authentication
    - SOC responded quickly
    - Account was disabled
    - Investigation logs were available


### What Did Not Go Well

    - Phishing email bypassed controls
    - MFA was not enabled
    - Some cloud telemetry was unavailable


### Corrective Actions

    - Enable MFA
    - Improve email filtering
    - Reduce account privileges
    - Enable additional cloud logging
    - Update phishing response playbook


---

## 50. Postmortem Metrics

Example:

| Metric | Result |
|---|---:|
| MTTD | 5 min |
| MTTA | 3 min |
| MTTC | 15 min |
| MTTR | 90 min |
| Affected Users | 1 |
| Affected Endpoints | 2 |
| Confirmed Data Loss | 0 |
| SLA | Met |


---

## 51. Postmortem Checklist

    [ ] Incident resolved
    [ ] Evidence preserved
    [ ] Timeline finalized
    [ ] Scope confirmed
    [ ] Root cause identified
    [ ] Contributing factors identified
    [ ] Detection reviewed
    [ ] Investigation reviewed
    [ ] Containment reviewed
    [ ] Eradication reviewed
    [ ] Recovery reviewed
    [ ] Communication reviewed
    [ ] Metrics calculated
    [ ] Detection gaps identified
    [ ] Control gaps identified
    [ ] Corrective actions created
    [ ] Owners assigned
    [ ] Deadlines assigned
    [ ] Validation plan created
    [ ] Playbooks updated
    [ ] Knowledge base updated
    [ ] Postmortem approved
    [ ] Actions tracked to completion


---

## 52. Professional Postmortem Workflow

    Incident
       ↓
    Resolve
       ↓
    Preserve Evidence
       ↓
    Reconstruct Timeline
       ↓
    Analyze Root Cause
       ↓
    Identify Gaps
       ↓
    Create Actions
       ↓
    Assign Owners
       ↓
    Implement
       ↓
    Validate
       ↓
    Monitor
       ↓
    Close


---

## 53. Portfolio Project

### Project

**SOC Incident Postmortem & Root Cause Analysis**

### Environment

- Wazuh
- Windows
- Sysmon
- Kali Linux
- Python
- GitHub
- Markdown


### Workflow

    Simulated Attack
          ↓
    Wazuh Detection
          ↓
    Investigation
          ↓
    Incident Response
          ↓
    Incident Report
          ↓
    Postmortem
          ↓
    Root Cause Analysis
          ↓
    Detection Gap Analysis
          ↓
    Corrective Actions
          ↓
    Retest


### AI Automation

AI can assist with:

- Timeline summarization
- Incident comparison
- Root cause analysis support
- Gap identification
- Postmortem drafting
- Executive summaries
- Improvement recommendations


Human validation remains mandatory.


---

## 54. Professional Repository Structure

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
    ├── Metrics/
    │
    ├── Postmortems/
    │
    └── Automation/


---

## 55. Key Takeaways

A professional postmortem should:

- Be blameless
- Be evidence-based
- Reconstruct the incident
- Identify root cause
- Identify contributing factors
- Evaluate detection
- Evaluate response
- Evaluate security controls
- Identify gaps
- Create measurable actions
- Assign ownership
- Validate improvements
- Reduce recurrence


The key principle is:

> **A postmortem is successful when the organization becomes measurably better because of what it learned from the incident.**


---

## 56. Final Postmortem Model

    Incident
       ↓
    Understand
       ↓
    Analyze
       ↓
    Identify Root Cause
       ↓
    Identify Gaps
       ↓
    Create Actions
       ↓
    Implement
       ↓
    Validate
       ↓
    Improve
       ↓
    Monitor


---

## 57. Conclusion

Incident Response Postmortems transform completed incidents into long-term security improvements.

A mature SOC should not stop when the threat has been contained.

It should ask:

> What happened?

> Why did it happen?

> What worked?

> What failed?

> What should change?

> How will we prove that the change worked?

The ultimate objective is:

    Incident
       ↓
    Analysis
       ↓
    Learning
       ↓
    Improvement
       ↓
    Validation
       ↓
    Stronger Security
