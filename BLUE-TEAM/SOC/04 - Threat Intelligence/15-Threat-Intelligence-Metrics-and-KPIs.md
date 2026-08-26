# 15 - Threat Intelligence Metrics and KPIs

## 1. Introduction

Threat Intelligence Metrics and Key Performance Indicators (KPIs) are used to measure the effectiveness, quality, operational value, and maturity of a Cyber Threat Intelligence (CTI) program.

A mature CTI program should not only collect intelligence.

It should demonstrate measurable security outcomes.

Basic model:

Threat Intelligence
    ↓
Analysis
    ↓
Dissemination
    ↓
Detection
    ↓
Investigation
    ↓
Response
    ↓
Measurement
    ↓
Improvement


---

## 2. Why CTI Metrics Matter

Metrics help organizations understand:

- Whether intelligence is useful
- Whether intelligence is timely
- Whether intelligence is accurate
- Whether intelligence improves detection
- Whether analysts are using intelligence
- Whether intelligence reduces response time
- Whether automation is effective
- Whether the CTI program is improving


---

## 3. Objectives of CTI Measurement

A CTI measurement program should:

1. Measure intelligence quality.
2. Measure intelligence timeliness.
3. Measure operational impact.
4. Measure detection improvement.
5. Measure response improvement.
6. Measure analyst efficiency.
7. Identify weaknesses.
8. Support management decisions.
9. Demonstrate ROI.
10. Improve the CTI lifecycle.


---

## 4. Metric Categories

CTI metrics can be grouped into:

1. Collection Metrics
2. Processing Metrics
3. Intelligence Quality Metrics
4. Timeliness Metrics
5. Dissemination Metrics
6. Detection Metrics
7. Threat Hunting Metrics
8. Incident Response Metrics
9. Automation Metrics
10. Business Impact Metrics
11. Program Maturity Metrics


---

## 5. Collection Metrics

Collection metrics measure how effectively intelligence is gathered.

Examples:

- Number of intelligence sources
- Number of active feeds
- Number of indicators collected
- Number of reports collected
- Source availability
- Feed update frequency
- Collection success rate


---

## 6. Number of Intelligence Sources

Track the number of active intelligence sources.

Example:

    Open Source Intelligence: 5
    Commercial Feeds: 3
    Government Sources: 4
    Internal Sources: 6

    Total:
    18 sources

The number alone is not a measure of quality.

A smaller number of high-quality sources may be better than many unreliable sources.


---

## 7. Feed Availability

Measure whether intelligence feeds are available when required.

Formula:

    Feed Availability =
    Available Feed Time
    --------------------
    Total Expected Time
    × 100


Example:

If a feed is available 99% of the expected time:

    Feed Availability = 99%


---

## 8. Collection Success Rate

Measure successful intelligence collection.

Formula:

    Collection Success Rate =
    Successful Collections
    -----------------------
    Total Collection Attempts
    × 100


This can identify unstable or unreliable collection systems.


---

## 9. Indicator Volume

Track the number of indicators collected.

Examples:

- IP addresses
- Domains
- URLs
- Hashes
- Email addresses

Example:

    Daily Indicators:
    25,000

    Weekly Indicators:
    175,000


Indicator volume should not be treated as intelligence quality.


---

## 10. Processing Metrics

Processing metrics measure how efficiently raw intelligence is transformed into usable data.

Examples:

- Processing time
- Normalization success
- Duplicate removal
- Enrichment success
- Parsing accuracy
- Validation rate


---

## 11. Data Normalization Rate

Measure how much incoming intelligence is successfully normalized.

Formula:

    Normalization Rate =
    Successfully Normalized Records
    --------------------------------
    Total Records
    × 100


A high normalization rate improves downstream automation.


---

## 12. Duplicate Indicator Rate

Duplicate indicators can waste storage and analyst time.

Formula:

    Duplicate Rate =
    Duplicate Indicators
    --------------------
    Total Indicators
    × 100


The goal is to reduce unnecessary duplication while preserving useful context.


---

## 13. Enrichment Success Rate

Measure how often indicators are successfully enriched.

Example:

    10,000 indicators received
    8,500 successfully enriched

    Enrichment Success Rate = 85%


Enrichment can include:

- Reputation
- WHOIS
- DNS
- ASN
- Geolocation
- Malware family
- Threat actor
- Campaign


---

## 14. Intelligence Quality

Quality is one of the most important CTI measurement areas.

Quality dimensions include:

- Accuracy
- Relevance
- Timeliness
- Completeness
- Context
- Confidence
- Actionability


---

## 15. Accuracy

Accuracy measures how often intelligence is correct.

Example:

    1,000 indicators investigated
    920 confirmed malicious

    Accuracy ≈ 92%

The methodology should define how "confirmed" is determined.


---

## 16. False Positive Rate

False positives reduce analyst efficiency.

Formula:

    False Positive Rate =
    False Positives
    ----------------
    Total Alerts
    × 100


Lower false positive rates generally improve operational efficiency.


---

## 17. True Positive Rate

True positive rate measures the percentage of intelligence-driven detections that are confirmed as relevant or malicious according to the defined detection criteria.

Formula:

    True Positive Rate =
    True Positives
    ---------------
    Total Relevant Alerts
    × 100


The exact denominator should be consistently defined.


---

## 18. Relevance Score

A CTI product can be evaluated based on whether it is relevant to the organization's:

- Industry
- Geography
- Technology
- Threat model
- Business assets
- Risk profile


A simple analyst feedback scale:

    1 = Not Relevant
    2 = Low Relevance
    3 = Moderately Relevant
    4 = Highly Relevant
    5 = Critical Relevance


---

## 19. Actionability

Actionability measures whether intelligence leads to a useful security action.

Possible actions:

- Detection created
- IOC blocked
- Vulnerability patched
- Threat hunted
- Incident investigated
- Account secured
- Control improved


---

## 20. Intelligence-to-Action Rate

Formula:

    Intelligence-to-Action Rate =
    Intelligence Products Resulting in Action
    -----------------------------------------
    Relevant Intelligence Products
    × 100


Example:

    100 relevant intelligence products
    35 resulted in security action

    Rate = 35%


This metric should be interpreted alongside relevance and quality.


---

## 21. Timeliness

Threat intelligence can lose value as threats evolve.

Important metrics include:

- Time to collect
- Time to process
- Time to analyze
- Time to validate
- Time to disseminate
- Time to action


---

## 22. Mean Time to Intelligence

Mean Time to Intelligence measures how long it takes to transform raw information into usable intelligence.

Example:

Threat Discovered
      ↓
Collection
      ↓
Analysis
      ↓
Validation
      ↓
Usable Intelligence


Formula:

    MTTI =
    Total Intelligence Processing Time
    ----------------------------------
    Number of Intelligence Products


---

## 23. Mean Time to Disseminate

Measures how quickly validated intelligence reaches consumers.

Example:

    Threat Validated: 10:00
    Intelligence Delivered: 10:20

    Time to Disseminate = 20 minutes


---

## 24. Mean Time to Detect

Measures how quickly intelligence helps identify malicious activity.

Formula:

    MTTD =
    Detection Time - Attack / Activity Time


CTI can improve MTTD by providing known indicators and TTP context.


---

## 25. Mean Time to Respond

Measures how quickly the organization responds after detection.

Formula:

    MTTR =
    Response Time - Detection Time


CTI can improve MTTR by providing:

- Threat context
- Related indicators
- Threat actor information
- Recommended actions


---

## 26. Intelligence Dissemination Metrics

Measure:

- Number of reports distributed
- Number of consumers
- Distribution time
- Consumer engagement
- Report access
- Feedback
- Action rate


---

## 27. Report Consumption Rate

Measure how often intelligence products are actually consumed.

Formula:

    Consumption Rate =
    Reports Accessed
    ----------------
    Reports Distributed
    × 100


A low consumption rate may indicate:

- Irrelevant reporting
- Poor timing
- Poor format
- Information overload


---

## 28. Consumer Engagement

Track:

- Report views
- Dashboard access
- API usage
- Intelligence searches
- Analyst feedback
- Detection creation


Engagement indicates whether intelligence is integrated into workflows.


---

## 29. Feedback Rate

Formula:

    Feedback Rate =
    Feedback Responses
    ------------------
    Intelligence Products
    × 100


Feedback helps improve:

- Content
- Format
- Frequency
- Relevance
- Dissemination channels


---

## 30. Threat Hunting Metrics

CTI can support threat hunting.

Metrics include:

- Number of hunts initiated from CTI
- Number of CTI-driven hunts
- Hunt findings
- Confirmed threats
- New IOCs discovered
- New TTPs identified


---

## 31. CTI-Driven Hunt Rate

Formula:

    CTI-Driven Hunt Rate =
    CTI-Initiated Hunts
    --------------------
    Total Hunts
    × 100


This measures how much threat intelligence contributes to hunting operations.


---

## 32. Hunt Success Rate

Formula:

    Hunt Success Rate =
    Hunts Producing Relevant Findings
    ---------------------------------
    Total CTI-Driven Hunts
    × 100


A "successful" hunt should have a clearly defined outcome.


---

## 33. New Intelligence Discovery

Threat hunting can generate new intelligence.

Track:

- New IOCs
- New malware
- New TTPs
- New infrastructure
- New attacker behaviors


This demonstrates the feedback loop between SOC and CTI.


---

## 34. Detection Metrics

CTI should improve detection capability.

Measure:

- Number of detections created
- Number of detections updated
- IOC match rate
- Detection coverage
- Detection accuracy
- Detection false positives


---

## 35. CTI-Driven Detection Rate

Formula:

    CTI-Driven Detection Rate =
    CTI-Based Detections
    ---------------------
    Total Relevant Detections
    × 100


This shows how much detection engineering benefits from CTI.


---

## 36. Detection Coverage

Measure how much relevant threat behavior is covered.

Example:

    Threat Actor Techniques:
    20

    Techniques Covered:
    15

    Detection Coverage:
    75%


Coverage should be evaluated against defined intelligence requirements and telemetry availability.


---

## 37. TTP Coverage

Map intelligence to MITRE ATT&CK techniques.

Example:

| TTP | Detection Available | Coverage |
|---|---|---|
| Phishing | Yes | Covered |
| PowerShell | Yes | Covered |
| Scheduled Task | Yes | Covered |
| Credential Dumping | Partial | Partial |
| Lateral Movement | No | Gap |

This helps identify detection gaps.


---

## 38. IOC Match Rate

Formula:

    IOC Match Rate =
    Events Matching Intelligence
    -----------------------------
    Events Searched
    × 100


A high match rate is not automatically good.

It may indicate:

- Real compromise
- Common infrastructure
- Poor-quality intelligence
- Overly broad indicators


---

## 39. Alert Enrichment Rate

Measure how many relevant alerts are enriched with CTI.

Formula:

    Alert Enrichment Rate =
    Alerts Enriched
    ----------------
    Relevant Alerts
    × 100


Higher enrichment can improve analyst investigation speed.


---

## 40. Analyst Efficiency

CTI should help analysts work faster and better.

Metrics include:

- Investigation time
- Enrichment time
- Manual lookup time
- Alerts handled
- Escalation accuracy
- Investigation quality


---

## 41. Investigation Time Reduction

Compare investigation time before and after CTI integration.

Example:

Before CTI:

    Average Investigation = 30 minutes

After CTI:

    Average Investigation = 18 minutes

Reduction:

    12 minutes per investigation


This can demonstrate operational value.


---

## 42. Manual Enrichment Reduction

Automation can reduce repetitive work.

Example:

Before:

    Analyst manually checks:
    IP reputation
    DNS
    WHOIS
    Threat feeds
    Malware database

After:

    Automated enrichment
        ↓
    Analyst reviews consolidated context


This can significantly reduce investigation effort.


---

## 43. Automation Metrics

Measure:

- Automated enrichment rate
- Automated routing rate
- Automated blocking rate
- Automation success rate
- Automation failure rate
- Manual intervention rate


---

## 44. Automation Success Rate

Formula:

    Automation Success Rate =
    Successful Automated Tasks
    --------------------------
    Total Automated Tasks
    × 100


Failures should be analyzed rather than simply hidden.


---

## 45. Human Intervention Rate

Formula:

    Human Intervention Rate =
    Tasks Requiring Human Intervention
    -----------------------------------
    Total Automated Tasks
    × 100


This helps determine where automation can be improved.


---

## 46. SOAR Metrics

Useful SOAR-related CTI metrics include:

- Playbooks executed
- Successful playbooks
- Failed playbooks
- Average execution time
- Automated response rate
- Analyst escalation rate


---

## 47. IOC Blocking Metrics

Track:

- Indicators received
- Indicators validated
- Indicators blocked
- Indicators expired
- False blocks
- Block effectiveness


Avoid measuring success only by the number of blocked indicators.


---

## 48. Vulnerability Intelligence Metrics

Measure:

- Critical CVEs identified
- Exploited CVEs identified
- Internally exposed CVEs
- Patch prioritization
- Time to remediation
- Vulnerabilities discovered through CTI


---

## 49. Threat Actor Tracking Metrics

Measure:

- Threat actors monitored
- Active campaigns
- New campaigns
- New TTPs
- New infrastructure
- Internal relevance


This helps maintain focus on threats relevant to the organization.


---

## 50. Campaign Tracking Metrics

Track:

- Active campaigns
- Campaigns affecting the industry
- Campaigns affecting the organization
- Campaign duration
- Number of associated IOCs
- Number of associated TTPs


---

## 51. Intelligence Source Performance

Each source should be evaluated.

Example:

| Source | Accuracy | Relevance | Timeliness | Actionability |
|---|---:|---:|---:|---:|
| Source A | High | High | High | High |
| Source B | Medium | High | High | Medium |
| Source C | Low | Medium | Low | Low |


This helps determine which feeds provide real value.


---

## 52. Source Value Score

A simple model can combine:

- Accuracy
- Relevance
- Timeliness
- Context
- Actionability

Example:

    Source Value =
    Accuracy
    + Relevance
    + Timeliness
    + Context
    + Actionability


The scoring methodology should be standardized.


---

## 53. Feed Cost Effectiveness

Commercial feeds should be evaluated against their value.

Consider:

    Feed Cost
        ↓
    Intelligence Quality
        ↓
    Detection Value
        ↓
    Incidents Identified
        ↓
    Analyst Time Saved
        ↓
    Business Risk Reduced


This supports procurement decisions.


---

## 54. Return on Intelligence

Return on Intelligence measures the value generated by CTI activities.

Possible benefits:

- Faster detection
- Faster response
- Reduced analyst workload
- Avoided incidents
- Better vulnerability prioritization
- Improved security decisions


There is no universal formula.

Organizations should define a model appropriate to their environment.


---

## 55. Business Impact Metrics

CTI should ultimately support business security.

Possible metrics:

- Incidents prevented
- Incidents detected earlier
- Critical vulnerabilities prioritized
- Business downtime avoided
- Analyst hours saved
- Risk reduced


---

## 56. Risk Reduction

CTI can contribute to risk reduction.

Example:

    Threat Identified
        ↓
    Vulnerability Prioritized
        ↓
    Patch Applied
        ↓
    Exploitation Risk Reduced


The organization should avoid claiming that CTI alone caused all risk reduction.


---

## 57. Executive KPIs

Executives generally need a small number of meaningful metrics.

Example dashboard:

    Critical Threats:
    5

    Active Exploited CVEs:
    3

    CTI-Driven Detections:
    42

    Detection Improvement:
    +18%

    Average Intelligence Delivery:
    25 minutes

    CTI-Driven Incidents:
    7

    Analyst Time Saved:
    35 hours


---

## 58. SOC Dashboard

A SOC dashboard may include:

    Active CTI Alerts
    ------------------
    24

    High-Confidence IOC Matches
    ----------------------------
    8

    CTI-Driven Investigations
    --------------------------
    15

    CTI-Driven Hunts
    -----------------
    6

    False Positive Rate
    --------------------
    4%

    Average Enrichment Time
    ------------------------
    2 minutes


---

## 59. CTI Operational Dashboard

Recommended sections:

### Intelligence

- New indicators
- Active campaigns
- Threat actors
- Critical vulnerabilities

### Operations

- IOC matches
- CTI alerts
- Hunts
- Incidents

### Performance

- MTTI
- MTTD
- MTTR
- False positive rate

### Quality

- Feed accuracy
- Relevance
- Confidence
- Consumer feedback


---

## 60. KPI Design Principles

Good KPIs should be:

- Specific
- Measurable
- Relevant
- Consistent
- Actionable
- Comparable over time


Avoid vanity metrics.


---

## 61. Vanity Metrics

Examples:

- Number of reports created
- Number of indicators collected
- Number of feeds connected

These numbers may look impressive but do not necessarily demonstrate security value.


---

## 62. Outcome-Based Metrics

Better metrics include:

- Detection improvement
- Investigation time reduction
- Response time reduction
- Vulnerability prioritization
- Threat hunting findings
- Confirmed threats detected


These demonstrate operational outcomes.


---

## 63. Leading Indicators

Leading indicators help predict future performance.

Examples:

- Intelligence coverage
- Threat actor monitoring
- Vulnerability intelligence coverage
- Detection coverage
- Feed health


---

## 64. Lagging Indicators

Lagging indicators measure outcomes after events occur.

Examples:

- Incidents detected
- Incidents prevented
- Response time
- Confirmed compromises
- Business impact


A mature program should use both leading and lagging indicators.


---

## 65. KPI Baseline

Before improving a process, establish a baseline.

Example:

    Average Investigation Time:
    30 minutes

    False Positive Rate:
    12%

    CTI-Driven Detections:
    10 per month


After improvements:

    Average Investigation Time:
    20 minutes

    False Positive Rate:
    6%

    CTI-Driven Detections:
    25 per month


The baseline makes improvement measurable.


---

## 66. KPI Targets

Targets should be realistic and organization-specific.

Example:

    Objective:
    Reduce CTI enrichment time.

    Baseline:
    10 minutes.

    Target:
    < 3 minutes.

    Measurement:
    Average enrichment time.

    Owner:
    SOC / CTI Team.


---

## 67. KPI Review Cycle

Review metrics regularly.

Example:

    Daily
      ↓
    Operational Monitoring

    Weekly
      ↓
    SOC / CTI Review

    Monthly
      ↓
    Management Review

    Quarterly
      ↓
    Program Review


---

## 68. KPI Trend Analysis

Single measurements may be misleading.

Track trends.

Example:

    Month 1:
    12% False Positive Rate

    Month 2:
    9%

    Month 3:
    7%

    Month 4:
    5%


This demonstrates improvement over time.


---

## 69. Benchmarking

Organizations can compare:

- Current performance
- Historical performance
- Internal teams
- Industry benchmarks
- Security objectives


Benchmarks should be used carefully because organizations have different environments and risk profiles.


---

## 70. CTI Maturity Metrics

A maturity assessment can consider:

### Level 1

Manual reporting.

### Level 2

Basic feeds and IOC searches.

### Level 3

SIEM and TIP integration.

### Level 4

SOAR and automated workflows.

### Level 5

AI-assisted, risk-based, closed-loop CTI.


Metrics should reflect both technical capability and operational effectiveness.


---

## 71. AI Metrics

AI-assisted CTI systems require additional measurements.

Examples:

- AI extraction accuracy
- AI classification accuracy
- AI summarization accuracy
- Human correction rate
- Hallucination rate
- Automation success rate
- Analyst time saved


---

## 72. AI Extraction Accuracy

Measure whether AI correctly extracts:

- IOCs
- TTPs
- Threat actors
- Malware
- CVEs
- Dates
- Relationships


Example:

    Correct Extractions:
    950

    Total Extractions:
    1,000

    Accuracy:
    95%


---

## 73. AI Human Correction Rate

Formula:

    Human Correction Rate =
    AI Outputs Requiring Correction
    -------------------------------
    Total AI Outputs
    × 100


A high correction rate indicates that the workflow requires improvement.


---

## 74. AI Hallucination Monitoring

Track cases where AI produces unsupported information.

Examples:

- Fake source
- Incorrect IOC
- False attribution
- Invented relationship
- Incorrect technical claim

Important controls:

- Grounding
- Source verification
- Structured prompts
- Human review
- Audit logging


---

## 75. AI Analyst Productivity

Measure whether AI actually improves analyst productivity.

Example:

Before AI:

    Report Preparation:
    60 minutes

After AI:

    Draft Preparation:
    15 minutes

Human Validation:
    20 minutes

Total:
    35 minutes

Time Saved:
    25 minutes


The objective is not merely automation.

The objective is improved quality and efficiency.


---

## 76. Portfolio Project

# Project: CTI Metrics and KPI Dashboard

## Objective

Build a dashboard demonstrating measurable performance of a threat intelligence program.

### Metrics

Include:

- Intelligence sources
- Feed health
- IOC volume
- IOC match rate
- False positive rate
- MTTI
- MTTD
- MTTR
- CTI-driven detections
- CTI-driven hunts
- Intelligence-to-action rate
- Analyst time saved


---

## 77. Portfolio Dashboard Architecture

Example:

Data Sources
     ↓
CTI Platform
     ↓
SIEM / SOAR
     ↓
Metrics Collection
     ↓
Analytics
     ↓
KPI Dashboard
     ↓
SOC / CTI / Management


Possible technologies:

- Wazuh
- Splunk
- Elastic
- Python
- SQL
- Grafana
- Power BI


---

## 78. Portfolio Documentation Structure

For the repository:

    15-Threat-Intelligence-Metrics-and-KPIs/
    │
    ├── README.md
    │
    ├── metrics/
    │   ├── intelligence-quality.md
    │   ├── timeliness.md
    │   ├── detection-metrics.md
    │   └── response-metrics.md
    │
    ├── kpis/
    │   ├── soc-kpis.md
    │   ├── executive-kpis.md
    │   └── business-kpis.md
    │
    ├── dashboard/
    │   └── cti-kpi-dashboard.md
    │
    ├── automation/
    │   └── automated-metrics.md
    │
    ├── ai/
    │   └── ai-metrics.md
    │
    ├── evidence/
    │   └── screenshots/
    │
    └── lessons-learned.md


---

## 79. CTI Metrics Checklist

### Quality

- [ ] Accuracy
- [ ] Relevance
- [ ] Timeliness
- [ ] Confidence
- [ ] Actionability

### Operations

- [ ] IOC matches
- [ ] CTI alerts
- [ ] Threat hunts
- [ ] CTI-driven incidents
- [ ] Detection coverage

### Performance

- [ ] MTTI
- [ ] MTTD
- [ ] MTTR
- [ ] False positive rate
- [ ] Enrichment time

### Business

- [ ] Risk reduction
- [ ] Analyst time saved
- [ ] Incidents detected
- [ ] Vulnerabilities prioritized
- [ ] Business impact

### AI

- [ ] Extraction accuracy
- [ ] Classification accuracy
- [ ] Human correction rate
- [ ] Hallucination monitoring
- [ ] Analyst productivity


---

## 80. Final Principle

A mature threat intelligence program should measure not how much intelligence it produces, but how much useful security value it creates.

The complete measurement model is:

**Collect → Analyze → Disseminate → Detect → Investigate → Respond → Measure → Improve**

The strongest CTI metrics connect intelligence activity to operational and business outcomes.

**Intelligence Volume → Intelligence Quality → Security Action → Security Outcome**

The ultimate objective is:

**Measure what improves security, not merely what is easy to count.**
