# Incident Response Metrics

## 1. Introduction

Incident Response Metrics are measurable indicators used to evaluate the effectiveness, efficiency, and maturity of an organization's incident response capability.

Metrics help security teams understand:

- How quickly incidents are detected
- How quickly analysts respond
- How efficiently incidents are contained
- How long recovery takes
- How effective security controls are
- Where response bottlenecks exist
- Whether improvements are working

The basic model is:

    Incident Data
         ↓
    Metrics
         ↓
    Analysis
         ↓
    Weakness Identification
         ↓
    Improvement
         ↓
    Validation


---

## 2. Objectives

Incident response metrics should help organizations:

- Measure response performance
- Identify bottlenecks
- Track security improvements
- Measure SOC efficiency
- Evaluate analyst workload
- Improve detection
- Improve containment
- Improve recovery
- Demonstrate security value
- Support management decisions


---

## 3. Why Metrics Matter

Without metrics:

    Incident
       ↓
    Response
       ↓
    "It seemed fast"


With metrics:

    Incident
       ↓
    Detection
       ↓
    Response
       ↓
    Measurement
       ↓
    Evidence
       ↓
    Improvement


Metrics turn security operations into measurable processes.


---

## 4. Metrics Categories

Incident response metrics can be grouped into:

### Detection Metrics

Measure how quickly threats are identified.

### Response Metrics

Measure how quickly the SOC reacts.

### Containment Metrics

Measure how quickly threats are contained.

### Recovery Metrics

Measure restoration and recovery.

### Quality Metrics

Measure alert and investigation quality.

### Efficiency Metrics

Measure analyst and process efficiency.

### Improvement Metrics

Measure long-term security improvement.


---

## 5. Mean Time to Detect

MTTD means:

**Mean Time to Detect**

It measures the average time between the beginning of malicious activity and detection.

Formula:

    MTTD =
    Total Detection Time
    --------------------
    Number of Incidents


Example:

    Incident 1 = 10 min
    Incident 2 = 20 min
    Incident 3 = 15 min

    MTTD =
    (10 + 20 + 15) / 3

    MTTD = 15 minutes


Lower MTTD generally indicates faster detection.


---

## 6. Mean Time to Acknowledge

MTTA means:

**Mean Time to Acknowledge**

It measures how quickly an analyst acknowledges an alert.

Formula:

    MTTA =
    Total Acknowledgement Time
    --------------------------
    Number of Alerts


Example:

    Alert 1 = 2 min
    Alert 2 = 4 min
    Alert 3 = 3 min

    MTTA =
    (2 + 4 + 3) / 3

    MTTA = 3 minutes


---

## 7. Mean Time to Investigate

MTTI measures the average time required to investigate an incident.

Formula:

    MTTI =
    Total Investigation Time
    ------------------------
    Number of Incidents


Example:

    Incident 1 = 20 min
    Incident 2 = 40 min
    Incident 3 = 30 min

    MTTI =
    90 / 3

    MTTI = 30 minutes


---

## 8. Mean Time to Contain

MTTC measures how quickly an incident is contained.

Formula:

    MTTC =
    Total Containment Time
    ----------------------
    Number of Incidents


Example:

    Incident 1 = 10 min
    Incident 2 = 20 min
    Incident 3 = 15 min

    MTTC =
    45 / 3

    MTTC = 15 minutes


---

## 9. Mean Time to Eradicate

MTTE measures how quickly the root threat is removed.

Examples:

- Malware removal
- Persistence removal
- Credential reset
- Attacker account removal
- Vulnerability remediation


Formula:

    MTTE =
    Total Eradication Time
    ----------------------
    Number of Incidents


---

## 10. Mean Time to Recover

MTTR can refer to:

**Mean Time to Recover**

It measures the average time required to restore normal operations after an incident.

Formula:

    MTTR =
    Total Recovery Time
    -------------------
    Number of Incidents


Example:

    Recovery Times:

    60 min
    90 min
    120 min

    MTTR =
    270 / 3

    MTTR = 90 minutes


---

## 11. Important Metric Terminology

Different organizations may use similar abbreviations differently.

For example:

    MTTD
    Mean Time to Detect

    MTTA
    Mean Time to Acknowledge

    MTTI
    Mean Time to Investigate

    MTTC
    Mean Time to Contain

    MTTR
    Mean Time to Respond / Recover / Resolve


Always define the exact meaning used by your organization.


---

## 12. Incident Response Timeline Metrics

A useful incident timeline is:

    Attack Begins
         ↓
    Detection
         ↓
    Acknowledgement
         ↓
    Investigation
         ↓
    Containment
         ↓
    Eradication
         ↓
    Recovery
         ↓
    Closure


Each stage can produce a measurable duration.


---

## 13. Alert Volume

Measure the number of alerts generated.

Example:

    Daily Alerts:
    5,000


Alert volume alone does not indicate SOC effectiveness.

A SOC should also measure:

- True positives
- False positives
- Actionable alerts
- Critical alerts
- Escalated alerts


---

## 14. False Positive Rate

False positives are alerts that appear suspicious but are determined to be benign.

Formula:

    False Positive Rate =
    False Positive Alerts
    ---------------------
    Total Alerts
    × 100


Example:

    False Positives = 2,000
    Total Alerts = 10,000

    FPR =
    2,000 / 10,000 × 100

    FPR = 20%


High false-positive rates can increase analyst workload.


---

## 15. True Positive Rate

True Positive Rate measures the proportion of alerts that correctly identify malicious activity.

Formula:

    TPR =
    True Positive Alerts
    --------------------
    Total Relevant Alerts
    × 100


A high-quality detection system should identify meaningful threats while minimizing unnecessary alerts.


---

## 16. False Negative Rate

False negatives are malicious events that were not detected.

Formula:

    False Negative Rate =
    Missed Malicious Events
    ----------------------
    Total Malicious Events
    × 100


False negatives are particularly important because they represent detection gaps.


---

## 17. Alert-to-Incident Conversion Rate

Measures how many alerts become confirmed incidents.

Formula:

    Alert-to-Incident Rate =
    Confirmed Incidents
    --------------------
    Total Alerts
    × 100


Example:

    Alerts = 10,000

    Confirmed Incidents = 100

    Rate =
    100 / 10,000 × 100

    = 1%


A low rate is not automatically bad.

It may indicate that the SOC is filtering large volumes of benign activity.


---

## 18. Alert Backlog

Alert backlog measures unresolved alerts.

Example:

    Start of Day:
    250 alerts

    New Alerts:
    500

    Resolved:
    600

    End of Day:
    150 alerts


Growing backlog may indicate:

- Staffing problems
- Alert overload
- Poor prioritization
- Inefficient workflows
- Excessive false positives


---

## 19. SLA Compliance

SLA means:

**Service Level Agreement**

Measure whether incidents were handled within defined time targets.

Example:

    Critical Incident SLA:
    Acknowledge within 15 minutes

    Actual:
    10 minutes

    Result:
    SLA Met


Formula:

    SLA Compliance =
    Incidents Meeting SLA
    ---------------------
    Total Applicable Incidents
    × 100


---

## 20. Escalation Rate

Measures how many alerts require escalation.

Formula:

    Escalation Rate =
    Escalated Cases
    ---------------
    Total Cases
    × 100


High escalation rates may indicate:

- Complex incidents
- Insufficient analyst skills
- Poor alert quality
- Inadequate playbooks


The metric must be interpreted in context.


---

## 21. Incident Severity Distribution

Track incidents by severity.

Example:

| Severity | Count |
|---|---:|
| Critical | 2 |
| High | 15 |
| Medium | 60 |
| Low | 120 |


This helps identify risk trends.


---

## 22. Incident Volume Trend

Track incidents over time.

Example:

| Month | Incidents |
|---|---:|
| January | 120 |
| February | 100 |
| March | 90 |
| April | 75 |


A declining trend may indicate successful security improvements.


---

## 23. Recurring Incident Rate

Measures repeated incidents of similar type.

Formula:

    Recurrence Rate =
    Repeat Incidents
    ----------------
    Total Incidents
    × 100


Example:

    Repeat Incidents = 20

    Total Incidents = 100

    Recurrence Rate = 20%


High recurrence may indicate unresolved root causes.


---

## 24. Incident Closure Rate

Measures the percentage of incidents closed within a reporting period.

Formula:

    Closure Rate =
    Closed Incidents
    ----------------
    Total Incidents
    × 100


Example:

    Closed = 95

    Total = 100

    Closure Rate = 95%


---

## 25. Mean Investigation Time

Measures average investigation duration.

Example:

    Incident 1 = 20 min
    Incident 2 = 30 min
    Incident 3 = 40 min

    Average =
    90 / 3

    = 30 minutes


This can help identify investigation complexity.


---

## 26. Automation Rate

Measures how much of the response workflow is automated.

Formula:

    Automation Rate =
    Automated Actions
    ------------------
    Total Eligible Actions
    × 100


Example:

    Automated Actions = 70

    Eligible Actions = 100

    Automation Rate = 70%


---

## 27. AI-Assisted Investigation Rate

If AI-assisted workflows are used, measure how frequently they support investigations.

Example:

    Investigations:
    100

    AI-Assisted:
    60

    AI-Assisted Investigation Rate:
    60%


This metric should measure usage, not automatically imply effectiveness.


---

## 28. AI Recommendation Acceptance Rate

Measure how many AI recommendations are accepted after human review.

Formula:

    Acceptance Rate =
    Accepted Recommendations
    -------------------------
    Reviewed Recommendations
    × 100


Example:

    Reviewed = 100

    Accepted = 75

    Acceptance Rate = 75%


Acceptance should not be treated as proof that AI recommendations are correct.


---

## 29. Mean Time to Enrich

Measures how long it takes to enrich an alert with contextual information.

Examples:

- IP reputation
- Domain information
- Hash reputation
- User context
- Asset context
- Threat intelligence


Automation can significantly reduce enrichment time.


---

## 30. Mean Time to Escalate

Measures how quickly an incident is escalated after meeting escalation criteria.

Formula:

    MTTEsc =
    Total Escalation Time
    ---------------------
    Number of Escalated Incidents


This can reveal communication or workflow delays.


---

## 31. Mean Time to Close

Measures the average time from incident creation to closure.

Formula:

    MTTClose =
    Total Incident Lifecycle Time
    -----------------------------
    Number of Closed Incidents


This provides an overall operational view.


---

## 32. Investigation Quality Metrics

Possible quality indicators:

- Evidence completeness
- Correct classification
- Correct severity
- Correct root cause
- Correct MITRE mapping
- Required documentation completed
- Appropriate escalation


Example:

    Investigation Quality Score:
    92%


Quality should not be measured only by speed.


---

## 33. Evidence Completeness

Measure whether required evidence was collected.

Example:

| Evidence | Collected |
|---|---|
| Authentication Logs | Yes |
| Endpoint Logs | Yes |
| Network Logs | Yes |
| Process Data | Yes |
| Cloud Logs | No |


Missing evidence may reduce investigation confidence.


---

## 34. Playbook Effectiveness

Evaluate whether playbooks help analysts respond effectively.

Possible measurements:

- Playbook usage
- Time saved
- Missing steps
- Analyst feedback
- Successful execution
- Number of playbook updates


Example:

    Playbook:
    Account Compromise

    Analyst Rating:
    4.5 / 5

    Improvement:
    Add cloud session revocation step


---

## 35. Detection Coverage

Measure coverage of relevant attack techniques.

Example:

| Technique | Coverage |
|---|---|
| Phishing | High |
| PowerShell | High |
| Credential Access | Medium |
| Lateral Movement | Low |
| Exfiltration | Medium |


Coverage should be validated through testing.


---

## 36. MITRE ATT&CK Coverage Metrics

A SOC can track:

- Techniques monitored
- Techniques detected
- Techniques tested
- Techniques without coverage


Example:

    Relevant Techniques:
    100

    Detected:
    70

    Tested:
    50

    Detection Coverage:
    70%


Coverage percentage alone does not guarantee detection effectiveness.


---

## 37. Mean Time Between Incidents

MTBI can measure the average time between incidents.

Formula:

    MTBI =
    Total Observation Period
    ------------------------
    Number of Incidents


Example:

    Observation Period:
    90 days

    Incidents:
    10

    MTBI:
    9 days


A higher MTBI may indicate reduced incident frequency, but context is important.


---

## 38. Business Impact Metrics

Measure:

- Downtime
- Number of affected users
- Number of affected systems
- Service disruption
- Data exposure
- Financial impact
- Productivity impact


Example:

    Downtime:
    45 minutes

    Users Affected:
    25

    Services Affected:
    1


---

## 39. Recovery Success Rate

Measures the percentage of recovery activities successfully completed.

Example:

    Successful Recoveries:
    98

    Total Recoveries:
    100

    Recovery Success Rate:
    98%


---

## 40. Backup Recovery Metrics

For incidents involving data or systems, track:

- Recovery Time Objective
- Recovery Point Objective
- Backup restoration time
- Backup success rate
- Restoration test success


### RTO

**Recovery Time Objective**

Maximum acceptable time to restore a service.


### RPO

**Recovery Point Objective**

Maximum acceptable amount of data loss measured in time.


---

## 41. Incident Response Cost

Possible cost categories:

- Analyst time
- Downtime
- Recovery
- External support
- Infrastructure
- Legal
- Compliance
- Business interruption


Cost analysis can support security investment decisions.


---

## 42. Analyst Workload

Measure:

- Alerts per analyst
- Incidents per analyst
- Investigation hours
- Overtime
- Case backlog


Example:

    Analyst:
    150 alerts/day

    Problem:
    High workload

    Improvement:
    Detection tuning + automation


Metrics should support sustainable operations.


---

## 43. Analyst Efficiency

A useful comparison:

    Manual Investigation:
    45 minutes

    Automated Enrichment:
    15 minutes

    Time Saved:
    30 minutes


Automation should reduce repetitive work while maintaining investigation quality.


---

## 44. Metrics Dashboard

A SOC dashboard may include:

    ┌────────────────────────────────┐
    │ INCIDENT RESPONSE DASHBOARD    │
    ├────────────────────────────────┤
    │ MTTD              12 min       │
    │ MTTA               4 min       │
    │ MTTI              25 min       │
    │ MTTC              18 min       │
    │ MTTR              90 min       │
    │ SLA Compliance      96%        │
    │ False Positive      12%        │
    │ Open Incidents       8         │
    │ Recurrence Rate      5%        │
    │ Automation Rate     65%        │
    └────────────────────────────────┘


---

## 45. Metrics Reporting

Metrics should be presented differently to different audiences.

### SOC Analysts

Focus on:

- Alert backlog
- MTTD
- MTTA
- Investigation time
- Detection quality


### SOC Manager

Focus on:

- SLA
- Incident trends
- MTTR
- Workload
- Automation
- Recurrence


### Management

Focus on:

- Risk
- Business impact
- Major incidents
- Trends
- Improvement
- Security investment


---

## 46. Metrics Should Drive Decisions

Use:

    Metric
       ↓
    Trend
       ↓
    Problem
       ↓
    Root Cause
       ↓
    Improvement
       ↓
    Validation


Example:

    MTTD Increasing
         ↓
    Alert Volume Increasing
         ↓
    Detection Noise
         ↓
    Detection Tuning
         ↓
    MTTD Improves


---

## 47. Metrics vs Vanity Metrics

Not every number is useful.

### Vanity Metric

    "We processed 100,000 alerts."


This does not demonstrate security effectiveness.

### Useful Metric

    "False-positive rate decreased
    from 30% to 12%."


Useful metrics should support decisions.


---

## 48. Metric Quality Principles

Good metrics should be:

- Relevant
- Measurable
- Consistent
- Actionable
- Comparable
- Traceable
- Understandable


Avoid metrics that encourage analysts to sacrifice investigation quality for speed.


---

## 49. Metrics and Analyst Behavior

Poorly designed metrics can create bad incentives.

Example:

    Goal:
    Close 100 alerts/day

Potential result:

    Analysts close alerts too quickly.


Better:

    Measure:
    Quality
    +
    SLA
    +
    Accuracy
    +
    Investigation completeness


Metrics should encourage good security outcomes.


---

## 50. Before-and-After Improvement

Example:

### Before

    MTTD:
    30 min

    MTTC:
    60 min

    False Positives:
    25%

    Automation:
    20%


### After

    MTTD:
    12 min

    MTTC:
    25 min

    False Positives:
    10%

    Automation:
    65%


This demonstrates measurable operational improvement.


---

## 51. Continuous Improvement Loop

    Metrics
       ↓
    Analyze
       ↓
    Identify Problem
       ↓
    Root Cause
       ↓
    Improvement
       ↓
    Implement
       ↓
    Test
       ↓
    Measure Again


---

## 52. Metrics Automation

Metrics can be automatically collected from:

- SIEM
- SOAR
- Ticketing system
- EDR
- Case management
- Threat intelligence platforms


Example:

    Wazuh
       ↓
    Incident Data
       ↓
    Python
       ↓
    KPI Calculation
       ↓
    Dashboard
       ↓
    Report


---

## 53. AI-Assisted Metrics Analysis

AI can assist with:

- Trend identification
- Anomaly detection
- Incident clustering
- KPI summarization
- Recurrence analysis
- Executive reporting
- Improvement recommendations


Example:

    12 Months of Metrics
          ↓
    AI Trend Analysis
          ↓
    MTTD Increasing
          ↓
    Alert Volume Increasing
          ↓
    Recommendation:
    Tune Detection Rules
          ↓
    Human Validation


---

## 54. Professional Metrics Workflow

    Data Collection
         ↓
    Data Validation
         ↓
    KPI Calculation
         ↓
    Dashboard
         ↓
    Trend Analysis
         ↓
    Management Review
         ↓
    Improvement
         ↓
    Validation


---

## 55. Portfolio Project

### Project

**SOC Incident Response Metrics & KPI Dashboard**

### Environment

- Wazuh
- Windows
- Sysmon
- Python
- CSV/JSON
- GitHub
- Markdown
- Dashboarding tools


### Workflow

    Security Events
         ↓
    Alerts
         ↓
    Incidents
         ↓
    Timestamp Collection
         ↓
    KPI Calculation
         ↓
    Dashboard
         ↓
    Trend Analysis
         ↓
    Improvement Recommendations


### Metrics

Track:

- MTTD
- MTTA
- MTTI
- MTTC
- MTTR
- SLA Compliance
- False Positive Rate
- Incident Volume
- Recurrence Rate
- Automation Rate


### AI Component

Use AI for:

- Trend analysis
- Recurrence detection
- KPI summarization
- Management report generation
- Improvement recommendations


AI outputs should be reviewed before operational decisions.


---

## 56. Example Dataset

Example incident data:

| Incident ID | Detection | Ack | Containment | Recovery |
|---|---:|---:|---:|---:|
| INC-001 | 10m | 3m | 15m | 60m |
| INC-002 | 20m | 5m | 20m | 90m |
| INC-003 | 15m | 4m | 10m | 45m |


This data can be used to calculate:

- MTTD
- MTTA
- MTTC
- MTTR


---

## 57. Example KPI Calculation

For the dataset above:

    MTTD =
    (10 + 20 + 15) / 3

    MTTD = 15 minutes


    MTTA =
    (3 + 5 + 4) / 3

    MTTA = 4 minutes


    MTTC =
    (15 + 20 + 10) / 3

    MTTC = 15 minutes


    MTTR =
    (60 + 90 + 45) / 3

    MTTR = 65 minutes


These metrics can be visualized in a SOC dashboard.


---

## 58. Professional Repository Structure

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
    ├── Continuous-Improvement/
    │
    └── Automation/


---

## 59. Metrics Checklist

    [ ] MTTD measured
    [ ] MTTA measured
    [ ] MTTI measured
    [ ] MTTC measured
    [ ] MTTR measured
    [ ] SLA compliance measured
    [ ] False positives measured
    [ ] False negatives considered
    [ ] Alert backlog tracked
    [ ] Incident volume tracked
    [ ] Incident severity tracked
    [ ] Recurrence tracked
    [ ] Investigation quality measured
    [ ] Detection coverage measured
    [ ] Automation measured
    [ ] Recovery measured
    [ ] Business impact tracked
    [ ] Trends reviewed
    [ ] Improvement actions identified
    [ ] Metrics validated


---

## 60. Key Takeaways

Incident response metrics help organizations understand whether their security operations are actually improving.

Important metrics include:

- MTTD
- MTTA
- MTTI
- MTTC
- MTTR
- SLA Compliance
- False Positive Rate
- Alert Backlog
- Incident Recurrence
- Detection Coverage
- Automation Rate
- Recovery Success Rate


The key principle is:

> **What gets measured can be understood, improved, and validated.**


---

## 61. Final Metrics Model

    Collect
       ↓
    Calculate
       ↓
    Analyze
       ↓
    Identify Gaps
       ↓
    Improve
       ↓
    Validate
       ↓
    Measure Again


---

## 62. Conclusion

Incident response metrics transform security operations from subjective assessment into measurable performance.

A mature SOC should continuously ask:

> How quickly are we detecting threats?

> How quickly are we responding?

> How effective is containment?

> How accurate are our detections?

> Are incidents recurring?

> Are our improvements actually working?

The ultimate objective is:

    Better Metrics
       ↓
    Better Visibility
       ↓
    Better Decisions
       ↓
    Better Detection
       ↓
    Faster Response
       ↓
    Lower Risk
