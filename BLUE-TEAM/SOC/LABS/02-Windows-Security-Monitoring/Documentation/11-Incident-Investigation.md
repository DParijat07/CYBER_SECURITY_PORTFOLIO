# Incident Investigation

## Purpose

Incident investigation is the process of determining what happened during a suspected security event, how it happened, what systems and accounts were involved, and whether the activity represents a true security incident.

In this Windows Security Monitoring Lab, incident investigation uses Windows telemetry collected by Wazuh to reconstruct activity and support a structured SOC investigation.

The investigation workflow is:

**Alert → Validate → Collect Evidence → Correlate Events → Build Timeline → Determine Root Cause → Assess Impact → Decide Response → Document Findings**

---

## Incident Investigation Objectives

The primary objectives are:

* Validate whether an alert represents suspicious activity.
* Identify the affected Windows endpoint.
* Identify the involved user account.
* Determine the source of the activity.
* Analyze relevant Windows Event IDs.
* Correlate authentication, process, PowerShell, and account activity.
* Build a chronological event timeline.
* Determine the likely attack or activity sequence.
* Assess potential impact.
* Identify indicators of compromise (IoCs).
* Determine whether escalation is required.
* Preserve investigation evidence.
* Document the investigation clearly.

---

## Incident Investigation Architecture

The investigation process follows:

```
Windows Endpoint
      ↓
Windows Event Logs
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Detection Alert
      ↓
Analyst Investigation
      ↓
Event Correlation
      ↓
Timeline Reconstruction
      ↓
Incident Assessment
      ↓
Response Decision
      ↓
Evidence + Report
```

---

## Incident Investigation vs Alert Analysis

Alert analysis and incident investigation are related but different activities.

| Activity               | Purpose                                                  |
| ---------------------- | -------------------------------------------------------- |
| Alert Analysis         | Determine whether an individual alert requires attention |
| Incident Investigation | Determine what happened across multiple related events   |
| Detection              | Identify potentially suspicious behavior                 |
| Investigation          | Establish context, sequence, cause, and impact           |
| Response               | Contain, eradicate, and recover from confirmed incidents |

A single alert may be benign.

Multiple related alerts and events may reveal a complete attack sequence.

---

# Investigation Workflow

## Step 1 — Identify the Alert

Start with the alert that triggered the investigation.

Record:

* Alert timestamp
* Alert rule
* Alert severity
* Endpoint
* Username
* Source IP
* Event ID
* Event channel
* Process information
* Command line
* Detection description

Example:

```
Alert:
Windows Failed Logon

Event ID:
4625

Endpoint:
WIN-MONITOR

User:
testuser
```

---

## Step 2 — Validate the Alert

Determine whether the alert is:

* Expected activity
* Administrative activity
* Normal user behavior
* Lab-generated activity
* Suspicious activity
* Potential security incident

Ask:

* Was this activity expected?
* Was the user authorized?
* Was the endpoint involved in the activity?
* Does the timestamp match known activity?
* Is the source IP expected?
* Are there related events?

Do not immediately classify every alert as malicious.

---

## Step 3 — Identify the Affected Endpoint

Determine which Windows system generated the event.

Record:

* Hostname
* Agent name
* Agent ID
* IP address
* Operating system
* Event source

This establishes the investigation scope.

---

## Step 4 — Identify the User

Determine which account was involved.

Important fields may include:

* `win.eventdata.targetUserName`
* `win.eventdata.subjectUserName`
* `win.eventdata.user`
* Account domain
* Logon ID

Compare the account with the expected user or administrative activity.

---

## Step 5 — Identify the Source

For authentication-related events, investigate the source.

Useful information may include:

* Source IP
* Workstation name
* Logon type
* Authentication package
* Target account
* Source computer

Example:

```
Source IP: 192.168.56.20
Target User: testuser
Logon Type: 3
Event ID: 4625
```

---

# Important Windows Events for Investigation

| Event ID | Activity             | Investigation Value                          |
| -------- | -------------------- | -------------------------------------------- |
| 4624     | Successful logon     | Identify successful authentication           |
| 4625     | Failed logon         | Identify authentication failures             |
| 4634     | Logoff               | Establish session termination                |
| 4672     | Special privileges   | Identify privileged sessions                 |
| 4688     | Process creation     | Identify executed processes                  |
| 4720     | Account creation     | Identify new accounts                        |
| 4738     | Account modification | Identify account changes                     |
| 4740     | Account lockout      | Investigate repeated authentication failures |

PowerShell events:

| Event ID | Activity                  |
| -------- | ------------------------- |
| 400      | PowerShell engine started |
| 403      | PowerShell engine stopped |
| 4103     | Module logging            |
| 4104     | Script Block Logging      |

Sysmon:

| Event ID | Activity         |
| -------- | ---------------- |
| 1        | Process creation |

---

# Event Correlation

Incident investigation should not depend on a single event.

Correlate related telemetry.

Example:

```
4625
Failed Logon
   ↓
4625
Failed Logon
   ↓
4624
Successful Logon
   ↓
4672
Privileged Logon
   ↓
4688
Process Creation
   ↓
4104
PowerShell Script Block
```

This sequence may indicate suspicious authentication followed by privileged activity and PowerShell execution.

The actual interpretation depends on the environment and investigation evidence.

---

# Authentication Investigation

Authentication events should be examined for:

* Repeated failed logons
* Successful logon after failures
* Unusual logon types
* Unusual source IP addresses
* Privileged logons
* Account lockouts
* Unexpected administrative accounts
* Activity outside the expected baseline

Useful events:

```
4624
4625
4634
4672
4740
```

---

## Failed Authentication Investigation

Investigate:

* Number of failures
* Time interval
* Target username
* Source IP
* Workstation
* Logon type
* Authentication package
* Whether a successful logon followed

Example investigation:

```
10 failed logons
      ↓
Same username
      ↓
Same source IP
      ↓
1 successful logon
      ↓
Investigate the successful session
```

Repeated failures followed by a successful authentication deserve additional investigation.

---

# Privileged Activity Investigation

Event ID `4672` can indicate that special privileges were assigned to a new logon session.

Investigate:

* Account name
* Logon ID
* Timestamp
* Source
* Associated 4624 event
* Subsequent process activity

Correlate:

```
4624
Successful Logon
      +
4672
Special Privileges
      +
4688
Process Creation
```

This helps determine what occurred after a privileged session was established.

---

# Process Investigation

Process investigation focuses on:

* Process name
* Executable path
* Command line
* Parent process
* Parent-child relationship
* User
* Timestamp
* Process ID
* Hash, when available
* Network activity, when available

Important telemetry:

```
Windows Security Event 4688
Sysmon Event 1
```

---

## Process Tree Investigation

A process should be investigated in context.

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

The process tree provides context that a single process event cannot provide.

Investigate whether the parent-child relationship is expected.

---

# PowerShell Investigation

PowerShell activity should be correlated with:

* User authentication
* Process creation
* Script Block Logging
* Module logging
* Parent process
* Command line
* Timestamp

Important events:

```
400
403
4103
4104
```

Process telemetry:

```
4688
Sysmon 1
```

Example:

```
4624
Successful Logon
    ↓
4688
powershell.exe
    ↓
4104
Script Block Activity
    ↓
4688
cmd.exe
```

The analyst should investigate the complete sequence rather than evaluating the PowerShell event alone.

---

# Account Activity Investigation

Investigate account-related events such as:

* Account creation
* Account modification
* Account lockout
* Privilege assignment
* Unexpected administrative activity

Important events:

```
4720
4738
4740
4672
```

Questions:

* Who created or modified the account?
* When did it happen?
* Was the activity authorized?
* Was the account subsequently used?
* Did process activity follow?

---

# Timeline Reconstruction

Timeline reconstruction is one of the most important investigation activities.

Create a chronological sequence of relevant events.

Example:

| Time     | Event | Activity         | Interpretation           |
| -------- | ----- | ---------------- | ------------------------ |
| 10:01:02 | 4625  | Failed logon     | Authentication failure   |
| 10:01:05 | 4625  | Failed logon     | Repeated failure         |
| 10:01:10 | 4624  | Successful logon | Authentication succeeded |
| 10:01:11 | 4672  | Privileged logon | Special privileges       |
| 10:01:20 | 4688  | PowerShell       | Process created          |
| 10:01:21 | 4104  | Script block     | PowerShell activity      |

The timeline should answer:

**What happened first?**

**What happened next?**

**What happened after authentication?**

**What processes were executed?**

**Was PowerShell involved?**

**What account performed the activity?**

---

# Wazuh Investigation

Wazuh provides centralized visibility into the Windows endpoint.

The analyst should use Wazuh to:

1. Locate the alert.
2. Review the alert details.
3. Identify the endpoint.
4. Identify the user.
5. Review the event ID.
6. Review the event channel.
7. Examine relevant event fields.
8. Search related events.
9. Correlate events by timestamp.
10. Investigate authentication activity.
11. Investigate process activity.
12. Investigate PowerShell activity.
13. Build the event timeline.
14. Assess the activity.
15. Record the investigation result.

Field names and dashboard search behavior may vary depending on the Wazuh version and configuration.

---

# Actionable Wazuh Search Examples

Use the Wazuh event fields available in the lab.

### Failed Logons

```
win.system.eventID:4625
```

### Successful Logons

```
win.system.eventID:4624
```

### Privileged Logons

```
win.system.eventID:4672
```

### Account Lockouts

```
win.system.eventID:4740
```

### Process Creation

```
win.system.eventID:4688
```

### PowerShell

```
win.system.eventID:4104
```

### PowerShell Process Creation

```
win.system.eventID:4688 AND win.eventdata.newProcessName:*powershell.exe*
```

### Sysmon Process Creation

```
win.system.eventID:1
```

### Investigate a Specific User

```
win.eventdata.targetUserName:"testuser"
```

### Investigate PowerShell Activity for a User

```
win.system.eventID:4104 AND win.eventdata.subjectUserName:"testuser"
```

### Authentication + Process Investigation

Search the relevant time range for:

```
4625 → 4624 → 4672 → 4688
```

### PowerShell Investigation

Search the relevant time range for:

```
4688 → 4104
```

These searches are investigation examples. Exact field names and search syntax can vary with Wazuh configuration and version.

---

# Investigation Correlation Matrix

| Investigation Question          | Primary Events | Supporting Events    |
| ------------------------------- | -------------- | -------------------- |
| Was authentication suspicious?  | 4625           | 4624, 4740           |
| Was privileged access obtained? | 4672           | 4624                 |
| What process executed?          | 4688           | Sysmon 1             |
| Was PowerShell executed?        | 4688           | 400, 403, 4103, 4104 |
| Was an account created?         | 4720           | 4624, 4672           |
| Was an account modified?        | 4738           | 4624                 |
| Was an account locked?          | 4740           | 4625                 |
| What happened after login?      | 4624           | 4672, 4688, 4104     |

---

# Structured Investigation Decision Table

| Observation                                    | Assessment        | Action                                | Disposition            |
| ---------------------------------------------- | ----------------- | ------------------------------------- | ---------------------- |
| Single expected failed logon                   | Likely benign     | Verify context                        | Close                  |
| Repeated failed logons                         | Suspicious        | Investigate source and account        | Monitor/Escalate       |
| Failed logons followed by success              | Higher concern    | Correlate session activity            | Escalate if suspicious |
| Unexpected privileged logon                    | Suspicious        | Investigate account and source        | Escalate               |
| Unknown process                                | Suspicious        | Investigate process tree/path         | Escalate if malicious  |
| PowerShell execution by expected administrator | Context dependent | Review command/script                 | Close or monitor       |
| Obfuscated/suspicious PowerShell               | High concern      | Investigate script and parent process | Escalate               |
| Unexpected account creation                    | High concern      | Identify creator and usage            | Escalate               |
| Account lockout with repeated failures         | Suspicious        | Investigate authentication source     | Monitor/Escalate       |
| Multiple correlated suspicious events          | High confidence   | Initiate incident response            | Escalate               |

---

# Root Cause Analysis

The investigation should attempt to determine the root cause.

Possible causes include:

* User error
* Misconfiguration
* Administrative activity
* Scheduled task
* Application behavior
* Credential issue
* Suspicious authentication
* Unauthorized account activity
* Suspicious process execution
* Malicious PowerShell activity

The analyst should avoid unsupported conclusions.

Use evidence-based statements such as:

```
"The observed activity is consistent with..."
```

rather than:

```
"The attacker definitely..."
```

unless the evidence supports that conclusion.

---

# Impact Assessment

Determine the potential impact.

Questions:

* Which endpoint was affected?
* Which user account was involved?
* Was privileged access obtained?
* Were suspicious processes executed?
* Was PowerShell used?
* Were accounts created or modified?
* Did activity continue after the initial event?
* Are additional endpoints involved?

Possible impact categories:

```
Low
Medium
High
Critical
```

Impact should be based on observed evidence and organizational context.

---

# Indicator of Compromise Collection

During investigation, collect relevant IoCs when available.

Examples:

* IP addresses
* Usernames
* Hostnames
* Process names
* Executable paths
* File hashes
* Domains
* URLs
* Suspicious command lines
* Malicious scripts
* Account names

Do not treat every normal value as an IoC.

Record why an indicator is considered suspicious.

---

# Evidence Collection

Store investigation evidence under:

```
Evidence/
```

Possible evidence:

* Wazuh alert screenshots
* Event details
* Event IDs
* Relevant log entries
* Process information
* PowerShell events
* Timeline
* IoC list
* Investigation notes
* Detection rule information

Evidence should be timestamped and clearly named.

Example:

```
Evidence/
├── alert-4625.png
├── successful-logon-4624.png
├── privileged-logon-4672.png
├── process-4688.png
└── powershell-4104.png
```

---

# Hands-On Lab Procedure

## Step 1 — Verify Wazuh

Confirm that the Windows endpoint is connected to the Wazuh Manager.

Verify:

* Agent status
* Endpoint visibility
* Event ingestion

---

## Step 2 — Generate Authentication Activity

Generate controlled failed authentication attempts in the authorized lab.

Verify Event ID:

```
4625
```

Record:

* Timestamp
* Username
* Source
* Logon type

---

## Step 3 — Generate Successful Authentication

Perform a controlled successful authentication.

Verify:

```
4624
```

Correlate it with the previous failed attempts.

---

## Step 4 — Generate Privileged Activity

Use an authorized administrative account in the lab.

Verify:

```
4672
```

Correlate it with the corresponding successful logon.

---

## Step 5 — Generate Process Activity

Launch a normal process.

Example:

```
cmd.exe
```

Execute:

```
whoami
```

Verify:

```
4688
```

If Sysmon is configured, verify:

```
Sysmon Event ID 1
```

---

## Step 6 — Generate PowerShell Activity

Launch PowerShell and perform controlled commands.

Example:

```
whoami

ipconfig
```

Verify:

```
400
403
4103
4104
```

Also verify process telemetry:

```
4688
Sysmon Event ID 1
```

---

## Step 7 — Investigate in Wazuh

Search for the generated events.

Review:

* Event ID
* Timestamp
* Endpoint
* Username
* Process
* Command line
* Parent process
* Source information

---

## Step 8 — Build a Timeline

Create a timeline containing the relevant events.

Example:

```
Authentication
     ↓
Privileged Activity
     ↓
Process Creation
     ↓
PowerShell Activity
```

---

## Step 9 — Perform Triage

Classify the activity:

```
Benign
Suspicious
Malicious / Confirmed Incident
```

Record the reasoning.

---

## Step 10 — Collect Evidence

Save screenshots and relevant event information under:

```
Evidence/
```

---

## Step 11 — Document Findings

Create the investigation result under:

```
Reports/
```

The report should contain:

* Summary
* Detection
* Timeline
* Evidence
* Analysis
* IoCs
* Impact assessment
* Root cause
* Disposition
* Recommended response

---

# Hands-On Investigation Scenarios

## Scenario 1 — Repeated Failed Logons

Generate multiple controlled failed authentication attempts.

Investigate:

```
4625 → 4625 → 4625
```

Determine:

* Source
* Account
* Frequency
* Time interval
* Whether the behavior is expected

---

## Scenario 2 — Failed Logons Followed by Success

Generate:

```
4625
4625
4624
```

Investigate whether the successful authentication is related to the failed attempts.

---

## Scenario 3 — Privileged Session

Generate:

```
4624
4672
```

Determine:

* Account
* Timestamp
* Logon ID
* Source
* Subsequent process activity

---

## Scenario 4 — Process Investigation

Generate:

```
4688
Sysmon 1
```

Investigate:

* Process
* Parent
* Path
* Command line
* User

---

## Scenario 5 — PowerShell Investigation

Generate:

```
4688
4104
```

Investigate:

* User
* Parent process
* Script block
* Command
* Timestamp

---

## Scenario 6 — Full Investigation Chain

Simulate:

```
Failed Authentication
        ↓
Successful Authentication
        ↓
Privileged Logon
        ↓
PowerShell Process
        ↓
PowerShell Script Block
```

Investigate the entire sequence and determine whether it represents:

```
Normal Administrative Activity
         OR
Suspicious Activity
```

Document the conclusion using evidence.

---

# Investigation Quality Criteria

A good investigation should:

* Start from a validated alert.
* Identify the affected endpoint.
* Identify involved accounts.
* Establish a timeline.
* Correlate multiple events.
* Analyze process and PowerShell activity.
* Identify relevant IoCs.
* Assess impact.
* Avoid unsupported assumptions.
* Preserve evidence.
* Produce a clear conclusion.
* Define the next action.

---

# Common Investigation Mistakes

Avoid:

* Investigating only one event.
* Ignoring timestamps.
* Ignoring source IP information.
* Ignoring the user account.
* Ignoring parent-child processes.
* Treating every PowerShell event as malicious.
* Treating every failed login as an attack.
* Failing to correlate events.
* Modifying evidence unnecessarily.
* Making unsupported conclusions.
* Closing alerts without documenting the reason.

---

# Investigation Checklist

* [ ] Alert identified
* [ ] Alert validated
* [ ] Endpoint identified
* [ ] User identified
* [ ] Source identified
* [ ] Event ID reviewed
* [ ] Authentication events reviewed
* [ ] Privileged activity reviewed
* [ ] Process activity reviewed
* [ ] PowerShell activity reviewed
* [ ] Related events correlated
* [ ] Timeline created
* [ ] IoCs identified
* [ ] Impact assessed
* [ ] Root cause assessed
* [ ] Evidence preserved
* [ ] Investigation documented
* [ ] Disposition determined
* [ ] Response/escalation decision recorded

---

# Professional SOC Relevance

Incident investigation is a core SOC analyst skill.

A SOC analyst must be able to move beyond:

```
"An alert occurred."
```

and determine:

```
What happened?
When did it happen?
Which system was affected?
Which account was involved?
What caused the alert?
What happened before it?
What happened after it?
Is the activity malicious?
What is the impact?
What should happen next?
```

This lab develops practical skills in:

* Alert investigation
* Event correlation
* Windows security telemetry
* Wazuh investigation
* Timeline analysis
* Authentication investigation
* Process investigation
* PowerShell investigation
* IoC identification
* Incident triage
* Evidence handling
* Security documentation

These skills directly support entry-level SOC and security monitoring roles.

---

# Conclusion

Incident investigation transforms security telemetry into an evidence-based understanding of what happened.

The Windows Security Monitoring Lab follows:

**Alert → Validate → Collect Evidence → Correlate Events → Build Timeline → Determine Root Cause → Assess Impact → Decide Response → Document Findings**

The goal is not simply to identify an alert.

The goal is to understand the complete activity sequence, determine whether the behavior is security-relevant, preserve supporting evidence, and make a defensible SOC decision.

**Final Investigation Workflow:**

```
Detect
  ↓
Validate
  ↓
Investigate
  ↓
Correlate
  ↓
Reconstruct Timeline
  ↓
Assess Impact
  ↓
Decide
  ↓
Document
```

---

## Related Documentation

* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-PowerShell-Monitoring.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
