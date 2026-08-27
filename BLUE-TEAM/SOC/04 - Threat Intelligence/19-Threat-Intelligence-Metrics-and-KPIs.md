# 19 - Threat Intelligence Metrics and KPIs

## 1. Introduction

Threat Intelligence (TI) metrics and Key Performance Indicators (KPIs) help a security team measure whether its intelligence program is producing useful and measurable security outcomes.

Collecting threat intelligence is not enough.

A mature program should answer:

- How much intelligence are we processing?
- How much of it is relevant?
- How quickly can we operationalize it?
- How much does it improve detection?
- How much time does it save analysts?
- How effectively does it support incident response?
- Is the intelligence reducing organizational risk?

Basic model:

Threat Intelligence
        ↓
    Processing
        ↓
   Operationalization
        ↓
      Detection
        ↓
   Investigation
        ↓
     Response
        ↓
      Metrics
        ↓
    Improvement


---

## 2. Objectives

The objectives of CTI metrics are to:

1. Measure intelligence effectiveness.
2. Measure intelligence quality.
3. Measure operational impact.
4. Measure analyst efficiency.
5. Identify weaknesses.
6. Improve detection.
7. Improve incident response.
8. Support management decisions.
9. Demonstrate security value.
10. Enable continuous improvement.


---

## 3. Why Metrics Matter

Without metrics, a CTI program may focus on activity instead of outcomes.

Example:

    "We processed 100,000 indicators."

This does not necessarily mean the program is effective.

A better question is:

    "How many of those indicators produced
    useful detections or improved investigations?"


Metrics should therefore focus on **security outcomes**, not just volume.


---

## 4. Metric Categories

CTI metrics can be grouped into:

- Collection metrics
- Quality metrics
- Processing metrics
- Operational metrics
- Detection metrics
- Investigation metrics
- Incident response metrics
- Threat hunting metrics
- Automation metrics
- Business metrics


---

## 5. Collection Metrics

Collection metrics measure intelligence acquisition.

Examples:

- Number of intelligence sources
- Number of feeds
- Indicators collected
- Reports collected
- New indicators per day
- New indicators per month
- Intelligence coverage


Example:

    10 feeds
    ↓
    50,000 indicators
    ↓
    5,000 new indicators
    ↓
    1,000 relevant indicators


Volume alone should not be treated as effectiveness.


---

## 6. Intelligence Source Coverage

Measure how many relevant threat sources are available.

Example:

    Strategic Sources
    Operational Sources
    Tactical Sources
    Technical Sources


Coverage should reflect the organization's actual threat landscape.


---

## 7. Source Reliability

Each intelligence source should be evaluated.

Possible rating:

    Excellent
    Good
    Moderate
    Poor


Factors include:

- Accuracy
- Relevance
- Timeliness
- Consistency
- Historical performance


---

## 8. IOC Quality

Useful IOC quality metrics include:

- Valid indicator percentage
- False positive rate
- Duplicate rate
- Expired indicator rate
- High-confidence indicator percentage


Example:

    10,000 indicators
       ↓
    9,000 valid
       ↓
    7,500 relevant
       ↓
    1,500 low-quality


---

## 9. Indicator Validity Rate

Formula:

    Indicator Validity Rate =
    Valid Indicators
    -----------------
    Total Indicators
    × 100


Example:

    9,500 valid
    10,000 total

    = 95%


A higher validity rate generally indicates better data quality.


---

## 10. False Positive Rate

Formula:

    False Positive Rate =
    False Positive Alerts
    ---------------------
    Total Alerts
    × 100


Example:

    20 false positives
    100 alerts

    = 20%


High false-positive rates can increase analyst workload.


---

## 11. Duplicate Rate

Formula:

    Duplicate Rate =
    Duplicate Indicators
    --------------------
    Total Indicators
    × 100


High duplication may indicate poor feed management or insufficient normalization.


---

## 12. Indicator Freshness

Measure how recently indicators were observed or updated.

Important attributes:

- First seen
- Last seen
- Age
- Expiration
- Current activity


Example:

    IOC A → Last seen yesterday
    IOC B → Last seen 8 months ago


IOC A may deserve greater operational attention.


---

## 13. Indicator Expiration Rate

Measure how many indicators become obsolete.

Formula:

    Expiration Rate =
    Expired Indicators
    ------------------
    Total Indicators
    × 100


Tracking expiration helps maintain intelligence quality.


---

## 14. Processing Metrics

Processing metrics measure how efficiently intelligence moves through the pipeline.

Examples:

- Processing time
- Enrichment time
- Validation time
- Deduplication time
- Queue size
- Processing failures


---

## 15. Mean Time to Enrich

MTTE measures how long it takes to enrich an indicator.

Formula:

    MTTE =
    Total Enrichment Time
    ---------------------
    Number of Enriched Indicators


Lower time generally indicates more efficient processing.


---

## 16. Mean Time to Operationalize

This measures the time between receiving intelligence and making it usable by security operations.

Example:

    Intelligence Received
          ↓
    Validation
          ↓
    Enrichment
          ↓
    Detection
          ↓
    Operational


The objective is to reduce unnecessary delays.


---

## 17. Intelligence-to-Detection Time

A useful metric:

    Intelligence Received
          ↓
    Detection Rule Created
          ↓
    Time Difference


Example:

    Threat discovered:
    09:00

    Detection deployed:
    13:00

    Intelligence-to-Detection Time:
    4 hours


---

## 18. Detection Metrics

Detection metrics measure whether CTI improves the organization's ability to detect threats.

Examples:

- CTI-driven detections
- IOC matches
- TTP detections
- Detection coverage
- Detection accuracy
- Detection improvement rate


---

## 19. CTI-Driven Detection Count

Measure how many detections were created or improved using threat intelligence.

Example:

    20 new detections
    8 improved detections

    CTI contributed to:
    28 detections


This demonstrates operational value.


---

## 20. IOC Match Rate

Formula:

    IOC Match Rate =
    Events Matching Known IOCs
    --------------------------
    Events Checked
    × 100


This helps understand how frequently monitored activity overlaps with known intelligence.


---

## 21. True Positive Rate

Formula:

    True Positive Rate =
    True Positive Alerts
    --------------------
    Total Alerts
    × 100


This can help evaluate detection quality.


---

## 22. Detection Precision

Precision measures how many detected events were actually relevant.

Formula:

    Precision =
    True Positives
    --------------------------
    True Positives + False Positives


High precision generally means analysts spend less time investigating irrelevant alerts.


---

## 23. Detection Coverage

Coverage measures how much of the relevant threat landscape is detected.

Coverage can include:

- Threat actors
- Techniques
- Malware
- Attack patterns
- Critical assets
- Relevant IOCs


Example:

    Relevant TTPs:
    20

    Detected TTPs:
    15

    Coverage:
    75%


---

## 24. MITRE ATT&CK Coverage

CTI can help identify relevant ATT&CK techniques.

Example:

    Relevant Techniques:
    30

    Covered Techniques:
    21

    Coverage:
    70%


Coverage should be interpreted carefully because not every ATT&CK technique is equally relevant to every organization.


---

## 25. Threat Hunting Metrics

Useful metrics include:

- CTI-driven hunts
- Hunting hypotheses
- Successful hunts
- New detections from hunts
- New IOCs discovered
- New TTPs discovered


---

## 26. CTI-Driven Hunt Rate

Measure how many threat hunts originated from intelligence.

Example:

    Total Hunts:
    40

    CTI-Driven Hunts:
    25

    CTI-Driven Hunt Rate:

    25 / 40 × 100
    = 62.5%


---

## 27. Successful Threat Hunts

A hunt may be considered successful when it produces meaningful findings.

Examples:

- Previously unknown activity
- New IOC
- New TTP
- Detection gap
- Compromised system
- Intelligence update


---

## 28. Investigation Metrics

Important metrics include:

- Investigation time
- Alerts investigated
- Escalation rate
- Enrichment time
- Analyst effort
- Investigation success rate


---

## 29. Mean Time to Investigate

Formula:

    MTTI =
    Total Investigation Time
    -----------------------
    Number of Investigations


Example:

    500 minutes
    50 investigations

    MTTI = 10 minutes


---

## 30. Alert Enrichment Rate

Formula:

    Alert Enrichment Rate =
    Enriched Alerts
    ----------------
    Total Alerts
    × 100


Higher enrichment coverage can improve analyst context.


---

## 31. Incident Response Metrics

CTI should support incident response.

Useful metrics:

- MTTD
- MTTR
- Time to contain
- Time to identify related IOCs
- Number of incidents supported by CTI
- Intelligence-driven response actions


---

## 32. Mean Time to Detect

MTTD measures the average time between an attack or suspicious event occurring and being detected.

Conceptually:

    Attack Occurs
         ↓
       Detect
         ↓
    Time Difference


Lower MTTD generally indicates faster detection.


---

## 33. Mean Time to Respond

MTTR can refer to different operational definitions.

In incident response contexts it commonly measures the time from detection or incident identification to response or recovery, depending on organizational definition.

Always define the exact start and end points when reporting the metric.


---

## 34. Time to Contain

Measure:

    Detection
       ↓
    Containment


Example:

    Detection:
    10:00

    Containment:
    10:45

    Time to Contain:
    45 minutes


CTI can reduce this time by quickly identifying related infrastructure and indicators.


---

## 35. Intelligence-Driven Incident Rate

Measure how many incidents were identified or materially supported through CTI.

Example:

    Total Incidents:
    100

    CTI-Supported:
    35

    CTI-Supported Incident Rate:
    35%


---

## 36. Automation Metrics

For automated CTI workflows measure:

- Automation success rate
- Enrichment success rate
- Workflow execution time
- API failure rate
- Manual intervention rate
- Analyst time saved
- Processing volume


---

## 37. Automation Success Rate

Formula:

    Automation Success Rate =
    Successful Runs
    ---------------
    Total Runs
    × 100


Example:

    980 successful
    1,000 total

    = 98%


---

## 38. Manual Intervention Rate

Formula:

    Manual Intervention Rate =
    Runs Requiring Human Intervention
    ---------------------------------
    Total Runs
    × 100


A very high rate may indicate that the workflow needs improvement.


---

## 39. Analyst Time Saved

Example:

Before automation:

    500 alerts
    × 6 minutes
    =
    3,000 minutes


After automation:

    500 alerts
    × 2 minutes
    =
    1,000 minutes


Estimated time saved:

    2,000 minutes


This can be converted into hours for management reporting.


---

## 40. Intelligence Consumption Metrics

Measure whether analysts actually use intelligence.

Examples:

- Intelligence views
- Intelligence searches
- Intelligence-enriched alerts
- Intelligence-driven investigations
- Intelligence-driven hunts


Unused intelligence may indicate poor relevance or poor delivery.


---

## 41. Intelligence Adoption

A useful question:

    Are analysts actually using CTI?


Measure:

    Analysts Using CTI
    ------------------
    Total Relevant Analysts
    × 100


Training and workflow integration can improve adoption.


---

## 42. Intelligence Relevance

A useful metric is the percentage of intelligence judged relevant to the organization's environment.

Example:

    10,000 indicators
    ↓
    2,000 relevant to organization

    Relevance Rate:
    20%


Low relevance may indicate excessive generic intelligence.


---

## 43. Intelligence Actionability

Actionability measures whether intelligence leads to an actionable security decision.

Examples:

- Detection created
- Rule updated
- Asset patched
- IOC blocked
- Threat hunt initiated
- Incident escalated


The goal is:

**Intelligence → Action**

not merely:

**Intelligence → Storage**


---

## 44. Actionability Rate

Formula:

    Actionability Rate =
    Actionable Intelligence Items
    -----------------------------
    Relevant Intelligence Items
    × 100


Example:

    200 actionable
    500 relevant

    = 40%


---

## 45. Intelligence-to-Action Pipeline

    Intelligence
         ↓
      Relevant?
         ↓
        Yes
         ↓
     Actionable?
         ↓
        Yes
         ↓
       Action
         ↓
      Measure
         ↓
      Improve


---

## 46. Executive Metrics

Management generally needs outcome-oriented metrics.

Useful examples:

- Critical threats identified
- High-risk vulnerabilities prioritized
- Incidents detected
- Incidents prevented
- Response time improvement
- Analyst time saved
- Detection coverage
- Risk reduction


Avoid presenting only technical feed-volume statistics.


---

## 47. Technical vs Executive Metrics

### Technical

    IOC count
    Feed count
    API calls
    Detection count
    Enrichment time


### Executive

    Risk reduced
    Incidents detected
    Response time improved
    Critical vulnerabilities addressed
    Analyst efficiency improved


Both levels are important.


---

## 48. KPI Dashboard

A CTI dashboard may contain:

    +---------------------------+
    | CTI KPI DASHBOARD         |
    +---------------------------+
    | Active IOCs       25,000  |
    | High Confidence     3,200 |
    | CTI Detections        84 |
    | CTI Hunts             21 |
    | Avg Enrichment     1.8s  |
    | Automation Success   98% |
    | False Positive       6%  |
    | Analyst Time Saved   42h |
    +---------------------------+


The exact metrics should reflect organizational priorities.


---

## 49. KPI Trends

Metrics should be monitored over time.

Example:

    Month 1 → 12 CTI detections
    Month 2 → 18
    Month 3 → 27
    Month 4 → 35


Increasing detections is not automatically positive.

It must be interpreted alongside:

- True positives
- False positives
- Threat activity
- Coverage
- Analyst workload


---

## 50. Avoid Vanity Metrics

A vanity metric looks impressive but provides little security insight.

Example:

    "We collected 10 million IOCs."


Better:

    "We operationalized 25,000 high-confidence
    relevant indicators and used them to improve
    detection and investigation."


---

## 51. Balanced Scorecard

A CTI program can use four perspectives:

### Quality

    Accuracy
    Relevance
    Freshness


### Speed

    Processing Time
    Enrichment Time
    Intelligence-to-Action Time


### Operational Impact

    Detections
    Hunts
    Incidents


### Business Value

    Risk Reduction
    Analyst Time Saved
    Response Improvement


---

## 52. Metric Relationships

Metrics should be connected.

Example:

    Better Intelligence Quality
             ↓
       Better Detection
             ↓
       Fewer False Positives
             ↓
      Faster Investigation
             ↓
       Faster Response
             ↓
        Lower Risk


This is more meaningful than looking at individual metrics in isolation.


---

## 53. Root Cause Analysis

If a metric becomes worse:

Example:

    False Positive Rate ↑


Investigate:

- Poor feed quality?
- Outdated indicators?
- Incorrect correlation?
- Weak filtering?
- Missing asset context?
- Poor detection logic?


Metrics should lead to improvement actions.


---

## 54. Metric Baselines

Before improving a process, establish a baseline.

Example:

    Current MTTI:
    15 minutes

    Target:
    8 minutes


Then measure performance after introducing:

- CTI enrichment
- Automation
- Better detection
- Analyst training


---

## 55. Setting Targets

Targets should be:

- Relevant
- Measurable
- Realistic
- Time-bound
- Risk-driven


Example:

    Reduce average IOC enrichment time
    from 5 minutes to less than 1 minute
    within 90 days.


---

## 56. Metric Review Cycle

Use:

    Measure
       ↓
    Analyze
       ↓
    Identify Gap
       ↓
    Improve
       ↓
    Measure Again


This creates continuous improvement.


---

## 57. Home Lab Project

# Project: Threat Intelligence KPI Dashboard

## Objective

Build a small CTI metrics dashboard using simulated or lab-generated data.

The dashboard should demonstrate:

- Intelligence volume
- Indicator quality
- Detection impact
- Investigation efficiency
- Automation performance
- Threat hunting activity


---

## 58. Lab Environment

Use:

- Python
- Wazuh
- Sysmon
- Windows VM
- Kali Linux
- CSV / JSON
- SQLite
- GitHub
- Optional dashboarding platform


Use simulated data where real organizational data is unavailable.


---

## 59. Lab Task 1 — Create Dataset

Create fields such as:

    timestamp
    indicator
    indicator_type
    source
    confidence
    reputation
    alert_id
    verdict
    enrichment_time
    investigation_time
    automated
    incident
    action_taken


---

## 60. Lab Task 2 — Calculate Quality Metrics

Calculate:

- Validity rate
- False positive rate
- Duplicate rate
- Expiration rate
- Relevance rate


Document each formula.


---

## 61. Lab Task 3 — Calculate SOC Metrics

Calculate:

- CTI alert count
- CTI-driven detections
- MTTI
- MTTD
- MTTR
- Time to contain
- CTI-supported incidents


---

## 62. Lab Task 4 — Calculate Automation Metrics

Calculate:

- Automation success rate
- Manual intervention rate
- Average enrichment time
- Analyst time saved
- API failure rate


---

## 63. Lab Task 5 — Create Dashboard

Display:

    KPI
    Current Value
    Target
    Trend
    Status


Possible dashboard sections:

    Intelligence Quality
    Detection
    Investigation
    Automation
    Incident Response


---

## 64. Lab Task 6 — Analyze Trends

Compare results over time.

Example:

    Week 1
    Week 2
    Week 3
    Week 4


Identify:

- Improvements
- Regressions
- Anomalies
- Root causes


---

## 65. Lab Task 7 — Create Management Summary

Write a short summary:

    "CTI automation reduced average enrichment
    time from X to Y and improved analyst
    investigation efficiency by Z%."


Use actual calculated values from your lab dataset rather than invented claims.


---

## 66. Lab Task 8 — Create Improvement Plan

For every weak metric:

    Metric
       ↓
    Problem
       ↓
    Root Cause
       ↓
    Improvement
       ↓
    Target
       ↓
    Re-measure


---

## 67. Portfolio Evidence

Include:

- KPI definitions
- Dataset
- Formulas
- Dashboard screenshots
- Trend analysis
- Automation metrics
- Investigation metrics
- Management summary
- Improvement plan
- Lessons learned


Never publish confidential organizational metrics or sensitive incident information.


---

## 68. Recommended Repository Structure

    19-Threat-Intelligence-Metrics-and-KPIs/
    │
    ├── README.md
    │
    ├── metrics/
    │   ├── collection-metrics.md
    │   ├── quality-metrics.md
    │   ├── detection-metrics.md
    │   ├── investigation-metrics.md
    │   └── automation-metrics.md
    │
    ├── formulas/
    │   └── kpi-formulas.md
    │
    ├── dataset/
    │   └── sample-cti-data.csv
    │
    ├── dashboard/
    │   └── cti-kpi-dashboard.md
    │
    ├── analysis/
    │   └── trend-analysis.md
    │
    ├── reports/
    │   └── management-summary.md
    │
    ├── evidence/
    │   └── screenshots/
    │
    └── lessons-learned.md


---

## 69. Interview Question

### What are important CTI KPIs?

Important KPIs include:

- Intelligence relevance
- Intelligence validity
- False positive rate
- IOC match rate
- CTI-driven detections
- CTI-driven threat hunts
- Mean time to enrich
- Mean time to investigate
- MTTD
- MTTR
- Automation success rate
- Analyst time saved


---

## 70. Interview Question

### Why is IOC volume not a good KPI by itself?

Because a large number of indicators does not necessarily mean useful intelligence.

High-volume intelligence may contain:

- Duplicates
- Expired indicators
- Low-confidence indicators
- Irrelevant indicators
- False positives


The focus should be on **quality, relevance, actionability, and security outcomes**.


---

## 71. Interview Question

### How do you measure CTI effectiveness?

I would measure whether intelligence improves security operations.

For example:

1. Does CTI improve detection?
2. Does it reduce investigation time?
3. Does it support threat hunting?
4. Does it improve incident response?
5. Does it reduce false positives?
6. Does automation save analyst time?
7. Does it contribute to measurable risk reduction?


---

## 72. Interview Question

### What is an actionable intelligence item?

An actionable intelligence item is intelligence that can support a specific security decision or action.

Examples:

- Create detection rule
- Start threat hunt
- Patch vulnerable asset
- Block malicious infrastructure
- Investigate endpoint
- Escalate incident


---

## 73. Interview Question

### How would you present CTI metrics to management?

I would focus on business and security outcomes rather than technical volume.

For example:

    "CTI-supported detections increased,
    false positives decreased, and automated
    enrichment reduced analyst investigation
    time."


Then connect those improvements to risk reduction and operational efficiency.


---

## 74. Learning Outcome

After completing this topic, you should be able to:

- Explain CTI metrics and KPIs.
- Differentiate metrics from KPIs.
- Measure intelligence quality.
- Measure intelligence relevance.
- Calculate false positive rate.
- Measure CTI-driven detections.
- Measure investigation performance.
- Measure automation effectiveness.
- Build a CTI KPI dashboard.
- Explain CTI value to technical and executive audiences.


---

## 75. Professional Skill Mapping

This topic demonstrates:

### Threat Intelligence

- Intelligence evaluation
- Intelligence quality management
- Intelligence measurement
- Operationalization

### SOC

- Alert investigation
- Detection measurement
- Threat hunting metrics
- Incident response metrics

### Automation

- Workflow measurement
- Automation performance
- Analyst time savings

### GRC

- KPI development
- Risk measurement
- Management reporting
- Continuous improvement


---

## 76. CTI Maturity Measurement

A simple maturity model:

### Level 1 — Initial

    Manual collection
    Limited metrics
    Reactive use


### Level 2 — Developing

    Multiple feeds
    Basic enrichment
    Basic KPIs


### Level 3 — Operational

    SIEM integration
    Automated enrichment
    CTI-driven detection


### Level 4 — Advanced

    Threat hunting
    SOAR
    Risk-based prioritization
    Continuous measurement


### Level 5 — Optimized

    Integrated intelligence ecosystem
    Advanced automation
    AI-assisted analysis
    Continuous optimization
    Business-aligned intelligence


---

## 77. Continuous Improvement Model

    Measure
       ↓
    Identify Gap
       ↓
    Improve Intelligence
       ↓
    Improve Detection
       ↓
    Improve Automation
       ↓
    Improve Response
       ↓
    Re-measure


A mature CTI program continuously learns from operational outcomes.


---

## 78. Complete CTI KPI Framework

    Intelligence Collection
            ↓
    Intelligence Quality
            ↓
    Processing Efficiency
            ↓
    Intelligence Relevance
            ↓
    Operationalization
            ↓
    Detection
            ↓
    Investigation
            ↓
    Threat Hunting
            ↓
    Incident Response
            ↓
    Automation
            ↓
    Business Impact
            ↓
    Continuous Improvement


---

## 79. Key Principles

Remember:

1. Measure outcomes, not just volume.
2. Define every metric clearly.
3. Establish baselines.
4. Track trends over time.
5. Combine technical and business metrics.
6. Measure intelligence quality.
7. Measure actionability.
8. Measure analyst efficiency.
9. Avoid vanity metrics.
10. Use metrics to drive improvement.


---

## 80. Final Principle

The success of a Threat Intelligence program should not be measured by how much intelligence it collects.

It should be measured by how effectively that intelligence improves security decisions.

The strongest CTI measurement model is:

**Quality → Relevance → Actionability → Detection → Investigation → Response → Risk Reduction**

A mature SOC should be able to demonstrate:

**"Our intelligence is not only being collected; it is being operationalized, measured, and used to improve security outcomes."**
