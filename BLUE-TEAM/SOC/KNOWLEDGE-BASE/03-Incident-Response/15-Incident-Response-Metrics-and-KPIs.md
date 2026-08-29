# Incident Response Metrics and KPIs

## 1. Introduction

Incident Response Metrics and Key Performance Indicators (KPIs) are used to measure the effectiveness, efficiency, and maturity of an organization's incident response capability.

Metrics help security teams understand:

- How quickly incidents are detected
- How quickly analysts respond
- How effectively incidents are contained
- How long recovery takes
- Where process bottlenecks exist
- Whether security controls are improving
- Whether the SOC is meeting its operational targets

The basic model is:

    Security Event
          ↓
    Detection
          ↓
    Investigation
          ↓
    Response
          ↓
    Containment
          ↓
    Recovery
          ↓
    Metrics
          ↓
    Improvement


---

## 2. Objectives

Incident response metrics should help organizations:

- Measure operational performance
- Identify bottlenecks
- Improve response speed
- Measure analyst effectiveness
- Identify recurring problems
- Track SLA performance
- Improve detection capabilities
- Support management decisions
- Measure security maturity
- Demonstrate continuous improvement


---

## 3. Metrics vs KPIs

### Metric

A metric is a measurable value.

Example:

    Average Incident Response Time:
    45 minutes


### KPI

A KPI is a metric directly connected to an important business or security objective.

Example:

    KPI:
    95% of High-Severity incidents
    contained within 30 minutes.


Therefore:

    Metrics
       ↓
    Measurement

    KPIs
       ↓
    Measurement + Objective


---

## 4. Why Incident Response Metrics Matter

Without metrics:

    Incident
       ↓
    Response
       ↓
    "It seemed fast"


With metrics:

    Incident
       ↓
    Timestamped Events
       ↓
    Calculate Performance
       ↓
    Compare Against Target
       ↓
    Identify Gap
       ↓
    Improve


Metrics replace assumptions with measurable evidence.


---

## 5. Incident Response Measurement Lifecycle

    Collect Timestamps
          ↓
    Calculate Metrics
          ↓
    Compare With Targets
          ↓
    Identify Gaps
          ↓
    Implement Improvements
          ↓
    Measure Again


This creates a continuous improvement cycle.


---

## 6. Important Incident Response Metrics

Common metrics include:

- MTTD
- MTTA
- MTTI
- MTTC
- MTTR
- Mean Time to Eradicate
- Mean Time to Recover
- Incident Resolution Time
- SLA Compliance
- False Positive Rate
- Incident Recurrence Rate
- Automation Rate


---

## 7. MTTD

### Mean Time to Detect

MTTD measures the average time between the occurrence of malicious activity and its detection.

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

## 8. MTTA

### Mean Time to Acknowledge

MTTA measures the average time between alert generation and analyst acknowledgment.

Formula:

    MTTA =
    Total Acknowledgment Time
    -------------------------
    Number of Alerts


Example:

    Alert 1 = 2 minutes
    Alert 2 = 5 minutes
    Alert 3 = 3 minutes

    MTTA = 3.33 minutes


---

## 9. MTTI

### Mean Time to Investigate

MTTI measures how long analysts take to investigate an alert or incident.

Example:

    Alert Created
         ↓
    Analyst Starts Investigation
         ↓
    Investigation Complete


A high MTTI may indicate:

- Complex investigations
- Poor tooling
- Missing telemetry
- Lack of analyst experience
- Poor documentation
- Excessive alert volume


---

## 10. MTTC

### Mean Time to Contain

MTTC measures the average time required to contain an incident after it has been identified.

Example:

    Incident Identified
          ↓
    10:00

    Contained
          ↓
    10:20

    MTTC = 20 minutes


Lower MTTC generally indicates faster containment.


---

## 11. MTTR

### Mean Time to Respond / Recover / Resolve

MTTR can have different meanings depending on organizational definitions.

Therefore, the organization should explicitly define what MTTR means.

For example:

    MTTR =
    Detection/Response Start
          ↓
    Incident Resolution


Never assume that every organization uses MTTR in exactly the same way.


---

## 12. Mean Time to Eradicate

Measures the average time required to completely remove the threat.

Example:

    Malware Identified
          ↓
    Malware Removed
          ↓
    Persistence Removed
          ↓
    Credentials Secured
          ↓
    Eradication Complete


---

## 13. Mean Time to Recover

Measures the average time required to restore affected systems or services.

Example:

    Incident Contained
          ↓
    System Restored
          ↓
    Security Validation
          ↓
    Service Available


---

## 14. Incident Resolution Time

Incident Resolution Time measures the total time required to resolve an incident.

Formula:

    Resolution Time =
    Incident Closure Time
    -
    Incident Start Time


Example:

    Start:
    10:00

    Closure:
    12:30

    Resolution Time:
    150 minutes


---

## 15. SLA Compliance

SLA compliance measures whether incidents are handled within defined service-level targets.

Example:

    High Severity SLA:
    Contain within 30 minutes

    Actual:
    25 minutes

    Result:
    SLA Met


Another example:

    Target:
    30 minutes

    Actual:
    45 minutes

    Result:
    SLA Breached


---

## 16. SLA Compliance Rate

Formula:

    SLA Compliance Rate =
    Incidents Within SLA
    ---------------------
    Total Applicable Incidents
    × 100


Example:

    95 incidents within SLA
    100 total incidents

    SLA Compliance =
    95 / 100 × 100

    = 95%


---

## 17. False Positive Rate

False Positive Rate measures how many alerts were incorrectly classified as malicious.

Formula:

    False Positive Rate =
    False Positive Alerts
    ---------------------
    Total Alerts
    × 100


Example:

    False Positives = 200
    Total Alerts = 1000

    False Positive Rate =
    20%


A high false-positive rate can contribute to alert fatigue.


---

## 18. False Negative Risk

False negatives occur when malicious activity is not detected.

This is particularly important because:

    False Positive
        ↓
    Wasted Analyst Time

    False Negative
        ↓
    Missed Threat
        ↓
    Potential Security Impact


False negatives can be difficult to measure because the organization may not know what it failed to detect.


---

## 19. Alert-to-Incident Conversion Rate

Measures how many alerts become confirmed security incidents.

Formula:

    Conversion Rate =
    Confirmed Incidents
    -------------------
    Total Alerts
    × 100


Example:

    50 incidents
    5000 alerts

    Conversion Rate =
    1%


A low conversion rate is not automatically bad, because detection systems may intentionally generate many alerts for investigation.


---

## 20. Incident Volume

Track incidents over time.

Example:

| Month | Incidents |
|---|---:|
| January | 40 |
| February | 35 |
| March | 52 |
| April | 31 |


Analyze:

- Trends
- Spikes
- Recurring attack types
- Seasonal patterns
- Major campaigns


---

## 21. Incident Severity Distribution

Track incidents by severity.

Example:

| Severity | Count |
|---|---:|
| Critical | 2 |
| High | 12 |
| Medium | 45 |
| Low | 100 |


This provides a better understanding of the organization's incident profile.


---

## 22. Incident Category Distribution

Track incident types.

Example:

| Category | Count |
|---|---:|
| Phishing | 60 |
| Malware | 25 |
| Account Compromise | 15 |
| Vulnerability Exploitation | 8 |
| Data Exfiltration | 2 |


This can identify areas requiring additional security controls.


---

## 23. Recurrence Rate

Measures how frequently similar incidents occur again.

Example:

    Phishing Incident
          ↓
    Controls Improved
          ↓
    Similar Phishing Incident
          ↓
    Recurrence


A high recurrence rate may indicate that corrective actions were ineffective.


---

## 24. Incident Recurrence Formula

A simple model:

    Recurrence Rate =
    Repeated Incident Types
    ------------------------
    Total Relevant Incidents
    × 100


Organizations should define what qualifies as a recurring incident.


---

## 25. Escalation Rate

Measures the percentage of incidents requiring escalation.

Formula:

    Escalation Rate =
    Escalated Incidents
    ------------------
    Total Incidents
    × 100


Example:

    20 escalated
    100 total

    = 20%


---

## 26. Automation Rate

Measures the percentage of response actions performed automatically.

Formula:

    Automation Rate =
    Automated Actions
    ------------------
    Total Eligible Actions
    × 100


Example:

    70 automated actions
    100 eligible actions

    = 70%


Automation should improve efficiency without reducing investigation quality.


---

## 27. Manual Effort

Track analyst time spent on incidents.

Example:

    Incident A:
    20 minutes

    Incident B:
    60 minutes

    Incident C:
    30 minutes


High manual effort may indicate opportunities for:

- SOAR
- Scripts
- Automation
- Better detection
- Better documentation
- Better enrichment


---

## 28. Investigation Efficiency

Measure how efficiently analysts move from alert to conclusion.

Possible measurements:

- Average investigation duration
- Number of investigation steps
- Number of enrichment actions
- Number of escalations
- Analyst workload


---

## 29. Evidence Completeness

Measure whether incident records contain required evidence.

Example:

    Required Evidence:
    100

    Complete:
    95

    Evidence Completeness:
    95%


This is particularly useful for professional incident response documentation.


---

## 30. Documentation Completion Rate

Measures how many incidents have complete documentation.

Formula:

    Documentation Completion =
    Fully Documented Incidents
    ---------------------------
    Total Closed Incidents
    × 100


Example:

    98 complete
    100 closed

    = 98%


---

## 31. Playbook Usage Rate

Measures how frequently documented playbooks are used during incidents.

Example:

    Eligible Incidents:
    100

    Playbook Used:
    85

    Usage Rate:
    85%


This can identify training or playbook availability issues.


---

## 32. Playbook Effectiveness

Playbook usage alone is not enough.

Evaluate:

- Response time
- Missing steps
- Analyst feedback
- Escalation clarity
- Automation opportunities
- Successful containment


A playbook can be used frequently but still be ineffective.


---

## 33. Detection Coverage

Measure how much of the relevant attack surface or ATT&CK techniques have detection coverage.

Example:

| Technique | Coverage |
|---|---|
| PowerShell | Yes |
| Credential Access | Partial |
| Lateral Movement | Yes |
| Data Exfiltration | No |


This helps identify detection engineering priorities.


---

## 34. MITRE ATT&CK Coverage

Map detections to ATT&CK techniques.

Example:

    T1059.001
        ↓
    PowerShell
        ↓
    Detection Rule
        ↓
    SIEM Alert


Track:

- Techniques covered
- Techniques partially covered
- Techniques without coverage


---

## 35. Threat Containment Rate

Measures the percentage of incidents successfully contained.

Formula:

    Containment Rate =
    Successfully Contained Incidents
    ---------------------------------
    Total Applicable Incidents
    × 100


---

## 36. Recovery Success Rate

Measures successful recovery of affected systems.

Example:

    Systems Recovered:
    48

    Systems Requiring Rework:
    2

    Recovery Success:
    96%


---

## 37. Business Impact Metrics

Security metrics should also consider business impact.

Possible measurements:

- Downtime
- Number of affected users
- Number of affected systems
- Data exposure
- Service disruption
- Recovery cost
- Productivity impact


Security performance should connect technical activity to business risk.


---

## 38. Cost per Incident

Organizations may estimate:

    Cost per Incident =
    Analyst Cost
    +
    Technology Cost
    +
    Recovery Cost
    +
    Business Impact


Exact calculation depends on organizational accounting practices.


---

## 39. Analyst Workload

Track:

- Alerts per analyst
- Incidents per analyst
- Investigation hours
- Escalations
- After-hours workload
- Case backlog


This can help identify staffing and process issues.


---

## 40. Alert Backlog

Track unresolved alerts.

Example:

    Opening Backlog:
    150

    New Alerts:
    500

    Resolved:
    450

    Closing Backlog:
    200


Increasing backlog may indicate:

- Alert overload
- Staffing problems
- Poor prioritization
- Excessive false positives
- Inefficient workflows


---

## 41. Mean Age of Open Incidents

Measures how long open incidents remain unresolved.

Example:

    Open Incidents:
    10

    Average Age:
    4.5 hours


A growing average age may indicate investigation bottlenecks.


---

## 42. Aging Analysis

Categorize open incidents.

Example:

| Age | Incidents |
|---|---:|
| < 1 hour | 10 |
| 1–4 hours | 6 |
| 4–24 hours | 3 |
| > 24 hours | 1 |


This helps SOC leads prioritize workload.


---

## 43. Trend Analysis

Metrics become more valuable when analyzed over time.

Example:

    January
    ↓
    February
    ↓
    March
    ↓
    April


Track whether:

- MTTD decreases
- MTTC decreases
- MTTR decreases
- False positives decrease
- Automation increases
- Recurrence decreases


---

## 44. Before and After Comparison

Example:

### Before Improvement

    MTTD: 30 min
    MTTA: 10 min
    MTTC: 60 min
    MTTR: 180 min


### After Improvement

    MTTD: 15 min
    MTTA: 4 min
    MTTC: 30 min
    MTTR: 90 min


This demonstrates measurable improvement.


---

## 45. KPI Dashboard

A SOC dashboard may display:

    ┌─────────────────────────────┐
    │       SOC PERFORMANCE       │
    ├─────────────────────────────┤
    │ MTTD              15 min    │
    │ MTTA               4 min    │
    │ MTTC              30 min    │
    │ MTTR              90 min    │
    │ SLA Compliance      96%     │
    │ FP Rate             8%      │
    │ Automation          65%     │
    └─────────────────────────────┘


Dashboards should focus on actionable information.


---

## 46. Operational vs Executive Metrics

### SOC Analysts

Need technical metrics:

- Alert volume
- Investigation time
- MTTD
- MTTA
- MTTC
- False positives


### SOC Managers

Need operational metrics:

- SLA compliance
- Backlog
- Incident trends
- Analyst workload
- Automation


### Executives

Need business-oriented metrics:

- Critical incidents
- Business impact
- Risk trends
- Recovery performance
- Security improvement


The same security data can be presented differently for different audiences.


---

## 47. Metric Context

Metrics should not be interpreted in isolation.

Example:

    MTTR increased


This may appear negative.

But perhaps:

    Incident Complexity Increased
          ↓
    Investigation Became More Thorough
          ↓
    MTTR Increased
          ↓
    False Negatives Decreased


Therefore, metrics require context.


---

## 48. Good KPI Characteristics

A useful KPI should be:

- Relevant
- Measurable
- Consistent
- Actionable
- Understandable
- Comparable
- Time-bound


Avoid collecting metrics that do not support decisions.


---

## 49. KPI Targets

Example:

| KPI | Target |
|---|---:|
| MTTD | < 15 min |
| MTTA | < 5 min |
| MTTC | < 30 min |
| SLA Compliance | > 95% |
| Documentation | > 95% |
| Automation | > 60% |


Targets should be based on organizational requirements and risk.


---

## 50. KPI Review Cycle

A useful review cycle is:

    Collect
       ↓
    Validate
       ↓
    Analyze
       ↓
    Compare
       ↓
    Identify Gap
       ↓
    Improve
       ↓
    Measure Again


---

## 51. Metrics Data Sources

Possible data sources include:

- SIEM
- SOAR
- EDR
- Ticketing system
- Case management platform
- Firewall
- IAM
- Cloud platforms
- Threat intelligence
- Incident response reports


Example:

    Wazuh
      ↓
    Alert
      ↓
    Ticket
      ↓
    Analyst Action
      ↓
    Closure
      ↓
    Metrics Database


---

## 52. Automated Metrics Collection

Automation can collect:

- Alert timestamps
- Acknowledgment time
- Investigation start
- Containment time
- Closure time
- SLA status
- Analyst assignment


This reduces manual reporting.


---

## 53. Python Metrics Automation

A simple portfolio implementation could use Python to calculate:

- MTTD
- MTTA
- MTTC
- MTTR
- SLA compliance
- Incident volume
- Severity distribution


Example workflow:

    Incident CSV
         ↓
    Python
         ↓
    Calculate Metrics
         ↓
    Generate Report
         ↓
    Dashboard


---

## 54. AI-Assisted Metrics Analysis

AI can assist with:

- Trend analysis
- Anomaly detection
- KPI summaries
- Recurring incident identification
- Root-cause pattern analysis
- Executive summaries
- Improvement recommendations


Example:

    Historical Metrics
          ↓
    AI Analysis
          ↓
    Trend Detection
          ↓
    Analyst Validation
          ↓
    Recommendation


AI output should be validated before being used for operational decisions.


---

## 55. Metric Quality Problems

Common problems include:

- Inconsistent timestamps
- Different metric definitions
- Missing data
- Incorrect severity
- Manual entry errors
- Incomplete incident records
- Changing measurement methods


Standard definitions are important.


---

## 56. Standardization

Organizations should define:

    Metric Name
    Definition
    Formula
    Data Source
    Owner
    Frequency
    Target
    Reporting Audience


Example:

    Metric:
    MTTD

    Definition:
    Average time from malicious activity
    to detection.

    Source:
    SIEM

    Owner:
    SOC Manager

    Frequency:
    Monthly


---

## 57. Portfolio Metrics Project

### Project

**SOC Incident Response KPI Dashboard**

### Environment

- Wazuh
- Python
- CSV/JSON
- Pandas
- Matplotlib
- GitHub


### Workflow

    Wazuh Alerts
         ↓
    Incident Records
         ↓
    Python Processing
         ↓
    KPI Calculation
         ↓
    Dashboard
         ↓
    Trend Analysis
         ↓
    Recommendations


### Metrics

    MTTD
    MTTA
    MTTI
    MTTC
    MTTR
    SLA Compliance
    False Positive Rate
    Incident Volume
    Severity Distribution
    Automation Rate


---

## 58. AI Automation Component

The portfolio project can include an AI-assisted reporting layer.

Example:

    Incident Data
         ↓
    KPI Calculation
         ↓
    Trend Detection
         ↓
    AI Summary
         ↓
    Analyst Validation
         ↓
    Management Report


Possible output:

    "MTTD decreased by 25% compared
    with the previous reporting period.

    However, phishing-related incidents
    increased by 18%.

    Recommended actions include improved
    email detection and additional
    user awareness training."


The analyst should verify the underlying data and recommendations.


---

## 59. Professional Repository Structure

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
    └── Automation/


---

## 60. KPI Review Checklist

    [ ] Metric definitions standardized
    [ ] Data sources identified
    [ ] Timestamps validated
    [ ] MTTD calculated
    [ ] MTTA calculated
    [ ] MTTI calculated
    [ ] MTTC calculated
    [ ] MTTR calculated
    [ ] SLA compliance calculated
    [ ] False positives reviewed
    [ ] Incident trends analyzed
    [ ] Severity distribution reviewed
    [ ] Recurrence analyzed
    [ ] Automation measured
    [ ] Detection gaps reviewed
    [ ] KPI targets reviewed
    [ ] Improvement actions created


---

## 61. Key Takeaways

Incident response metrics help organizations:

- Measure security performance
- Identify operational bottlenecks
- Improve detection
- Improve response
- Improve containment
- Reduce recovery time
- Measure SLA performance
- Identify recurring problems
- Improve automation
- Demonstrate security maturity


The key principle is:

> **A security team cannot reliably improve what it does not consistently measure.**


---

## 62. Final Incident Response KPI Model

    Security Event
          ↓
    Detection
          ↓
    Investigation
          ↓
    Response
          ↓
    Containment
          ↓
    Recovery
          ↓
    Metrics
          ↓
    KPI Analysis
          ↓
    Gap Identification
          ↓
    Improvement
          ↓
    Re-measurement


---

## 63. Conclusion

Incident response metrics and KPIs transform security operations from a purely reactive function into a measurable and continuously improving capability.

A mature SOC should not only ask:

> "Did we resolve the incident?"

It should also ask:

> "How quickly did we detect it, how efficiently did we respond, where did the process fail, and are our improvements producing measurable results?"

The ultimate objective is:

    Measure
       ↓
    Understand
       ↓
    Improve
       ↓
    Validate
       ↓
    Measure Again
