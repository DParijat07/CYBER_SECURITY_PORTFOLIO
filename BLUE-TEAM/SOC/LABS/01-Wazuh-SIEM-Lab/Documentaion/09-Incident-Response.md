# Wazuh SIEM Lab — Incident Response

## 1. Purpose

This document covers the incident-response phase of the Wazuh SIEM laboratory.

The objective is to demonstrate how a SOC analyst responds to a validated security incident after completing alert triage and investigation.

The incident-response process focuses on:

- Containment
- Eradication
- Recovery
- Validation
- Post-incident monitoring
- Documentation
- Lessons learned

All response activities must be performed only against authorized laboratory systems.

---

## 2. Incident Response Objectives

After completing this phase, the learner should be able to:

1. Understand the incident-response lifecycle.
2. Determine when an alert should become an incident.
3. Define the scope of a security incident.
4. Perform basic containment in a laboratory.
5. Perform basic eradication activities.
6. Recover an affected endpoint.
7. Validate that the threat has been removed.
8. Perform post-incident monitoring.
9. Document response actions.
10. Produce an incident-response report.
11. Identify lessons learned.
12. Recommend improvements to security controls.

---

## 3. Alert vs Incident

Not every alert should be treated as an incident.

A simplified decision process is:

**Alert → Triage → Investigation → Evidence of Security Impact → Incident → Incident Response**

An incident is a security event or series of events that requires a coordinated response according to the defined security process.

---

## 4. Incident Response Lifecycle

The laboratory follows this simplified lifecycle:

**Preparation → Identification → Containment → Eradication → Recovery → Post-Incident Monitoring → Lessons Learned**

Each stage should be documented.

---

## 5. Preparation

Preparation takes place before an incident occurs.

The Wazuh laboratory should have:

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Agent
- Monitored endpoint
- Appropriate log sources
- File Integrity Monitoring where required
- Sysmon where applicable
- Network connectivity
- Evidence storage
- Documentation templates

The purpose of preparation is to ensure that useful telemetry is available when an incident occurs.

---

## 6. Incident Identification

An incident may begin with:

- Wazuh alert
- Authentication anomaly
- Suspicious process
- File modification
- Malware detection
- Network activity
- Multiple correlated alerts

The analyst should first validate the alert.

Record:

- Incident ID
- Date
- Time
- Analyst
- Initial Alert
- Affected Host
- Affected User
- Rule ID
- Severity
- Initial Classification

---

## 7. Incident Declaration

An alert may be escalated to an incident when investigation provides sufficient evidence that security requires a coordinated response.

Example:

**Initial Alert → Investigation → Supporting Evidence → Security Impact → Incident Declared**

Do not declare an incident solely because an alert has a high severity level.

---

## 8. Incident Scope

Define what is affected.

Determine:

- Affected endpoint
- Affected account
- Affected process
- Affected files
- Relevant network connections
- Related alerts
- Potentially affected systems

Example:

- Affected Host: LAB-WINDOWS
- Affected Account: LAB-USER
- Initial Detection: Suspicious Process
- Related Activity: File Modification and Network Connection

The scope should be updated as new evidence is discovered.

---

## 9. Incident Severity

Use a simple laboratory classification:

| Severity | Description |
|---|---|
| Low | Limited impact and low-risk activity |
| Medium | Suspicious activity requiring investigation |
| High | Confirmed security incident with significant impact |
| Critical | Severe or widespread impact requiring immediate response |

Severity should consider:

- Asset importance
- User privilege
- Confidence
- Scope
- Impact
- Availability
- Confidentiality
- Integrity

---

## 10. Evidence Preservation

Before making significant changes to the affected system, preserve relevant evidence where practical.

Capture:

- Wazuh alert
- Alert metadata
- Relevant logs
- Event details
- Screenshots
- Timeline
- Process information
- File information
- Network information
- Indicators of compromise

Store evidence under:

**01-Wazuh-SIEM-Lab/Evidence/Incident-Response/INC-001/**

Do not publish passwords, API keys, authentication tokens, private information, or other sensitive data.

---

## 11. Containment

Containment limits the impact of an incident.

The goal is to prevent further damage while preserving the ability to investigate.

Laboratory containment actions may include:

- Disconnecting the test endpoint from the lab network
- Disabling a compromised test account
- Stopping a suspicious test process
- Blocking a test indicator
- Restricting a vulnerable service
- Isolating a laboratory VM

Only perform actions against systems you are authorized to control.

---

## 12. Short-Term Containment

Short-term containment immediately limits the incident.

Example:

**Suspicious Endpoint → Network Isolation → Prevent Further Activity → Preserve Evidence**

The analyst should record:

- Containment Action
- Date
- Time
- Performed By
- Reason
- Expected Result
- Actual Result

---

## 13. Long-Term Containment

Long-term containment focuses on maintaining a safe environment while remediation is performed.

Examples:

- Keep affected system isolated.
- Restrict unnecessary services.
- Disable compromised test accounts.
- Apply temporary firewall restrictions.
- Increase monitoring.
- Maintain enhanced logging.

The objective is to prevent recurrence while preparing for eradication and recovery.

---

## 14. Eradication

Eradication removes the underlying cause or malicious artifacts.

Depending on the laboratory scenario, this may include:

- Removing malicious test files
- Removing unauthorized accounts
- Removing persistence mechanisms
- Correcting insecure configuration
- Patching vulnerable software
- Resetting credentials
- Removing unauthorized processes
- Rebuilding a laboratory VM

Document every action.

---

## 15. Credential Remediation

If a test account is considered compromised, appropriate laboratory remediation may include:

**Identify Account → Disable Account → Reset Credential → Review Authentication Activity → Re-enable if Appropriate → Monitor**

Never expose actual credentials in portfolio documentation.

---

## 16. Malware or Suspicious File Removal

If the laboratory scenario includes a known test artifact:

1. Identify the file.
2. Preserve relevant evidence.
3. Record its location.
4. Record its hash where appropriate.
5. Remove or quarantine it.
6. Verify removal.
7. Monitor for recurrence.

Example:

**Suspicious File → Evidence Preserved → Hash Recorded → File Removed → System Checked → Monitoring Enabled**

Only use safe, authorized laboratory artifacts.

---

## 17. Recovery

Recovery returns the affected system to a trusted operational state.

Possible activities:

- Restore clean configuration
- Restore clean files
- Rebuild the laboratory VM
- Re-enable authorized services
- Reset credentials
- Verify security controls
- Reconnect the endpoint to the lab network

Recovery should occur only after sufficient eradication.

---

## 18. Recovery Validation

Before returning an endpoint to normal operation, validate:

- Suspicious processes are no longer present.
- Unauthorized accounts are removed or disabled.
- Suspicious files are removed.
- Configuration is correct.
- Security controls are functioning.
- Wazuh agent is reporting normally.
- No unexpected alerts remain.
- Network connectivity is appropriate.

Example:

**Eradication Complete → System Validation → Security Controls Checked → Monitoring Verified → Return to Service**

---

## 19. Post-Incident Monitoring

Continue monitoring after recovery.

Review:

- Authentication events
- Process activity
- File changes
- Network connections
- Wazuh alerts
- Security configuration
- Recurrence of indicators

Example:

**Recovery → Enhanced Monitoring → No Recurrence → Incident Closure**

If suspicious activity returns, reopen the investigation.

---

## 20. Incident Closure Criteria

An incident may be considered ready for closure when:

- [ ] Investigation is complete.
- [ ] Evidence is preserved.
- [ ] Root cause is documented.
- [ ] Containment is complete.
- [ ] Eradication is complete.
- [ ] Recovery is complete.
- [ ] Security controls are validated.
- [ ] Post-incident monitoring is complete.
- [ ] No unexpected recurrence is observed.
- [ ] Final report is completed.
- [ ] Lessons learned are documented.

---

## 21. Incident Response Timeline

Create a response timeline.

| Time | Action | Analyst | Result |
|---|---|---|---|
| 10:00 | Alert received | Analyst | Investigation started |
| 10:05 | Evidence collected | Analyst | Evidence preserved |
| 10:15 | Endpoint isolated | Analyst | Activity contained |
| 10:30 | Suspicious artifact removed | Analyst | Eradication completed |
| 10:45 | System validated | Analyst | Recovery approved |
| 11:00 | Monitoring enabled | Analyst | Post-incident monitoring |

Replace example values with actual laboratory results.

---

## 22. Incident Response Action Log

Maintain an action log for every significant response step.

| Action ID | Time | Action | Reason | Result | Status |
|---|---|---|---|---|---|
| ACT-001 | | | | | |
| ACT-002 | | | | | |
| ACT-003 | | | | | |
| ACT-004 | | | | | |

This demonstrates structured SOC documentation.

---

## 23. Incident Response Decision Process

Use the following decision process:

**Incident Identified → Determine Whether Activity Is Ongoing → Assess Containment Requirement → Preserve Evidence → Contain if Required → Eradicate → Recover → Validate → Monitor → Close**

If activity is no longer ongoing, continue investigation and evidence preservation before making unnecessary changes.

---

## 24. Example Scenario — Suspicious Authentication

### Scenario

A Wazuh alert identifies multiple authentication failures against a laboratory account.

### Investigation

Review:

1. Source IP
2. Username
3. Authentication timestamps
4. Successful authentication events
5. Process activity
6. File activity
7. Network activity

Possible workflow:

**Authentication Alert → Review Source → Review Account → Review Timeline → Check Successful Login → Check Process Activity → Check File Activity**

If the activity is determined to be an authorized laboratory test:

- Classification: Benign / Authorized Test
- Response: Document and Close

If evidence demonstrates unexpected compromise:

- Classification: Security Incident
- Response: Contain → Investigate → Eradicate → Recover → Monitor

The final decision must be based on evidence.

---

## 25. Example Scenario — Suspicious Process

### Scenario

A suspicious process is identified on a Windows laboratory endpoint.

### Response Workflow

**Alert → Process Investigation → Evidence Preservation → Endpoint Containment → Process Analysis → Artifact Removal → System Validation → Recovery → Monitoring**

Record each action and its result.

---

## 26. Example Scenario — File Integrity Alert

### Scenario

Wazuh detects an unexpected modification to a monitored file.

### Investigation

Review:

- File path
- Modification time
- User
- Process
- Related authentication
- Related network activity

### Response

If unauthorized:

**Preserve Evidence → Identify Cause → Contain → Restore Trusted File → Validate → Monitor**

---

## 27. Root Cause Review

After response, determine why the incident occurred.

Possible causes:

- Weak authentication
- Excessive privileges
- Misconfiguration
- Unpatched software
- Unauthorized account
- Malicious file
- Inadequate monitoring
- Security control failure

Document the root cause only when supported by evidence.

---

## 28. Control Improvement

Use the incident to improve security controls.

### Detection

- Improve Wazuh rules.
- Add additional log sources.
- Improve alert thresholds.
- Add correlation logic.

### Prevention

- Strengthen authentication.
- Reduce privileges.
- Patch vulnerable software.
- Improve endpoint configuration.

### Monitoring

- Add additional telemetry.
- Improve File Integrity Monitoring.
- Improve process monitoring.
- Improve network visibility.

---

## 29. Lessons Learned

After the incident, document:

1. What happened?
2. How was it detected?
3. What worked well?
4. What did not work?
5. What telemetry was missing?
6. Was the alert accurate?
7. Was response sufficiently fast?
8. Could containment be improved?
9. Could detection be improved?
10. What preventive controls should be added?

---

## 30. Incident Response Report

Each significant laboratory incident should have a final report.

Recommended structure:

- Incident ID
- Date
- Analyst
- Severity
- Status
- Executive Summary
- Affected Asset
- Affected User
- Initial Detection
- Investigation Summary
- Timeline
- Indicators of Compromise
- Root Cause
- Impact
- Containment Actions
- Eradication Actions
- Recovery Actions
- Validation
- Post-Incident Monitoring
- Lessons Learned
- Detection Improvements
- Prevention Recommendations
- Final Classification
- Closure Date

---

## 31. Incident Report Example Structure

### Executive Summary

Briefly describe:

- What happened
- How it was detected
- Which system was affected
- What response was performed
- Final outcome

### Technical Findings

Document:

- Alerts
- Events
- Timeline
- IoCs
- Processes
- Files
- Network activity

### Response

Document:

- Containment
- Eradication
- Recovery
- Validation

### Conclusion

Provide the final evidence-based assessment.

---

## 32. Evidence Directory

Recommended structure:

**01-Wazuh-SIEM-Lab/**

- **Evidence/**
  - **Incident-Response/**
    - **INC-001/**
      - Screenshots/
      - Logs/
      - Evidence-Notes.md
    - **INC-002/**
      - Screenshots/
      - Logs/
      - Evidence-Notes.md
    - **INC-003/

- **Reports/**
  - **Incident-Response/**
    - INC-001.md
    - INC-002.md
    - INC-003.md

Use sanitized evidence for public GitHub documentation.

---

## 33. Incident Response Checklist

### Identification

- [ ] Alert validated.
- [ ] Incident declared if appropriate.
- [ ] Affected asset identified.
- [ ] Affected user identified.
- [ ] Scope defined.
- [ ] Severity assigned.

### Evidence

- [ ] Initial alert preserved.
- [ ] Relevant logs collected.
- [ ] Timeline created.
- [ ] IoCs documented.
- [ ] Screenshots captured.
- [ ] Sensitive information removed.

### Containment

- [ ] Ongoing activity assessed.
- [ ] Endpoint isolated if required.
- [ ] Account restricted if required.
- [ ] Suspicious process controlled if required.
- [ ] Evidence preserved.

### Eradication

- [ ] Root cause addressed.
- [ ] Malicious artifacts removed.
- [ ] Unauthorized accounts addressed.
- [ ] Vulnerabilities/configuration issues corrected.
- [ ] Credentials reset where required.

### Recovery

- [ ] System restored.
- [ ] Security configuration validated.
- [ ] Wazuh monitoring verified.
- [ ] Endpoint reconnected safely.
- [ ] Security controls tested.

### Post-Incident

- [ ] Enhanced monitoring performed.
- [ ] No recurrence observed.
- [ ] Final report completed.
- [ ] Lessons learned documented.
- [ ] Detection improvements identified.
- [ ] Prevention improvements identified.

---

## 34. Common Incident Response Mistakes

### Acting Before Preserving Evidence

Where practical, preserve relevant evidence before making major changes.

### Removing Everything Immediately

Destroying useful evidence can make investigation more difficult.

### Ignoring the Root Cause

Removing an artifact without fixing the underlying cause can allow recurrence.

### Recovering Too Early

Returning a system to service before validation may reintroduce the risk.

### Failing to Monitor After Recovery

A system should be monitored after recovery for recurring activity.

### Not Documenting Actions

Every significant response action should be recorded.

### Publishing Sensitive Evidence

Sanitize all public screenshots, logs, and reports.

---

## 35. SOC Incident Response Workflow

Use this as the standard workflow for the Wazuh laboratory:

**Alert → Triage → Investigation → Incident Declaration → Evidence Preservation → Containment → Eradication → Recovery → Validation → Post-Incident Monitoring → Lessons Learned → Incident Closure**

---

## 36. Portfolio Evidence

The GitHub portfolio should demonstrate the complete response process.

Recommended evidence:

1. Initial Wazuh alert.
2. Investigation timeline.
3. Evidence collection.
4. IoC documentation.
5. Containment action.
6. Eradication action.
7. Recovery action.
8. Validation results.
9. Post-incident monitoring.
10. Final incident report.
11. Lessons learned.
12. Detection improvement recommendations.

The objective is to demonstrate practical SOC incident-response capability.

---

## 37. Success Criteria

The incident-response phase is complete when the learner can demonstrate the complete lifecycle of a controlled security incident.

The learner should be able to explain:

- What happened?
- How was it detected?
- What evidence was collected?
- Why was it classified as an incident?
- How was it contained?
- How was the root cause addressed?
- How was the system recovered?
- How was recovery validated?
- How was recurrence monitored?
- What was learned?

---

## 38. Final Outcome

After completing this phase, the Wazuh laboratory should demonstrate the following SOC capability:

**Telemetry → Detection → Alert → Triage → Investigation → Incident Declaration → Evidence Preservation → Containment → Eradication → Recovery → Validation → Monitoring → Lessons Learned → Documentation**

This demonstrates that the laboratory is being used as a practical SOC environment rather than simply as a SIEM installation.

---

## 39. Next Step

After completing Incident Response, continue with:

**Detection Rules**

The next phase should focus on understanding Wazuh detection rules, rule levels, rule groups, custom rules, rule testing, tuning, false-positive reduction, and detection engineering.
