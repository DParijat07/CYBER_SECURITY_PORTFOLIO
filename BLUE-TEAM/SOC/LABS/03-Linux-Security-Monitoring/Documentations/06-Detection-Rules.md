# Detection Rules

## 1. Purpose

This document explains the basic concept of **security detection rules** and how they are used in the Linux Security Monitoring Lab.

The objective is to understand:

* What a detection rule is
* Why detection rules are important in a SOC
* The difference between an event, log, detection, and alert
* How Wazuh analyzes collected Linux events
* Basic Linux security detection scenarios
* How to test detections safely in the home lab
* How to validate that expected alerts are generated
* How to document detection evidence

This stage focuses on **basic detection logic**.

Advanced custom rule development and complex correlation are outside the scope of this beginner lab.

---

# 2. What Is a Detection Rule?

A detection rule is logic used by a security monitoring system to identify an event or activity that may require investigation.

In simple terms:

```
Log/Event
    ↓
Detection Rule
    ↓
Condition Matches
    ↓
Security Alert
```

For example:

```
Failed SSH Authentication
        ↓
Detection Logic
        ↓
Suspicious Authentication Activity
        ↓
Alert
```

A detection rule does not automatically mean that an attack has occurred.

It identifies activity that deserves attention.

---

# 3. Why Detection Rules Matter in a SOC

A Linux system can generate a large number of events.

A SOC analyst cannot manually inspect every event.

Detection rules help prioritize potentially important activity.

Without detection:

```
Thousands of Events
        ↓
  Manual Review
        ↓
  Difficult to Monitor
```

With detection:

```
Thousands of Events
        ↓
   Detection Rules
        ↓
 Relevant Security Events
        ↓
       Alerts
        ↓
    SOC Analyst
```

Detection therefore helps reduce the amount of data that requires immediate human attention.

---

# 4. Event → Log → Collection → Detection → Alert

The complete monitoring workflow is:

```
User / System Activity
          ↓
        Event
          ↓
   Linux Logging
          ↓
      Local Log
          ↓
    Wazuh Agent
          ↓
    Wazuh Server
          ↓
      Detection
          ↓
        Alert
          ↓
      Analysis
          ↓
    Investigation
          ↓
      Response
```

Each stage has a different purpose.

| Stage         | Purpose                                           |
| ------------- | ------------------------------------------------- |
| Event         | Something happens                                 |
| Log           | Event is recorded                                 |
| Collection    | Log reaches central monitoring                    |
| Detection     | Security logic evaluates the event                |
| Alert         | Important activity is presented for investigation |
| Analysis      | Analyst examines the alert                        |
| Investigation | Analyst determines what happened                  |
| Response      | Appropriate action is taken                       |

---

# 5. Wazuh Detection Concept

Wazuh analyzes collected events and applies detection rules to them.

Simplified architecture:

```
Ubuntu 22.04 LTS
       ↓
  Linux Logs
       ↓
  Wazuh Agent
       ↓
  Wazuh Server
       ↓
Wazuh Analysis Engine
       ↓
  Detection Rules
       ↓
      Alerts
       ↓
 Wazuh Dashboard
```

The Wazuh detection engine evaluates incoming events and determines whether configured detection conditions are satisfied.

---

# 6. Basic Detection Categories

The Linux Security Monitoring Lab focuses on the following beginner-level detection categories:

1. Authentication failures
2. Successful authentication
3. Privilege activity
4. User/account activity
5. Process activity
6. Service activity
7. Shell activity
8. Multiple related security events

These categories are useful for developing basic SOC monitoring skills.

---

# 7. Detection Scenario 1 — Failed SSH Authentication

Repeated failed SSH authentication attempts are an important security monitoring scenario.

A simplified detection concept is:

```
SSH Authentication Attempt
          ↓
Authentication Failure
          ↓
   Detection Logic
          ↓
Potential Suspicious Activity
          ↓
         Alert
```

A single failed login does not necessarily indicate an attack.

For example:

```
1 Failed Login
      ↓
Could be User Error
```

Multiple failures may be more interesting:

```
Multiple Failed Logins
          ↓
  Same / Related Source
          ↓
Potential Brute-Force Activity
          ↓
     Investigation
```

The actual Wazuh rule and alert level depend on the event and Wazuh's configured rules.

---

# 8. Detection Scenario 2 — Successful SSH Authentication

Successful authentication is also useful for monitoring.

A successful login can help answer:

* Which account logged in?
* When did the login occur?
* From where did the login originate?
* Was the login expected?

The detection concept is:

```
Successful SSH Login
        ↓
Authentication Event
        ↓
Monitoring / Detection
        ↓
Possible Alert or Investigation
```

A successful login is not inherently malicious.

It becomes more interesting when it is unexpected or associated with other suspicious activity.

---

# 9. Detection Scenario 3 — Privileged Activity

The use of `sudo` is an important Linux security event.

Example:

```
sudo whoami
```

The event may be recorded in:

```
/var/log/auth.log
```

The detection concept is:

```
User
 ↓
sudo Command
 ↓
Privilege Activity
 ↓
Detection
 ↓
Alert / Monitoring
```

Not every `sudo` command is suspicious.

For example:

```
Authorized Administrator
        ↓
   sudo apt update
        ↓
   Normal Activity
```

But:

```
Unexpected Account
        ↓
    sudo Command
        ↓
  Potentially Suspicious
```

The context determines the security significance.

---

# 10. Detection Scenario 4 — User Account Changes

Account creation or modification can be security-relevant.

Examples:

```
New User Created
User Modified
Group Membership Changed
User Disabled
```

Simplified detection logic:

```
Account Change
      ↓
Security Event
      ↓
   Detection
      ↓
Alert / Investigation
```

Account-related events should be evaluated against expected administrative activity.

---

# 11. Detection Scenario 5 — Process Activity

Process execution can provide important endpoint security information.

Example:

```
New Process
    ↓
Process Information
    ↓
Detection Logic
    ↓
Potentially Suspicious Activity
```

A process itself is not necessarily malicious.

For example:

```
/usr/bin/bash
```

may be completely normal.

Security analysis requires additional context such as:

* User
* Command
* Parent process
* Time
* Frequency
* Related events

Detailed process monitoring is covered later in:

`09-Process-Monitoring.md`

---

# 12. Detection Scenario 6 — Service Activity

Service changes can be useful security indicators.

Examples:

```
Service Started
Service Stopped
Service Restarted
Unexpected Service Activity
```

Simplified workflow:

```
Service Activity
       ↓
  System Event
       ↓
   Detection
       ↓
      Alert
       ↓
  Investigation
```

For example, an unexpected service start may deserve investigation.

---

# 13. Detection Scenario 7 — Shell Activity

Shell activity can be security-relevant because attackers frequently use command-line tools after obtaining access.

Examples include:

```
Command Execution
Shell Session
Administrative Command
Suspicious Command
```

However, command-line activity must be interpreted carefully.

A command such as:

```
sudo systemctl status ssh
```

may be completely normal during administration.

The same command executed by an unexpected account at an unusual time may deserve investigation.

---

# 14. Detection Scenario 8 — Multiple Related Events

A single event may not provide enough evidence.

Multiple events can provide better context.

For example:

```
Failed SSH Login
        ↓
Failed SSH Login
        ↓
Successful SSH Login
        ↓
   sudo Activity
        ↓
  Suspicious Process
```

Individually, some events may appear normal.

Together, they may represent a more interesting sequence.

This is the basic idea behind event correlation.

For this beginner lab, the objective is to understand the concept rather than build complex correlation rules.

---

# 15. Wazuh Alert Levels

Wazuh alerts include severity information.

At a beginner level, think of alert severity as a way to help prioritize investigation.

A simplified model is:

```
Lower Severity
      ↓
Informational / Low Concern
      ↓
   Medium Concern
      ↓
    High Concern
      ↓
 Critical Concern
```

The exact severity and alert level depend on the Wazuh rule that matches the event.

An alert's severity should not be treated as proof that an incident occurred.

The analyst must investigate the context.

---

# 16. Detection Rule vs Alert

These terms should not be confused.

## Detection Rule

The logic used to identify an event.

```
Condition
   ↓
Rule Match
```

## Alert

The security notification produced when the detection condition is satisfied.

```
Rule Match
   ↓
  Alert
```

Therefore:

```
Event
  ↓
Rule Evaluation
  ↓
Rule Match
  ↓
Alert
```

---

# 17. Existing Wazuh Rules

Wazuh includes predefined detection rules for many common security events.

For this beginner lab, the preferred approach is to first understand and validate existing detections before creating complex custom rules.

This keeps the learning process focused on:

```
Understand
   ↓
  Test
   ↓
 Observe
   ↓
 Analyze
   ↓
Document
```

rather than immediately building advanced detection logic.

---

# 18. Where Wazuh Rules Are Managed

Wazuh's rule system contains predefined rules and supports custom rules.

For learning purposes, the important concept is:

```
Wazuh Event
     ↓
 Rules Engine
     ↓
 Matching Rule
     ↓
     Alert
```

Custom detection rules can be introduced later when there is a specific monitoring requirement that cannot be handled adequately by existing rules.

The current lab focuses on using and validating existing detections first.

---

# 19. Detection Testing Method

Each detection should follow a controlled testing process.

```
1. Define Scenario
       ↓
2. Generate Controlled Event
       ↓
3. Confirm Local Log
       ↓
4. Confirm Wazuh Collection
       ↓
5. Check Detection
       ↓
6. Observe Alert
       ↓
7. Analyze Alert
       ↓
8. Capture Evidence
```

This provides a repeatable approach to detection testing.

---

# 20. Test Environment

Detection testing must use the authorized home lab.

Primary endpoint:

```
Ubuntu 22.04 LTS
```

Monitoring:

```
Wazuh Agent
      ↓
Wazuh Server
      ↓
Wazuh Dashboard
```

Testing systems may include other authorized virtual machines in the home lab.

---

# 21. Detection Test 1 — Failed Authentication

## Objective

Verify that a controlled failed SSH authentication attempt can be detected.

## Procedure

From an authorized lab machine, perform one controlled failed SSH authentication attempt against the Ubuntu VM.

Use an intentionally incorrect password.

Then verify the local log:

```
sudo grep "Failed password" /var/log/auth.log
```

Expected flow:

```
SSH Attempt
    ↓
Authentication Failure
    ↓
   auth.log
    ↓
Wazuh Agent
    ↓
Wazuh Server
    ↓
 Detection
    ↓
   Alert
```

Do not perform repeated password guessing.

---

# 22. Detection Test 2 — Successful Authentication

## Objective

Observe how a successful SSH login is represented.

Perform a normal authorized SSH login.

Then check:

```
sudo grep "Accepted" /var/log/auth.log
```

Look for the corresponding event in Wazuh.

Record:

* Username
* Time
* Source IP, if available
* Authentication method
* Alert or event information

---

# 23. Detection Test 3 — Sudo Activity

## Objective

Observe a privilege-related event.

Run:

```
sudo whoami
```

Then inspect:

```
sudo grep "sudo:" /var/log/auth.log
```

Look for the corresponding event in Wazuh.

The basic flow is:

```
sudo Command
     ↓
Authentication Log
     ↓
Wazuh Collection
     ↓
  Detection
     ↓
Alert / Event
```

---

# 24. Detection Test 4 — Service Activity

Use a harmless service-status command:

```
systemctl status ssh
```

This does not change the service state.

Then inspect recent journal entries:

```
sudo journalctl --since "10 minutes ago"
```

The objective is to understand where service-related information can appear.

Do not stop or modify important services merely to generate an event.

---

# 25. Detection Test 5 — Process Activity

View current processes:

```
ps aux
```

Then inspect the relevant monitoring data available in Wazuh.

The objective is to understand:

```
Process
  ↓
Endpoint Telemetry
  ↓
Collection
  ↓
Detection / Monitoring
```

Detailed process detection is covered later in:

`09-Process-Monitoring.md`

---

# 26. Exact Wazuh Validation Procedure

Detection testing must be validated from the Linux endpoint through the Wazuh Dashboard.

The following procedure should be used for each detection test.

## Step 1 — Confirm the Wazuh Agent Is Running

On the Ubuntu 22.04 LTS endpoint:

```
sudo systemctl status wazuh-agent
```

Expected result:

```
Active: active (running)
```

If the agent is not running, do not continue with central validation.

Start it if required:

```
sudo systemctl start wazuh-agent
```

Then check again:

```
sudo systemctl status wazuh-agent
```

---

## Step 2 — Confirm the Linux Event Exists Locally

Generate the controlled test event.

For example, for SSH authentication:

```
sudo grep "Failed password" /var/log/auth.log
```

For successful authentication:

```
sudo grep "Accepted" /var/log/auth.log
```

For sudo activity:

```
sudo grep "sudo:" /var/log/auth.log
```

The event must first exist on the Ubuntu endpoint.

If the event does not exist locally, troubleshoot Linux logging before troubleshooting Wazuh.

---

## Step 3 — Confirm the Wazuh Agent Is Processing Logs

Check the Wazuh Agent log:

```
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Look for recent messages related to the agent's operation.

Also confirm the agent remains active:

```
sudo systemctl is-active wazuh-agent
```

Expected result:

```
active
```

---

## Step 4 — Open the Wazuh Dashboard

Open the Wazuh Dashboard used by the home lab.

Navigate to the area used for viewing security alerts/events.

The exact dashboard labels can vary between Wazuh versions, so use the current alert/event view available in the installed version.

---

## Step 5 — Filter by the Ubuntu Agent

Identify the Ubuntu 22.04 LTS endpoint in the Wazuh Dashboard.

Use the available agent filter to narrow the results to:

```
Ubuntu 22.04 LTS
```

This prevents unrelated events from other lab machines from confusing the validation.

---

## Step 6 — Set the Time Range

Set the Dashboard time range to include the moment when the controlled test was performed.

For a simple test, a recent time range such as:

```
Last 15 minutes
```

is normally sufficient.

If the event was generated earlier, select a time range that includes the actual event timestamp.

---

## Step 7 — Find the Test Event or Alert

Search/filter for information related to the test.

For example:

### Failed SSH Test

Look for authentication-related information such as:

```
Failed password
SSH
Authentication failure
```

### Successful SSH Test

Look for:

```
Accepted
SSH
Successful authentication
```

### Sudo Test

Look for:

```
sudo
privilege
command execution
```

Do not rely only on the exact wording above because event descriptions can vary depending on the Linux log format and Wazuh rule that processes the event.

---

## Step 8 — Open the Alert/Event Details

Open the matching Wazuh alert/event.

Record the available information.

Important fields include:

* Timestamp
* Agent name
* Agent ID, if displayed
* Rule ID, if displayed
* Rule description
* Rule level/severity
* Source IP, if available
* Source/user information, if available
* Decoder/event source, if displayed
* Full log/event data
* MITRE ATT&CK information, if available

Do not manually invent a rule ID or severity.

Record the actual values shown by your Wazuh installation.

---

## Step 9 — Compare the Dashboard Event With the Linux Log

Return to Ubuntu and compare the event with the local log.

For example:

```
Ubuntu Local Log
      ↓
Failed SSH Event
      ↓
Wazuh Agent
      ↓
Wazuh Dashboard
      ↓
Matching Alert/Event
```

Compare:

* Timestamp
* Username
* Source IP
* Event description
* Authentication result

The purpose is to confirm that the Wazuh alert/event corresponds to the event that was intentionally generated.

---

## Step 10 — Confirm Detection

Determine which of the following occurred:

### Case A — Detection and Alert

```
Local Event
     ↓
Wazuh Collection
     ↓
Detection Rule Match
     ↓
   Alert
```

Record:

```
Detection: PASS
Alert: PASS
```

### Case B — Collection but No Alert

```
Local Event
     ↓
Wazuh Collection
     ↓
No Matching Detection
     ↓
No Alert
```

Record:

```
Collection: PASS
Detection: NOT OBSERVED
Alert: NOT GENERATED
```

This is not automatically a failure.

Not every collected event generates a security alert.

### Case C — No Central Event

```
Local Event
     ↓
Wazuh Collection Failure
     ↓
No Central Event
```

Record:

```
Local Event: PASS
Collection: FAIL
Detection: NOT TESTABLE
Alert: NOT TESTABLE
```

Investigate the Wazuh Agent and log collection configuration.

---

# 27. Exact Wazuh Validation Checklist

Use this checklist for every detection test.

```
[ ] Controlled test activity performed
[ ] Linux event generated
[ ] Local Linux log contains the event
[ ] Wazuh Agent is active
[ ] Wazuh Agent log checked
[ ] Wazuh Dashboard opened
[ ] Ubuntu agent selected/filtered
[ ] Correct time range selected
[ ] Test event/alert located
[ ] Alert/event details opened
[ ] Timestamp compared
[ ] Username compared
[ ] Source IP compared, if available
[ ] Event/log content compared
[ ] Rule information recorded, if available
[ ] Alert severity recorded, if available
[ ] Detection result recorded
[ ] Evidence captured
```

---

# 28. Detection Validation Matrix

| Scenario                      | Local Event | Agent Active | Central Event | Detection | Alert | Status |
| ----------------------------- | ----------- | ------------ | ------------- | --------- | ----- | ------ |
| Failed SSH authentication     | ☐           | ☐            | ☐             | ☐         | ☐     | ☐      |
| Successful SSH authentication | ☐           | ☐            | ☐             | ☐         | ☐     | ☐      |
| Sudo activity                 | ☐           | ☐            | ☐             | ☐         | ☐     | ☐      |
| Service activity              | ☐           | ☐            | ☐             | ☐         | ☐     | ☐      |
| Process activity              | ☐           | ☐            | ☐             | ☐         | ☐     | ☐      |

Not every normal event is expected to generate a security alert.

The important objective is to understand the difference between **event visibility** and **security detection**.

---

# 29. What If No Alert Is Generated?

No alert does not automatically mean that the monitoring system is broken.

Use this troubleshooting sequence:

```
Was the Event Generated?
        ↓
       YES
        ↓
Was it Logged Locally?
        ↓
       YES
        ↓
Was it Collected by Wazuh?
        ↓
       YES
        ↓
Did a Detection Rule Match?
        ↓
       NO
        ↓
No Alert Expected
```

Possible explanations include:

* No matching rule exists
* The event does not meet the rule condition
* The event is informational
* The required log source is not being collected
* The event format differs from the expected format

---

# 30. Detection Troubleshooting

## Problem 1 — Event Does Not Exist Locally

Check:

```
sudo tail -n 30 /var/log/auth.log
```

or:

```
sudo journalctl --since "10 minutes ago"
```

If the event is not present locally, investigate Linux logging first.

---

## Problem 2 — Event Exists Locally but Not in Wazuh

Check:

```
sudo systemctl status wazuh-agent
```

Then:

```
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Also verify the relevant log source is configured for collection.

---

## Problem 3 — Event Reaches Wazuh but No Alert Appears

This may be normal.

Ask:

```
Did a Wazuh detection rule match the event?
```

Not every collected event produces an alert.

---

## Problem 4 — Wazuh Agent Stops After Configuration

Check:

```
sudo systemctl status wazuh-agent
```

Then:

```
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Review recent configuration changes.

---

# 31. Evidence Requirements

Store detection evidence under:

```
03-Linux-Security-Monitoring/
└── Evidence/
```

Recommended evidence:

### Evidence 01 — Failed Authentication

Show:

```
sudo grep "Failed password" /var/log/auth.log
```

and the corresponding Wazuh event or alert.

### Evidence 02 — Successful Authentication

Show the successful authentication event and corresponding Wazuh data.

### Evidence 03 — Sudo Activity

Show:

```
sudo grep "sudo:" /var/log/auth.log
```

and the corresponding Wazuh event if available.

### Evidence 04 — Detection Alert

Capture the relevant Wazuh alert showing:

* Rule information
* Alert severity
* Event description
* Timestamp
* Endpoint
* Source information where available

### Evidence 05 — Detection Validation

Record whether the expected detection condition was met.

Do not include passwords, private keys, tokens, or unnecessary sensitive information.

---

# 32. Detection Test Record

Use the following format for each detection test:

```
Detection Scenario:
Date:
Endpoint:
Test Activity:
Expected Event:
Local Log Source:
Central Event:
Detection Rule:
Alert Generated:
Alert Severity:
Result:
Evidence File:
```

Example:

```
Detection Scenario: Controlled SSH Authentication Failure
Endpoint: Ubuntu 22.04 LTS
Test Activity: One unauthorized-password test in the lab
Expected Event: Failed SSH authentication
Local Log Source: /var/log/auth.log
Central Event: Observed
Detection Rule: Recorded from Wazuh
Alert Generated: Yes
Result: Successful
```

Replace the example values with the actual results from the lab.

---

# 33. Detection Quality

A useful detection should ideally be:

```
Relevant
   +
Understandable
   +
Testable
   +
Actionable
```

A detection that produces large numbers of irrelevant alerts can create analyst fatigue.

This is known as:

```
Alert Fatigue
```

At the beginner level, the goal is to understand why detections should identify activity that is useful for investigation.

---

# 34. False Positive Concept

A false positive occurs when an alert indicates potentially suspicious activity but the activity is actually legitimate.

Example:

```
sudo Activity
      ↓
    Alert
      ↓
 Investigation
      ↓
Authorized Administrator
      ↓
 False Positive
```

This is an important SOC concept.

An alert is a starting point for investigation, not automatically proof of malicious activity.

---

# 35. False Negative Concept

A false negative occurs when suspicious activity happens but the monitoring system does not detect it.

Example:

```
Suspicious Activity
        ↓
No Matching Detection
        ↓
      No Alert
        ↓
Potentially Missed Activity
```

This is why detection coverage and validation are important.

---

# 36. Detection Coverage

The lab should gradually build coverage across important Linux activity categories.

| Category           | Initial Coverage |
| ------------------ | ---------------- |
| Authentication     | Yes              |
| Privilege Activity | Yes              |
| User Activity      | Basic            |
| Process Activity   | Basic            |
| Service Activity   | Basic            |
| Shell Activity     | Basic            |
| File Activity      | Basic            |

The objective is not to create a detection rule for every possible Linux event.

The objective is to build a useful beginner-level monitoring capability.

---

# 37. Detection Workflow

The detection workflow for this lab is:

```
                        Linux Endpoint
                              │
                              ↓
                       Event Generated
                              │
                              ↓
                          Local Log
                              │
                              ↓
                         Wazuh Agent
                              │
                              ↓
                         Wazuh Server
                              │
                              ↓
                       Detection Rules
                              │
                 ┌────────────┴────────────┐
                 ↓                         ↓
           Rule Matches               No Match
                 ↓                         ↓
               Alert                   Event Only
                 ↓
            SOC Analysis
```

This is the basic relationship between event collection and detection.

---

# 38. Security and Authorization

Detection testing must be performed only against authorized home-lab systems.

Permitted activities include:

* Testing the Ubuntu VM
* Performing controlled SSH authentication tests
* Running harmless `sudo` commands
* Observing system activity
* Testing Wazuh detection on the user's own lab environment

Do not perform authentication testing or security testing against external systems without authorization.

---

# 39. Detection Completion Criteria

The detection stage is complete when:

* [ ] I understand what a detection rule is.
* [ ] I understand the difference between an event and an alert.
* [ ] I understand the role of Wazuh detection rules.
* [ ] I understand authentication detection.
* [ ] I understand privilege-activity detection.
* [ ] I understand basic process detection.
* [ ] I understand service-event detection.
* [ ] I understand shell-activity detection.
* [ ] I understand false positives.
* [ ] I understand false negatives.
* [ ] I tested at least three Linux security scenarios.
* [ ] I verified local event generation.
* [ ] I verified centralized collection.
* [ ] I checked whether the expected detection matched.
* [ ] I captured detection evidence.

---

# 40. SOC Learning Outcome

After completing this stage, the learner should be able to explain:

> How a collected Linux event becomes a security alert through detection logic.

The complete flow is:

```
Linux Activity
      ↓
  Linux Event
      ↓
   Linux Log
      ↓
Wazuh Collection
      ↓
 Detection Rule
      ↓
   Rule Match
      ↓
 Security Alert
      ↓
  SOC Analyst
```

The learner should also understand:

```
Event ≠ Alert
Alert ≠ Confirmed Incident
```

An alert requires analysis and investigation before determining whether malicious activity actually occurred.

---

# 41. Success Criteria

This stage is successful when the learner can:

1. Explain what a detection rule does.
2. Explain the difference between collection and detection.
3. Identify basic Linux security detection scenarios.
4. Understand how Wazuh evaluates collected events.
5. Test controlled authentication activity.
6. Test controlled privilege activity.
7. Observe basic process and service activity.
8. Verify whether expected events reach Wazuh.
9. Determine whether a detection rule matched.
10. Understand why some events do not generate alerts.
11. Recognize the concepts of false positives and false negatives.
12. Document detection tests with evidence.

---

# 42. Related Documentation

* `01-Lab-Objective.md`
* `02-Lab-Setup.md`
* `03-Linux-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-Shell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
