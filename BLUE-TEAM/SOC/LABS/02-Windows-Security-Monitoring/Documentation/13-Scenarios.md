# Security Monitoring Scenarios

## Purpose

This document contains controlled security monitoring scenarios for the Windows Security Monitoring Lab.

The scenarios are designed to demonstrate the complete defensive workflow:

**Generate → Collect → Detect → Analyze → Investigate → Respond → Verify → Document**

All activities must be performed only against the authorized Windows lab environment.

---

# Scenario Objectives

The objectives are to practice:

* Windows security event generation
* Wazuh log collection
* Detection rule validation
* Alert triage
* Event correlation
* Authentication monitoring
* Process monitoring
* PowerShell monitoring
* Incident investigation
* Incident response
* Evidence collection
* Timeline construction
* SOC documentation

---

# Scenario 1 — Repeated Failed Authentication

## Objective

Detect and investigate repeated failed Windows authentication attempts.

## Activity

Generate multiple controlled failed authentication attempts against a test account.

Expected event:

```
Event ID: 4625
```

## Investigation

Review:

* Username
* Source IP
* Workstation
* Logon type
* Timestamp
* Number of failures
* Time interval

## Wazuh Search

```
win.system.eventID:4625
```

## Expected Analysis

A single failed login may be normal.

Multiple failures involving the same account and source within a short period should be investigated.

## Evidence

Capture:

* Wazuh alert
* Event details
* Username
* Source
* Timestamp
* Detection rule

## Expected Result

The analyst should be able to determine whether the activity is:

```
Benign
Suspicious
Potentially malicious
```

---

# Scenario 2 — Failed Authentication Followed by Successful Login

## Objective

Investigate whether repeated failed authentication attempts were followed by a successful session.

## Activity

Generate:

```
4625
4625
4624
```

## Investigation

Correlate:

* Username
* Source
* Timestamp
* Logon type
* Logon ID

## Wazuh Searches

```
win.system.eventID:4625

win.system.eventID:4624
```

## Investigation Sequence

```
Failed Logon
     ↓
Failed Logon
     ↓
Successful Logon
     ↓
Investigate Session
     ↓
Review Subsequent Activity
```

## Expected Result

The analyst should determine whether the successful login was expected and whether suspicious activity occurred afterward.

---

# Scenario 3 — Privileged Logon

## Objective

Monitor and investigate privileged authentication activity.

## Activity

Use an authorized administrative test account.

Expected events:

```
4624
4672
```

## Investigation

Review:

* Account
* Source
* Logon ID
* Timestamp
* Privileges
* Subsequent process activity

## Wazuh Searches

```
win.system.eventID:4624

win.system.eventID:4672
```

## Correlation

```
4624
   +
4672
   ↓
Investigate Processes
   ↓
Investigate PowerShell
```

## Expected Result

Determine whether the privileged session was legitimate and authorized.

---

# Scenario 4 — Process Creation

## Objective

Investigate Windows process creation telemetry.

## Activity

Launch a controlled process.

Example:

```
cmd.exe
```

Execute:

```
whoami
```

Expected event:

```
Windows Security Event 4688
```

If Sysmon is configured:

```
Sysmon Event ID 1
```

## Wazuh Searches

```
win.system.eventID:4688

win.system.eventID:1
```

## Investigation

Review:

* Process name
* Executable path
* Command line
* Parent process
* User
* Timestamp
* Process ID

## Expected Result

The analyst should reconstruct the process execution context.

---

# Scenario 5 — Parent-Child Process Analysis

## Objective

Understand how parent-child relationships improve process investigation.

## Activity

Generate a controlled process chain.

Example:

```
explorer.exe
     ↓
powershell.exe
     ↓
cmd.exe
     ↓
whoami.exe
```

## Investigation

Determine:

* Parent process
* Child process
* User
* Command line
* Execution time

## Expected Result

The analyst should identify whether the process chain is expected for the generated activity.

---

# Scenario 6 — PowerShell Monitoring

## Objective

Investigate PowerShell activity using Windows PowerShell telemetry and process events.

## Activity

Execute controlled commands:

```
whoami

ipconfig
```

Expected telemetry may include:

```
400
403
4103
4104
4688
```

If Sysmon is configured:

```
Sysmon Event ID 1
```

## Wazuh Searches

```
win.system.eventID:4104

win.system.eventID:4688 AND win.eventdata.newProcessName:*powershell.exe*
```

## Investigation

Review:

* User
* Parent process
* Command line
* Script block
* Timestamp
* Process relationship

## Expected Result

Determine whether the PowerShell activity is normal administrative/lab activity.

---

# Scenario 7 — Suspicious PowerShell Simulation

## Objective

Practice investigating PowerShell activity that appears suspicious without executing harmful payloads.

## Activity

Use harmless commands that contain unusual command-line characteristics for detection testing.

Examples:

```
powershell.exe -NoProfile

powershell.exe -ExecutionPolicy Bypass -Command "Get-Date"
```

These are used only as controlled detection-test examples in the authorized lab.

## Investigation

Review:

* Command line
* Parent process
* User
* Timestamp
* Script block
* Related authentication

## Wazuh Searches

```
win.system.eventID:4104

win.system.eventID:4688
```

## Expected Result

The analyst should distinguish:

**Suspicious-looking behavior**

from

**Confirmed malicious activity**

The presence of one indicator does not automatically prove compromise.

---

# Scenario 8 — Account Creation

## Objective

Monitor creation of a new Windows account.

## Activity

Create a dedicated test account in the authorized Windows lab.

Expected event:

```
Event ID: 4720
```

## Investigation

Review:

* New account name
* Creator
* Timestamp
* Domain
* Related privileges

## Wazuh Search

```
win.system.eventID:4720
```

## Follow-Up Investigation

Search for subsequent activity involving the new account:

```
4624

4625

4672
```

## Expected Result

Determine whether the account creation was authorized.

---

# Scenario 9 — Account Modification

## Objective

Investigate changes to an existing Windows account.

## Activity

Perform a controlled modification to the test account.

Expected event:

```
Event ID: 4738
```

## Investigation

Review:

* Account
* Modifier
* Timestamp
* Changed attributes
* Related authentication

## Wazuh Search

```
win.system.eventID:4738
```

## Expected Result

Identify who modified the account and determine whether the change was expected.

---

# Scenario 10 — Account Lockout

## Objective

Investigate an account lockout caused by repeated authentication failures.

## Activity

Generate controlled failed authentication attempts against the test account until the lab policy produces a lockout.

Expected event:

```
Event ID: 4740
```

## Investigation

Review:

* Locked account
* Timestamp
* Source/workstation
* Previous 4625 events

## Wazuh Searches

```
win.system.eventID:4740

win.system.eventID:4625
```

## Correlation

```
4625
   ↓
4625
   ↓
4625
   ↓
4740
   ↓
Investigate Source
```

## Expected Result

Determine whether the lockout was caused by expected lab activity.

---

# Scenario 11 — Authentication to Process Correlation

## Objective

Determine what happened after a user successfully authenticated.

## Activity

Generate:

```
4624
   ↓
4688
```

## Investigation

Correlate:

* User
* Logon ID
* Process
* Timestamp
* Parent process

## Wazuh Searches

```
win.system.eventID:4624

win.system.eventID:4688
```

## Expected Result

Build a short timeline from authentication to process execution.

---

# Scenario 12 — Authentication to PowerShell Correlation

## Objective

Investigate PowerShell activity following user authentication.

## Activity

Generate:

```
4624
   ↓
4688
   ↓
4104
```

## Investigation

Determine:

* Which user authenticated?
* Which process launched PowerShell?
* What PowerShell activity occurred?
* Was the activity expected?

## Expected Result

Demonstrate user → authentication → process → PowerShell correlation.

---

# Scenario 13 — Privileged Logon to PowerShell

## Objective

Investigate PowerShell activity initiated from a privileged session.

## Activity

Generate:

```
4624
   ↓
4672
   ↓
4688
   ↓
4104
```

## Investigation

Review the complete sequence.

Important questions:

* Was the account authorized?
* Was the privileged session expected?
* Who launched PowerShell?
* What command was executed?
* Was the activity part of normal administration?

## Expected Result

Demonstrate higher-context investigation of privileged PowerShell activity.

---

# Scenario 14 — Full Incident Investigation

## Objective

Perform a complete investigation using multiple telemetry sources.

## Activity

Generate the following controlled sequence:

```
4625
   ↓
4625
   ↓
4624
   ↓
4672
   ↓
4688
   ↓
4104
```

## Investigation Workflow

```
Alert
  ↓
Validate
  ↓
Identify Endpoint
  ↓
Identify User
  ↓
Review Authentication
  ↓
Review Privileges
  ↓
Review Process
  ↓
Review PowerShell
  ↓
Build Timeline
  ↓
Assess Impact
  ↓
Decide Response
  ↓
Document
```

## Expected Result

Produce a complete investigation report explaining whether the sequence represents:

```
Authorized Lab Activity
```

or:

```
Suspicious Activity
```

---

# Scenario 15 — Incident Response Simulation

## Objective

Practice the complete incident response lifecycle.

## Activity

Use a controlled test condition that generates suspicious telemetry.

## Workflow

```
Detect
  ↓
Validate
  ↓
Investigate
  ↓
Contain
  ↓
Eradicate
  ↓
Recover
  ↓
Verify
  ↓
Document
```

## Controlled Containment Examples

Depending on the scenario:

* Stop a test process.
* Disable a dedicated test account.
* Disconnect the test endpoint from the isolated lab network.

## Eradication

Remove the test condition.

Examples:

* Remove test account.
* Remove test artifacts.
* Restore modified configuration.
* Stop test processes.

## Recovery

Restore the endpoint to its expected lab state.

## Verification

Confirm:

* Wazuh Agent is operational.
* Windows logging is operational.
* Security telemetry is still collected.
* No unexpected test activity remains.

---

# Scenario 16 — Detection Failure Investigation

## Objective

Understand the difference between collection failure and detection failure.

## Activity

Generate a known Windows event.

Example:

```
Event ID 4625
```

## Investigation

First verify the event locally in Windows Event Viewer.

Then verify Wazuh receives the event.

### Case A — Event Exists Locally but Not in Wazuh

Likely investigation area:

```
Collection Pipeline
```

Check:

* Wazuh Agent
* `ossec.conf`
* Event channel
* Agent connectivity
* Agent restart
* Manager ingestion

### Case B — Event Exists in Wazuh but No Alert

Likely investigation area:

```
Detection Rule
```

Check:

* Rule condition
* Event fields
* Rule ID
* Rule syntax
* Rule testing
* Detection thresholds

## Expected Result

Demonstrate that:

**Collection ≠ Detection**

---

# Scenario 17 — False Positive Investigation

## Objective

Practice identifying legitimate activity that triggers a detection.

## Activity

Generate expected administrative PowerShell or authentication activity.

## Investigation

Determine:

* Why the rule triggered
* Whether the activity was authorized
* Which fields caused the match
* Whether the rule is too broad

## Outcome

Possible dispositions:

```
False Positive
Benign Activity
Detection Tuning Required
```

## Expected Result

Document why the alert should not be escalated as a security incident.

---

# Scenario 18 — Detection Tuning

## Objective

Improve detection quality without unnecessarily reducing visibility.

## Activity

Identify a detection generating repeated benign alerts.

## Investigation

Review:

* Rule condition
* Event frequency
* User
* Process
* Source
* Baseline
* Expected administrative behavior

## Tuning Options

Possible approaches:

* Add contextual fields.
* Adjust thresholds.
* Add exclusions for known legitimate activity.
* Improve correlation.
* Increase required event count.
* Reduce overly broad matching.

## Expected Result

Reduce false positives while preserving meaningful detection coverage.

---

# Scenario 19 — Timeline Reconstruction

## Objective

Create a complete event timeline from multiple Windows events.

## Activity

Use generated events from the previous scenarios.

## Timeline

Create a table:

| Time     | Event ID | Activity         | User     | Source     | Assessment  |
| -------- | -------: | ---------------- | -------- | ---------- | ----------- |
| 10:00:01 |     4625 | Failed logon     | testuser | Lab source | Suspicious  |
| 10:00:03 |     4625 | Failed logon     | testuser | Lab source | Suspicious  |
| 10:00:06 |     4624 | Successful logon | testuser | Lab source | Investigate |
| 10:00:07 |     4672 | Privileged logon | testuser | Lab source | Investigate |
| 10:00:15 |     4688 | PowerShell       | testuser | Local      | Investigate |
| 10:00:16 |     4104 | Script block     | testuser | Local      | Investigate |

## Expected Result

The analyst should be able to reconstruct the complete sequence.

---

# Scenario 20 — End-to-End SOC Workflow

## Objective

Demonstrate the complete capability developed through this lab.

## Workflow

```
Windows Activity
      ↓
Event Generation
      ↓
Log Collection
      ↓
Wazuh
      ↓
Detection
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
Incident Decision
      ↓
Response
      ↓
Verification
      ↓
Documentation
```

## Required Evidence

Capture:

* Windows Event Viewer evidence
* Wazuh alert
* Wazuh event details
* Detection rule
* Related events
* Investigation timeline
* Response action
* Verification
* Final report

## Expected Result

Demonstrate the ability to perform a complete entry-level SOC workflow using a Windows endpoint and Wazuh.

---

# Scenario Validation Matrix

| Scenario                        | Detection | Investigation | Correlation | Response | Documentation |
| ------------------------------- | --------- | ------------- | ----------- | -------- | ------------- |
| Failed authentication           | ✓         | ✓             | ✓           | ✓        | ✓             |
| Successful login after failures | ✓         | ✓             | ✓           | ✓        | ✓             |
| Privileged logon                | ✓         | ✓             | ✓           | ✓        | ✓             |
| Process creation                | ✓         | ✓             | ✓           | ✓        | ✓             |
| Process tree                    | ✓         | ✓             | ✓           | ✓        | ✓             |
| PowerShell                      | ✓         | ✓             | ✓           | ✓        | ✓             |
| Account creation                | ✓         | ✓             | ✓           | ✓        | ✓             |
| Account modification            | ✓         | ✓             | ✓           | ✓        | ✓             |
| Account lockout                 | ✓         | ✓             | ✓           | ✓        | ✓             |
| Full incident                   | ✓         | ✓             | ✓           | ✓        | ✓             |
| False positive                  | ✓         | ✓             | ✓           | —        | ✓             |
| Detection tuning                | ✓         | ✓             | ✓           | —        | ✓             |
| Timeline reconstruction         | ✓         | ✓             | ✓           | —        | ✓             |
| End-to-end SOC workflow         | ✓         | ✓             | ✓           | ✓        | ✓             |

---

# Evidence Structure

Store scenario evidence under:

```
Evidence/
```

Recommended naming:

```
Evidence/
├── Scenario-01-Failed-Authentication/
├── Scenario-02-Authentication-Correlation/
├── Scenario-03-Privileged-Logon/
├── Scenario-04-Process-Creation/
├── Scenario-05-Process-Tree/
├── Scenario-06-PowerShell/
├── Scenario-07-Suspicious-PowerShell/
├── Scenario-08-Account-Creation/
├── Scenario-09-Account-Modification/
├── Scenario-10-Account-Lockout/
└── Scenario-20-End-to-End/
```

---

# Scenario Report Structure

Each significant scenario should be documented with:

```
Scenario Name
Objective
Lab Setup
Activity Performed
Expected Telemetry
Actual Telemetry
Wazuh Detection
Investigation
Timeline
Findings
Response
Verification
Evidence
Lessons Learned
```

---

# Scenario Success Criteria

A scenario is considered successful when the analyst can:

* Generate the expected activity.
* Confirm Windows telemetry.
* Confirm Wazuh collection.
* Trigger or observe the appropriate detection.
* Investigate the alert.
* Correlate related events.
* Build a timeline where applicable.
* Determine the security significance.
* Perform an appropriate controlled response.
* Verify the result.
* Preserve evidence.
* Document the findings.

---

# Safety and Authorization

All scenarios in this document are intended for an isolated, authorized home lab.

Do not perform these activities against:

* Systems you do not own.
* Systems without explicit authorization.
* Production environments.
* Public infrastructure.
* Third-party accounts.

Use dedicated test accounts and isolated virtual machines wherever possible.

The purpose of this lab is defensive security monitoring and incident-response practice.

---

# Professional SOC Relevance

These scenarios demonstrate practical SOC capabilities rather than only theoretical knowledge.

The most important skill demonstrated by this lab is the ability to connect:

**Telemetry → Detection → Investigation → Decision → Response**

A strong SOC analyst should be able to explain not only that an alert occurred, but also:

* What generated it.
* Why it was detected.
* Which endpoint was involved.
* Which user was involved.
* What happened before the alert.
* What happened after the alert.
* Whether the activity was legitimate.
* Whether the incident requires escalation.
* What response should be taken.
* How the result was verified.

---

# Conclusion

The Windows Security Monitoring Lab uses controlled scenarios to transform individual Windows security events into realistic SOC investigation exercises.

The complete workflow is:

**Generate → Collect → Detect → Analyze → Investigate → Respond → Verify → Document**

The scenarios progressively develop skills in:

* Authentication monitoring
* Process monitoring
* PowerShell monitoring
* Account monitoring
* Event correlation
* Alert investigation
* Incident response
* Detection troubleshooting
* False-positive analysis
* Timeline reconstruction
* SOC documentation

The final objective is to demonstrate a complete defensive monitoring capability using a Windows endpoint and Wazuh.

---

## Related Documentation

* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-PowerShell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
