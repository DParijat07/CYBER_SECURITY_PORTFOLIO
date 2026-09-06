# Authentication Monitoring

## Purpose

Authentication monitoring is the process of collecting, analyzing, and correlating Windows authentication events to identify unauthorized access, credential abuse, brute-force activity, account compromise, and suspicious privileged access.

In this lab, Windows authentication telemetry is collected and analyzed through Wazuh.

The primary objective is to understand normal authentication behavior and identify activity that requires investigation.

---

# Authentication Monitoring Objectives

The objectives of this lab are to:

* Monitor successful authentication
* Monitor failed authentication
* Identify repeated authentication failures
* Detect suspicious successful logons
* Monitor privileged logons
* Monitor account lockouts
* Identify unusual logon types
* Correlate authentication events
* Establish an authentication baseline
* Investigate suspicious authentication activity
* Generate evidence for SOC investigation

---

# Authentication Monitoring Architecture

The monitoring flow is:

```
Windows Endpoint
      ↓
Windows Security Logs
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Authentication Events
      ↓
Detection Rules
      ↓
Wazuh Alerts
      ↓
Analyst Investigation
      ↓
Triage / Escalation / Closure
```

---

# Important Windows Authentication Events

| Event ID | Event                       | Security Relevance                            |
| -------- | --------------------------- | --------------------------------------------- |
| 4624     | Successful Logon            | Identifies successful authentication          |
| 4625     | Failed Logon                | Identifies failed authentication              |
| 4634     | Logoff                      | Helps establish session duration              |
| 4672     | Special Privileges Assigned | Indicates privileged logon activity           |
| 4740     | Account Locked Out          | May indicate repeated authentication failures |

---

# Event ID 4624 — Successful Logon

Event ID 4624 indicates that an account successfully logged on to Windows.

Important fields may include:

```
TargetUserName
TargetDomainName
LogonType
IpAddress
WorkstationName
LogonId
```

A successful logon is not automatically malicious.

The analyst must determine:

* Who logged in?
* From where?
* When?
* Using which logon type?
* Is the activity expected?
* Were there previous failed attempts?
* Did suspicious activity occur after authentication?

---

# Successful Logon Investigation

When investigating Event ID 4624, record:

* Username
* Domain
* Source IP
* Workstation
* Logon type
* Timestamp
* Logon ID
* Endpoint

Then correlate the event with:

* Previous failed logons
* Privileged events
* Process creation
* PowerShell execution
* Account changes
* Other endpoint activity

---

# Event ID 4625 — Failed Logon

Event ID 4625 indicates a failed logon attempt.

Important fields may include:

```
TargetUserName
TargetDomainName
LogonType
IpAddress
FailureReason
Status
SubStatus
```

A single failed authentication attempt may be normal.

Multiple failures involving the same account, source IP, or short time period require additional investigation.

---

# Failed Logon Investigation

For a failed authentication event, determine:

* Which account was targeted?
* Which endpoint received the attempt?
* What was the source IP?
* What logon type was used?
* How many failures occurred?
* Were the attempts distributed across multiple accounts?
* Did a successful authentication occur afterward?

---

# Event ID 4634 — Logoff

Event ID 4634 indicates that a logon session was terminated.

It can help analysts understand:

* Session duration
* User activity timeline
* Login/logout relationships
* Whether a suspicious session ended

Logoff events are normally used together with authentication events rather than analyzed independently.

---

# Event ID 4672 — Special Privileges Assigned

Event ID 4672 indicates that special privileges were assigned to a new logon session.

This event is particularly important when associated with:

* Administrator accounts
* SYSTEM
* Unexpected users
* Unusual endpoints
* Suspicious source addresses
* Unusual timestamps

A privileged event alone does not prove compromise.

It should be correlated with the corresponding successful logon and subsequent activity.

---

# Event ID 4740 — Account Lockout

Event ID 4740 indicates that a user account was locked out.

Possible causes include:

* Repeated incorrect passwords
* Brute-force attempts
* Password spraying
* Stale credentials
* Scheduled tasks using old credentials
* Services using outdated credentials
* Legitimate user mistakes

The analyst should investigate the surrounding authentication activity before determining the cause.

---

# Logon Types

| Logon Type | Meaning           | Monitoring Relevance      |
| ---------- | ----------------- | ------------------------- |
| 2          | Interactive       | Local interactive login   |
| 3          | Network           | Network resource access   |
| 4          | Batch             | Scheduled/batch activity  |
| 5          | Service           | Service account activity  |
| 7          | Unlock            | Workstation unlock        |
| 8          | NetworkCleartext  | Network authentication    |
| 9          | NewCredentials    | Alternate credentials     |
| 10         | RemoteInteractive | Remote Desktop            |
| 11         | CachedInteractive | Cached domain credentials |

Logon type must always be interpreted in context.

For example, Logon Type 10 may be expected for an administrator using Remote Desktop, but unexpected RDP authentication can require investigation.

---

# Interactive Logon Monitoring

Interactive authentication should be monitored for:

* Unusual users
* Unusual endpoints
* Unusual login times
* Unexpected administrative access
* Authentication after repeated failures

Baseline normal interactive authentication before creating high-confidence detections.

---

# Network Logon Monitoring

Network logons can occur when users or systems access network resources.

Monitor for:

* Unusual source systems
* Unexpected accounts
* Repeated authentication failures
* Authentication between unusual hosts
* Service-account anomalies

---

# Remote Interactive Logon

Remote Interactive Logon, commonly associated with Remote Desktop activity, should receive additional attention.

Investigate:

* Source IP
* Username
* Login time
* Number of previous failures
* Destination endpoint
* Privilege level
* Processes executed after login

A successful remote logon following many failed attempts should be investigated carefully.

---

# Authentication Baseline

A baseline helps distinguish normal authentication from suspicious authentication.

Record normal:

* User accounts
* Login times
* Source systems
* Source IP addresses
* Logon types
* Administrative accounts
* Remote access patterns

Example baseline:

```
Normal User:
Local interactive login
Expected workstation
Business hours

Administrator:
Administrative workstation
Expected maintenance window
Known source
```

Any major deviation should trigger additional investigation.

---

# Authentication Detection Logic

Authentication detection should consider more than individual events.

Useful detection patterns include:

```
Multiple failed logons
       ↓
Same account / source
       ↓
Short time period
       ↓
Successful logon
       ↓
Privileged activity
       ↓
Suspicious process activity
```

Correlation provides stronger detection confidence than a single authentication event.

---

# Failed Logon Threshold Detection

Repeated failed authentication attempts may indicate:

* Brute-force activity
* Password spraying
* Credential guessing
* Misconfigured services
* User error

Example conceptual threshold:

```
5+ failed authentication events
within a short time period
from the same source
against the same account
```

The threshold must be tuned against the normal environment to reduce false positives.

---

# Successful Logon After Failed Attempts

A particularly useful correlation is:

```
Failed Logon
      ↓
Failed Logon
      ↓
Failed Logon
      ↓
Successful Logon
```

This pattern does not automatically indicate compromise.

Investigate:

* Source IP
* Target account
* Number of failures
* Time interval
* Logon type
* Subsequent privileged activity
* Subsequent process activity

---

# Account Lockout Correlation

A useful investigation sequence is:

```
4625 — Failed Logon
      ↓
4625 — Failed Logon
      ↓
4625 — Failed Logon
      ↓
4740 — Account Lockout
```

This may indicate repeated authentication failures.

The analyst should determine whether the activity originated from:

* A user
* A workstation
* A service
* A scheduled task
* An external source

---

# Authentication Event Correlation

Authentication investigation should correlate multiple event types.

Example:

```
4625 Failed Logon
      ↓
4624 Successful Logon
      ↓
4672 Privileged Logon
      ↓
4688 Process Creation
      ↓
PowerShell Activity
```

This sequence provides significantly more context than analyzing Event ID 4625 alone.

---

# Actionable Wazuh Search Examples

Wazuh search syntax may vary depending on the Wazuh/OpenSearch version, index configuration, and field mappings.

The following are practical search patterns for this lab.

## Search 1 — All Failed Logons

Search for Windows failed authentication events:

```
win.system.eventID:4625
```

Use this search to identify:

* Failed authentication attempts
* Targeted usernames
* Source IP addresses
* Authentication frequency
* Authentication time patterns

---

## Search 2 — All Successful Logons

Search for successful authentication:

```
win.system.eventID:4624
```

Review:

```
win.eventdata.targetUserName
win.eventdata.ipAddress
win.eventdata.logonType
```

Compare successful logons with preceding failed authentication events.

---

## Search 3 — Privileged Authentication

Search for special privilege assignment:

```
win.system.eventID:4672
```

Investigate:

* Username
* Logon ID
* Endpoint
* Timestamp
* Corresponding 4624 event
* Subsequent process activity

---

## Search 4 — Account Lockouts

Search for account lockout events:

```
win.system.eventID:4740
```

Investigate:

* Locked account
* Caller computer
* Timestamp
* Previous 4625 events
* Possible stale credentials
* Possible password attack

---

## Search 5 — Specific Username

When investigating a particular account, search using the username field:

```
win.eventdata.targetUserName:"Administrator"
```

Replace `Administrator` with the account being investigated.

Use this to build an account-specific authentication timeline.

---

## Search 6 — Specific Source IP

When investigating a suspicious source:

```
win.eventdata.ipAddress:"192.168.1.100"
```

Replace the example address with the source IP identified in the alert.

Use the result to determine whether the same source generated:

* Failed logons
* Successful logons
* Multiple targeted accounts
* Privileged authentication

---

## Search 7 — Remote Interactive Authentication

Search for successful authentication events:

```
win.system.eventID:4624
```

Then inspect:

```
win.eventdata.logonType:10
```

This can help identify Remote Desktop authentication activity.

Investigate the source IP, username, timestamp, and subsequent endpoint activity.

---

## Search 8 — Authentication Activity for One Account

Combine the Event ID and username when supported by the configured search syntax:

```
win.system.eventID:4625 AND win.eventdata.targetUserName:"testuser"
```

This helps determine whether a specific account is experiencing repeated authentication failures.

---

## Search 9 — Failed and Successful Authentication Timeline

Search separately for:

```
win.system.eventID:4625
```

and:

```
win.system.eventID:4624
```

Sort results chronologically and compare:

```
Timestamp
Username
Source IP
Logon Type
Endpoint
```

This is useful for identifying a:

```
Failed → Failed → Failed → Successful
```

authentication sequence.

---

## Search 10 — Privileged Authentication After Login

Search:

```
win.system.eventID:4624
```

and:

```
win.system.eventID:4672
```

Then correlate:

* Username
* Logon ID
* Endpoint
* Timestamp

The objective is to determine whether a successful login resulted in privileged access.

---

# Wazuh Authentication Investigation

When an authentication alert is received:

1. Open the alert in Wazuh.
2. Record the alert timestamp.
3. Identify the affected agent.
4. Identify the username.
5. Identify the source IP.
6. Identify the Windows Event ID.
7. Identify the logon type.
8. Review the authentication result.
9. Search for previous failed attempts.
10. Search for successful authentication.
11. Search for privileged activity.
12. Search for account lockouts.
13. Search for process creation after authentication.
14. Build a timeline.
15. Compare activity against the authentication baseline.
16. Determine whether the activity is expected or suspicious.
17. Assign an appropriate severity.
18. Escalate, contain, monitor, or close the alert.
19. Document the investigation.

---

# Structured Authentication Triage Decision Table

| Observation                                            | Initial Assessment | Analyst Action                                          | Typical Disposition   |
| ------------------------------------------------------ | ------------------ | ------------------------------------------------------- | --------------------- |
| Single failed logon from known user/device             | Likely benign      | Check baseline and surrounding events                   | Close / Monitor       |
| Multiple failed logons from known user/device          | Needs review       | Check frequency, timing, and user activity              | Monitor / Investigate |
| Multiple failures from unknown source                  | Suspicious         | Investigate source IP and targeted accounts             | Investigate           |
| Multiple accounts targeted from one source             | High concern       | Check for password-spraying pattern                     | Escalate              |
| Failed logons followed by successful logon             | Suspicious         | Correlate source, user, timing, and post-login activity | Investigate           |
| Successful login from known source during normal hours | Likely benign      | Validate against baseline                               | Close / Monitor       |
| Successful login from unusual source                   | Suspicious         | Validate user, source, location/context, and timing     | Investigate           |
| Remote Interactive login from unexpected source        | High concern       | Investigate RDP activity and subsequent processes       | Escalate              |
| Privileged logon by expected administrator             | Potentially benign | Validate maintenance/change activity                    | Close / Monitor       |
| Privileged logon by unexpected account                 | High concern       | Investigate account and subsequent activity             | Escalate              |
| Account lockout after repeated failures                | Suspicious         | Correlate 4625 and 4740 events                          | Investigate           |
| New authentication followed by suspicious process      | High concern       | Expand investigation to endpoint activity               | Escalate              |
| Authentication followed by PowerShell activity         | High concern       | Correlate PowerShell and process telemetry              | Escalate              |
| Authentication matches approved maintenance activity   | Benign             | Record supporting evidence                              | Close                 |
| Authentication cannot be validated                     | Unknown            | Gather additional evidence and escalate if necessary    | Investigate           |
| Authentication indicates confirmed unauthorized access | Critical           | Follow incident response procedure                      | Escalate / Respond    |

---

# Authentication Investigation Example

Example scenario:

```
4625 — Failed Logon
Username: administrator
Source: 192.168.1.50

↓

4625 — Failed Logon
Username: administrator
Source: 192.168.1.50

↓

4625 — Failed Logon
Username: administrator
Source: 192.168.1.50

↓

4624 — Successful Logon
Username: administrator
Source: 192.168.1.50
```

The analyst should then search for:

```
4672 — Privileged Activity
4688 — Process Creation
PowerShell Events
Account Changes
```

If suspicious activity follows the successful authentication, the alert should be escalated for deeper endpoint investigation.

If the source and activity match an approved administrator workflow, the analyst should document the validation and close or monitor the alert.

---

# Authentication Monitoring Scenarios

## Scenario 1 — Normal Login

Generate a normal interactive login.

Verify:

```
4624
Expected username
Expected endpoint
Expected logon type
```

Expected result:

```
Authentication is recorded
No suspicious alert is generated
```

---

## Scenario 2 — Failed Authentication

Generate controlled failed authentication attempts.

Verify:

```
4625
Username
Source
Timestamp
```

Expected result:

```
Failed authentication is collected
Relevant detection logic identifies suspicious repetition when threshold is reached
```

---

## Scenario 3 — Repeated Failed Authentication

Generate multiple controlled authentication failures.

Verify:

```
Event frequency
Source
Target account
Detection threshold
```

Expected result:

```
Repeated authentication activity is identified
```

---

## Scenario 4 — Successful Login After Failures

Generate controlled failed attempts followed by a successful login.

Verify:

```
4625
4625
4625
4624
```

Expected result:

```
Authentication sequence can be correlated and investigated
```

---

## Scenario 5 — Privileged Authentication

Perform authorized administrative activity in the lab.

Verify:

```
4624
4672
```

Expected result:

```
Privileged authentication can be identified and correlated
```

---

## Scenario 6 — Account Lockout

Generate controlled authentication failures until the test account is locked.

Verify:

```
4625
4740
```

Expected result:

```
Account lockout is visible and can be correlated with preceding failures
```

---

# Evidence Collection

Capture evidence such as:

* Wazuh alert screenshot
* Event ID
* Username
* Source IP
* Timestamp
* Logon type
* Rule ID
* Rule severity
* Related events
* Investigation timeline
* Analyst conclusion

Store evidence under:

```
Evidence/
```

Do not collect unnecessary personal or sensitive information.

---

# Authentication Monitoring Checklist

## Authentication Visibility

* [ ] Windows Security logs are collected
* [ ] Event ID 4624 is visible
* [ ] Event ID 4625 is visible
* [ ] Event ID 4634 is visible
* [ ] Event ID 4672 is visible
* [ ] Event ID 4740 is visible

## Investigation

* [ ] Username identified
* [ ] Source identified
* [ ] Logon type identified
* [ ] Timestamp verified
* [ ] Related events searched
* [ ] Authentication baseline checked
* [ ] Suspicious activity classified

## Detection

* [ ] Failed authentication detection tested
* [ ] Repeated failures tested
* [ ] Successful-after-failure pattern tested
* [ ] Privileged authentication reviewed
* [ ] Account lockout reviewed

## Documentation

* [ ] Evidence captured
* [ ] Timeline documented
* [ ] Analyst conclusion recorded
* [ ] Final disposition recorded

---

# Common Authentication Monitoring Mistakes

## Mistake 1 — Treating Every Failed Login as an Attack

A single failed login is common.

**Better approach:**

Analyze frequency, source, account, timing, and surrounding events.

---

## Mistake 2 — Ignoring Successful Authentication

A successful login after repeated failures may provide important context.

**Better approach:**

Always correlate successful and failed authentication.

---

## Mistake 3 — Ignoring Logon Type

The same username may legitimately authenticate through different mechanisms.

**Better approach:**

Always inspect the logon type.

---

## Mistake 4 — Ignoring Source Information

The source can help distinguish expected activity from suspicious activity.

**Better approach:**

Record and investigate source IP/workstation information.

---

## Mistake 5 — Investigating Events in Isolation

Individual events often provide insufficient context.

**Better approach:**

Correlate authentication with privilege, process, PowerShell, and account activity.

---

## Mistake 6 — Creating Overly Sensitive Detection Rules

Very low thresholds can generate excessive false positives.

**Better approach:**

Establish a baseline and tune detection thresholds.

---

# Professional SOC Relevance

Authentication monitoring is a fundamental SOC capability.

A SOC analyst should be able to:

* Interpret Windows authentication events
* Identify suspicious authentication patterns
* Investigate failed logons
* Correlate successful and failed authentication
* Identify privileged access
* Investigate remote authentication
* Analyze account lockouts
* Build authentication timelines
* Use SIEM search effectively
* Distinguish false positives from genuine security events
* Escalate suspicious activity appropriately
* Document investigation findings

These skills directly support SOC L1 alert triage and incident investigation.

---

# Conclusion

Authentication monitoring provides visibility into who is accessing Windows systems, when they are accessing them, how they authenticate, and whether the authentication behavior matches the expected baseline.

The investigation process should follow:

```
Detect
  ↓
Identify User
  ↓
Identify Source
  ↓
Identify Logon Type
  ↓
Correlate Events
  ↓
Build Timeline
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

**Authentication events should be analyzed as part of a sequence, not as isolated logs.**

Related documentation:

* `07-Alert-Analysis.md`
* `09-Process-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
