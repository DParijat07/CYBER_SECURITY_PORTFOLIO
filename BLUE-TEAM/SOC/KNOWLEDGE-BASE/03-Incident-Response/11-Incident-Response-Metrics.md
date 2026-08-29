# Incident Response Metrics

## 1. Introduction

Incident Response Metrics are measurable indicators used to evaluate the effectiveness, efficiency, and maturity of an organization's incident response capability.

Metrics help security teams understand:

- How quickly incidents are detected
- How quickly analysts respond
- How quickly threats are contained
- How long recovery takes
- How effective security controls are
- Where response bottlenecks exist
- Whether security improvements are working

The basic model is:

    Security Event
          ↓
       Detection
          ↓
        Triage
          ↓
       Response
          ↓
      Containment
          ↓
       Recovery
          ↓
      Measurement
          ↓
      Improvement


---

## 2. Objectives of Incident Response Metrics

The main objectives are to:

- Measure SOC performance
- Identify response delays
- Measure incident severity
- Evaluate detection capabilities
- Evaluate containment effectiveness
- Measure recovery performance
- Identify recurring problems
- Support management decisions
- Improve security controls
- Demonstrate security maturity


---

## 3. Why Metrics Matter

Without metrics, incident response performance is difficult to measure.

Example:

    "Our SOC responds quickly."

This is subjective.

A measurable statement is:

    "The SOC reduced average MTTR
    from 90 minutes to 45 minutes."


Metrics turn assumptions into measurable evidence.


---

## 4. Metric Categories

Incident response metrics can be divided into:

### Detection Metrics

Measure how quickly threats are identified.

### Response Metrics

Measure how quickly analysts react.

### Containment Metrics

Measure how quickly threats are controlled.

### Recovery Metrics

Measure how quickly normal operations are restored.

### Quality Metrics

Measure the effectiveness of investigations.

### Business Metrics

Measure organizational impact.

### Improvement Metrics

Measure whether corrective actions work.


---

## 5. Key Incident Response Metrics

Common metrics include:

- MTTD
- MTTA
- MTTC
- MTTR
- MTTI
- Incident Volume
- False Positive Rate
- Escalation Rate
- SLA Compliance
- Detection Coverage
- Automation Rate
- Recurrence Rate
- Recovery Time


---

## 6. Mean Time to Detect (MTTD)

MTTD measures the average time between the beginning of malicious activity and its detection.

Formula:

    MTTD =
    Total Detection Time
    --------------------
    Number of Incidents


Example:

    Incident 1 = 10 minutes
    Incident 2 = 20 minutes
    Incident 3 = 30 minutes

    MTTD = (10 + 20 + 30) / 3

    MTTD = 20 minutes


Lower MTTD generally indicates faster detection.


---

## 7. Mean Time to Acknowledge (MTTA)

MTTA measures the average time between alert generation and analyst acknowledgment.

Formula:

    MTTA =
    Total Acknowledgment Time
    -------------------------
    Number of Alerts


Example:

    Alert 1 = 2 minutes
    Alert 2 = 4 minutes
    Alert 3 = 6 minutes

    MTTA = 4 minutes


A high MTTA may indicate:

- Alert overload
- Staffing problems
- Poor prioritization
- Notification issues


---

## 8. Mean Time to Investigate (MTTI)

MTTI measures the average time required to investigate an incident.

Formula:

    MTTI =
    Total Investigation Time
    ------------------------
    Number of Incidents


Example:

    Investigation 1 = 20 minutes
    Investigation 2 = 40 minutes
    Investigation 3 = 30 minutes

    MTTI = 30 minutes


---

## 9. Mean Time to Contain (MTTC)

MTTC measures the average time required to contain an incident.

Formula:

    MTTC =
    Total Containment Time
    ----------------------
    Number of Incidents


Example:

    Endpoint 1 = 15 minutes
    Endpoint 2 = 30 minutes
    Endpoint 3 = 45 minutes

    MTTC = 30 minutes


Lower MTTC generally indicates faster containment.


---

## 10. Mean Time to Recover

Mean Time to Recover measures the average time required to restore affected systems or services.

Formula:

    MTTR-Recovery =
    Total Recovery Time
    -------------------
    Number of Incidents


Example:

    Recovery 1 = 2 hours
    Recovery 2 = 4 hours
    Recovery 3 = 3 hours

    Average = 3 hours


---

## 11. Mean Time to Respond

MTTR is sometimes used as Mean Time to Respond.

However, organizations may define MTTR differently.

Possible definitions include:

- Mean Time to Respond
- Mean Time to Remediate
- Mean Time to Recover
- Mean Time to Resolve


Therefore, organizations should clearly document the exact definition used.


---

## 12. MTTR

A common security definition is:

    MTTR =
    Time from incident identification
    to incident resolution


Example:

    Detection = 10:00
    Resolution = 11:30

    MTTR = 90 minutes


Lower MTTR generally indicates faster incident resolution.


---

## 13. MTTI vs MTTD vs MTTA vs MTTC

These metrics measure different stages.

| Metric | Measures |
|---|---|
| MTTD | Detection speed |
| MTTA | Alert acknowledgment |
| MTTI | Investigation speed |
| MTTC | Containment speed |
| MTTR | Resolution/recovery speed |


Example:

    Attack
      ↓
    MTTD
      ↓
    MTTA
      ↓
    MTTI
      ↓
    MTTC
      ↓
    MTTR


---

## 14. Incident Volume

Incident volume measures the number of incidents handled during a period.

Example:

    January = 120 incidents
    February = 150 incidents
    March = 100 incidents


High incident volume may indicate:

- Increased attacks
- Poor detection tuning
- More visibility
- Increased false positives
- Security control changes


Incident volume alone does not indicate SOC performance.


---

## 15. Alert Volume

Alert volume measures the number of security alerts generated.

Example:

    Daily Alerts = 10,000
    True Security Incidents = 100


A high alert volume can create analyst fatigue.

Therefore, alert volume should be analyzed alongside alert quality.


---

## 16. False Positive Rate

False Positive Rate measures the percentage of alerts incorrectly classified as malicious or suspicious.

Formula:

    False Positive Rate =
    False Positive Alerts
    ---------------------
    Total Alerts
    × 100


Example:

    Total Alerts = 1,000
    False Positives = 700

    False Positive Rate =
    700 / 1,000 × 100

    = 70%


A high false positive rate can reduce SOC efficiency.


---

## 17. True Positive Rate

True Positive Rate measures how many actual malicious events are correctly detected.

Formula:

    True Positive Rate =
    True Positive Alerts
    --------------------
    Actual Malicious Events
    × 100


A higher rate generally indicates better detection effectiveness.


---

## 18. False Negative Rate

False Negative Rate measures malicious activity that was not detected.

Formula:

    False Negative Rate =
    Missed Malicious Events
    -----------------------
    Actual Malicious Events
    × 100


False negatives can be especially dangerous because threats may remain undetected.


---

## 19. Precision

Precision measures how many alerts classified as positive were actually positive.

Formula:

    Precision =
    True Positives
    ------------------------
    True Positives + False Positives


High precision generally means alerts are more actionable.


---

## 20. Recall

Recall measures how many actual malicious events were detected.

Formula:

    Recall =
    True Positives
    ------------------------
    True Positives + False Negatives


High recall generally means fewer malicious events are missed.


---

## 21. Precision vs Recall

Security detection often requires balancing precision and recall.

    High Precision
        ↓
    Fewer False Positives

    High Recall
        ↓
    Fewer Missed Threats


Example:

    Detection Rule A
    Precision = 95%
    Recall = 60%

    Detection Rule B
    Precision = 75%
    Recall = 90%


The appropriate balance depends on the use case and risk.


---

## 22. Alert-to-Incident Conversion Rate

This measures how many alerts become confirmed incidents.

Formula:

    Conversion Rate =
    Confirmed Incidents
    -------------------
    Total Alerts
    × 100


Example:

    Alerts = 5,000
    Incidents = 100

    Conversion Rate = 2%


A very low conversion rate may indicate excessive alert noise.


---

## 23. Escalation Rate

Escalation Rate measures the percentage of alerts or incidents escalated to higher-level analysts.

Formula:

    Escalation Rate =
    Escalated Cases
    ----------------
    Total Cases
    × 100


Example:

    Total Cases = 500
    Escalated = 100

    Escalation Rate = 20%


---

## 24. SLA Compliance

SLA compliance measures whether incidents were handled within defined service-level targets.

Formula:

    SLA Compliance =
    Cases Within SLA
    ----------------
    Total Cases
    × 100


Example:

    Total Incidents = 100
    Within SLA = 95

    SLA Compliance = 95%


---

## 25. SLA Breach Rate

Formula:

    SLA Breach Rate =
    SLA Breaches
    -------------
    Total Cases
    × 100


Example:

    100 incidents
    5 SLA breaches

    SLA Breach Rate = 5%


A breach should be investigated rather than simply recorded.


---

## 26. Incident Severity Distribution

Track incidents by severity.

Example:

| Severity | Count |
|---|---:|
| Critical | 3 |
| High | 15 |
| Medium | 70 |
| Low | 120 |


This helps understand the organization's threat landscape.


---

## 27. Incident Category Distribution

Track incident types.

Example:

| Category | Incidents |
|---|---:|
| Phishing | 80 |
| Malware | 30 |
| Account Compromise | 20 |
| Vulnerability Exploitation | 10 |
| Insider Threat | 5 |


This can help prioritize security investments.


---

## 28. Recurrence Rate

Recurrence Rate measures how often similar incidents happen again.

Formula:

    Recurrence Rate =
    Repeated Incidents
    ------------------
    Total Incidents
    × 100


A high recurrence rate may indicate ineffective remediation.


---

## 29. Repeat Incident Analysis

Example:

    Phishing Incident
          ↓
    Remediation
          ↓
    Same Campaign
          ↓
    Repeated Incident
          ↓
    Root Cause Not Fully Addressed


The goal should be to reduce recurrence over time.


---

## 30. Containment Success Rate

Measures how often containment actions successfully stop malicious activity.

Formula:

    Containment Success Rate =
    Successful Containments
    ------------------------
    Total Containment Attempts
    × 100


Example:

    95 successful
    100 attempts

    = 95%


---

## 31. Automation Rate

Automation Rate measures the percentage of response actions performed automatically.

Formula:

    Automation Rate =
    Automated Actions
    ------------------
    Total Actions
    × 100


Example:

    800 automated actions
    1,000 total actions

    = 80%


Automation can reduce repetitive analyst workload.


---

## 32. Playbook Success Rate

Measures how effectively incident response playbooks work.

Possible measurement:

    Successful Playbook Executions
    -------------------------------
    Total Playbook Executions
    × 100


A low rate may indicate:

- Poor documentation
- Missing steps
- Incorrect assumptions
- Tool integration problems


---

## 33. Detection Coverage

Detection coverage measures how much of the relevant attack surface is monitored.

Coverage can include:

- Endpoints
- Servers
- Network devices
- Cloud
- Identity
- Applications
- Databases


Example:

    90% of critical endpoints
    have EDR telemetry.


---

## 34. MITRE ATT&CK Detection Coverage

Organizations can map detections to MITRE ATT&CK techniques.

Example:

| Technique | Detection |
|---|---|
| T1059 | PowerShell Monitoring |
| T1078 | Account Monitoring |
| T1087 | Account Discovery |
| T1021 | Remote Services |


This helps identify detection gaps.


---

## 35. Mean Time Between Incidents

Mean Time Between Incidents measures the average time between incidents.

Formula:

    MTBI =
    Observation Period
    ------------------
    Number of Incidents


Example:

    Observation Period = 90 days
    Incidents = 9

    MTBI = 10 days


Increasing MTBI may indicate reduced incident frequency.


---

## 36. Mean Time Between Failures

This can be used for security controls or systems.

Example:

    EDR Failure
       ↓
    Recovery
       ↓
    Another Failure


Tracking control reliability helps identify technology problems.


---

## 37. Analyst Workload

Useful workload metrics include:

- Alerts per analyst
- Cases per analyst
- Incidents per shift
- Average investigation time
- Open case count
- Backlog size


Example:

    Analyst
       ↓
    500 Alerts
       ↓
    50 Cases
       ↓
    5 Confirmed Incidents


---

## 38. Case Backlog

Case backlog measures unresolved cases.

Example:

    Opening Backlog = 100
    New Cases = 300
    Closed Cases = 350

    Closing Backlog = 50


A growing backlog may indicate capacity problems.


---

## 39. Mean Age of Open Cases

Measures how long unresolved cases remain open.

Example:

    Case 1 = 2 days
    Case 2 = 5 days
    Case 3 = 3 days

    Average Age = 3.3 days


Older cases may require escalation or review.


---

## 40. Investigation Quality Metrics

Quality can be measured using:

- Evidence completeness
- Correct severity
- Correct classification
- Correct escalation
- Required documentation
- Root cause identification


Example:

    Investigation Quality Score = 92%


Quality metrics should not encourage analysts to close cases prematurely.


---

## 41. Incident Documentation Completeness

Measure whether required incident fields are completed.

Possible fields:

- Incident ID
- Severity
- Timestamp
- Affected assets
- IoCs
- Timeline
- Actions
- Root cause
- Resolution


---

## 42. Communication Metrics

Possible metrics include:

- Time to notify
- Notification SLA compliance
- Update frequency
- Communication completeness
- Stakeholder satisfaction


Example:

    Critical Incident Notification SLA:
    15 minutes

    Actual:
    12 minutes

    Result:
    SLA Met


---

## 43. Recovery Metrics

Recovery metrics include:

- Recovery time
- Service restoration rate
- Backup recovery success
- System validation success
- Recovery SLA compliance


Example:

    RTO = 4 hours
    Actual Recovery = 3 hours

    Result = RTO achieved


---

## 44. RTO

Recovery Time Objective defines the maximum acceptable time to restore a service after disruption.

Example:

    RTO = 4 hours


If recovery takes 6 hours:

    RTO Breach = Yes


---

## 45. RPO

Recovery Point Objective defines the maximum acceptable amount of data loss measured in time.

Example:

    RPO = 1 hour


This means the organization should be able to recover data to a point no more than approximately one hour before the disruption, depending on the recovery design.


---

## 46. Business Impact Metrics

Possible metrics:

- Downtime
- Revenue loss
- Customers affected
- Employees affected
- Services unavailable
- Data affected
- Recovery cost


Security metrics should connect technical performance with business impact.


---

## 47. Cost per Incident

Organizations can estimate:

    Cost per Incident =
    Investigation Cost
    +
    Response Cost
    +
    Recovery Cost
    +
    Business Loss


This can help management evaluate security investments.


---

## 48. Security Improvement Metrics

After corrective actions, compare performance.

Example:

### Before

    MTTD = 30 min
    MTTC = 60 min
    False Positive Rate = 70%


### After

    MTTD = 15 min
    MTTC = 35 min
    False Positive Rate = 45%


This demonstrates measurable improvement.


---

## 49. KPI vs KRI

### KPI

Key Performance Indicator measures performance.

Example:

    MTTR
    SLA Compliance
    Automation Rate


### KRI

Key Risk Indicator measures risk exposure.

Example:

    Critical Vulnerabilities
    Unsupported Systems
    Unprotected Accounts


Both are useful for security management.


---

## 50. Leading vs Lagging Indicators

### Leading Indicators

Help predict future performance.

Examples:

- Patch compliance
- MFA coverage
- EDR coverage
- Detection coverage
- Security training completion


### Lagging Indicators

Measure outcomes after events.

Examples:

- Number of incidents
- Recovery time
- Data loss
- Business impact


A mature program uses both.


---

## 51. Dashboard Design

A SOC dashboard may contain:

    ┌─────────────────────────────┐
    │ INCIDENT RESPONSE DASHBOARD │
    ├─────────────────────────────┤
    │ MTTD          15 min        │
    │ MTTA           4 min        │
    │ MTTC          30 min        │
    │ MTTR          90 min        │
    │ SLA           95%           │
    │ FP Rate       45%           │
    │ Open Cases    32            │
    └─────────────────────────────┘


---

## 52. SOC Dashboard Metrics

Useful dashboard widgets include:

- Alerts today
- Confirmed incidents
- Critical incidents
- MTTD
- MTTA
- MTTC
- MTTR
- SLA compliance
- False positive rate
- Open cases
- Incident trends
- Top incident categories
- Top affected assets


---

## 53. Management Dashboard

Executive dashboards should focus on:

- Major incidents
- Business impact
- Response performance
- Risk trends
- SLA compliance
- Critical vulnerabilities
- Security improvement
- Resource requirements


Avoid overwhelming executives with raw technical telemetry.


---

## 54. Metric Correlation

Metrics should be analyzed together.

Example:

    Alert Volume ↑
         +
    False Positive Rate ↑
         ↓
    Analyst Workload ↑
         ↓
    MTTA ↑
         ↓
    Detection Response ↓


This provides more useful insight than looking at one metric alone.


---

## 55. Metric Manipulation Risk

Metrics can be misleading if optimized incorrectly.

Example:

    Goal:
    Reduce MTTR


If analysts close cases too quickly:

    MTTR ↓
    Quality ↓


Therefore, metrics should be balanced with quality and risk measures.


---

## 56. Balanced SOC Scorecard

A balanced scorecard may include:

### Speed

- MTTD
- MTTA
- MTTC
- MTTR

### Quality

- False Positive Rate
- Investigation Quality
- Detection Accuracy

### Coverage

- Endpoint Coverage
- Log Coverage
- Detection Coverage

### Efficiency

- Automation Rate
- Analyst Workload

### Risk

- Recurrence Rate
- Critical Incident Count

### Business

- SLA Compliance
- Downtime
- Business Impact


---

## 57. Metrics Review Frequency

Metrics can be reviewed at different intervals.

### Daily

- Alerts
- Critical incidents
- Open cases

### Weekly

- MTTA
- MTTR
- SLA
- Backlog

### Monthly

- Trends
- Incident categories
- Detection performance
- Recurrence

### Quarterly

- Security maturity
- Control effectiveness
- Strategic improvements


---

## 58. Metrics Collection Sources

Metrics can be collected from:

- SIEM
- SOAR
- EDR
- Ticketing system
- Case management platform
- Vulnerability management platform
- IAM
- Cloud platforms
- Incident response reports


---

## 59. Automated Metrics Collection

Example:

    SIEM
      ↓
    SOAR
      ↓
    Case Management
      ↓
    Metrics Database
      ↓
    Dashboard


Automation reduces manual reporting.


---

## 60. AI-Assisted Metrics Analysis

AI can assist with:

- Trend identification
- Anomaly detection
- Incident clustering
- Performance analysis
- Root cause pattern identification
- Executive summary generation
- Predictive workload analysis


Example:

    Historical SOC Metrics
          ↓
    AI Analysis
          ↓
    Trend Detection
          ↓
    Analyst Validation
          ↓
    Management Insight


AI should support decision-making rather than replace security judgment.


---

## 61. Portfolio Project Example

A strong cybersecurity portfolio project can demonstrate:

### Project

**SOC Incident Response Metrics Dashboard**

### Environment

- Wazuh
- Sysmon
- Windows
- Linux
- Python
- Dashboarding Platform

### Metrics

- MTTD
- MTTA
- MTTC
- MTTR
- False Positive Rate
- Incident Volume
- SLA Compliance
- Automation Rate


### Workflow

    Wazuh Alerts
          ↓
    Incident Tickets
          ↓
    Timestamp Extraction
          ↓
    Python Processing
          ↓
    Metric Calculation
          ↓
    Dashboard
          ↓
    Performance Analysis


---

## 62. Example Dataset

| Incident | Detect | Acknowledge | Contain | Resolve |
|---|---|---|---|---|
| INC-001 | 10:00 | 10:05 | 10:25 | 11:00 |
| INC-002 | 11:00 | 11:03 | 11:20 | 12:10 |
| INC-003 | 13:00 | 13:10 | 13:40 | 15:00 |


From this data, calculate:

- MTTD
- MTTA
- MTTC
- MTTR


This can become a practical SOC analytics project.


---

## 63. Example KPI Report

    Reporting Period:
    August 2026

    Total Incidents:
    120

    Critical:
    3

    High:
    18

    Medium:
    65

    Low:
    34

    MTTD:
    14 minutes

    MTTA:
    4 minutes

    MTTC:
    28 minutes

    MTTR:
    82 minutes

    SLA Compliance:
    96%

    False Positive Rate:
    42%

    Automation Rate:
    68%


---

## 64. Metric Improvement Cycle

The goal is not simply to collect numbers.

Use:

    Measure
       ↓
    Analyze
       ↓
    Identify Weakness
       ↓
    Improve
       ↓
    Measure Again


This creates continuous improvement.


---

## 65. Incident Response Metrics Checklist

    [ ] MTTD defined
    [ ] MTTA defined
    [ ] MTTI defined
    [ ] MTTC defined
    [ ] MTTR defined
    [ ] Incident volume tracked
    [ ] Alert volume tracked
    [ ] False positives tracked
    [ ] False negatives considered
    [ ] SLA compliance tracked
    [ ] Escalation rate tracked
    [ ] Recurrence rate tracked
    [ ] Automation rate tracked
    [ ] Detection coverage tracked
    [ ] Case backlog tracked
    [ ] Recovery metrics tracked
    [ ] Business impact measured
    [ ] Trends reviewed
    [ ] Metrics validated
    [ ] Improvement actions tracked


---

## 66. Professional Metrics Workflow

The complete workflow is:

    Collect Data
        ↓
    Validate Data
        ↓
    Calculate Metrics
        ↓
    Build Dashboard
        ↓
    Analyze Trends
        ↓
    Identify Gaps
        ↓
    Implement Improvements
        ↓
    Measure Again


---

## 67. Key Takeaways

Important incident response metrics include:

- MTTD
- MTTA
- MTTI
- MTTC
- MTTR
- False Positive Rate
- True Positive Rate
- False Negative Rate
- Precision
- Recall
- SLA Compliance
- Automation Rate
- Recurrence Rate
- Detection Coverage
- Recovery Time


Metrics should always be interpreted in context.

A lower number is not automatically better.


---

## 68. Final Incident Response Metrics Model

    Security Events
          ↓
       Detection
          ↓
        Triage
          ↓
      Investigation
          ↓
      Containment
          ↓
        Recovery
          ↓
       Resolution
          ↓
        Metrics
          ↓
      Performance
          ↓
       Analysis
          ↓
      Improvement
          ↓
    Better Response


---

## 69. Conclusion

Incident Response Metrics provide measurable evidence of how effectively a security team detects, investigates, contains, and resolves cybersecurity incidents.

A mature SOC does not only ask:

> "How many incidents did we handle?"

It also asks:

> "How quickly did we detect them, how effectively did we respond, what was the business impact, and are we improving over time?"

The ultimate objective is:

    Measure
       ↓
    Understand
       ↓
    Improve
       ↓
    Validate
       ↓
    Repeat

This turns incident response from a reactive function into a measurable and continuously improving security capability.
