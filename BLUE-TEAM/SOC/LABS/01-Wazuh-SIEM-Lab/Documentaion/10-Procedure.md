# Wazuh SIEM Lab — Procedure

## 1. Purpose

This document provides the practical step-by-step procedure for performing the Wazuh SIEM laboratory.

The procedure connects the previously documented lab setup, installation, configuration, log collection, detection, alert analysis, investigation, and response activities into one repeatable SOC workflow.

All activities must be performed only against authorized laboratory systems.

---

## 2. Lab Objective

The objective of this procedure is to demonstrate an end-to-end SOC monitoring workflow using Wazuh.

The practical workflow is:

**Generate Event → Collect Telemetry → Detect → Alert → Analyze → Investigate → Respond → Document**

---

## 3. Prerequisites

Before starting the procedure, verify that:

- Wazuh Manager is installed and operational.
- Wazuh Dashboard is accessible.
- Required Wazuh agents are installed.
- Agents are connected to the Manager.
- Required log sources are configured.
- Laboratory network connectivity is working.
- Test endpoints are available.
- Evidence storage is prepared.
- The systems being tested are authorized laboratory systems.

---

## 4. Lab Components

The laboratory may contain:

| Component | Purpose |
|---|---|
| Wazuh Manager | Central security monitoring and analysis |
| Wazuh Dashboard | Alert visualization and investigation |
| Wazuh Agent | Endpoint telemetry collection |
| Windows Endpoint | Windows security monitoring |
| Linux Endpoint | Linux security monitoring |
| Sysmon | Windows endpoint telemetry |
| Laboratory Network | Controlled communication environment |

The exact components may vary depending on the implemented laboratory architecture.

---

## 5. Pre-Lab Verification

Before generating any security events, verify the monitoring environment.

### Step 1 — Check Wazuh Manager

Confirm that the Wazuh Manager service is operational.

Verify:

- Service status
- Manager availability
- Rule engine availability
- Log processing

### Step 2 — Check Dashboard

Open the Wazuh Dashboard and confirm that it is accessible.

Verify that the dashboard can display:

- Agents
- Security events
- Alerts
- Monitoring information

### Step 3 — Check Agents

Verify that the required agents are connected.

Record:

- Agent name
- Agent ID
- Operating system
- IP address
- Connection status

### Step 4 — Verify Time

Confirm that the Manager and monitored endpoints have synchronized system time.

Accurate timestamps are important for incident investigation.

---

## 6. Verify Log Collection

Before performing detection exercises, confirm that telemetry is being received.

Check for:

- Authentication events
- System events
- Process activity
- File activity
- Security events
- Network-related telemetry where configured

If expected events are not appearing, troubleshoot log collection before continuing.

---

## 7. Generate a Controlled Test Event

Generate a harmless and authorized event on a monitored endpoint.

Examples include:

- Failed authentication attempt
- Test file modification
- Controlled process execution
- Configuration change
- Authorized test activity

The selected event should be appropriate for the laboratory.

---

## 8. Verify Event Reception

After generating the test event:

1. Open the Wazuh Dashboard.
2. Navigate to the relevant security events or alerts.
3. Identify the monitored endpoint.
4. Locate the generated event.
5. Record the timestamp.
6. Record the relevant rule information.
7. Verify that the event contains useful context.

If the event is not visible, investigate the monitoring pipeline.

---

## 9. Analyze the Alert

When an alert is generated, review:

- Alert timestamp
- Rule ID
- Rule description
- Rule level
- Rule group
- Agent
- Host
- User
- Source IP
- Event information

Determine why Wazuh generated the alert.

---

## 10. Perform Initial Triage

Classify the alert during initial triage.

Ask:

1. Is the activity expected?
2. Is the affected system known?
3. Is the user authorized?
4. Is the source expected?
5. Is the alert a known false positive?
6. Are there related alerts?
7. Does the event require further investigation?

Possible outcomes:

- Benign
- False positive
- Suspicious
- Potential incident
- Confirmed incident
- Inconclusive

---

## 11. Define the Investigation Scope

If further investigation is required, define:

- Affected host
- Affected user
- Source IP
- Relevant time period
- Related processes
- Related files
- Related network activity
- Related alerts

Avoid expanding the investigation without a reason.

---

## 12. Build an Investigation Timeline

Record important events chronologically.

Example:

| Time | Event | Host/User | Source | Significance |
|---|---|---|---|---|
| | Initial event | | | |
| | Authentication event | | | |
| | Process event | | | |
| | File event | | | |
| | Network event | | | |

The timeline should contain evidence-supported events.

---

## 13. Correlate Related Events

Search for events related to the original alert.

Correlate using:

- Timestamp
- Host
- User
- IP address
- Process
- File
- Rule ID
- Event type

Example:

**Authentication Failure**

→

**Successful Login**

→

**Process Execution**

→

**File Modification**

→

**Network Connection**

Correlation provides additional context for the investigation.

---

## 14. Investigate Authentication Activity

Review authentication-related events.

Check:

- Username
- Source IP
- Destination host
- Success/failure status
- Timestamp
- Logon information where available
- Number of attempts

Determine whether the authentication behavior appears normal or suspicious.

---

## 15. Investigate Process Activity

Review relevant process telemetry.

Check:

- Process name
- Process path
- Parent process
- User
- Command-line information where available
- Execution time
- Related child processes

Determine whether the process was expected.

---

## 16. Investigate File Activity

Review relevant file events.

Check:

- File name
- File path
- Operation
- User
- Timestamp
- Related process
- Hash where available

Determine whether the file activity was authorized.

---

## 17. Investigate Network Activity

Where network telemetry is available, review:

- Source IP
- Destination IP
- Port
- Protocol
- Connection time
- Related process

Determine whether the connection was expected.

---

## 18. Identify Indicators

Record relevant indicators discovered during the investigation.

Examples:

- IP addresses
- Domains
- File hashes
- File paths
- User accounts
- Process names
- Commands

Use a structured record.

| Indicator Type | Value | Source | Context |
|---|---|---|---|
| IP | | | |
| Domain | | | |
| Hash | | | |
| File | | | |
| Process | | | |
| User | | | |

---

## 19. Assess Impact

Determine whether the activity affected:

- Confidentiality
- Integrity
- Availability
- User accounts
- System access
- Data
- Services

Record the observed or potential impact.

Do not claim impact without supporting evidence.

---

## 20. Determine Root Cause

Investigate the probable cause of the activity.

Possible causes include:

- User error
- Misconfiguration
- Weak credentials
- Unauthorized access
- Compromised account
- Suspicious process
- Vulnerable service
- Malicious file
- Security-control failure

If the root cause cannot be established, record it as unknown or inconclusive.

---

## 21. Incident Decision

Use the following decision process:

**Alert**

↓

**Expected Activity?**

- Yes → Document → Close
- No → Continue Investigation

↓

**Suspicious Evidence?**

- No → Document → Close
- Yes → Continue

↓

**Security Incident Confirmed?**

- No → Document as Suspicious/Inconclusive
- Yes → Initiate Incident Response

---

## 22. Incident Response Handoff

If the investigation confirms a security incident, hand the case to the incident-response process.

Record:

- Incident ID
- Initial alert
- Investigation summary
- Affected systems
- Affected users
- Timeline
- Evidence
- IoCs
- Impact
- Recommended response actions

Continue with:

**09-Incident-Response.md**

---

## 23. Evidence Collection

Capture appropriate laboratory evidence.

Examples:

- Dashboard screenshots
- Alert details
- Event details
- Relevant logs
- Timeline
- Investigation notes
- IoC records
- Final classification

Store evidence in:

```text
Evidence/
├── Screenshots/
└── Logs/
```

Sensitive information must be removed before publishing the material publicly.

---

## 24. Investigation Report

Create a report for significant investigations.

Recommended sections:

1. Executive Summary
2. Initial Detection
3. Investigation Scope
4. Timeline
5. Evidence
6. Findings
7. Indicators
8. Impact
9. Root Cause
10. Classification
11. Recommendations
12. Conclusion

Store reports in the appropriate `Reports/` directory.

---

## 25. Detection Testing Procedure

For a custom detection:

1. Define the detection objective.
2. Identify the required telemetry.
3. Create the detection logic.
4. Implement the rule.
5. Generate a controlled test event.
6. Verify event collection.
7. Verify rule matching.
8. Confirm alert generation.
9. Review alert details.
10. Evaluate false positives.
11. Tune the rule if required.
12. Retest.
13. Document the result.

---

## 26. File Integrity Monitoring Procedure

For an authorized test file:

1. Identify a monitored test file.
2. Record its original state.
3. Perform a controlled modification.
4. Wait for telemetry collection.
5. Review the generated Wazuh alert.
6. Identify the file.
7. Identify the user.
8. Record the timestamp.
9. Determine whether the change was expected.
10. Capture evidence.
11. Document the result.

---

## 27. Authentication Monitoring Procedure

For a controlled authentication test:

1. Select an authorized laboratory account.
2. Generate a controlled failed authentication event.
3. Verify event collection.
4. Locate the Wazuh alert.
5. Record the rule information.
6. Review the source information.
7. Check for related authentication events.
8. Determine whether the activity was expected.
9. Capture evidence.
10. Document the result.

Do not perform uncontrolled authentication attacks against systems or accounts that you do not own or have permission to test.

---

## 28. Process Monitoring Procedure

For an authorized process test:

1. Select a monitored endpoint.
2. Execute a harmless test process.
3. Verify process telemetry.
4. Locate the relevant event.
5. Review process details.
6. Review the parent process where available.
7. Review associated user information.
8. Correlate related events.
9. Capture evidence.
10. Document the result.

---

## 29. End-to-End SOC Exercise

Perform the complete workflow:

### Phase 1 — Generate

Generate a controlled security event.

### Phase 2 — Collect

Verify that Wazuh receives the event.

### Phase 3 — Detect

Confirm that the relevant rule detects the activity.

### Phase 4 — Alert

Locate the generated alert.

### Phase 5 — Triage

Determine whether the alert requires investigation.

### Phase 6 — Investigate

Correlate related events and build a timeline.

### Phase 7 — Assess

Determine scope, impact, and probable root cause.

### Phase 8 — Respond

If an incident is confirmed, perform the authorized response procedure.

### Phase 9 — Document

Record evidence, findings, and conclusions.

### Phase 10 — Review

Identify lessons learned and improvements.

---

## 30. Procedure Checklist

### Environment

- [ ] Wazuh Manager operational.
- [ ] Dashboard accessible.
- [ ] Agents connected.
- [ ] Endpoint monitoring operational.
- [ ] System time verified.

### Detection

- [ ] Test event generated.
- [ ] Event collected.
- [ ] Detection rule matched.
- [ ] Alert generated.
- [ ] Alert reviewed.

### Investigation

- [ ] Affected host identified.
- [ ] User identified.
- [ ] Time window defined.
- [ ] Related events searched.
- [ ] Timeline created.
- [ ] Authentication reviewed.
- [ ] Process activity reviewed.
- [ ] File activity reviewed.
- [ ] Network activity reviewed.
- [ ] IoCs recorded.

### Assessment

- [ ] Scope determined.
- [ ] Impact assessed.
- [ ] Root cause investigated.
- [ ] Activity classified.

### Documentation

- [ ] Screenshots captured.
- [ ] Relevant logs preserved.
- [ ] Investigation notes completed.
- [ ] Report completed.
- [ ] Lessons learned recorded.

---

## 31. Troubleshooting During the Procedure

If an expected event does not appear:

1. Check endpoint connectivity.
2. Check Wazuh agent status.
3. Verify the relevant log source.
4. Verify log collection configuration.
5. Check system timestamps.
6. Check Wazuh Manager processing.
7. Review relevant Wazuh logs.
8. Verify that the event actually occurred.
9. Check whether the event matched an existing rule.
10. Document the issue if unresolved.

Do not modify multiple components simultaneously without recording the changes.

---

## 32. Evidence Naming Convention

Use consistent names for laboratory evidence.

Recommended format:

```text
YYYY-MM-DD_<Lab>_<Scenario>_<Evidence-Type>_<Number>
```

Example:

```text
2026-09-02_Wazuh_AuthenticationAlert_Screenshot_01.png
```

For logs:

```text
2026-09-02_Wazuh_AuthenticationAlert_Log_01.txt
```

Use sanitized data before publishing evidence.

---

## 33. Procedure Completion Record

| Field | Value |
|---|---|
| Lab | Wazuh SIEM Lab |
| Procedure Date | |
| Analyst | |
| Scenario | |
| Initial Event | |
| Rule ID | |
| Affected Host | |
| Affected User | |
| Final Classification | |
| Evidence Captured | |
| Report Created | |
| Status | |

---

## 34. Final Validation

Before considering the procedure complete, confirm that:

- Telemetry was collected successfully.
- The expected detection was triggered.
- The alert was analyzed.
- Related events were investigated.
- Evidence was collected.
- Findings were documented.
- The activity was classified.
- Response was performed where required.
- The final result was recorded.

---

## 35. Expected Outcome

Successful completion of this procedure demonstrates an end-to-end SOC workflow using Wazuh.

The practical capability demonstrated is:

**Monitor → Detect → Alert → Triage → Investigate → Assess → Respond → Document**

This procedure should be repeatable for different authorized laboratory scenarios.

---

## 36. Next Step

After completing the general laboratory procedure, continue with:

**11-Scenarios.md**

The next document will define structured hands-on SOC investigation scenarios that can be executed inside the Wazuh laboratory.
