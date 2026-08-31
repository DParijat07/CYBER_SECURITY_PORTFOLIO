# Wazuh SIEM Lab — Incident Investigation

## 1. Purpose

This document covers the incident-investigation phase of the Wazuh SIEM laboratory.

The objective is to move beyond individual alert analysis and perform a structured investigation of potentially malicious activity using Wazuh telemetry.

The investigation process should help a SOC analyst determine:

- What happened
- When it happened
- Which system was affected
- Which user or account was involved
- How the activity occurred
- What other events are related
- Whether the activity is benign, suspicious, or malicious
- What evidence supports the conclusion
- What action should be taken next

All activities must be performed only against authorized laboratory systems.

---

## 2. Investigation Objectives

After completing this phase, the learner should be able to:

1. Understand the difference between alert triage and incident investigation.
2. Define an investigation scope.
3. Build an incident timeline.
4. Identify affected assets.
5. Identify relevant users and accounts.
6. Correlate multiple security events.
7. Investigate authentication activity.
8. Investigate process activity.
9. Investigate file activity.
10. Investigate network-related telemetry.
11. Use Wazuh to search for related events.
12. Identify indicators of compromise.
13. Determine a probable root cause.
14. Assess the impact of a laboratory incident.
15. Document investigative findings.
16. Recommend appropriate containment and remediation actions.

---

## 3. Alert Triage vs Incident Investigation

Alert triage is the initial assessment of an alert.

Incident investigation is a deeper analysis performed when the activity requires additional examination.

```text
Alert
  ↓
Initial Triage
  ↓
Suspicious Activity?
  ↓
Yes
  ↓
Incident Investigation
  ↓
Evidence Collection
  ↓
Correlation
  ↓
Timeline
  ↓
Root Cause
  ↓
Impact
  ↓
Conclusion
```

The purpose of investigation is to build an evidence-based understanding of the incident.

---

## 4. Investigation Lifecycle

A practical investigation lifecycle is:

```text
1. Identify
      ↓
2. Scope
      ↓
3. Collect
      ↓
4. Correlate
      ↓
5. Analyze
      ↓
6. Determine Cause
      ↓
7. Assess Impact
      ↓
8. Document
      ↓
9. Recommend Response
```

This process can be adapted to the complexity of the incident.

---

## 5. Define the Investigation

Before searching through large amounts of telemetry, define the investigation.

Record:

```text
Investigation ID:
Date:
Analyst:
Initial Alert:
Affected Endpoint:
Initial Timestamp:
Initial User:
Initial Rule:
Initial Severity:
Investigation Status:
```

Example:

```text
Investigation ID: WAZUH-INV-001
Initial Alert: Authentication Activity
Affected Endpoint: LINUX-ENDPOINT
Status: Open
```

---

## 6. Establish the Scope

Determine the initial scope.

Questions:

1. Which endpoint generated the alert?
2. Which user was involved?
3. What time period should be examined?
4. Which event sources are relevant?
5. Are other endpoints involved?
6. Are related alerts present?
7. Is there evidence of lateral activity?

Start narrow and expand the investigation when evidence requires it.

---

## 7. Investigation Time Window

Do not limit investigation to the exact alert timestamp.

Use:

```text
Pre-Event Activity
       ↓
Initial Event
       ↓
Detection
       ↓
Post-Event Activity
```

The investigation window should be selected according to the scenario.

For example:

```text
Before:
Authentication attempts

During:
Successful authentication

After:
Process execution
File modification
Network activity
```

The purpose is to establish sequence and context.

---

## 8. Identify the Affected Asset

Determine the affected system.

Record:

- Hostname
- Agent ID
- IP address
- Operating system
- Asset role
- Criticality

Example:

```text
Hostname:
WIN-ENDPOINT

OS:
Windows

Role:
Laboratory Endpoint
```

Asset context helps determine the potential importance of an event.

---

## 9. Identify the User

Determine whether an account is associated with the incident.

Record:

- Username
- Account type
- Privilege level
- Authentication activity
- Related processes

Ask:

```text
Is this account legitimate?
Is this account authorized?
Is this account privileged?
Was the activity expected?
```

---

## 10. Identify the Initial Event

The initial event is the activity that caused the investigation to begin.

Examples:

- Failed authentication
- Successful authentication
- Suspicious process
- File modification
- Malware detection
- Configuration change
- Unusual network activity

Record the original alert exactly as observed.

---

## 11. Preserve Initial Evidence

Before modifying the environment, preserve relevant evidence.

Capture:

- Alert screenshot
- Alert metadata
- Rule information
- Timestamp
- Agent information
- Relevant event details
- Related logs

Store evidence under:

```text
01-Wazuh-SIEM-Lab/
└── Evidence/
    └── Incident-Investigation/
```

Do not expose sensitive credentials, tokens, keys, or personal information.

---

## 12. Search for Related Events

An initial alert should be treated as the starting point.

Search for:

```text
Same Host
+
Same User
+
Same Source
+
Same Time Window
+
Related Event Types
```

This may reveal additional activity.

---

## 13. Correlation Strategy

A simple correlation model is:

```text
Authentication
      ↓
Process
      ↓
File
      ↓
Network
      ↓
Additional Alerts
```

For example:

```text
Failed Login
      ↓
Successful Login
      ↓
New Process
      ↓
File Modification
      ↓
Outbound Connection
```

This sequence provides more investigative context than an isolated alert.

---

## 14. Build an Incident Timeline

Timeline analysis is one of the most important investigation techniques.

Create a table such as:

| Time | Host | User | Event | Source | Significance |
|---|---|---|---|---|---|
| 10:01 | Linux | test-user | Failed Login | auth log | Initial activity |
| 10:02 | Linux | test-user | Successful Login | auth log | Authentication |
| 10:03 | Linux | test-user | Process Started | system telemetry | Follow-up activity |
| 10:04 | Linux | test-user | File Modified | FIM | Potential impact |

The actual values should come from laboratory evidence.

---

## 15. Authentication Investigation

Authentication activity can reveal how access occurred.

Review:

- Failed logins
- Successful logins
- Source IP
- Username
- Authentication method
- Login time
- Session activity
- Privilege changes

Example:

```text
Multiple Failed Attempts
          ↓
Successful Authentication
          ↓
New Session
```

This pattern may require investigation if it is unexpected.

---

## 16. Process Investigation

After identifying a suspicious authentication event, examine process activity around the same period.

Review:

- Process name
- Parent process
- Command line
- User
- Execution path
- Process start time
- Related child processes
- Network activity

Example:

```text
Authentication
      ↓
Shell
      ↓
Command Execution
      ↓
New Process
```

Use evidence rather than assumptions when interpreting the activity.

---

## 17. Parent-Child Process Relationship

Parent-child relationships provide useful endpoint context.

Example:

```text
Parent Process
      ↓
Child Process
      ↓
Child Process
```

An analyst should ask:

- Is the parent expected?
- Is the child expected?
- Is the execution path legitimate?
- Is the user authorized?
- Was the process executed at an expected time?

An unusual parent-child relationship can be an important investigative clue.

---

## 18. Command-Line Investigation

Where command-line telemetry is available, examine:

- Executable
- Arguments
- User
- Working directory
- Parent process
- Execution time

Avoid assuming that a command is malicious simply because it looks unusual.

Evaluate the command in its environment and operational context.

---

## 19. File Activity Investigation

Investigate file changes around the incident.

Review:

- File path
- File name
- Change type
- Timestamp
- User
- Associated process
- Hash information where available

Example:

```text
Process Execution
       ↓
File Created
       ↓
File Modified
       ↓
File Integrity Alert
```

This can help identify the relationship between process and file activity.

---

## 20. Network Activity Investigation

Where network telemetry is available, examine:

- Source IP
- Destination IP
- Destination port
- Protocol
- Timestamp
- Associated process
- Connection frequency

Example:

```text
Process
   ↓
Network Connection
   ↓
Destination
   ↓
Related Events
```

Network activity should be interpreted in context.

---

## 21. Indicator of Compromise

An Indicator of Compromise (IoC) is an observable artifact that may indicate malicious activity.

Potential IoCs include:

- Suspicious IP address
- Suspicious domain
- File hash
- Suspicious file
- Unexpected account
- Unusual process
- Malicious URL
- Persistence artifact

Not every unusual artifact is automatically malicious.

Validate indicators before classifying them.

---

## 22. IoC Documentation

Create an IoC table:

| Type | Value | Source | First Seen | Last Seen | Confidence |
|---|---|---|---|---|---|
| IP | | Wazuh | | | |
| Hash | | Endpoint | | | |
| File | | FIM | | | |
| Account | | Authentication | | | |
| Process | | Endpoint | | | |

Use laboratory-generated or publicly safe test values.

Do not publish sensitive organizational indicators.

---

## 23. MITRE ATT&CK Context

Where Wazuh maps an alert to MITRE ATT&CK, record:

- Tactic
- Technique
- Technique ID
- Alert relationship

Use ATT&CK mapping as investigative context.

Do not assume that an ATT&CK mapping alone proves that an attack occurred.

The evidence must support the conclusion.

---

## 24. Event Correlation Example

Consider:

```text
Event 1:
Multiple Failed Logins

        ↓

Event 2:
Successful Login

        ↓

Event 3:
New Shell / Process

        ↓

Event 4:
File Modification

        ↓

Event 5:
Network Connection
```

The analyst should investigate whether these events are related.

Potential questions:

- Same host?
- Same user?
- Same time window?
- Same process?
- Same source?
- Same destination?

---

## 25. Determine the Attack Vector

The attack vector describes how the suspicious activity gained access or occurred.

Possible categories include:

- Authentication abuse
- Exploitation
- Malicious file
- Misconfiguration
- Compromised account
- Unauthorized administrative activity

The investigation should identify the most likely vector based on available evidence.

Do not claim an attack vector without supporting evidence.

---

## 26. Determine the Root Cause

Root cause is the underlying reason the incident occurred.

Examples:

```text
Weak Authentication
Misconfiguration
Unpatched Service
Compromised Account
Unauthorized Administrative Action
Malicious File
```

The root cause should be supported by the evidence collected during the investigation.

---

## 27. Impact Assessment

Determine what was affected.

Consider:

### Confidentiality

Was sensitive information potentially accessed?

### Integrity

Were files or configurations modified?

### Availability

Was a service or system disrupted?

### Account Security

Was an account potentially compromised?

### Scope

Was one endpoint affected or were multiple systems involved?

For a laboratory, document the simulated impact clearly.

---

## 28. Evidence-Based Classification

At the end of the investigation, classify the incident.

Possible outcomes:

```text
Benign
False Positive
Suspicious
Confirmed Malicious
Inconclusive
```

Use **Inconclusive** when available evidence is insufficient to confidently determine what occurred.

This is preferable to making unsupported claims.

---

## 29. Investigation Confidence

Record confidence in the conclusion.

Example:

```text
Low Confidence
Medium Confidence
High Confidence
```

Confidence should reflect:

- Amount of evidence
- Quality of telemetry
- Correlation strength
- Timeline consistency
- Alternative explanations

---

## 30. Containment Recommendation

If suspicious or malicious activity is confirmed in the laboratory, document an appropriate containment recommendation.

Examples:

- Isolate affected endpoint
- Disable compromised test account
- Stop malicious process
- Block malicious test indicator
- Preserve evidence
- Restrict affected service

Actions must be appropriate to the authorized laboratory environment.

---

## 31. Eradication Recommendation

Eradication focuses on removing the cause of the incident.

Possible actions:

- Remove malicious artifacts
- Remove unauthorized accounts
- Correct vulnerable configuration
- Patch affected software
- Reset compromised credentials
- Remove persistence
- Rebuild the laboratory endpoint when appropriate

Document what would be performed in a real environment versus what was actually performed in the lab.

---

## 32. Recovery Recommendation

Recovery focuses on safely returning the affected system to normal operation.

Examples:

- Restore system configuration
- Restore clean files
- Re-enable authorized services
- Reset credentials
- Monitor the endpoint
- Validate security controls

Continue monitoring after recovery to identify recurring activity.

---

## 33. Lessons Learned

After completing the investigation, document:

1. What happened?
2. What detection identified it?
3. What telemetry was useful?
4. What telemetry was missing?
5. What caused the activity?
6. What could have prevented it?
7. What detection could be improved?
8. What monitoring should be added?

This converts a laboratory incident into a learning opportunity.

---

## 34. Incident Investigation Report

Create a structured report for each significant laboratory scenario.

Recommended structure:

```text
Incident ID:
Date:
Analyst:
Severity:
Affected Asset:
Affected User:
Initial Alert:
Investigation Scope:

Executive Summary:

Timeline:

Evidence:

Indicators:

Event Correlation:

Root Cause:

Impact:

Classification:

Confidence:

Containment Recommendation:

Eradication Recommendation:

Recovery Recommendation:

Lessons Learned:
```

---

## 35. Example Investigation Scenario

### Scenario

A laboratory Linux endpoint generates multiple failed authentication alerts.

### Initial Observation

```text
Multiple Authentication Failures
```

### Investigation

```text
Failed Authentication
        ↓
Identify Source
        ↓
Identify User
        ↓
Review Time Pattern
        ↓
Check Successful Login
        ↓
Check Process Activity
        ↓
Check File Activity
        ↓
Check Network Activity
```

### Possible Finding

If evidence shows only controlled test activity generated by the analyst:

```text
Classification:
Benign / Laboratory Activity
```

If unexpected activity is observed and supporting evidence exists:

```text
Classification:
Suspicious
```

The final classification must be based on the actual laboratory evidence.

---

## 36. Investigation Scenario Matrix

Maintain a record of investigation exercises.

| ID | Scenario | Initial Alert | Investigation Result | Classification | Evidence |
|---|---|---|---|---|---|
| INV-001 | Authentication Activity | Login Alert | | | |
| INV-002 | File Modification | FIM Alert | | | |
| INV-003 | Process Activity | Endpoint Alert | | | |
| INV-004 | Sysmon Activity | Sysmon Alert | | | |
| INV-005 | Correlated Activity | Multiple Alerts | | | |

---

## 37. Evidence Directory

Organize investigation evidence consistently.

Recommended structure:

```text
01-Wazuh-SIEM-Lab/
│
├── Evidence/
│   └── Incident-Investigation/
│       ├── INV-001/
│       ├── INV-002/
│       ├── INV-003/
│       └── INV-004/
│
└── Reports/
    └── Incident-Investigation/
        ├── INV-001.md
        ├── INV-002.md
        └── INV-003.md
```

Use sanitized evidence for public GitHub documentation.

---

## 38. Evidence Handling

Maintain evidence integrity during the laboratory exercise.

Record:

- Evidence name
- Collection time
- Source
- Description
- Analyst
- Related investigation ID

Where appropriate, calculate hashes for exported evidence files.

Example:

```bash
sha256sum evidence-file
```

The purpose is to demonstrate basic evidence-integrity practices.

---

## 39. Chain of Custody Concept

For professional investigations, evidence handling may require chain-of-custody documentation.

A basic laboratory record can include:

```text
Evidence ID:
Collected By:
Date:
Time:
Source:
Description:
Hash:
Storage Location:
Transferred To:
Transfer Time:
Notes:
```

This is a simplified educational implementation.

---

## 40. Investigation Quality Checklist

### Scope

- [ ] Initial alert identified.
- [ ] Affected endpoint identified.
- [ ] User identified.
- [ ] Investigation window defined.

### Evidence

- [ ] Initial alert preserved.
- [ ] Relevant logs collected.
- [ ] Related events identified.
- [ ] IoCs documented.
- [ ] Evidence sources recorded.

### Analysis

- [ ] Timeline created.
- [ ] Authentication analyzed.
- [ ] Process activity analyzed.
- [ ] File activity analyzed.
- [ ] Network activity analyzed where available.
- [ ] Events correlated.
- [ ] Root cause assessed.
- [ ] Impact assessed.

### Conclusion

- [ ] Classification assigned.
- [ ] Confidence recorded.
- [ ] Findings documented.
- [ ] Recommendations provided.
- [ ] Lessons learned recorded.

---

## 41. Common Investigation Mistakes

### Starting Without Scope

Searching everything without a defined scope can create unnecessary noise.

### Ignoring the Timeline

Events should be understood chronologically.

### Relying on One Alert

A single alert rarely provides complete context.

### Ignoring Benign Explanations

Legitimate administrative activity can generate security alerts.

### Making Unsupported Claims

Do not label activity malicious without evidence.

### Failing to Document

An investigation that is not documented is difficult to reproduce or review.

### Publishing Sensitive Evidence

Always sanitize screenshots and exported logs before publishing them.

---

## 42. SOC Analyst Investigation Workflow

Use the following workflow as the standard laboratory process:

```text
Alert
  ↓
Triage
  ↓
Define Scope
  ↓
Preserve Evidence
  ↓
Search Related Events
  ↓
Build Timeline
  ↓
Correlate Telemetry
  ↓
Identify IoCs
  ↓
Determine Attack Vector
  ↓
Determine Root Cause
  ↓
Assess Impact
  ↓
Classify Incident
  ↓
Recommend Response
  ↓
Document Findings
  ↓
Lessons Learned
```

---

## 43. Portfolio Evidence

The GitHub portfolio should demonstrate the investigation process rather than simply showing screenshots.

Recommended portfolio evidence:

1. Lab architecture.
2. Initial alert.
3. Alert metadata.
4. Timeline.
5. Related events.
6. IoC table.
7. Investigation notes.
8. Root-cause analysis.
9. Impact assessment.
10. Final classification.
11. Response recommendations.
12. Lessons learned.

This demonstrates practical SOC investigation capability.

---

## 44. Success Criteria

The incident-investigation phase is complete when the learner can take a suspicious Wazuh alert and perform a structured investigation.

The learner should be able to answer:

```text
What happened?

When did it happen?

Which endpoint was affected?

Which user was involved?

What was the initial detection?

What other events are related?

What indicators were identified?

What was the likely attack vector?

What was the root cause?

What was the impact?

What evidence supports the conclusion?

What should be done next?
```

The learner should be able to support the final classification with evidence.

---

## 45. Final Outcome

After completing this phase, the learner should be able to demonstrate a complete SOC investigation workflow:

```text
Telemetry
    ↓
Alert
    ↓
Triage
    ↓
Investigation
    ↓
Correlation
    ↓
Timeline
    ↓
Evidence
    ↓
Root Cause
    ↓
Impact
    ↓
Classification
    ↓
Response Recommendation
    ↓
Documentation
```

This transforms the Wazuh laboratory from a simple SIEM installation into a practical SOC investigation environment.

---

## 46. Next Step

After completing incident investigation, continue with:

**Incident Response**

The next phase should focus on containment, eradication, recovery, validation, post-incident monitoring, and lessons learned.
