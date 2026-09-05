# Detection Rules

## Purpose

The purpose of this document is to explain how collected Windows security telemetry is analyzed using detection rules to identify potentially suspicious or security-relevant activity.

Detection rules are the bridge between **collected telemetry** and **SOC alerts**.

The objective of this lab is not to alert on every Windows event, but to identify meaningful patterns that require analyst attention.

---

## Detection Objectives

The detection process should identify security-relevant behavior involving:

* Authentication failures
* Suspicious authentication patterns
* Privileged logons
* Account creation
* Account modification
* Account lockouts
* Suspicious process execution
* PowerShell activity
* Suspicious command execution
* Endpoint security events
* Other abnormal Windows activity

The detection strategy should prioritize **high-value security signals** over unnecessary alerts.

---

# Detection Workflow

The detection workflow used in this lab is:

```
Windows Activity
      ↓
Event Generation
      ↓
Log Collection
      ↓
Collected Telemetry
      ↓
Detection Rule
      ↓
Rule Match
      ↓
    Alert
      ↓
Alert Analysis
      ↓
Investigation
      ↓
Response
```

The detection stage begins only after the required telemetry is successfully collected.

---

# Detection vs Collection

Log collection answers:

> What events are being generated?

Detection answers:

> Which events or event patterns may represent suspicious activity?

For example:

```
Event ID 4625
Failed Logon
      ↓
Event Collected
      ↓
Detection Condition
      ↓
Repeated Failures
      ↓
    Alert
```

A single collected event does not necessarily represent an attack.

Detection logic provides the context required to determine whether an event deserves investigation.

---

# Detection Rule Components

A useful detection rule normally contains:

* Event source
* Event identifier
* Relevant fields
* Detection condition
* Severity
* Description
* Investigation context
* MITRE ATT&CK mapping where applicable
* Expected response

Conceptually:

```
Event Source
     +
Event ID
     +
Detection Condition
     +
Context
     ↓
Detection Rule
     ↓
Alert
```

---

# Wazuh Detection Rules

Wazuh uses rules to analyze security events and identify conditions that may require attention.

Rules can be used to:

* Match specific events
* Match event fields
* Identify patterns
* Increase alert severity
* Group related events
* Detect repeated activity
* Generate security alerts

Wazuh rules are commonly defined in XML format.

Custom detection rules should be developed carefully and tested against controlled lab activity.

---

# Windows Event-Based Detection

Windows Event IDs provide useful detection signals.

Important examples include:

| Event ID | Activity                        | Detection Use                                      |
| -------- | ------------------------------- | -------------------------------------------------- |
| `4624`   | Successful logon                | Authentication monitoring                          |
| `4625`   | Failed logon                    | Brute-force or suspicious authentication detection |
| `4672`   | Special privileges assigned     | Privileged activity monitoring                     |
| `4688`   | Process creation                | Process execution monitoring                       |
| `4720`   | User account created            | Account activity detection                         |
| `4738`   | User account changed            | Account modification monitoring                    |
| `4740`   | Account locked out              | Repeated authentication failure investigation      |
| `4104`   | PowerShell Script Block Logging | PowerShell activity detection                      |

These events should be interpreted within context rather than treated as malicious by default.

---

# Authentication Detection

Authentication activity is one of the most important Windows detection areas.

## Failed Authentication

Event ID `4625` can indicate a failed logon.

A single failed authentication may be normal.

Repeated failures may indicate:

* Incorrect credentials
* Password spraying
* Brute-force activity
* Misconfigured services
* Automated authentication attempts

Therefore, detection should consider frequency and context.

---

## Example Detection Logic

```
Event ID 4625
      ↓
Multiple failures
      ↓
Same account / source
      ↓
Threshold exceeded
      ↓
    Alert
      ↓
Analyst Investigation
```

The detection threshold should be appropriate for the lab environment.

---

# Privileged Activity Detection

Event ID `4672` can indicate that special privileges were assigned to a new logon.

This event is useful for monitoring privileged authentication activity.

The analyst should investigate:

* Account involved
* Logon type
* Source
* Timestamp
* Whether the account normally performs privileged activity
* Related process activity
* Related authentication failures

The event alone should not automatically be considered malicious.

---

# Process Detection

Event ID `4688` provides process creation telemetry when process auditing is configured.

Process detection can evaluate:

* Process name
* Parent process
* Command line
* User
* Execution path
* Process relationships
* Unusual execution patterns

Example:

```
User Activity
      ↓
Process Created
      ↓
Parent/Child Analysis
      ↓
Suspicious Pattern?
   ↙        ↘
 No          Yes
 ↓            ↓
```

Normal       Alert
↓
Investigation

Process detection becomes more useful when combined with Sysmon telemetry.

---

# PowerShell Detection

PowerShell is a legitimate administrative tool and should not automatically be treated as malicious.

Detection should focus on suspicious characteristics such as:

* Unusual execution
* Suspicious command patterns
* Encoded commands
* Unexpected parent processes
* Execution by unusual users
* Abnormal administrative activity
* Script Block Logging events

A useful detection model is:

```
PowerShell Activity
       ↓
Collect Telemetry
       ↓
Analyze Context
       ↓
Suspicious Pattern?
    ↙       ↘
  No         Yes
  ↓           ↓
Record       Alert
```

This reduces false positives compared with alerting on every PowerShell execution.

---

# Account Activity Detection

Account-related events should be monitored for unexpected changes.

Important events include:

* `4720` — User account created
* `4738` — User account changed
* `4740` — Account locked out

Example:

```
Account Created
      ↓
Identify Creator
      ↓
Identify New Account
      ↓
Check Authorization
      ↓
Expected?
   ↙     ↘
 Yes      No
 ↓         ↓
```

Normal     Alert

---

# Detection Severity

Detection rules should assign an appropriate severity level.

Severity should reflect:

* Potential impact
* Confidence
* Suspiciousness
* Business relevance
* Available context

A simple lab classification can be:

| Severity | Meaning                              |
| -------- | ------------------------------------ |
| Low      | Informational or low-risk activity   |
| Medium   | Activity requiring analyst review    |
| High     | Strongly suspicious activity         |
| Critical | Potentially severe security incident |

Severity should not be assigned only because an event is unusual.

---

# Rule Correlation

Some detections become stronger when multiple events are correlated.

Example:

```
4625 Failed Logon
      ↓
4625 Failed Logon
      ↓
4625 Failed Logon
      ↓
4624 Successful Logon
      ↓
Suspicious Authentication Sequence
      ↓
      Alert
```

Another example:

```
PowerShell Execution
      +
Suspicious Command
      +
Unusual Parent Process
      ↓
Higher Confidence Detection
```

Correlation reduces dependence on isolated events.

---

# Detection Rule Example

A simple Wazuh custom rule can be used to identify a specific Windows event.

Example:

```
<group name="windows,authentication,">

  <rule id="100001" level="5">
    <field name="win.system.eventID">4625</field>
    <description>Windows failed logon detected</description>
  </rule>

</group>
```

This example demonstrates the basic structure of a custom detection rule.

The rule:

* Matches Windows Event ID `4625`
* Assigns a defined alert level
* Generates a descriptive alert
* Places the detection within relevant rule groups

Custom rule IDs should be selected according to the Wazuh custom-rule numbering conventions used in the lab.

---

# Threshold-Based Detection

A single event may not be enough to generate a meaningful alert.

Threshold logic can improve detection quality.

Conceptually:

```
Failed Logon
      ↓
Count Events
      ↓
Threshold Reached?
   ↙       ↘
 No         Yes
 ↓           ↓
```

Continue      Alert

For example, repeated failed authentication events within a short period may receive a higher detection priority than an isolated failure.

Threshold values should be documented and tested within the lab.

---

# False Positives

A false positive occurs when legitimate activity triggers a detection that appears suspicious.

Common causes include:

* Administrative activity
* Automated services
* Scheduled tasks
* Software updates
* Security tools
* System maintenance
* Incorrect detection thresholds

False positives should be investigated rather than immediately ignored.

The objective is to improve the rule while maintaining useful security coverage.

---

# Detection Tuning

Detection rules should be continuously evaluated.

The tuning process is:

```
Detection Rule
      ↓
   Testing
      ↓
Alert Generated
      ↓
Analyst Review
      ↓
False Positive?
   ↙       ↘
 Yes        No
  ↓          ↓
```

Tune Rule   Keep Rule
↓
Retest
↓
Validate

Detection tuning improves:

* Alert quality
* Analyst efficiency
* Detection accuracy
* Signal-to-noise ratio
* Investigation speed

---

# MITRE ATT&CK Mapping

Where appropriate, detections should be mapped to the relevant MITRE ATT&CK technique.

Examples:

| Activity                     | Potential ATT&CK Area                                                 |
| ---------------------------- | --------------------------------------------------------------------- |
| Password guessing            | Credential Access                                                     |
| Account discovery/activity   | Account Discovery / Persistence-related activity depending on context |
| PowerShell abuse             | Command and Scripting Interpreter: PowerShell                         |
| Suspicious process execution | Execution                                                             |
| Account creation             | Persistence / Account Manipulation depending on context               |

ATT&CK mapping should be based on the behavior being detected rather than simply the Event ID.

---

# Detection Testing

Every custom detection should be tested using controlled activity.

Testing process:

1. Identify the behavior to detect.
2. Identify the required Windows telemetry.
3. Confirm telemetry collection.
4. Configure the detection rule.
5. Generate the controlled event.
6. Confirm the event reaches Wazuh.
7. Verify the rule matches.
8. Review the generated alert.
9. Check severity.
10. Check false-positive behavior.
11. Document the result.
12. Tune and retest if required.

---

# Detection Validation Scenarios

## Scenario 1 — Failed Authentication

Generate controlled failed authentication attempts.

Expected result:

```
Failed Authentication
        ↓
Event ID 4625
        ↓
Wazuh Collection
        ↓
Detection Rule
        ↓
      Alert
```

Verify:

* Event ID
* Username
* Host
* Timestamp
* Source information
* Rule ID
* Alert severity

---

## Scenario 2 — Repeated Authentication Failures

Generate multiple controlled failed authentication attempts.

Verify whether the configured detection logic identifies the repeated pattern.

Expected workflow:

```
Multiple 4625 Events
        ↓
   Correlation
        ↓
   Threshold
        ↓
      Alert
        ↓
  Investigation
```

---

## Scenario 3 — Process Creation

Execute a benign process.

Verify:

* Event ID `4688`
* Process name
* User
* Parent process where available
* Command line where available

The purpose is to validate process telemetry and detection logic.

---

## Scenario 4 — PowerShell Activity

Execute a benign PowerShell command.

Verify:

* PowerShell telemetry
* Relevant Event IDs
* Detection conditions
* Alert generation if the configured rule is designed to detect the behavior

Normal PowerShell usage should not automatically produce a high-severity alert.

---

## Scenario 5 — Account Activity

Perform controlled account activity within the lab.

Verify:

* Account-related event
* Event ID
* User involved
* Timestamp
* Detection rule
* Alert severity

---

# Detection Evidence

Evidence should demonstrate that the detection rule works as intended.

Capture:

* Windows Event Viewer evidence
* Wazuh alert
* Rule ID
* Event ID
* Timestamp
* Hostname
* Relevant event fields
* Detection severity
* MITRE ATT&CK mapping where applicable
* Analyst interpretation
* Final validation result

Store evidence in:

`../Evidence/`

---

# Detection Troubleshooting

If a detection does not trigger, troubleshoot in this order:

```
Activity Generated?
      ↓
     Yes
      ↓
Event Visible Locally?
      ↓
     Yes
      ↓
Event Collected by Wazuh?
      ↓
     Yes
      ↓
Required Fields Available?
      ↓
     Yes
      ↓
Rule Loaded Correctly?
      ↓
     Yes
      ↓
Rule Condition Matched?
      ↓
     Yes
      ↓
    Alert
```

If the event is missing from Wazuh, investigate **log collection**.

If the event is available but the rule does not match, investigate **detection configuration**.

This prevents collection problems from being incorrectly treated as detection problems.

---

# Detection Quality Criteria

A good detection should be:

* Relevant
* Testable
* Understandable
* Documented
* Actionable
* Appropriately prioritized
* Resistant to unnecessary false positives
* Supported by sufficient telemetry

The best detection is not necessarily the one that generates the most alerts.

The objective is to generate **useful alerts that help analysts make decisions**.

---

# Detection Checklist

Before considering a detection complete:

* [ ] Required telemetry is collected.
* [ ] Detection objective is documented.
* [ ] Event source is identified.
* [ ] Event ID or relevant field is identified.
* [ ] Detection condition is defined.
* [ ] Rule is configured.
* [ ] Rule ID is documented.
* [ ] Severity is appropriate.
* [ ] Detection has been tested.
* [ ] Alert has been validated.
* [ ] False positives have been reviewed.
* [ ] MITRE ATT&CK mapping has been considered.
* [ ] Evidence has been captured.
* [ ] Detection has been documented.

---

# Professional SOC Relevance

Detection engineering is a core SOC capability.

Understanding detection rules helps analysts:

* Understand why alerts are generated
* Validate security monitoring
* Investigate suspicious behavior
* Identify detection gaps
* Tune false positives
* Improve alert quality
* Map detections to ATT&CK
* Support incident response
* Communicate detection logic during interviews

A SOC analyst should understand not only **how to investigate an alert**, but also **what telemetry and logic caused the alert to exist**.

---

# Conclusion

Detection rules transform collected Windows telemetry into actionable security alerts.

The key relationship is:

**Collection provides visibility. Detection provides security signal.**

A professional detection workflow is:

**Generate → Collect → Validate → Detect → Alert → Analyze → Investigate → Respond → Verify → Document**

The next stage of this lab focuses on analyzing the alerts produced by these detections.

Related documentation:

`05-Log-Collection.md`

`07-Alert-Analysis.md`
