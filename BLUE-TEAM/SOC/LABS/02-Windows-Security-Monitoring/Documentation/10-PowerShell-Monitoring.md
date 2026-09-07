# PowerShell Monitoring

## Purpose

PowerShell monitoring is the process of collecting and analyzing PowerShell execution activity to identify suspicious scripting, unauthorized administrative activity, command execution, and potential post-authentication threats.

PowerShell is a legitimate Windows administration and automation framework. Therefore, the objective of monitoring is not to treat every PowerShell execution as malicious, but to identify PowerShell activity that is unusual, unauthorized, or inconsistent with the endpoint baseline.

In this lab, PowerShell activity is monitored using:

* Windows PowerShell Operational logs
* PowerShell Event IDs
* Windows process creation events
* Sysmon process creation telemetry
* Wazuh
* Command-line information
* Script Block Logging
* Parent-child process relationships

---

# PowerShell Monitoring Objectives

The objectives of this lab are to:

* Understand PowerShell security telemetry
* Monitor PowerShell execution
* Understand important PowerShell Event IDs
* Collect PowerShell Operational logs
* Analyze Script Block Logging
* Analyze PowerShell command lines
* Identify the PowerShell user
* Identify the parent process
* Detect unusual PowerShell activity
* Correlate PowerShell with authentication events
* Correlate PowerShell with process events
* Investigate PowerShell alerts using Wazuh
* Establish a PowerShell baseline
* Test PowerShell monitoring
* Document investigation findings

---

# PowerShell Monitoring Architecture

The monitoring workflow is:

```
User / Application
      ↓
PowerShell Execution
      ↓
Windows PowerShell Logs
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
PowerShell Telemetry
      ↓
Detection Rules
      ↓
Wazuh Alert
      ↓
Analyst Investigation
      ↓
Triage / Response / Documentation
```

Additional process telemetry may provide:

```
PowerShell
    ↓
4688 / Sysmon Event ID 1
    ↓
Parent Process
    ↓
Command Line
    ↓
Process Correlation
```

---

# Why PowerShell Monitoring Matters

PowerShell is widely used by:

* System administrators
* Security teams
* Developers
* IT automation
* Configuration management
* Windows management tools

The same capabilities can also be abused by attackers.

Therefore:

**PowerShell execution is a telemetry source, not automatically an indicator of compromise.**

An analyst should investigate PowerShell using multiple contextual factors:

```
User
↓
Parent Process
↓
Command Line
↓
Script Content
↓
Timestamp
↓
Endpoint
↓
Authentication Context
↓
Baseline
```

---

# PowerShell Logging Sources

Important telemetry sources include:

| Source                     | Purpose                                 |
| -------------------------- | --------------------------------------- |
| PowerShell Operational Log | Records PowerShell operational activity |
| Event ID 400               | PowerShell engine startup               |
| Event ID 403               | PowerShell engine shutdown              |
| Event ID 4103              | Module logging                          |
| Event ID 4104              | Script Block Logging                    |
| Windows Event ID 4688      | Process creation                        |
| Sysmon Event ID 1          | Detailed process creation               |

Using multiple sources improves investigation context.

---

# Logging Configuration

This section configures the Windows monitoring VM to generate useful PowerShell security telemetry.

The configuration should be performed only on the authorized home-lab Windows system.

---

## Step 1 — Verify PowerShell Version

Open PowerShell and run:

```
$PSVersionTable
```

Record:

```
PSVersion
PSEdition
OS
```

This establishes the PowerShell environment being monitored.

---

## Step 2 — Open Local Group Policy

On supported Windows editions, open:

```
Win + R
```

Enter:

```
gpedit.msc
```

Navigate to:

```
Computer Configuration
    ↓
Administrative Templates
    ↓
Windows Components
    ↓
Windows PowerShell
```

The exact policy names may vary by Windows version.

---

## Step 3 — Enable PowerShell Module Logging

Locate:

```
Turn on Module Logging
```

Set the policy to:

```
Enabled
```

For the lab, configure the module name pattern as:

```
*
```

This provides broad module visibility for the test environment.

Apply the policy.

---

## Step 4 — Enable PowerShell Script Block Logging

Locate:

```
Turn on PowerShell Script Block Logging
```

Set:

```
Enabled
```

Apply the policy.

This enables Script Block Logging and allows PowerShell script blocks to be recorded in the PowerShell Operational log.

---

## Step 5 — Enable Script Block Invocation Logging

If the policy is available, locate:

```
Turn on PowerShell Script Block Invocation Logging
```

Enable it when detailed lab-level visibility is desired.

For a beginner SOC lab, the primary requirement is Script Block Logging.

---

## Step 6 — Apply Group Policy

Open an elevated Command Prompt or PowerShell session.

Run:

```
gpupdate /force
```

Wait for the policy update to complete.

If requested by Windows, restart the system or start a new PowerShell session.

---

## Step 7 — Verify PowerShell Operational Log

Open:

```
Event Viewer
```

Navigate to:

```
Applications and Services Logs
    ↓
Microsoft
    ↓
Windows
    ↓
PowerShell
    ↓
Operational
```

Confirm that the channel exists and is enabled.

---

## Step 8 — Generate Test PowerShell Activity

Open a new PowerShell session.

Run:

```
Get-Date
```

Then:

```
Get-Service
```

Then:

```
Get-Process
```

These are benign commands designed to generate normal PowerShell telemetry.

---

## Step 9 — Verify Event ID 400

In:

```
PowerShell
    ↓
Operational
```

Search for:

```
Event ID 400
```

Verify:

* Timestamp
* User
* Host
* PowerShell host information

Event ID 400 indicates PowerShell engine startup.

---

## Step 10 — Verify Event ID 403

Close the PowerShell session.

Search for:

```
Event ID 403
```

Verify the timestamp and session information.

Event ID 403 indicates PowerShell engine shutdown.

---

## Step 11 — Verify Event ID 4103

If Module Logging is enabled, search:

```
Event ID 4103
```

Run another benign command if required:

```
Get-Service
```

Review the event for available module and command information.

Record:

```
Timestamp
User
Command
Module
```

---

## Step 12 — Verify Event ID 4104

Search:

```
Event ID 4104
```

Run:

```
Get-Date
```

or:

```
Get-Service
```

Review the Script Block Logging event.

Record:

```
Timestamp
User
Script Block
Host
```

---

# Wazuh PowerShell Log Collection Configuration

After Windows is generating PowerShell telemetry, configure the Wazuh agent to collect the PowerShell Operational channel.

---

## Step 13 — Open Wazuh Agent Configuration

On the Windows endpoint, open:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Create or verify the Windows Event Channel collection entry for PowerShell.

The collection pattern is:

```
<localfile>
  <location>Microsoft-Windows-PowerShell/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Keep the configuration inside the appropriate Wazuh configuration structure.

---

## Step 14 — Verify Existing Collection Configuration

Before adding another entry, check whether PowerShell collection already exists.

Look for:

```
Microsoft-Windows-PowerShell/Operational
```

Do not create duplicate collection entries unnecessarily.

---

## Step 15 — Restart the Wazuh Agent

Open PowerShell as Administrator.

Run:

```
Restart-Service -Name wazuh
```

Verify:

```
Get-Service -Name wazuh
```

Expected:

```
Status = Running
```

---

## Step 16 — Verify Wazuh Collection

Generate:

```
Get-Date

Get-Service
```

Then open the Wazuh dashboard.

Search for PowerShell events using:

```
win.system.channel:"Microsoft-Windows-PowerShell/Operational"
```

If the exact field mapping differs in your Wazuh version, search for:

```
Microsoft-Windows-PowerShell
```

and inspect the returned event fields.

---

# PowerShell Event ID Reference

| Event ID | Meaning                   | Primary Use                  |
| -------- | ------------------------- | ---------------------------- |
| 400      | PowerShell engine started | Session start                |
| 403      | PowerShell engine stopped | Session end                  |
| 4103     | Module Logging            | Module / command activity    |
| 4104     | Script Block Logging      | Script block visibility      |
| 4688     | Process Creation          | PowerShell process execution |
| Sysmon 1 | Process Creation          | Enhanced process telemetry   |

---

# PowerShell Monitoring Fields

Important investigation fields include:

| Field               | Purpose                                 |
| ------------------- | --------------------------------------- |
| User                | Identifies account executing PowerShell |
| Host                | Identifies affected endpoint            |
| Timestamp           | Establishes execution sequence          |
| Event ID            | Identifies PowerShell activity type     |
| Command Line        | Shows execution parameters              |
| Script Block        | Shows logged script content             |
| Parent Process      | Shows what launched PowerShell          |
| Parent Command Line | Provides additional context             |
| Process ID          | Identifies process instance             |
| Logon ID            | Correlates activity with authentication |
| Channel             | Identifies telemetry source             |

Field names may differ depending on Wazuh decoders and Windows event mappings.

---

# PowerShell Baseline

Before creating aggressive detections, establish normal PowerShell behavior.

Record:

* Normal users
* Normal endpoints
* Normal PowerShell versions
* Normal administrative tasks
* Normal scripts
* Normal parent processes
* Normal execution times
* Normal command patterns

Example:

```
Administrator
    ↓
explorer.exe
    ↓
powershell.exe
    ↓
Get-Service
```

may be normal administrative activity.

An unusual PowerShell process launched by an unexpected application should receive additional investigation.

---

# PowerShell Parent-Child Analysis

Parent-child relationships provide valuable context.

Example:

```
explorer.exe
     ↓
powershell.exe
```

This may be normal.

Another example:

```
management-tool.exe
     ↓
powershell.exe
```

may be legitimate if the tool is approved.

An unexpected application launching PowerShell should be investigated.

The analyst should ask:

* Is the parent process expected?
* Is the user expected?
* Is the command expected?
* Is the endpoint expected?
* Is the execution time expected?

---

# PowerShell Command-Line Analysis

Command-line information may reveal how PowerShell was launched.

Examples of benign administrative activity may include:

```
powershell.exe -Command "Get-Date"
```

or:

```
powershell.exe -Command "Get-Service"
```

Potential investigation indicators include:

* Obfuscated commands
* Encoded command parameters
* Unexpected script files
* Commands launched from unusual directories
* Unexpected download-related behavior
* Unusual execution policies
* Multiple chained commands
* Commands inconsistent with the user's role

A single command-line indicator should not automatically be treated as malicious.

---

# Script Block Analysis

When Event ID 4104 is available, inspect the script block carefully.

Questions include:

1. What script was executed?
2. Which user executed it?
3. Which endpoint executed it?
4. When was it executed?
5. Was the script expected?
6. Is the script associated with an approved task?
7. Does the script contain suspicious or unusual behavior?
8. Did another process launch PowerShell?

The analyst should correlate script content with surrounding events.

---

# Suspicious PowerShell Indicators

Potential indicators requiring investigation include:

* PowerShell launched by an unusual parent process
* PowerShell executed by an unexpected account
* PowerShell launched from an unusual location
* Encoded command parameters
* Obfuscated script content
* Unexpected script execution
* PowerShell activity immediately after suspicious authentication
* PowerShell activity following privileged authentication
* PowerShell spawned by an unexpected application
* PowerShell executing an unknown script
* Multiple suspicious PowerShell events in a short period

These indicators increase investigation priority but do not independently prove malicious activity.

---

# Authentication-to-PowerShell Correlation

PowerShell activity should be correlated with authentication events.

Example:

```
4625 — Failed Logon
      ↓
4625 — Failed Logon
      ↓
4624 — Successful Logon
      ↓
4672 — Special Privileges
      ↓
4688 — powershell.exe
      ↓
4104 — Script Block
```

This sequence should receive higher investigation priority than an isolated PowerShell event.

---

# Process-to-PowerShell Correlation

Process telemetry can reveal how PowerShell was launched.

Example:

```
explorer.exe
     ↓
powershell.exe
     ↓
child-process.exe
```

Compare this with:

```
suspicious-application.exe
     ↓
powershell.exe
     ↓
child-process.exe
```

The second sequence should receive additional investigation if the parent process is unexpected.

---

# Actionable Wazuh Search Examples

Wazuh/OpenSearch field names and search behavior can vary depending on version and configuration.

Use these as practical investigation patterns.

## Search 1 — PowerShell Operational Events

```
win.system.channel:"Microsoft-Windows-PowerShell/Operational"
```

Review:

* Event ID
* User
* Timestamp
* Host
* PowerShell activity

---

## Search 2 — PowerShell Engine Startup

```
win.system.eventID:400
```

Use this to identify PowerShell engine startup activity.

---

## Search 3 — PowerShell Engine Shutdown

```
win.system.eventID:403
```

Correlate with Event ID 400 to establish PowerShell session boundaries.

---

## Search 4 — PowerShell Module Logging

```
win.system.eventID:4103
```

Review the available command and module information.

---

## Search 5 — PowerShell Script Block Logging

```
win.system.eventID:4104
```

Review:

* Script block content
* User
* Timestamp
* Host
* Related process activity

---

## Search 6 — PowerShell Process Creation

Search Windows process creation events:

```
win.system.eventID:4688
```

Then inspect the process field for:

```
powershell.exe
```

If your Wazuh field mapping supports direct filtering, a pattern may be:

```
win.system.eventID:4688 AND win.eventdata.newProcessName:*powershell.exe*
```

---

## Search 7 — Sysmon PowerShell Process

```
win.system.eventID:1
```

Then inspect:

```
win.eventdata.image
win.eventdata.commandLine
win.eventdata.parentImage
```

Filter for PowerShell when supported by your configured field mapping.

---

## Search 8 — PowerShell Activity for a Specific User

Example:

```
win.system.eventID:4104 AND win.eventdata.subjectUserName:"testuser"
```

Replace `testuser` with the account under investigation.

---

## Search 9 — PowerShell Activity Around an Authentication Event

First search:

```
win.system.eventID:4624
```

Identify:

```
User
Timestamp
Logon ID
```

Then search for PowerShell activity around the same time:

```
win.system.eventID:4104
```

Correlate:

```
Username
Timestamp
Logon ID
Endpoint
```

---

## Search 10 — PowerShell and Privileged Activity

Search:

```
win.system.eventID:4672
```

Then investigate PowerShell events:

```
win.system.eventID:4104
```

Correlate the user, endpoint, and timestamp.

---

# PowerShell Detection Logic

A practical detection strategy should combine PowerShell telemetry with context.

Conceptual logic:

```
PowerShell Execution
      +
Unexpected User
      +
Unusual Parent Process
      +
Suspicious Command Line
      +
Unusual Timing
      ↓
Higher Investigation Priority
```

Another pattern:

```
4624 Successful Logon
      ↓
4672 Privileged Access
      ↓
4688 PowerShell
      ↓
4104 Script Block
      ↓
Suspicious Script Content
      ↓
High-Priority Investigation
```

---

# Detection Severity

| Observation                                             | Initial Severity    |
| ------------------------------------------------------- | ------------------- |
| Normal PowerShell administration                        | Informational / Low |
| Expected script execution                               | Low                 |
| Unusual PowerShell execution                            | Medium              |
| Unexpected user executing PowerShell                    | Medium–High         |
| Suspicious parent-child relationship                    | Medium–High         |
| Suspicious command line                                 | High                |
| Suspicious script block                                 | High                |
| Suspicious PowerShell after unauthorized authentication | High                |
| Confirmed malicious PowerShell activity                 | Critical            |

Severity should be adjusted after investigation.

---

# Structured PowerShell Triage Decision Table

| Observation                                     | Initial Assessment  | Analyst Action                              | Typical Disposition |
| ----------------------------------------------- | ------------------- | ------------------------------------------- | ------------------- |
| PowerShell launched by expected administrator   | Likely benign       | Validate against baseline                   | Close / Monitor     |
| PowerShell launched during approved maintenance | Benign if validated | Confirm change/activity record              | Close               |
| PowerShell launched by unexpected user          | Suspicious          | Review authentication and command line      | Investigate         |
| PowerShell launched by expected parent          | Potentially benign  | Review command and user context             | Monitor             |
| PowerShell launched by unusual parent           | Suspicious          | Investigate process tree                    | Escalate            |
| PowerShell from unusual executable path         | Suspicious          | Verify binary and execution context         | Investigate         |
| Normal Script Block activity                    | Likely benign       | Compare with baseline                       | Close / Monitor     |
| Unknown script execution                        | Suspicious          | Review script, user, parent, and timing     | Investigate         |
| Obfuscated or encoded command                   | High concern        | Analyze command and surrounding telemetry   | Escalate            |
| PowerShell after repeated failed logons         | High concern        | Correlate authentication and process events | Escalate            |
| PowerShell after privileged logon               | High concern        | Investigate privileged session              | Escalate            |
| Suspicious script plus unusual child process    | High concern        | Expand endpoint investigation               | Escalate            |
| Activity matches approved automation            | Benign              | Document validation                         | Close               |
| Activity cannot be validated                    | Unknown             | Gather additional evidence                  | Investigate         |
| Confirmed unauthorized PowerShell activity      | Critical            | Follow incident response procedure          | Escalate / Respond  |

---

# Hands-On Lab Procedure

## Lab Objective

Generate controlled PowerShell activity on the Windows monitoring VM, verify that Windows records the activity, confirm that Wazuh receives the telemetry, and perform a basic SOC investigation.

Only perform the activity on the authorized home-lab Windows VM.

---

## Lab Requirements

Use:

```
Windows Monitoring VM
      +
Wazuh Agent
      +
Wazuh Manager / Dashboard
```

Recommended:

```
PowerShell Operational Logging
Script Block Logging
Sysmon
```

---

## Step 1 — Verify Wazuh Agent

Open PowerShell as Administrator.

Run:

```
Get-Service -Name wazuh
```

Expected:

```
Status = Running
```

If required:

```
Start-Service -Name wazuh
```

---

## Step 2 — Verify PowerShell Operational Logging

Open:

```
Event Viewer
```

Navigate to:

```
Applications and Services Logs
    ↓
Microsoft
    ↓
Windows
    ↓
PowerShell
    ↓
Operational
```

Generate controlled PowerShell activity during the following steps.

---

## Step 3 — Generate Benign PowerShell Activity

Open PowerShell and execute:

```
Get-Date
```

Then:

```
Get-Service
```

Then:

```
Get-Process
```

These commands are intended only to generate normal PowerShell administrative telemetry.

---

## Step 4 — Verify Event ID 400

Return to the PowerShell Operational log.

Search for:

```
Event ID: 400
```

Record:

* Timestamp
* User
* Host
* PowerShell host information

---

## Step 5 — Verify Event ID 403

After closing the PowerShell session, check:

```
Event ID: 403
```

Use the 400 and 403 events to understand the beginning and end of the PowerShell session.

---

## Step 6 — Verify Event ID 4103

If Module Logging is enabled, search:

```
Event ID: 4103
```

Review the available command/module information.

Record:

```
User
Timestamp
Command
Module
```

---

## Step 7 — Verify Event ID 4104

If Script Block Logging is enabled, search:

```
Event ID: 4104
```

Review the recorded script block.

Use only benign commands in this lab.

Record:

```
User
Timestamp
Script Block
Host
```

---

## Step 8 — Generate Process Telemetry

Launch PowerShell through a normal process context.

Verify:

```
Event ID 4688
```

If Sysmon is configured:

```
Event ID 1
```

Record:

```
powershell.exe
Parent Process
Command Line
User
Timestamp
```

---

## Step 9 — Generate a Controlled Child Process

From PowerShell, execute:

```
cmd.exe /c whoami
```

Then:

```
cmd.exe /c ipconfig
```

Review the resulting process telemetry.

Expected process relationship may resemble:

```
powershell.exe
      ↓
cmd.exe
      ↓
whoami.exe
```

or:

```
powershell.exe
      ↓
cmd.exe
      ↓
ipconfig.exe
```

The exact process tree may vary.

---

## Step 10 — Verify Activity in Wazuh

Open the Wazuh dashboard.

Search:

```
win.system.eventID:4104
```

Then search:

```
win.system.eventID:400
```

and:

```
win.system.eventID:403
```

Also search:

```
win.system.eventID:4688
```

Review the events and identify:

* Agent
* Timestamp
* User
* PowerShell activity
* Process
* Parent process
* Command line

---

## Step 11 — Correlate PowerShell and Authentication

Search:

```
win.system.eventID:4624
```

Identify the user and timestamp.

Then search:

```
win.system.eventID:4104
```

and:

```
win.system.eventID:4688
```

Build a timeline:

```
4624 — Successful Logon
      ↓
400 — PowerShell Started
      ↓
4103 / 4104 — PowerShell Activity
      ↓
4688 — Process Creation
      ↓
403 — PowerShell Stopped
```

---

## Step 12 — Perform PowerShell Triage

Ask:

1. Was the user expected?
2. Was the endpoint expected?
3. Was the parent process expected?
4. Was the command expected?
5. Was the script expected?
6. Was the execution time normal?
7. Did privileged authentication occur?
8. Were suspicious child processes created?

Classify the activity:

```
Benign
Suspicious
Unknown
```

---

## Step 13 — Capture Evidence

Capture screenshots showing:

* PowerShell Event ID 400
* Event ID 403
* Event ID 4103, if enabled
* Event ID 4104, if enabled
* Event ID 4688
* Sysmon Event ID 1, if used
* Wazuh event
* Process relationship
* Authentication correlation

Store evidence under:

```
Evidence/
```

Suggested filenames:

```
powershell-event-400.png
powershell-event-403.png
powershell-event-4103.png
powershell-event-4104.png
powershell-process-4688.png
wazuh-powershell-event.png
powershell-auth-correlation.png
```

---

# Hands-On Validation Matrix

| Test | Activity                 | Expected Telemetry          | Expected Result             |
| ---- | ------------------------ | --------------------------- | --------------------------- |
| 1    | Start PowerShell         | 400                         | Engine startup visible      |
| 2    | Run `Get-Date`           | 4103 / 4104 when configured | Command activity visible    |
| 3    | Run `Get-Service`        | 4103 / 4104 when configured | Command activity visible    |
| 4    | Stop PowerShell          | 403                         | Engine shutdown visible     |
| 5    | Launch PowerShell        | 4688 / Sysmon 1             | Process creation visible    |
| 6    | Run `cmd.exe /c whoami`  | 4688 / Sysmon 1             | Child process visible       |
| 7    | Correlate authentication | 4624 + PowerShell events    | Timeline created            |
| 8    | Investigate in Wazuh     | Multiple events             | SOC investigation completed |

---

# Evidence Requirements

Capture:

* Wazuh PowerShell alert/event
* Event ID
* Agent name
* Hostname
* Username
* Timestamp
* PowerShell command
* Script block, when available
* Parent process
* Process ID
* Authentication event
* Analyst conclusion

Store evidence under:

```
Evidence/
```

---

# Troubleshooting PowerShell Monitoring

## Problem 1 — Event ID 400/403 Not Appearing

Check:

* PowerShell Operational channel
* Windows Event Viewer
* PowerShell execution
* Wazuh collection configuration
* Wazuh agent connectivity

---

## Problem 2 — Event ID 4103 Not Appearing

Check whether PowerShell Module Logging is enabled.

Also verify:

* PowerShell version
* Group Policy configuration
* Operational event channel
* Wazuh collection

---

## Problem 3 — Event ID 4104 Not Appearing

Check whether Script Block Logging is enabled.

Verify:

* Group Policy configuration
* PowerShell Operational channel
* Wazuh collection
* Event generation

---

## Problem 4 — Events Visible Locally but Not in Wazuh

Check the collection pipeline:

```
Windows PowerShell Log
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Wazuh Indexer
      ↓
Wazuh Dashboard
```

---

## Problem 5 — PowerShell Events Arrive but No Alert Appears

This may indicate a detection issue rather than a collection issue.

Check:

* Decoder
* Rule conditions
* Rule ID
* Rule level
* Event fields
* Detection thresholds

---

## Problem 6 — Too Many PowerShell Alerts

Possible causes:

* Detection rule too broad
* Normal administration being flagged
* Insufficient baseline
* Excessively sensitive command matching

Improve detection by adding context:

```
User
Parent Process
Command Line
Script Content
Endpoint
Authentication
Baseline
```

---

# Common PowerShell Monitoring Mistakes

## Mistake 1 — Treating Every PowerShell Event as Malicious

PowerShell is a legitimate Windows administration tool.

**Better approach:**

Analyze context before classifying activity.

---

## Mistake 2 — Relying Only on Command-Line Detection

Command lines can be useful but may not provide enough context.

**Better approach:**

Correlate command line with user, parent process, authentication, and script telemetry.

---

## Mistake 3 — Ignoring Script Block Logging

Script Block Logging can provide valuable investigation context when properly configured.

**Better approach:**

Use 4104 alongside process and authentication telemetry.

---

## Mistake 4 — Ignoring the Parent Process

The process that launched PowerShell can significantly change the investigation context.

**Better approach:**

Always investigate parent-child relationships.

---

## Mistake 5 — Ignoring Legitimate Automation

Automated PowerShell scripts may generate large amounts of telemetry.

**Better approach:**

Establish a baseline for approved scripts and automation.

---

# Professional SOC Relevance

PowerShell monitoring is an important endpoint security capability.

A SOC analyst should be able to:

* Understand PowerShell telemetry
* Interpret Events 400 and 403
* Interpret Event 4103
* Interpret Event 4104
* Analyze PowerShell process creation
* Review command lines
* Analyze script blocks
* Investigate parent-child relationships
* Correlate PowerShell with authentication
* Use Wazuh searches
* Triage PowerShell alerts
* Identify false positives
* Escalate suspicious activity
* Document investigation findings

These skills are directly relevant to SOC L1 alert triage and endpoint investigation.

---

# Conclusion

PowerShell monitoring provides visibility into scripting and administrative activity occurring on Windows endpoints.

The investigation workflow should follow:

```
PowerShell Execution
      ↓
Identify User
      ↓
Identify Endpoint
      ↓
Review Event ID
      ↓
Review Command / Script
      ↓
Review Parent Process
      ↓
Correlate Authentication
      ↓
Correlate Process Activity
      ↓
Compare Baseline
      ↓
Assess Risk
      ↓
Respond / Escalate / Close
      ↓
Document
```

The key principle is:

**PowerShell is not inherently malicious; suspicious PowerShell activity is determined by context, behavior, execution chain, and deviation from the expected baseline.**

Related documentation:

* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
