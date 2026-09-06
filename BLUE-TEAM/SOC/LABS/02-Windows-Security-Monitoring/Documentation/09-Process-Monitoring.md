# Process Monitoring

## Purpose

Process monitoring is the practice of collecting and analyzing process execution activity on a Windows endpoint to identify suspicious, unauthorized, or abnormal behavior.

Processes are one of the most important sources of endpoint security telemetry because many attacks eventually require execution of a process.

In this lab, Windows process activity is monitored using:

* Windows Security Event Logs
* Windows Event ID 4688
* Sysmon Process Creation Event ID 1
* Wazuh
* Process metadata
* Command-line information
* Parent-child process relationships

The objective is to understand normal process activity and identify process behavior that requires investigation.

---

# Process Monitoring Objectives

The objectives of this lab are to:

* Monitor Windows process creation
* Collect process execution telemetry
* Understand Event ID 4688
* Understand Sysmon Event ID 1
* Analyze process names
* Analyze executable paths
* Analyze command lines
* Analyze parent-child relationships
* Identify unusual process execution
* Detect suspicious process behavior
* Correlate process activity with authentication events
* Investigate process alerts using Wazuh
* Establish a process baseline
* Document investigation findings

---

# Process Monitoring Architecture

The monitoring workflow is:

```
Windows Endpoint
      ↓
Process Creation
      ↓
Windows Security / Sysmon
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Process Telemetry
      ↓
Detection Rules
      ↓
Wazuh Alert
      ↓
Analyst Investigation
      ↓
Triage / Response / Documentation
```

---

# Why Process Monitoring Matters

Authentication tells an analyst:

```
Who accessed the system?
```

Process monitoring helps answer:

```
What did the user or system execute?
```

For example:

```
4624 — Successful Logon
      ↓
4672 — Privileged Logon
      ↓
4688 — Process Creation
      ↓
PowerShell Execution
```

This sequence provides much more context than authentication activity alone.

Process monitoring can therefore help identify:

* Suspicious administrative activity
* Unauthorized software execution
* Script execution
* Unexpected command interpreters
* Abnormal parent-child relationships
* Execution from unusual directories
* Potential post-authentication activity

---

# Windows Event ID 4688 — Process Creation

Windows Security Event ID 4688 records the creation of a new process when appropriate auditing is enabled.

Important information may include:

```
New Process Name
Creator Process Name
Process ID
Creator Process ID
Subject User
Command Line
```

Availability of individual fields depends on Windows auditing configuration and event generation.

---

# Event ID 4688 Investigation

When investigating Event ID 4688, examine:

* Timestamp
* Hostname
* Username
* New process name
* Process path
* Command line
* Parent/creator process
* Process ID
* Parent process ID

The primary questions are:

1. Who launched the process?
2. What process was launched?
3. Where was the executable located?
4. What command-line arguments were used?
5. Which process launched it?
6. Was the execution expected?
7. What happened immediately before and after execution?

---

# Sysmon Event ID 1 — Process Creation

Sysmon Event ID 1 provides detailed process creation telemetry.

Useful fields may include:

```
Image
CommandLine
ParentImage
ParentCommandLine
User
ProcessId
ParentProcessId
CurrentDirectory
Hashes
IntegrityLevel
```

Sysmon configuration determines which telemetry is collected and how much detail is available.

---

# Windows Security vs Sysmon Process Monitoring

| Capability                  | Event ID 4688           | Sysmon Event ID 1            |
| --------------------------- | ----------------------- | ---------------------------- |
| Process creation            | Yes                     | Yes                          |
| Process name                | Yes                     | Yes                          |
| User information            | Yes                     | Yes                          |
| Command line                | Can be available        | Available when configured    |
| Parent process              | Yes                     | Yes                          |
| Hash information            | Limited                 | Can provide hashes           |
| Detailed endpoint telemetry | Moderate                | Higher                       |
| Primary use                 | Native Windows auditing | Enhanced endpoint visibility |

Using both sources can provide stronger visibility when configured correctly.

---

# Process Monitoring Fields

Important fields for investigation include:

| Field               | Purpose                                                  |
| ------------------- | -------------------------------------------------------- |
| Process Name        | Identifies executed process                              |
| Process Path        | Shows executable location                                |
| Command Line        | Shows execution parameters                               |
| Parent Process      | Identifies process responsible for launching the process |
| Parent Command Line | Provides additional execution context                    |
| Username            | Identifies account associated with execution             |
| Process ID          | Identifies process instance                              |
| Parent Process ID   | Links process to parent                                  |
| Timestamp           | Establishes execution sequence                           |
| Hash                | Helps identify executable integrity                      |

Not every event source provides every field.

---

# Process Name Analysis

Start by determining whether the process is expected.

Common legitimate Windows processes include:

```
explorer.exe
services.exe
svchost.exe
lsass.exe
winlogon.exe
taskhostw.exe
powershell.exe
cmd.exe
```

A legitimate process name does not automatically make execution safe.

Attackers can abuse legitimate binaries, rename executables, or execute them from unusual locations.

Therefore, process name should always be analyzed together with:

```
Path
Command Line
Parent Process
User
Timestamp
```

---

# Executable Path Analysis

The executable location provides important context.

Expected system locations commonly include:

```
C:\Windows\System32\
C:\Windows\SysWOW64\
```

Potentially suspicious locations may include:

```
C:\Users\<user>\Downloads\
C:\Users\<user>\AppData\Local\Temp\
C:\Users\<user>\AppData\Roaming\
C:\ProgramData\
```

An unusual location is an investigation indicator, not proof of malicious activity.

---

# Command-Line Analysis

Command-line arguments can provide important context that is not visible from the process name alone.

For example:

```
powershell.exe -File script.ps1
```

provides more information than:

```
powershell.exe
```

Look for:

* Script execution
* Encoded or obfuscated parameters
* Download-related parameters
* Unexpected administrative commands
* Unusual arguments
* Execution of files from temporary locations

Command-line content should be interpreted within the context of the user, endpoint, parent process, and expected administrative activity.

---

# Parent-Child Process Analysis

Parent-child relationships are extremely useful for detecting abnormal process execution.

Example:

```
explorer.exe
     ↓
powershell.exe
```

This may be legitimate or suspicious depending on the context.

Another example:

```
winword.exe
     ↓
powershell.exe
```

This deserves additional investigation because the parent process and child process relationship may be unusual for normal office activity.

The analyst should not classify a process as malicious based only on the parent-child relationship.

---

# Process Tree Analysis

A process tree can be represented as:

```
User Logon
    ↓
explorer.exe
    ↓
application.exe
    ↓
child-process.exe
    ↓
powershell.exe
```

The analyst should determine:

* Where execution started
* Which user initiated it
* Which process launched the next process
* Whether the chain is expected
* Whether suspicious execution appears later in the chain

Process trees help reconstruct endpoint activity.

---

# Suspicious Process Indicators

Potential indicators requiring investigation include:

* Executable launched from a temporary directory
* Executable launched from a user's Downloads directory
* Unexpected command shell execution
* Unexpected PowerShell execution
* Unusual parent-child relationship
* Process executed by an unexpected user
* Administrative process executed outside normal maintenance windows
* Suspicious command-line arguments
* Unknown executable
* Newly introduced executable
* Process execution immediately after suspicious authentication
* Multiple related suspicious processes

These are investigation indicators and do not independently prove malicious activity.

---

# Suspicious Command Interpreters

Monitor execution of:

```
cmd.exe
powershell.exe
pwsh.exe
wscript.exe
cscript.exe
```

These tools have legitimate administrative uses.

Therefore, detection should consider:

```
User
Parent Process
Command Line
Path
Timestamp
Endpoint
Baseline
```

---

# Process Baseline

A process baseline describes normal process execution within the lab environment.

Record:

* Common processes
* Common executable paths
* Normal administrative tools
* Normal users
* Normal parent-child relationships
* Normal maintenance times

Example:

```
explorer.exe
    ↓
cmd.exe
    ↓
ipconfig.exe
```

may be expected during troubleshooting.

However:

```
UnknownProcess.exe
    ↓
powershell.exe
```

should be investigated if it is not part of the established baseline.

---

# Hands-On Lab Procedure

## Lab Objective

Generate controlled process activity on the Windows monitoring VM, confirm that Windows records the process creation event, verify that Wazuh collects the event, and investigate the resulting telemetry.

The lab should be performed only on the authorized Windows home-lab machine.

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

Optional:

```
Sysmon
```

Required telemetry:

```
Windows Security Event ID 4688
```

Optional enhanced telemetry:

```
Sysmon Event ID 1
```

---

## Step 1 — Verify Wazuh Agent

On the Windows monitoring VM, open PowerShell as Administrator.

Check the Wazuh service:

```
Get-Service -Name wazuh
```

Expected result:

```
Status = Running
```

If the service is stopped:

```
Start-Service -Name wazuh
```

Verify again:

```
Get-Service -Name wazuh
```

---

## Step 2 — Verify Windows Process Auditing

Open:

```
Event Viewer
```

Navigate to:

```
Windows Logs
    ↓
Security
```

Generate a normal process later in the procedure and verify that Event ID 4688 appears.

If 4688 does not appear, verify that process creation auditing is enabled in the lab.

---

## Step 3 — Generate a Normal Process

Open PowerShell and execute:

```
notepad.exe
```

Close Notepad after it opens.

Then generate another simple process:

```
calc.exe
```

This creates controlled process activity without requiring offensive actions.

---

## Step 4 — Verify Event ID 4688 Locally

Open:

```
Event Viewer
    ↓
Windows Logs
    ↓
Security
```

Search for:

```
Event ID: 4688
```

Open the newly generated event.

Record:

```
TimeCreated
New Process Name
Creator Process Name
Subject User
Process ID
Creator Process ID
Command Line
```

If command-line information is not available, verify the relevant Windows auditing configuration.

---

## Step 5 — Generate Command-Line Activity

Open PowerShell and execute:

```
cmd.exe /c whoami
```

Then:

```
cmd.exe /c ipconfig
```

These are benign commands that generate useful process telemetry.

The expected process chain may resemble:

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

The exact process tree depends on how the commands are launched.

---

## Step 6 — Generate PowerShell Process Activity

From an authorized PowerShell session, execute:

```
powershell.exe -NoProfile -Command "Get-Date"
```

This is a benign test intended to generate process telemetry.

Do not use offensive payloads or destructive commands for this lab.

---

## Step 7 — Verify the Process in Wazuh

Open the Wazuh dashboard.

Search for Windows process creation events using:

```
win.system.eventID:4688
```

Review the returned events.

Identify:

* Agent
* Timestamp
* Username
* Process
* Parent process
* Command line
* Event ID

If your Wazuh field mappings differ, search for the event ID first and inspect the available fields.

---

## Step 8 — Verify Sysmon Event ID 1

If Sysmon is installed and configured:

Open:

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

Search for:

```
Event ID: 1
```

Generate another benign process if necessary:

```
notepad.exe
```

Verify that the Sysmon process creation event contains fields such as:

```
Image
CommandLine
ParentImage
User
ProcessId
ParentProcessId
```

---

## Step 9 — Investigate the Parent-Child Relationship

For each test event, record:

```
Parent Process
      ↓
Child Process
```

Example:

```
powershell.exe
      ↓
cmd.exe
      ↓
whoami.exe
```

Determine whether the relationship is expected.

Document why the process chain is considered:

```
Normal
Suspicious
Unknown
```

---

## Step 10 — Investigate the Executable Path

Review the executable location.

Example:

```
C:\Windows\System32\notepad.exe
```

Determine whether the location matches the expected installation path.

Record:

```
Process
Path
User
Parent
Timestamp
```

---

## Step 11 — Investigate Command Line

Review the command line associated with the process.

For example:

```
cmd.exe /c whoami
```

Determine:

* Which command was executed?
* Which user executed it?
* Which process launched it?
* Was the command expected?
* Does it match the lab baseline?

---

## Step 12 — Correlate With Authentication

Search for the user's recent authentication events.

Start with:

```
win.system.eventID:4624
```

Then identify the corresponding process events:

```
win.system.eventID:4688
```

Compare:

```
Authentication Time
Process Creation Time
Username
Endpoint
```

Construct a simple timeline:

```
4624 — Successful Logon
      ↓
4688 — powershell.exe
      ↓
4688 — cmd.exe
      ↓
4688 — whoami.exe
```

---

## Step 13 — Perform Process Triage

Use the following decision process:

```
Is the process known?
       ↓
   YES → Is the path expected?
                ↓
           YES → Is the parent expected?
                        ↓
                   YES → Is the command line expected?
                                ↓
                           YES → Likely benign
                                ↓
                           NO → Investigate
```

If the process is unknown or the path/parent/command line is unusual:

```
Unknown / Suspicious
       ↓
Gather more evidence
       ↓
Correlate authentication
       ↓
Review process tree
       ↓
Assess severity
       ↓
Escalate if required
```

---

## Step 14 — Record Evidence

Capture screenshots showing:

* Windows Event ID 4688
* Wazuh process event
* Sysmon Event ID 1, if used
* Process name
* Process path
* Command line
* Parent process
* Username
* Timestamp
* Related authentication event

Store screenshots under:

```
Evidence/
```

Suggested evidence naming:

```
process-event-4688.png
wazuh-process-alert.png
sysmon-process-event-1.png
process-tree-analysis.png
authentication-correlation.png
```

---

## Step 15 — Document the Result

Create a short investigation record containing:

```
Test:
Normal Process Monitoring

Endpoint:
Windows Monitoring VM

User:
<lab-user>

Process:
<process-name>

Parent Process:
<parent-process>

Event ID:
4688 / Sysmon 1

Command Line:
<command-line>

Result:
Process successfully collected and investigated.

Classification:
Benign / Suspicious / Unknown

Evidence:
Evidence/<filename>
```

---

# Hands-On Validation Matrix

| Test | Activity                         | Expected Telemetry | Expected Result                            |
| ---- | -------------------------------- | ------------------ | ------------------------------------------ |
| 1    | Launch Notepad                   | 4688 / Sysmon 1    | Process creation visible                   |
| 2    | Launch Calculator                | 4688 / Sysmon 1    | Process creation visible                   |
| 3    | Run `cmd.exe /c whoami`          | 4688 / Sysmon 1    | CMD and child activity visible             |
| 4    | Run `cmd.exe /c ipconfig`        | 4688 / Sysmon 1    | Process activity visible                   |
| 5    | Launch PowerShell                | 4688 / Sysmon 1    | PowerShell process visible                 |
| 6    | Review parent-child relationship | Process metadata   | Process tree documented                    |
| 7    | Correlate login and process      | 4624 + 4688        | Authentication-to-process timeline created |

---

# Actionable Wazuh Search Examples

Wazuh/OpenSearch field names and search syntax can vary depending on version and configuration.

Use the following as practical search patterns.

## Search 1 — Windows Process Creation

Search for Event ID 4688:

```
win.system.eventID:4688
```

Review:

```
win.eventdata.newProcessName
win.eventdata.commandLine
win.eventdata.creatorProcessName
```

---

## Search 2 — Sysmon Process Creation

Search for Sysmon Event ID 1:

```
win.system.eventID:1
```

Confirm that the event belongs to:

```
Microsoft-Windows-Sysmon/Operational
```

Review:

```
win.eventdata.image
win.eventdata.commandLine
win.eventdata.parentImage
win.eventdata.user
```

Exact field names depend on the Wazuh decoder and Sysmon event mapping.

---

## Search 3 — PowerShell Process Creation

Search process creation events and inspect the process name or command line for PowerShell.

Example pattern:

```
win.system.eventID:4688 AND win.eventdata.newProcessName:*powershell.exe*
```

If wildcard behavior differs in the configured Wazuh/OpenSearch environment, search for Event ID 4688 first and filter the returned process fields.

---

## Search 4 — CMD Execution

Search for command shell execution:

```
win.system.eventID:4688 AND win.eventdata.newProcessName:*cmd.exe*
```

Investigate:

* User
* Parent process
* Command line
* Execution path
* Timestamp

---

## Search 5 — Processes From Temporary Locations

Search process creation events and investigate paths containing:

```
\Temp\
```

Example investigation pattern:

```
win.system.eventID:4688 AND win.eventdata.newProcessName:*Temp*
```

Use the returned events to identify whether an executable was launched from an unusual location.

---

## Search 6 — Specific User Process Activity

When investigating a user:

```
win.system.eventID:4688 AND win.eventdata.subjectUserName:"testuser"
```

Replace `testuser` with the account under investigation.

Use this to build a user-specific process timeline.

---

## Search 7 — Process Activity After Authentication

Search:

```
win.system.eventID:4624
```

Then correlate the timestamp and user with:

```
win.system.eventID:4688
```

The objective is to determine what processes were launched after authentication.

---

## Search 8 — Privileged Process Activity

Search:

```
win.system.eventID:4672
```

Then correlate the same user and logon session with:

```
win.system.eventID:4688
```

This can help identify processes executed following privileged authentication.

---

# Process Detection Logic

A process detection rule should consider multiple attributes.

Conceptual logic:

```
Process Created
     +
Unusual Process
     +
Unusual Path
     +
Suspicious Parent
     +
Suspicious Command Line
     +
Unexpected User
     ↓
Higher Investigation Priority
```

Avoid relying on a single indicator wherever possible.

---

# Example Detection Logic

Example conceptual detection:

```
IF
    process = powershell.exe
AND
    parent process = unusual application
AND
    command line = unusual
THEN
    generate investigation alert
```

Another example:

```
IF
    process created from temporary directory
AND
    process executed by unexpected user
THEN
    generate higher-priority alert
```

These conditions should be tuned against the environment before being treated as high-confidence detections.

---

# Detection Severity

| Condition                                   | Initial Severity |
| ------------------------------------------- | ---------------- |
| Normal process                              | Informational    |
| Known administrative process                | Low              |
| Unusual process                             | Low–Medium       |
| Unknown executable                          | Medium           |
| Suspicious command line                     | Medium–High      |
| Suspicious parent-child relationship        | Medium–High      |
| Suspicious process after unauthorized login | High             |
| Privileged suspicious process execution     | High             |
| Confirmed malicious execution               | Critical         |

Severity should be adjusted based on investigation evidence and organizational context.

---

# Structured Process Triage Decision Table

| Observation                                                         | Initial Assessment | Analyst Action                                    | Typical Disposition |
| ------------------------------------------------------------------- | ------------------ | ------------------------------------------------- | ------------------- |
| Known process from expected path                                    | Likely benign      | Validate user and parent process                  | Close / Monitor     |
| Known process from unusual path                                     | Suspicious         | Verify executable and execution context           | Investigate         |
| Unknown executable                                                  | Suspicious         | Review path, hash, user, parent, and command line | Investigate         |
| Process launched by expected parent                                 | Likely benign      | Compare with baseline                             | Close / Monitor     |
| Unusual parent-child relationship                                   | Suspicious         | Investigate process tree and command line         | Investigate         |
| PowerShell launched by administrator during maintenance             | Potentially benign | Validate approved activity                        | Close / Monitor     |
| PowerShell launched by unexpected user                              | Suspicious         | Review command line and authentication history    | Escalate            |
| CMD launched from normal administrative workflow                    | Likely benign      | Validate activity                                 | Close               |
| CMD/PowerShell launched by unusual application                      | High concern       | Investigate parent process and user context       | Escalate            |
| Process executed from Temp/Downloads                                | Suspicious         | Verify file origin and execution context          | Investigate         |
| Suspicious process after failed-login sequence and successful login | High concern       | Correlate authentication and process telemetry    | Escalate            |
| Suspicious process after privileged logon                           | High concern       | Investigate privileged activity and process chain | Escalate            |
| Process with suspicious command line                                | High concern       | Analyze command line and related events           | Escalate            |
| Process activity matches approved change                            | Benign             | Record supporting evidence                        | Close               |
| Process cannot be validated                                         | Unknown            | Gather additional endpoint evidence               | Investigate         |
| Confirmed unauthorized process execution                            | Critical           | Follow incident response procedure                | Escalate / Respond  |

---

# Wazuh Process Investigation

When a process alert is received:

1. Open the Wazuh alert.
2. Record the timestamp.
3. Identify the endpoint.
4. Identify the username.
5. Identify the process.
6. Identify the executable path.
7. Review the command line.
8. Identify the parent process.
9. Review the parent command line.
10. Check the process ID.
11. Check the parent process ID.
12. Search for related authentication events.
13. Search for related PowerShell events.
14. Review preceding and subsequent process activity.
15. Compare the process against the baseline.
16. Determine whether execution is expected.
17. Assess severity.
18. Escalate, monitor, close, or respond.
19. Document the investigation.

---

# Process Investigation Example

Example scenario:

```
4625 — Failed Logon
      ↓
4625 — Failed Logon
      ↓
4624 — Successful Logon
      ↓
4672 — Privileged Logon
      ↓
4688 — powershell.exe
      ↓
Unusual Command Line
```

Investigation questions:

* Who authenticated?
* Where did authentication originate?
* Was the account expected?
* Was privileged access expected?
* What launched PowerShell?
* What command line was used?
* Was the command expected?
* What processes were created afterward?

Possible conclusion:

```
Suspicious authentication
      +
Privileged access
      +
Suspicious process execution
      ↓
Escalate for incident investigation
```

---

# Process Monitoring Scenarios

## Scenario 1 — Normal Process Creation

Launch a normal Windows application.

Verify:

```
4688
or
Sysmon Event ID 1
```

Confirm:

* Process name
* User
* Parent process
* Timestamp

Expected result:

```
Process activity is collected successfully.
```

---

## Scenario 2 — Command Prompt

Open:

```
cmd.exe
```

Verify:

```
Process creation event
Parent process
Username
Command line
```

Expected result:

```
CMD execution is visible in Wazuh.
```

---

## Scenario 3 — PowerShell

Open PowerShell using an authorized lab account.

Verify:

```
powershell.exe
Process creation
Parent process
Command line
```

Expected result:

```
PowerShell execution is visible and can be investigated.
```

---

## Scenario 4 — Unusual Process Path

Execute a controlled test executable from a temporary lab directory.

Verify:

```
Process name
Process path
User
Parent process
Timestamp
```

Expected result:

```
The unusual execution location can be identified during investigation.
```

---

## Scenario 5 — Authentication-to-Process Correlation

Perform controlled authentication activity followed by process execution.

Verify:

```
4624
4672
4688 / Sysmon Event ID 1
```

Expected result:

```
Authentication and process activity can be correlated into one timeline.
```

---

# Evidence Requirements

Capture:

* Wazuh process alert screenshot
* Event ID
* Agent name
* Hostname
* Username
* Process name
* Executable path
* Command line
* Parent process
* Timestamp
* Process ID
* Parent Process ID
* Related authentication events
* Related PowerShell events
* Investigation conclusion

Store evidence under:

```
Evidence/
```

---

# Process Monitoring Checklist

## Visibility

* [ ] Windows process creation logging enabled
* [ ] Event ID 4688 visible
* [ ] Sysmon installed if used
* [ ] Sysmon Event ID 1 visible
* [ ] Process fields parsed correctly
* [ ] Wazuh receives process events

## Investigation

* [ ] Process identified
* [ ] User identified
* [ ] Executable path reviewed
* [ ] Command line reviewed
* [ ] Parent process reviewed
* [ ] Process tree reviewed
* [ ] Authentication activity correlated
* [ ] Baseline compared

## Detection

* [ ] Normal process activity tested
* [ ] CMD execution tested
* [ ] PowerShell execution tested
* [ ] Unusual path tested
* [ ] Suspicious process patterns reviewed
* [ ] False positives considered

## Documentation

* [ ] Evidence captured
* [ ] Timeline documented
* [ ] Analyst decision recorded
* [ ] Final disposition recorded

---

# Troubleshooting Process Monitoring

## Problem 1 — Event ID 4688 Not Appearing

Check:

* Windows process creation auditing
* Advanced Audit Policy configuration
* Security event log
* Wazuh collection configuration
* Agent connectivity

---

## Problem 2 — Sysmon Event ID 1 Not Appearing

Check:

* Sysmon installation
* Sysmon service
* Sysmon configuration
* Operational event channel
* Wazuh collection configuration

---

## Problem 3 — Event Exists Locally but Not in Wazuh

This generally indicates a collection or forwarding problem.

Check:

```
Windows Event Viewer
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Wazuh Indexer / Dashboard
```

---

## Problem 4 — Process Event Exists but No Alert

This may indicate a detection-rule issue rather than a collection issue.

Check:

* Rule conditions
* Rule ID
* Rule level
* Decoder fields
* Rule syntax
* Detection thresholds

---

## Problem 5 — Too Many Process Alerts

Possible causes:

* Detection rule too broad
* Normal processes being flagged
* Threshold too low
* Insufficient baseline

Improve detection by adding context such as:

```
User
Parent Process
Path
Command Line
Frequency
Baseline
```

---

# Common Process Monitoring Mistakes

## Mistake 1 — Treating Every PowerShell Execution as Malicious

PowerShell is widely used for legitimate administration.

**Better approach:**

Analyze user, parent process, command line, path, timing, and baseline.

---

## Mistake 2 — Trusting the Process Name

A familiar process name does not guarantee legitimate execution.

**Better approach:**

Check path, hash when available, command line, and parent process.

---

## Mistake 3 — Ignoring Parent Processes

The parent process often provides important context.

**Better approach:**

Always investigate the process tree.

---

## Mistake 4 — Ignoring Authentication Context

A suspicious process immediately after unusual authentication is more significant than the same process during approved administration.

**Better approach:**

Correlate authentication and process telemetry.

---

## Mistake 5 — Creating Extremely Broad Rules

Broad rules generate excessive alerts.

**Better approach:**

Use multiple contextual conditions and establish a process baseline.

---

# Professional SOC Relevance

Process monitoring is a core endpoint detection capability.

A SOC analyst should be able to:

* Interpret Windows process creation events
* Analyze Event ID 4688
* Analyze Sysmon Event ID 1
* Understand parent-child process relationships
* Analyze command lines
* Identify unusual execution paths
* Correlate authentication and process activity
* Investigate PowerShell and command-shell execution
* Perform process-tree analysis
* Use SIEM searches
* Triage process alerts
* Distinguish legitimate administration from suspicious behavior
* Document investigation findings

These capabilities are directly relevant to SOC L1 alert triage and endpoint investigation.

---

# Conclusion

Process monitoring provides visibility into what is executing on a Windows endpoint and how processes are related to one another.

The investigation workflow should follow:

```
Process Created
      ↓
Identify User
      ↓
Identify Process
      ↓
Review Path
      ↓
Review Command Line
      ↓
Identify Parent Process
      ↓
Build Process Tree
      ↓
Correlate Authentication
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

**A process should be analyzed in context — process name, path, command line, parent process, user, timestamp, and related security events.**

Related documentation:

* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `10-PowerShell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
