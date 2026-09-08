# Troubleshooting

## Purpose

Troubleshooting is the process of identifying, isolating, and resolving problems that prevent the Windows Security Monitoring Lab from working as expected.

In this lab, troubleshooting focuses on the complete monitoring pipeline:

**Windows Activity → Event Generation → Windows Logs → Wazuh Agent → Wazuh Manager → Detection → Alert → Investigation**

The objective is not only to fix the problem, but also to determine **where the monitoring pipeline failed**.

---

# Troubleshooting Objectives

The primary objectives are:

* Verify Windows security logging.
* Verify PowerShell logging.
* Verify Sysmon telemetry.
* Verify Wazuh Agent connectivity.
* Verify Wazuh log collection.
* Verify Wazuh Manager ingestion.
* Verify detection rules.
* Identify collection failures.
* Identify detection failures.
* Reduce false positives.
* Restore monitoring functionality.
* Document troubleshooting steps and results.

---

# Troubleshooting Methodology

Use a layered troubleshooting approach:

```
1. Generate Event
       ↓
2. Verify Windows Log
       ↓
3. Verify Wazuh Agent
       ↓
4. Verify Collection
       ↓
5. Verify Wazuh Manager
       ↓
6. Verify Detection Rule
       ↓
7. Verify Alert
       ↓
8. Investigate Result
```

Do not immediately modify detection rules when the underlying event was never collected.

---

# Troubleshooting Decision Tree

```
Event Generated?
      │
   No ─┴─ Yes
   │         ↓
Fix Event   Event Visible in Windows?
Generation       │
              No ┴ Yes
              │     ↓
          Fix Logging   Event Visible in Wazuh?
                          │
                       No ┴ Yes
                       │     ↓
                   Fix Collection   Alert Generated?
                                      │
                                   No ┴ Yes
                                   │     ↓
                               Fix Detection   Continue Investigation
```

---

# Problem Classification

Most problems in this lab fall into one of five categories.

| Category         | Example                                 |
| ---------------- | --------------------------------------- |
| Event Generation | Expected event is not created           |
| Windows Logging  | Event log is disabled or incomplete     |
| Collection       | Wazuh does not receive the event        |
| Detection        | Event arrives but no alert is generated |
| Investigation    | Alert exists but analysis is incomplete |

This distinction is critical.

---

# Basic Health Checks

Before troubleshooting an individual event, verify the overall lab.

Check:

* Windows VM is running.
* Network connectivity is available.
* Wazuh Agent is running.
* Wazuh Manager is running.
* Agent is connected.
* Windows Event Logs are functioning.
* PowerShell logging is configured.
* Sysmon is running if used.
* Wazuh dashboard is accessible.

---

# Windows Event Log Troubleshooting

## Verify Event Viewer

Open:

```
Event Viewer
```

Navigate to:

```
Windows Logs
    ├── Security
    ├── System
    └── Application
```

For PowerShell:

```
Applications and Services Logs
    └── Microsoft
        └── Windows PowerShell
            └── Operational
```

For Sysmon:

```
Applications and Services Logs
    └── Microsoft
        └── Windows
            └── Sysmon
                └── Operational
```

---

# Security Log Troubleshooting

Expected security events include:

```
4624
4625
4634
4672
4688
4720
4738
4740
```

If an expected event is missing:

1. Verify the activity was actually generated.
2. Check the Security log.
3. Verify audit policy.
4. Confirm the event category is enabled.
5. Generate the activity again.
6. Recheck the log.

---

# Windows Audit Policy Troubleshooting

Open:

```
Local Security Policy
```

Navigate to:

```
Advanced Audit Policy Configuration
    ↓
System Audit Policies
```

Review relevant categories such as:

* Logon/Logoff
* Account Management
* Detailed Tracking
* Policy Change

The exact available settings depend on Windows edition and configuration.

After changing audit settings, generate a new test event rather than relying on historical events.

---

# Wazuh Agent Troubleshooting

The Windows Wazuh Agent configuration is commonly located at:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Verify that the configuration contains the required event-channel collection entries.

Example:

```
<localfile>
  <location>Security</location>
  <log_format>eventchannel</log_format>
</localfile>
```

---

# Verify Wazuh Agent Service

Run PowerShell as Administrator:

```
Get-Service -Name wazuh
```

Expected state:

```
Running
```

If the service is stopped:

```
Start-Service -Name wazuh
```

After configuration changes:

```
Restart-Service -Name wazuh
```

---

# Verify Agent Connectivity

Check the Wazuh dashboard for the Windows agent.

Verify:

* Agent is registered.
* Agent is active.
* Agent has recent communication.
* Agent is associated with the expected endpoint.

If the agent is disconnected, investigate connectivity before investigating detection rules.

---

# Wazuh Collection Troubleshooting

If an event exists in Windows but not in Wazuh, investigate the collection pipeline.

Check:

1. Windows Event Log
2. Wazuh Agent configuration
3. Event channel name
4. `eventchannel` log format
5. Agent service status
6. Agent connectivity
7. Wazuh Manager ingestion

Example collection configuration:

```
<localfile>
  <location>System</location>
  <log_format>eventchannel</log_format>
</localfile>
```

---

# PowerShell Collection Troubleshooting

Verify the PowerShell Operational channel:

```
Microsoft-Windows-PowerShell/Operational
```

Verify expected events:

```
400
403
4103
4104
```

Verify Wazuh configuration:

```
<localfile>
  <location>Microsoft-Windows-PowerShell/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Restart the Wazuh Agent after configuration changes:

```
Restart-Service -Name wazuh
```

Then generate new PowerShell activity and verify the event locally before checking Wazuh.

---

# Sysmon Troubleshooting

Verify that Sysmon is installed and running.

Check:

```
Services
```

and:

```
Event Viewer
    ↓
Applications and Services Logs
    ↓
Microsoft
    ↓
Windows
    ↓
Sysmon
    ↓
Operational
```

Verify:

```
Event ID 1
Process Creation
```

If Sysmon events are missing:

* Verify Sysmon service.
* Verify Sysmon configuration.
* Generate a new process.
* Check the Sysmon Operational log.
* Verify Wazuh collection.

---

# Wazuh Detection Troubleshooting

A common situation is:

```
Windows Event
     ↓
Wazuh Event
     ↓
No Alert
```

This indicates that collection may be working while detection may not be.

Check:

* Rule ID
* Rule condition
* Event fields
* Event ID
* Rule level
* Rule syntax
* Rule placement
* Rule loading
* Detection thresholds

---

# Collection vs Detection Failure

This distinction is extremely important.

### Collection Failure

```
Event exists in Windows
         ↓
Event does NOT appear in Wazuh
```

Likely problem:

**Collection**

### Detection Failure

```
Event exists in Windows
         ↓
Event appears in Wazuh
         ↓
No alert
```

Likely problem:

**Detection rule**

### Investigation Failure

```
Alert exists
     ↓
Analyst cannot determine context
```

Likely problem:

**Investigation process**

---

# Custom Rule Troubleshooting

Custom Wazuh rules are commonly stored in:

```
/var/ossec/etc/rules/local_rules.xml
```

Do not modify the default Wazuh ruleset when a custom rule can be used instead.

After changing a rule:

1. Save the configuration.
2. Validate the rule.
3. Test the rule.
4. Restart/reload the relevant Wazuh service as appropriate.
5. Generate a new test event.
6. Verify the resulting alert.

---

# Rule Testing

Wazuh provides:

```
/var/ossec/bin/wazuh-logtest
```

Use it to test how Wazuh processes an event and whether the expected rule matches.

The purpose is to determine:

* Which decoder processes the event.
* Which fields are extracted.
* Which rule matches.
* Why a rule does or does not trigger.

This is especially useful when a detection rule appears logically correct but does not generate an alert.

---

# Rule Troubleshooting Checklist

Check:

* [ ] Correct event ID
* [ ] Correct field name
* [ ] Correct event channel
* [ ] Correct rule syntax
* [ ] Unique rule ID
* [ ] Appropriate rule level
* [ ] Correct rule file
* [ ] Rule successfully loaded
* [ ] Event actually reaches Wazuh
* [ ] Rule condition matches the real event

---

# Field Troubleshooting

Do not assume that the field name you expect is identical to the field name available in the actual Wazuh event.

Inspect the actual event.

Examples of Windows fields may include:

```
win.system.eventID
win.system.providerName
win.system.channel
win.eventdata.targetUserName
win.eventdata.subjectUserName
win.eventdata.ipAddress
win.eventdata.commandLine
win.eventdata.newProcessName
win.eventdata.parentProcessName
```

Field availability depends on the event and Wazuh parsing.

---

# Wazuh Search Troubleshooting

If a search produces no result:

### Step 1

Verify the event exists in Windows.

### Step 2

Verify the event reaches Wazuh.

### Step 3

Search using the event ID.

Example:

```
win.system.eventID:4625
```

### Step 4

Expand the time range.

### Step 5

Search by endpoint or username.

### Step 6

Inspect the actual event fields.

### Step 7

Adjust the search based on the fields present in the event.

---

# Authentication Troubleshooting

Expected events:

```
4624
4625
4634
4672
4740
```

If authentication events are missing:

* Verify the activity occurred.
* Check Security log.
* Verify audit policy.
* Check Wazuh Security collection.
* Restart the agent if configuration changed.
* Generate a new authentication event.

---

# Process Monitoring Troubleshooting

Expected:

```
4688
```

and, if Sysmon is configured:

```
Sysmon Event 1
```

If process events are missing:

1. Generate a new process.
2. Check Windows Security log.
3. Check Sysmon Operational log.
4. Verify audit policy.
5. Verify Wazuh collection.
6. Verify event fields.

---

# PowerShell Troubleshooting

Expected telemetry may include:

```
400
403
4103
4104
```

If `4104` is missing:

* Verify Script Block Logging.
* Check PowerShell Operational log.
* Confirm the test command actually executed.
* Generate a new PowerShell activity.
* Check Wazuh collection.

Do not assume that every PowerShell execution will produce every PowerShell event.

---

# Time Synchronization

Accurate timestamps are critical for event correlation.

If timestamps appear inconsistent:

Check:

* Windows system time
* Wazuh Manager time
* Time zone
* VM time synchronization
* NTP configuration where available

Incorrect time can produce an incorrect incident timeline.

---

# Network Connectivity Troubleshooting

If the Wazuh Agent is disconnected:

Check:

* Windows network adapter
* Virtual machine network configuration
* IP address
* Routing
* Firewall
* Wazuh Manager availability

Basic Windows checks:

```
ipconfig

ping <WAZUH-MANAGER-IP>
```

Use only the appropriate connectivity tests for the isolated lab network.

---

# Firewall Troubleshooting

A firewall can interfere with communication between the Windows Agent and Wazuh Manager.

Check:

* Windows Defender Firewall
* Virtual network configuration
* Wazuh Manager connectivity
* Required communication paths

Do not permanently disable security controls merely to make the lab work.

Prefer identifying and correcting the specific connectivity issue.

---

# Agent Configuration Troubleshooting

After modifying:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

check for:

* XML syntax errors
* Incorrect event channel names
* Duplicate configuration
* Incorrect log format
* Unsupported configuration
* Missing closing tags

Then restart:

```
Restart-Service -Name wazuh
```

Always verify that the agent returns to a healthy state after configuration changes.

---

# Common Problems and Solutions

| Problem                            | Likely Cause                | Investigation                |
| ---------------------------------- | --------------------------- | ---------------------------- |
| No Windows event                   | Audit/logging configuration | Check Event Viewer           |
| Event exists locally but not Wazuh | Collection problem          | Check Agent configuration    |
| Agent disconnected                 | Connectivity/service issue  | Check service and network    |
| PowerShell events missing          | Logging configuration       | Check PowerShell Operational |
| Sysmon events missing              | Sysmon/configuration        | Check Sysmon Operational     |
| Event reaches Wazuh but no alert   | Detection rule              | Test rule                    |
| Search returns nothing             | Wrong field/time range      | Inspect actual event         |
| Timeline is inconsistent           | Time synchronization        | Check clocks                 |
| Too many alerts                    | Broad detection             | Tune rule                    |
| Expected alert missing             | Incorrect rule condition    | Inspect event fields         |

---

# Troubleshooting Scenarios

## Scenario 1 — Event Viewer Shows 4625 but Wazuh Does Not

### Observation

```
Windows Event Viewer
      ↓
4625 exists

Wazuh
      ↓
4625 missing
```

### Diagnosis

Likely collection failure.

### Investigation

Check:

* Security collection
* Agent status
* `ossec.conf`
* Wazuh connectivity

---

## Scenario 2 — Wazuh Shows 4625 but No Alert

### Observation

```
Windows
   ↓
4625
   ↓
Wazuh
   ↓
Event visible
   ↓
No detection
```

### Diagnosis

Likely detection rule problem.

### Investigation

Check:

* Event fields
* Rule ID
* Rule condition
* Rule loading
* Rule testing

---

## Scenario 3 — PowerShell Works Locally but Not in Wazuh

### Observation

```
PowerShell Operational
     ↓
4104 exists

Wazuh
     ↓
4104 missing
```

### Diagnosis

Likely collection configuration issue.

### Investigation

Check:

```
Microsoft-Windows-PowerShell/Operational
```

and:

```
<log_format>eventchannel</log_format>
```

---

## Scenario 4 — Wazuh Alert Has Unexpected Fields

### Observation

The event is detected, but expected fields are missing or named differently.

### Diagnosis

The actual event structure differs from the assumed field mapping.

### Action

Inspect the complete event and update the investigation or detection logic based on the real telemetry.

---

## Scenario 5 — Too Many Alerts

### Observation

A detection generates excessive alerts during normal lab activity.

### Diagnosis

Possible false-positive or overly broad detection.

### Action

Review:

* Baseline
* Event frequency
* Rule conditions
* User context
* Process context

Then tune the detection carefully.

---

# Troubleshooting Evidence

Document troubleshooting evidence under:

```
Evidence/
```

Capture:

* Original problem
* Event Viewer evidence
* Wazuh status
* Configuration evidence
* Error messages
* Rule testing results
* Corrective action
* Verification result

Example:

```
Evidence/
└── Troubleshooting/
    ├── event-viewer.png
    ├── wazuh-agent-status.png
    ├── configuration.png
    └── verification.png
```

---

# Troubleshooting Report

For significant problems, document:

```
Reports/Troubleshooting-Report.md
```

Recommended structure:

```
Problem
Symptoms
Expected Behavior
Observed Behavior
Investigation
Root Cause
Corrective Action
Verification
Evidence
Lessons Learned
```

---

# Troubleshooting Checklist

## Windows

* [ ] Windows VM running
* [ ] Event Viewer accessible
* [ ] Security log operational
* [ ] System log operational
* [ ] PowerShell Operational log operational
* [ ] Sysmon Operational log operational if configured
* [ ] Audit policy verified

## Wazuh Agent

* [ ] Agent installed
* [ ] Agent service running
* [ ] Agent connected
* [ ] `ossec.conf` verified
* [ ] Event channels configured
* [ ] Agent restarted after configuration changes

## Wazuh Manager

* [ ] Manager available
* [ ] Agent visible
* [ ] Events arriving
* [ ] Detection rules loaded
* [ ] Custom rules tested

## Detection

* [ ] Correct Event ID
* [ ] Correct field
* [ ] Correct rule syntax
* [ ] Rule ID unique
* [ ] Detection tested
* [ ] False positives reviewed

## Investigation

* [ ] Endpoint identified
* [ ] User identified
* [ ] Source identified
* [ ] Timeline verified
* [ ] Related events correlated
* [ ] Evidence collected

---

# Troubleshooting Best Practices

Follow these principles:

### 1. Start at the Source

Verify that Windows actually generated the expected telemetry.

### 2. Work Layer by Layer

Do not jump directly from a missing alert to a detection-rule change.

### 3. Inspect Real Data

Use actual event fields rather than assumptions.

### 4. Change One Thing at a Time

This makes it easier to identify the actual cause.

### 5. Test After Every Change

Generate new activity and verify the result.

### 6. Preserve Evidence

Record the original problem and the solution.

### 7. Avoid Destructive Fixes

Do not disable security controls simply to bypass the problem.

### 8. Document Root Cause

A working system is not enough; understand why it failed.

---

# Professional SOC Relevance

Troubleshooting is an important SOC skill because monitoring systems are not useful if telemetry silently stops working.

A SOC analyst should be able to distinguish:

**Event Generation Problem**

from:

**Logging Problem**

from:

**Collection Problem**

from:

**Detection Problem**

from:

**Investigation Problem**

The practical troubleshooting model is:

```
Source
  ↓
Telemetry
  ↓
Collection
  ↓
Detection
  ↓
Alert
  ↓
Investigation
```

This helps analysts avoid wasting time investigating the wrong layer.

---

# Conclusion

Troubleshooting ensures that the Windows Security Monitoring Lab remains reliable and that security telemetry can be trusted during investigation.

The core troubleshooting principle is:

**Verify → Isolate → Diagnose → Fix → Test → Verify → Document**

The most important distinction is:

```
Event exists in Windows
        ↓
Is it collected by Wazuh?
        ↓
Is it detected?
        ↓
Can it be investigated?
```

A professional SOC analyst should be able to identify exactly where the monitoring pipeline fails and restore it without unnecessarily weakening security controls.

---

## Related Documentation

* `03-Windows-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-PowerShell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `15-Lessons-Learned.md`
