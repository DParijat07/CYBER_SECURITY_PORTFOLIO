# Log Collection

## Purpose

The purpose of this document is to explain how Windows security telemetry is collected from the monitoring endpoint and made available for security monitoring, analysis, and investigation.

Effective log collection ensures that security events generated on the Windows endpoint are available to the SOC analyst.

---

## Log Collection Objectives

The collection process should provide useful telemetry for:

* Authentication activity
* Account activity
* Privileged activity
* Process execution
* PowerShell activity
* System activity
* Application activity
* Sysmon telemetry
* Other security-relevant endpoint events

The objective is to collect the required telemetry first and then use that telemetry for security analysis and detection.

---

# Lab-Specific Collection Configuration

## Lab Environment

The Windows Security Monitoring Lab uses the following architecture:

```
Windows Monitoring VM
        │
        │ Windows Event Logs
        ▼
   Wazuh Agent
        │
        │ Log Collection
        ▼
   Wazuh Manager
        │
        │ Collected Telemetry
        ▼
   Security Analysis
```

The Windows VM is the primary monitored endpoint.

The Wazuh agent collects configured Windows event channels and forwards the telemetry to the Wazuh manager.

---

## Wazuh Agent Configuration File

The Windows Wazuh agent configuration file is:

`C:\Program Files (x86)\ossec-agent\ossec.conf`

Wazuh uses the `<localfile>` configuration section to define log sources. For Windows Event Channels, the `log_format` should be set to `eventchannel`.

Before modifying the configuration file:

1. Create a backup of `ossec.conf`.
2. Open the file with administrative privileges.
3. Add the required `<localfile>` blocks inside the `<ossec_config>` section.
4. Save the configuration.
5. Restart the Wazuh agent.
6. Verify that telemetry is being collected.

---

# Actual Wazuh Collection Configuration

The following configuration is the baseline collection configuration for this Windows Security Monitoring Lab.

Add these blocks inside the Wazuh agent's `<ossec_config>` section:

```
<!-- Windows Security Event Log -->
<localfile>
  <location>Security</location>
  <log_format>eventchannel</log_format>
</localfile>

<!-- Windows System Event Log -->
<localfile>
  <location>System</location>
  <log_format>eventchannel</log_format>
</localfile>

<!-- Windows Application Event Log -->
<localfile>
  <location>Application</location>
  <log_format>eventchannel</log_format>
</localfile>

<!-- PowerShell Operational Log -->
<localfile>
  <location>Microsoft-Windows-PowerShell/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>

<!-- Sysmon Operational Log -->
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

These are collection blocks only. They tell the Wazuh agent **which Windows event channels to collect**. They do not create custom detection rules. Wazuh documents the same `eventchannel` approach for Windows Event Channels, PowerShell, and Sysmon.

---

## Recommended Lab Configuration

For the initial Windows monitoring lab, the recommended collection scope is:

| Windows Channel        |          Collect? | Purpose                                              |
| ---------------------- | ----------------: | ---------------------------------------------------- |
| Security               |               Yes | Authentication, accounts, privileges, process events |
| System                 |               Yes | System and service activity                          |
| Application            |               Yes | Application-related events                           |
| PowerShell/Operational |               Yes | PowerShell telemetry                                 |
| Sysmon/Operational     | Yes, if installed | Enhanced endpoint telemetry                          |

The Sysmon channel should only be configured if Sysmon is installed on the Windows endpoint.

---

# Optional Event Filtering

Wazuh can also filter Windows Event Channel data using the `<query>` option.

For example, the following configuration collects only specific Security events:

```
<localfile>
  <location>Security</location>
  <log_format>eventchannel</log_format>
  <query>Event/System[EventID = 4625]</query>
</localfile>
```

This example collects failed logon events with:

`Event ID 4625`

Wazuh supports XPath-style queries for filtering Windows Event Channel events.

However, **do not use aggressive filtering during the initial lab setup**.

For this lab, collecting the relevant event channels first provides broader visibility and makes investigation and detection validation easier.

---

# Collection vs Detection

## Log Collection

**Log collection answers:**

> What telemetry did the endpoint generate?

Collection moves endpoint events from Windows to the monitoring platform.

Example:

```
User Login
     ↓
Windows generates Event ID 4624
     ↓
Security Event Log
     ↓
Wazuh Agent
     ↓
Wazuh Manager
     ↓
Collected Event
```

At this stage, the primary objective is:

**Visibility**

---

## Detection

**Detection answers:**

> Does the collected telemetry represent behavior that should be investigated?

Detection logic analyzes collected events and determines whether a security condition has been met.

Example:

```
Multiple Event ID 4625
         ↓
   Detection Rule
         ↓
   Threshold/Pattern
         ↓
       Alert
         ↓
   SOC Analysis
```

Detection is therefore a separate stage from collection.

---

## Important Distinction

The relationship is:

```
Endpoint Activity
      ↓
Event Generation
      ↓
LOG COLLECTION
      ↓
Collected Telemetry
      ↓
DETECTION
      ↓
Alert
      ↓
ANALYSIS
      ↓
INVESTIGATION
      ↓
RESPONSE
```

**Collection does not equal detection.**

A Windows event can be successfully collected without generating an alert.

For example:

```
Event ID 4624
Successful Logon
      ↓
Collected by Wazuh
      ↓
No suspicious condition
      ↓
No alert required
```

This is still successful log collection.

---

# Applying the Wazuh Configuration

After editing:

`C:\Program Files (x86)\ossec-agent\ossec.conf`

save the configuration and restart the Wazuh agent.

Run PowerShell as Administrator:

```
Restart-Service -Name Wazuh
```

Wazuh documents `Restart-Service -Name wazuh` as the Windows method for applying configuration changes.

---

# Collection Verification

## Step 1 — Generate Activity

Generate controlled activity on the Windows monitoring endpoint.

Examples:

* Normal user login
* Controlled failed authentication
* Normal process execution
* Benign PowerShell command

---

## Step 2 — Verify Locally

Open:

`Event Viewer`

Check the relevant event channel.

Verify:

* Event ID
* Timestamp
* Username
* Computer
* Process
* Event details

---

## Step 3 — Verify Wazuh Collection

Confirm:

1. Wazuh agent is running.
2. Wazuh agent is connected.
3. Windows event exists locally.
4. Wazuh receives the event.
5. Event information is preserved.

The objective at this stage is to verify **collection**, not necessarily alert generation.

---

# Collection Testing Scenarios

## Authentication Collection Test

Generate controlled authentication activity.

Verify:

* Successful authentication events
* Failed authentication events
* Timestamp
* Username
* Hostname
* Source information where available

The objective is to confirm that authentication telemetry reaches Wazuh.

---

## Process Collection Test

Execute a normal application.

Verify:

* Process creation event
* Process name
* Process ID
* User
* Timestamp
* Parent process where available
* Command line where configured

The objective is to confirm that process telemetry is being collected.

---

## PowerShell Collection Test

Execute a benign PowerShell command within the authorized lab environment.

Verify:

* PowerShell process activity
* PowerShell operational events
* Script Block Logging where enabled
* Module logging where enabled

The objective is to confirm PowerShell telemetry collection.

---

## Sysmon Collection Test

If Sysmon is installed:

1. Generate normal process activity.
2. Generate normal network activity.
3. Open the Sysmon operational channel.
4. Verify that expected events are present.
5. Confirm that Wazuh receives the configured Sysmon telemetry.

The Wazuh agent can collect the Sysmon operational channel using the same `<localfile>` and `eventchannel` configuration shown above.

---

# Event Integrity

Collected events should preserve important contextual information.

Important fields include:

* Timestamp
* Hostname
* Event ID
* User/account
* Source
* Process
* Command line
* IP address where available
* Event description
* Log source

Missing fields can reduce the analyst's ability to investigate an alert.

---

# Time Synchronization

Accurate timestamps are important for incident investigation.

Ensure that the Windows endpoint and monitoring infrastructure use appropriate system time settings.

Accurate time allows analysts to:

* Build reliable timelines
* Correlate multiple events
* Identify event sequences
* Compare endpoint and network activity
* Determine the order of actions

---

# Baseline Collection

Before running suspicious or controlled security scenarios, collect normal endpoint activity.

Examples:

* Normal logons
* Normal process execution
* Normal PowerShell activity
* Normal system activity
* Normal application events

The baseline provides context for later investigations.

---

# Log Filtering

Log collection and detection should be treated as separate functions.

Collection determines:

> Which telemetry should reach the monitoring platform?

Detection determines:

> Which collected telemetry should result in a security alert?

Simplified:

```
Windows Events
      ↓
Collection Configuration
      ↓
Collected Telemetry
      ↓
Detection Rules
      ↓
Alerts
```

Collection filtering can reduce unnecessary telemetry.

Detection rules identify potentially suspicious patterns within the telemetry that is available for analysis.

---

# Log Retention

The lab should retain sufficient telemetry to support investigation exercises.

Retention requirements depend on:

* Available storage
* Event volume
* Lab duration
* Investigation requirements
* Monitoring objectives

Important investigation evidence should be preserved separately when required.

---

# Troubleshooting the Collection Pipeline

If an expected event is missing, troubleshoot the collection pipeline step by step.

```
Event Generated?
      ↓
     Yes
      ↓
Visible Locally?
      ↓
     Yes
      ↓
Correct Channel?
      ↓
     Yes
      ↓
Wazuh Agent Collecting?
      ↓
     Yes
      ↓
Received by Wazuh Manager?
      ↓
     Yes
      ↓
Event Available for Analysis?
```

If the event is visible locally but unavailable in Wazuh, investigate the **collection configuration**.

If the event is available in Wazuh but does not generate an alert, investigate the **detection configuration**.

This distinction is important when troubleshooting SOC monitoring systems.

---

# Configuration Validation

After modifying the Wazuh configuration, verify that the configuration is valid before relying on the collection pipeline.

Wazuh provides configuration testing tools for its components. The relevant Wazuh log collector validation command is:

```
/var/ossec/bin/wazuh-logcollector -t
```

This command is normally run on the Wazuh component where the relevant configuration is being tested. Wazuh documents `wazuh-logcollector -t` for validating local file/log collection configuration.

For the Windows endpoint, the practical validation should additionally include:

* Restarting the Wazuh agent
* Confirming the Wazuh service is running
* Generating test events
* Confirming the events reach the Wazuh manager

---

# Evidence Requirements

Capture evidence demonstrating successful log collection.

Examples:

* `ossec.conf` collection configuration
* Windows Event Viewer
* Security events
* System events
* PowerShell events
* Sysmon events
* Wazuh agent status
* Wazuh collected event
* Event timestamps
* Relevant Event IDs
* Collection verification results

Store evidence in:

`../Evidence/`

Do not include credentials, authentication tokens, private keys, or other sensitive information in screenshots.

---

# Collection Checklist

Before moving to detection development, verify:

* [ ] Wazuh agent is installed.
* [ ] `ossec.conf` has been backed up.
* [ ] Security event collection is configured.
* [ ] System event collection is configured.
* [ ] Application event collection is configured.
* [ ] PowerShell collection is configured where required.
* [ ] Sysmon collection is configured when Sysmon is installed.
* [ ] Wazuh agent has been restarted.
* [ ] Security events are generated.
* [ ] Security events are visible locally.
* [ ] Wazuh receives configured telemetry.
* [ ] Event timestamps are reliable.
* [ ] Important event fields are available.
* [ ] Baseline telemetry has been observed.
* [ ] Collection evidence has been captured.

---

# Professional SOC Relevance

Log collection is a fundamental SOC capability.

An analyst cannot reliably detect or investigate threats when the required telemetry is missing.

Understanding collection helps analysts:

* Identify telemetry gaps
* Validate monitoring infrastructure
* Troubleshoot missing events
* Understand data sources
* Correlate security events
* Build investigation timelines
* Support detection engineering
* Support incident response

---

# Conclusion

Reliable log collection connects endpoint activity with the centralized monitoring environment.

The primary objective is to ensure that the **right security telemetry is collected, complete, timely, and available for analysis**.

The key distinction is:

**Collection provides visibility. Detection identifies security-relevant behavior.**

The complete workflow is:

**Generate → Collect → Analyze → Detect → Investigate → Respond → Verify → Document**

Related documentation:

`04-Security-Monitoring-Configuration.md`

`06-Detection-Rules.md`
