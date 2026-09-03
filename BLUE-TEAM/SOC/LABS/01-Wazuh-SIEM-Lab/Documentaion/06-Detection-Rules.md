# Wazuh SIEM Lab — Detection Rules

## 1. Purpose

This document covers the detection-rule component of the Wazuh SIEM laboratory.

The objective is to understand how Wazuh identifies security-relevant events, evaluates them against detection rules, generates alerts, and supports SOC analysts in detecting suspicious activity.

The practical work in this section is performed only against authorized laboratory systems.

---

## 2. Detection Rules Objectives

After completing this phase, the learner should be able to:

1. Understand the purpose of Wazuh detection rules.
2. Understand how Wazuh evaluates security events.
3. Understand rule IDs and rule levels.
4. Understand rule groups and classifications.
5. Identify relevant built-in detection rules.
6. Understand custom detection rules.
7. Create basic custom rules in a controlled laboratory.
8. Test detection rules.
9. Analyze generated alerts.
10. Identify false positives.
11. Tune detection rules.
12. Document detection logic.

---

## 3. What Is a Detection Rule?

A detection rule defines conditions that determine whether a security event should generate an alert.

A simplified detection process is:

**Event → Decoder → Rule Matching → Alert → Investigation**

Rules can evaluate information such as:

- Event type
- Log source
- User
- Process
- Source IP
- Destination IP
- Event ID
- File activity
- Authentication activity
- Command execution
- Previous rule matches
- Related events

---

## 4. Wazuh Detection Workflow

The simplified Wazuh detection workflow is:

**Endpoint → Log Generation → Wazuh Agent → Wazuh Manager → Decoder → Rule Engine → Alert → Dashboard**

The Wazuh Manager receives events and processes them through decoders and rules.

When an event matches the required conditions, Wazuh can generate an alert for further SOC analysis.

---

## 5. Built-In Rules

Wazuh provides predefined detection rules for many security events.

Built-in rules can detect activities such as:

- Authentication failures
- Successful authentication
- Privilege-related activity
- Suspicious commands
- File changes
- Configuration changes
- Malware-related events
- System events
- Network-related events
- Security-policy violations

Before creating a custom rule, check whether an appropriate built-in rule already exists.

---

## 6. Rule ID

Each Wazuh rule has a unique rule ID.

The rule ID allows an analyst to identify the exact rule that generated an alert.

Example alert information may include:

- Rule ID
- Rule description
- Rule level
- Rule groups
- Timestamp
- Agent
- Decoder
- Source information

The rule ID is useful during:

- Alert investigation
- Troubleshooting
- Rule tuning
- Detection documentation
- Incident analysis

---

## 7. Rule Level

Wazuh rules have severity levels.

The rule level helps communicate the potential importance of an event.

A higher rule level does not automatically mean that an incident has occurred.

The analyst should consider:

- Event context
- Asset importance
- User context
- Frequency
- Related events
- Confidence
- Potential impact

A useful SOC principle is:

**Alert Severity ≠ Incident Severity**

The alert must still be investigated.

---

## 8. Rule Groups

Rules can belong to one or more groups.

Groups help categorize related detections.

Examples of security-related categories include:

- Authentication
- Authentication failures
- Access control
- System activity
- File integrity
- Malware
- Network activity
- Windows events
- Linux events

Groups help analysts filter and investigate related alerts.

---

## 9. Rule Description

A rule should have a clear description explaining what it detects.

A good description should communicate:

- What activity was detected
- Which component generated the event
- Why the activity is relevant

Example:

**"Multiple authentication failures detected for a monitored account."**

Avoid vague descriptions such as:

**"Suspicious event detected."**

Clear descriptions improve analyst triage.

---

## 10. Rule Matching

A detection rule may match an event based on different conditions.

Common matching concepts include:

- Event decoder
- Event ID
- Program name
- Log location
- Source IP
- Destination IP
- User
- Command
- Message content
- Previous rule
- Frequency
- Time-based conditions

The rule should be specific enough to detect the intended behavior while minimizing unnecessary alerts.

---

## 11. Rule Dependencies

Some rules can depend on previously matched events.

This allows Wazuh to detect sequences or related activity rather than evaluating every event independently.

Conceptually:

**Event A → Event B → Event C → Detection**

This is useful for identifying behavioral patterns.

For example:

**Multiple Failed Logins → Successful Login → Suspicious Activity**

The individual events may appear less significant by themselves, while the sequence may require investigation.

---

## 12. Custom Detection Rules

Custom rules allow the SOC analyst to create organization-specific detections.

Custom rules can be useful when:

- Built-in rules do not detect a required event.
- A laboratory scenario requires a specific detection.
- An organization has unique security requirements.
- Existing rules generate excessive false positives.
- Additional context is required.

Custom rules should be carefully tested before being used in production.

---

## 13. Custom Rule Design Principles

A good custom rule should be:

- Specific
- Understandable
- Testable
- Documented
- Relevant
- Maintainable
- Resistant to unnecessary false positives

Before creating a rule, define:

1. What behavior should be detected?
2. What log source contains the required information?
3. Which fields identify the behavior?
4. What conditions should trigger the alert?
5. What severity is appropriate?
6. What false positives are expected?
7. How will the rule be tested?

---

## 14. Detection Logic

A detection rule should have clearly defined logic.

Example:

**Objective:** Detect repeated authentication failures.

Detection logic:

**Authentication Event → Failure Status → Same Account → Repeated Attempts → Generate Alert**

The logic should be documented before implementation.

---

## 15. Example Laboratory Detection

### Scenario

A monitored Windows endpoint generates multiple failed authentication events.

### Detection Objective

Identify repeated authentication failures that may indicate:

- Incorrect credentials
- User error
- Automated authentication attempts
- Password spraying
- Brute-force activity

### Investigation Context

The analyst should review:

- Username
- Source IP
- Destination host
- Timestamp
- Number of failures
- Successful login after failures
- Related authentication events

The detection alone does not prove malicious activity.

---

## 16. Windows Detection Example

Windows security events can provide valuable authentication and endpoint telemetry.

Relevant information may include:

- Event ID
- Account name
- Source address
- Logon type
- Authentication status
- Timestamp
- Computer name

A SOC analyst can use this information to build or tune detection logic.

---

## 17. Linux Detection Example

Linux logs can provide information about:

- SSH authentication
- Failed login attempts
- Successful login
- sudo activity
- Privilege escalation
- User activity
- System services

Example detection concept:

**Repeated SSH Authentication Failures → Investigate Source → Check Successful Login → Correlate With Other Events**

---

## 18. File Integrity Detection

File Integrity Monitoring can generate events when monitored files are:

- Created
- Modified
- Deleted
- Changed

Detection logic can be based on:

**File Change → Identify File → Identify User → Identify Process → Determine Authorization → Investigate if Unexpected**

A file-integrity alert should be evaluated in context.

Legitimate software updates can also modify files.

---

## 19. Process Detection

Process-related detections can help identify suspicious endpoint activity.

Useful information includes:

- Process name
- Process path
- Parent process
- User
- Command-line information
- Timestamp
- Related network connections

A suspicious process should be investigated rather than automatically classified as malicious.

---

## 20. Network-Related Detection

Network telemetry can help identify:

- Unexpected connections
- Suspicious destinations
- Unusual ports
- Repeated connection attempts
- Unexpected services

A network detection should be correlated with endpoint and authentication activity when possible.

---

## 21. Detection Correlation

Individual alerts may not provide enough context.

Correlation combines related events.

Example:

**Failed Authentication**

+

**Successful Authentication**

+

**Suspicious Process**

+

**Unexpected Network Connection**

=

**Higher-Confidence Investigation**

Correlation improves detection quality and reduces dependence on isolated alerts.

---

## 22. Detection Tuning

Detection tuning improves the quality of alerts.

The objectives are:

- Reduce false positives.
- Improve detection accuracy.
- Increase useful context.
- Reduce analyst workload.
- Maintain visibility into genuine threats.

Tuning should be based on observed laboratory results and documented evidence.

---

## 23. False Positives

A false positive occurs when a legitimate activity triggers a security detection.

Examples:

- Administrator activity
- Scheduled tasks
- Software updates
- Backup operations
- Security scans
- Automated system processes
- User mistakes

Do not simply disable a noisy rule.

First determine why the alert is occurring.

---

## 24. False Positive Analysis

When a rule produces frequent alerts:

1. Identify the rule.
2. Review the triggering events.
3. Determine whether the activity is legitimate.
4. Identify the common characteristics.
5. Determine whether the detection can be made more specific.
6. Test the updated logic.
7. Verify that legitimate activity remains visible.
8. Document the tuning decision.

---

## 25. Detection Rule Testing

Every custom detection rule should be tested in the laboratory.

Testing process:

**Create Rule → Generate Test Event → Observe Event → Check Rule Match → Review Alert → Validate Severity → Check False Positives → Document Result**

The test should confirm that the rule detects the intended activity.

---

## 26. Detection Test Record

Document each test using the following format:

| Field | Value |
|---|---|
| Test ID | |
| Date | |
| Detection Rule | |
| Rule ID | |
| Test Objective | |
| Test Event | |
| Expected Result | |
| Actual Result | |
| Alert Generated | |
| False Positive | |
| Final Status | |

---

## 27. Detection Rule Documentation

Each important detection should have supporting documentation.

Recommended information:

- Detection name
- Purpose
- Rule ID
- Rule level
- Rule group
- Data source
- Detection logic
- Expected behavior
- Possible false positives
- Test procedure
- Test result
- Tuning history

This makes the detection easier to maintain.

---

## 28. Detection Engineering Workflow

Use the following workflow:

**Security Requirement → Data Source → Detection Hypothesis → Detection Logic → Rule Development → Testing → Validation → Tuning → Documentation → Monitoring**

This demonstrates a structured detection-engineering process.

---

## 29. Detection Quality

A useful detection should balance:

**Detection Coverage + Accuracy + Context + Maintainability**

A detection that generates thousands of low-value alerts may create more problems than it solves.

The goal is not to generate the maximum number of alerts.

The goal is to generate **useful, actionable alerts**.

---

## 30. Alert Enrichment

Detection quality can be improved by providing additional context.

Useful enrichment may include:

- Host information
- Username
- Source IP
- Destination IP
- Process information
- File information
- Previous related alerts
- Asset importance
- Threat-intelligence context

Enrichment helps analysts make faster decisions.

---

## 31. Detection Coverage

Maintain a record of important detection areas.

| Detection Area | Covered | Evidence |
|---|---|---|
| Authentication | | |
| Privilege Activity | | |
| Process Activity | | |
| File Integrity | | |
| Network Activity | | |
| Malware Activity | | |
| Persistence | | |
| Configuration Changes | | |

This can be expanded as the laboratory develops.

---

## 32. Detection Rule Validation Checklist

### Rule Design

- [ ] Detection objective defined.
- [ ] Data source identified.
- [ ] Detection logic documented.
- [ ] Expected behavior defined.
- [ ] Severity considered.

### Implementation

- [ ] Rule created or identified.
- [ ] Rule syntax validated.
- [ ] Rule ID documented.
- [ ] Rule group documented.

### Testing

- [ ] Test event generated.
- [ ] Rule matched expected event.
- [ ] Alert generated.
- [ ] Alert reviewed.
- [ ] False positives evaluated.

### Tuning

- [ ] Unnecessary alerts identified.
- [ ] Rule specificity reviewed.
- [ ] Detection logic tuned where necessary.
- [ ] Retesting completed.

### Documentation

- [ ] Detection purpose documented.
- [ ] Test results documented.
- [ ] Evidence captured.
- [ ] Lessons learned recorded.

---

## 33. Detection Investigation Workflow

When a detection generates an alert:

**Alert → Rule ID → Rule Description → Event Details → Host → User → Timestamp → Related Events → Classification → Investigation**

The rule is only the starting point.

The SOC analyst must determine whether the underlying activity is:

- Benign
- Suspicious
- Malicious
- Authorized
- False positive
- Requires further investigation

---

## 34. Detection and Incident Response

Detection is part of the broader SOC workflow.

**Telemetry → Detection → Alert → Triage → Investigation → Incident Declaration → Response → Recovery → Monitoring**

A detection rule should therefore support the downstream investigation and response process.

---

## 35. Practical Laboratory Exercises

### Exercise 1 — Authentication Detection

Generate controlled authentication events on the laboratory endpoint.

Tasks:

1. Generate failed authentication events.
2. Observe Wazuh alerts.
3. Identify the rule ID.
4. Review the rule description.
5. Analyze the event details.
6. Determine whether the activity is expected.
7. Capture evidence.

---

### Exercise 2 — File Integrity Detection

Modify an authorized monitored test file.

Tasks:

1. Modify the test file.
2. Observe Wazuh.
3. Identify the generated alert.
4. Review file information.
5. Identify the user responsible.
6. Determine whether the change was authorized.
7. Document the result.

---

### Exercise 3 — Process Detection

Generate a controlled process event on the laboratory endpoint.

Tasks:

1. Execute the authorized test activity.
2. Observe the generated telemetry.
3. Identify the relevant alert.
4. Review process information.
5. Correlate with other events.
6. Document the detection.

---

### Exercise 4 — Custom Detection

Create a basic custom detection for an authorized laboratory event.

Tasks:

1. Define the detection objective.
2. Identify the required log source.
3. Design the detection logic.
4. Implement the rule.
5. Test the rule.
6. Review the alert.
7. Tune the rule if required.
8. Document the final result.

Only perform controlled testing against laboratory systems.

---

## 36. Evidence Collection

Capture evidence such as:

- Wazuh alert screenshots
- Rule information
- Event details
- Detection results
- Test results
- Relevant logs
- Before-and-after comparison
- False-positive analysis
- Tuning results

Store evidence in the lab's `Evidence/` directory.

Sensitive information must be removed before publishing evidence to GitHub.

---

## 37. Detection Rule Report

For significant custom detections, create a report containing:

### Detection Information

- Detection Name
- Rule ID
- Rule Level
- Rule Group
- Data Source

### Detection Objective

Describe what the detection is designed to identify.

### Detection Logic

Describe the conditions required for the detection.

### Testing

Describe how the detection was tested.

### Results

Document:

- Expected behavior
- Actual behavior
- Alert generated
- False positives
- Detection accuracy

### Tuning

Document any changes made to improve the detection.

### Final Assessment

State whether the detection is suitable for continued laboratory use.

---

## 38. Common Detection Rule Mistakes

### Creating Rules Without Understanding the Data

A rule should be based on actual event structure.

### Making Rules Too Broad

Broad rules can generate excessive false positives.

### Making Rules Too Specific

Overly restrictive rules may miss relevant activity.

### Ignoring Context

An event should be evaluated with related telemetry.

### Skipping Testing

A detection should be validated before relying on it.

### Ignoring False Positives

Repeated false positives can reduce SOC effectiveness.

### Not Documenting Changes

Detection tuning should be traceable.

---

## 39. Detection Engineering Best Practices

Follow these principles:

1. Start with a clear detection objective.
2. Understand the available telemetry.
3. Prefer high-value detections.
4. Keep detection logic understandable.
5. Test every custom rule.
6. Monitor false positives.
7. Tune carefully.
8. Preserve useful context.
9. Document detection changes.
10. Review detection coverage regularly.

---

## 40. Final Detection Workflow

The complete laboratory detection workflow is:

**Security Requirement → Telemetry → Detection Logic → Rule → Test Event → Alert → Analysis → Tuning → Validation → Documentation**

This workflow demonstrates practical detection-engineering capability.

---

## 41. Success Criteria

The Detection Rules phase is complete when the learner can:

- Explain the purpose of Wazuh rules.
- Identify rule IDs.
- Interpret rule levels.
- Understand rule groups.
- Identify built-in detections.
- Create basic custom detections.
- Test detection rules.
- Analyze generated alerts.
- Identify false positives.
- Tune detection logic.
- Document detection results.
- Connect detections with the SOC investigation workflow.

---

## 42. Final Outcome

After completing this phase, the Wazuh laboratory should demonstrate that the learner can move beyond simply viewing alerts and understand how security detections are created, tested, analyzed, and improved.

The practical capability demonstrated is:

**Telemetry → Detection → Alert → Analysis → Tuning → Validation → Documentation**

This forms an important foundation for SOC alert triage, incident investigation, and detection engineering.

---

## 43. Next Step

After completing Detection Rules, continue with:

**07-Alert-Analysis.md**

The next phase will focus on practical analysis of Wazuh alerts, including alert prioritization, event context, affected hosts, users, timestamps, rule information, related events, false-positive identification, and SOC triage decisions.
