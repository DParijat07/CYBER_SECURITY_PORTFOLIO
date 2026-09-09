# Linux Security Monitoring — Lab Objective

## Purpose

The purpose of this lab is to build practical skills in monitoring, detecting, investigating, and responding to security-relevant activity on a Linux endpoint.

The lab focuses on understanding Linux security telemetry and using a centralized monitoring platform such as Wazuh to collect and analyze endpoint activity.

The objective is not simply to generate Linux logs, but to understand how endpoint activity becomes security telemetry that can support a SOC investigation and lead to an appropriate response action.

---

## Primary Objectives

The primary objectives of this lab are to:

1. Understand Linux security monitoring fundamentals.
2. Identify important Linux log sources.
3. Understand authentication and authorization events.
4. Configure Linux security telemetry for monitoring.
5. Collect Linux logs using the Wazuh agent.
6. Monitor SSH authentication activity.
7. Monitor user and account activity.
8. Monitor process and command execution.
9. Monitor privilege escalation activity.
10. Monitor system and service activity.
11. Create and validate detection rules.
12. Analyze security alerts.
13. Correlate multiple Linux events.
14. Investigate simulated security incidents.
15. Perform controlled incident-response actions.
16. Verify that response actions were successful.
17. Troubleshoot collection and detection failures.
18. Document investigation findings, response actions, and evidence.

---

## Lab Workflow

The overall workflow of the lab is:

Linux Activity
→ Event Generation
→ Log Generation
→ Log Collection
→ Security Telemetry
→ Detection
→ Alert
→ Analysis
→ Investigation
→ Response
→ Recovery
→ Verification
→ Documentation

This workflow represents the basic operational cycle followed by a SOC analyst when investigating endpoint security events.

---

## Security Monitoring Scope

The lab focuses on monitoring the following Linux security activities:

### Authentication

* Successful SSH authentication
* Failed SSH authentication
* Repeated authentication failures
* Authentication from unusual source addresses
* User session activity
* Account lockout or access-control events where applicable

### User and Account Activity

* User creation
* User modification
* Group membership changes
* Account privilege changes
* User deletion
* Changes to authentication configuration

### Privilege Activity

* `sudo` usage
* Privilege escalation attempts
* Root-level command execution
* Changes involving privileged accounts
* Unauthorized privilege assignment

### Process Activity

* Process creation
* Process termination
* Suspicious command execution
* Shell activity
* Parent-child process relationships
* Execution from unusual locations

### System Activity

* Service activity
* Configuration changes
* System errors
* Kernel or system messages
* Important system-level events

### File and Configuration Activity

* Changes to important configuration files
* Changes to authentication-related files
* Changes to security-sensitive directories
* Permission changes
* File integrity events where monitoring is configured

---

## Primary Linux Log Sources

The lab will primarily investigate common Linux telemetry sources such as:

| Log Source          | Monitoring Purpose                                                       |
| ------------------- | ------------------------------------------------------------------------ |
| `/var/log/auth.log` | Authentication and authorization activity on Debian/Ubuntu-based systems |
| `/var/log/secure`   | Authentication and authorization activity on RHEL/CentOS-based systems   |
| `/var/log/syslog`   | General system activity on Debian/Ubuntu-based systems                   |
| `/var/log/messages` | General system activity on RHEL/CentOS-based systems                     |
| `journalctl`        | systemd journal and centralized Linux event information                  |
| `auditd` logs       | Security auditing and privileged activity                                |
| Shell history       | Command execution context where appropriate                              |
| Application logs    | Application-specific security activity                                   |

The exact log paths depend on the Linux distribution and logging configuration used in the lab.

---

## Monitoring Architecture

The conceptual architecture for this lab is:

Linux Endpoint
→ Linux Logs / Journald / Audit Telemetry
→ Wazuh Agent
→ Log Collection
→ Wazuh Manager
→ Detection
→ Alert
→ Triage
→ Investigation
→ Response
→ Recovery
→ Verification
→ Documentation

The architecture demonstrates how endpoint telemetry can be converted into an actionable SOC workflow.

### Architecture-to-Response Alignment

| Monitoring Stage        | Primary Activity                    | Expected Output                      | Response Relationship                      |
| ----------------------- | ----------------------------------- | ------------------------------------ | ------------------------------------------ |
| Linux Activity          | User/process/system activity occurs | Security-relevant behavior           | Generates telemetry                        |
| Event Generation        | OS records activity                 | Linux event/log                      | Provides investigation data                |
| Log Collection          | Wazuh Agent collects telemetry      | Centralized event                    | Enables monitoring                         |
| Detection               | Rules identify suspicious behavior  | Detection/alert                      | Initiates triage                           |
| Alert Analysis          | Analyst validates alert             | Validated finding                    | Determines investigation priority          |
| Investigation           | Events are correlated               | Incident understanding               | Identifies affected account/process/system |
| Containment             | Risk is temporarily reduced         | Threat activity limited              | Stops or limits ongoing activity           |
| Eradication/Remediation | Root cause is addressed             | Malicious/unwanted condition removed | Restores security posture                  |
| Recovery                | System returns to expected state    | Service restored                     | Prepares endpoint for normal operation     |
| Verification            | Analyst confirms remediation        | Verified secure state                | Confirms response effectiveness            |
| Documentation           | Evidence and decisions recorded     | Investigation record                 | Creates professional proof-of-work         |

### Response Actions Covered by the Lab

Depending on the simulated scenario, controlled response actions may include:

* Terminating a suspicious test process.
* Disabling a simulated compromised test account.
* Removing unauthorized test group membership.
* Revoking unnecessary privileges.
* Stopping an unauthorized test service.
* Removing a controlled test persistence mechanism.
* Correcting an intentionally modified configuration.
* Rotating credentials in the controlled lab where appropriate.
* Restoring the endpoint to its expected baseline.
* Re-running detection checks after remediation.

Response actions must only be performed against authorized lab systems and test accounts.

---

## Architecture Diagram

The following SVG represents the monitoring-to-response architecture of the lab.

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="1400" height="520" viewBox="0 0 1400 520">
  <title>Linux Security Monitoring Lab Architecture</title>
  <desc>Linux endpoint telemetry flows through Wazuh collection, detection, alert analysis, investigation, response, recovery, verification and documentation.</desc>

  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
      <path d="M0,0 L10,3 L0,6 Z" fill="currentColor"/>
    </marker>
  </defs>

  <g font-family="Arial, Helvetica, sans-serif" font-size="18" fill="currentColor" stroke="currentColor" stroke-width="2">

    <rect x="30" y="170" width="170" height="90" rx="12"/>
    <text x="115" y="205" text-anchor="middle" stroke="none">Linux</text>
    <text x="115" y="230" text-anchor="middle" stroke="none">Endpoint</text>

    <rect x="240" y="170" width="170" height="90" rx="12"/>
    <text x="325" y="205" text-anchor="middle" stroke="none">Logs &amp;</text>
    <text x="325" y="230" text-anchor="middle" stroke="none">Telemetry</text>

    <rect x="450" y="170" width="170" height="90" rx="12"/>
    <text x="535" y="205" text-anchor="middle" stroke="none">Wazuh</text>
    <text x="535" y="230" text-anchor="middle" stroke="none">Agent / Manager</text>

    <rect x="660" y="170" width="170" height="90" rx="12"/>
    <text x="745" y="205" text-anchor="middle" stroke="none">Detection</text>
    <text x="745" y="230" text-anchor="middle" stroke="none">&amp; Alert</text>

    <rect x="870" y="170" width="170" height="90" rx="12"/>
    <text x="955" y="205" text-anchor="middle" stroke="none">Investigation</text>
    <text x="955" y="230" text-anchor="middle" stroke="none">&amp; Triage</text>

    <rect x="1080" y="170" width="170" height="90" rx="12"/>
    <text x="1165" y="205" text-anchor="middle" stroke="none">Response</text>
    <text x="1165" y="230" text-anchor="middle" stroke="none">&amp; Containment</text>

    <line x1="200" y1="215" x2="240" y2="215" marker-end="url(#arrow)"/>
    <line x1="410" y1="215" x2="450" y2="215" marker-end="url(#arrow)"/>
    <line x1="620" y1="215" x2="660" y2="215" marker-end="url(#arrow)"/>
    <line x1="830" y1="215" x2="870" y2="215" marker-end="url(#arrow)"/>
    <line x1="1040" y1="215" x2="1080" y2="215" marker-end="url(#arrow)"/>

    <rect x="1080" y="350" width="170" height="80" rx="12"/>
    <text x="1165" y="382" text-anchor="middle" stroke="none">Recovery</text>
    <text x="1165" y="407" text-anchor="middle" stroke="none">&amp; Verification</text>

    <rect x="870" y="350" width="170" height="80" rx="12"/>
    <text x="955" y="382" text-anchor="middle" stroke="none">Evidence &amp;</text>
    <text x="955" y="407" text-anchor="middle" stroke="none">Documentation</text>

    <line x1="1165" y1="260" x2="1165" y2="350" marker-end="url(#arrow)"/>
    <line x1="1080" y1="390" x2="1040" y2="390" marker-end="url(#arrow)"/>

    <path d="M870,390 C700,390 535,330 535,260" fill="none" marker-end="url(#arrow)"/>
    <text x="710" y="375" text-anchor="middle" stroke="none" font-size="15">
      Re-monitor after remediation
    </text>

  </g>
</svg>
```

The architecture intentionally closes the loop: **response does not end the investigation**. The endpoint must be monitored again to verify that the response action was effective.

---

## Security Scenarios

The lab will use controlled and authorized scenarios to generate realistic security telemetry.

Examples include:

1. Multiple failed SSH authentication attempts.
2. Successful SSH authentication after failed attempts.
3. `sudo` privilege usage.
4. Creation of a new Linux user.
5. Modification of an existing user.
6. Group membership changes.
7. Suspicious command execution.
8. Shell process creation.
9. Service activity.
10. Security-sensitive configuration changes.
11. Authentication-to-process correlation.
12. Privilege-to-process correlation.
13. Full incident investigation.
14. Incident-response simulation.
15. Detection tuning and false-positive analysis.

All activity will be performed inside the authorized home lab environment.

---

## Measurable Lab Deliverables

The lab must produce measurable outputs rather than only configuration screenshots.

### Deliverable 1 — Linux Endpoint Monitoring

**Target:**

* 1 Linux endpoint successfully monitored.
* Wazuh agent connected and reporting.
* Endpoint visible in the monitoring platform.

**Evidence:**

* Agent status screenshot.
* Wazuh endpoint/agent identification.
* Timestamp showing recent communication.

**Pass Criteria:**

The Linux endpoint is actively reporting telemetry to Wazuh.

---

### Deliverable 2 — Log Collection

**Target:**

Demonstrate collection of at least **4 distinct Linux telemetry sources/categories**, such as:

* Authentication logs
* System logs
* Journald
* Audit logs
* Service logs

**Evidence:**

* Local Linux log evidence.
* Corresponding centralized Wazuh event evidence.

**Pass Criteria:**

The selected telemetry is visible locally and can be observed centrally.

---

### Deliverable 3 — Authentication Monitoring

**Target:**

Generate and investigate at least:

* 3 failed authentication events.
* 1 successful authentication event.
* 1 authentication correlation scenario.

**Evidence:**

* Failed authentication events.
* Successful authentication event.
* Source/user information.
* Investigation timeline.

**Pass Criteria:**

The analyst can explain who authenticated, what happened, when it happened, and whether the activity is suspicious.

---

### Deliverable 4 — Privilege Monitoring

**Target:**

Generate at least **2 controlled privilege-related events**, such as:

* `sudo` activity.
* Privileged command execution.
* Group/privilege modification.

**Evidence:**

* Original event.
* User involved.
* Command or activity.
* Wazuh event/alert where applicable.

**Pass Criteria:**

The analyst can determine whether the privilege activity is authorized or suspicious.

---

### Deliverable 5 — Process Monitoring

**Target:**

Generate and investigate at least **3 process/command execution events**.

Examples:

* Normal shell command.
* Administrative command.
* Controlled suspicious command simulation.

**Evidence:**

* Process/command telemetry.
* Parent process where available.
* User context.
* Timestamp.

**Pass Criteria:**

The analyst can reconstruct the process activity and identify the responsible user/process context.

---

### Deliverable 6 — Detection Rules

**Target:**

Create and validate at least **3 detection scenarios**.

Example coverage:

| Detection                      | Expected Result           |
| ------------------------------ | ------------------------- |
| Repeated failed authentication | Alert generated           |
| Privileged activity            | Alert or detectable event |
| Suspicious process/command     | Alert or detectable event |

**Evidence:**

* Detection rule configuration.
* Test event.
* Generated alert.
* Rule validation result.

**Pass Criteria:**

Each selected detection reliably identifies the intended test behavior.

---

### Deliverable 7 — Alert Investigation

**Target:**

Perform at least **3 complete alert investigations**.

Each investigation should document:

* Alert
* Event
* Endpoint
* User
* Source
* Timestamp
* Related events
* Assessment
* Disposition

**Pass Criteria:**

The investigation reaches a defensible conclusion supported by telemetry.

---

### Deliverable 8 — Incident Investigation

**Target:**

Complete at least **2 multi-event investigations**.

Each investigation should correlate at least **3 related events**.

Example:

Authentication Failure
→ Successful Authentication
→ Privileged Activity
→ Process Execution

**Pass Criteria:**

The analyst reconstructs a coherent event timeline and identifies the likely security significance.

---

### Deliverable 9 — Response Actions

**Target:**

Perform at least **2 controlled response actions** against test activity.

Examples:

* Disable a test account.
* Terminate a controlled suspicious process.
* Remove unauthorized test privilege.
* Stop a controlled test service.

**Evidence:**

* Pre-response state.
* Response action.
* Post-response state.
* Verification evidence.

**Pass Criteria:**

The response action reduces or removes the simulated security risk without unnecessarily disrupting the lab environment.

---

### Deliverable 10 — Response Verification

**Target:**

After every response action, perform at least **1 verification check**.

Verification may include:

* Re-checking account status.
* Confirming process termination.
* Confirming privilege removal.
* Confirming service state.
* Confirming the original detection condition no longer exists.

**Pass Criteria:**

The analyst can demonstrate that the response action achieved its intended result.

---

### Deliverable 11 — Evidence Package

The final lab should contain evidence for:

* Endpoint connectivity
* Log collection
* Detection
* Alerts
* Investigation
* Response
* Verification

Evidence should be stored under:

`Evidence/`

**Pass Criteria:**

Another analyst should be able to understand what happened by reviewing the evidence without requiring undocumented assumptions.

---

### Deliverable 12 — Incident Report

Produce at least **1 professional incident investigation report** under:

`Reports/`

The report should contain:

1. Incident Summary
2. Detection
3. Affected Endpoint
4. User/Account
5. Timeline
6. Evidence
7. Analysis
8. Root Cause
9. Impact Assessment
10. Containment
11. Remediation
12. Recovery
13. Verification
14. Lessons Learned

**Pass Criteria:**

The report demonstrates the complete monitoring-to-response lifecycle.

---

## Measurable Completion Scorecard

| Area                             |     Minimum Target |
| -------------------------------- | -----------------: |
| Monitored Linux endpoints        |                  1 |
| Telemetry sources/categories     |                  4 |
| Failed authentication events     |                 3+ |
| Successful authentication events |                 1+ |
| Privilege events                 |                 2+ |
| Process/command events           |                 3+ |
| Detection scenarios              |                 3+ |
| Alert investigations             |                 3+ |
| Multi-event investigations       |                 2+ |
| Controlled response actions      |                 2+ |
| Verification checks              |                 2+ |
| Professional incident reports    |                 1+ |
| Evidence packages                | 1 complete package |

These numbers are minimum lab targets. Additional scenarios can be added after the baseline objectives are completed.

---

## Learning Outcomes

After completing this lab, the learner should be able to:

* Explain the purpose of Linux security monitoring.
* Identify important Linux security log sources.
* Understand authentication-related Linux events.
* Explain the role of `journald` and traditional log files.
* Understand Linux audit telemetry.
* Configure and verify log collection.
* Monitor SSH authentication activity.
* Investigate failed and successful authentication.
* Monitor user and privilege activity.
* Analyze Linux process execution.
* Identify suspicious command execution patterns.
* Build basic detection logic.
* Investigate alerts using Wazuh.
* Correlate authentication, privilege, and process activity.
* Reconstruct an event timeline.
* Select an appropriate response action.
* Perform controlled containment and remediation.
* Verify that response actions were effective.
* Troubleshoot monitoring failures.
* Produce professional investigation documentation.

---

## Success Criteria

The lab will be considered successful when the following conditions are demonstrated:

* Linux endpoint is connected to the monitoring platform.
* Relevant Linux logs are successfully collected.
* Authentication events are visible centrally.
* User and privilege activity can be monitored.
* Process activity can be investigated.
* Security-relevant events generate detectable telemetry.
* Detection rules can identify selected scenarios.
* Alerts can be investigated using available event context.
* Multiple events can be correlated into a timeline.
* At least two controlled response actions are successfully performed.
* Response actions are verified.
* Collection and detection problems can be diagnosed.
* Evidence is captured and organized.
* At least one professional incident report is produced.
* Investigation results are documented professionally.

---

## Scope

This lab is limited to:

* Authorized Linux virtual machines.
* Personal/home laboratory infrastructure.
* Defensive security monitoring.
* Security telemetry collection.
* Detection engineering.
* Alert analysis.
* Incident investigation.
* Controlled incident response.
* Documentation and evidence collection.

The lab does not authorize monitoring or attacking systems belonging to other individuals or organizations.

---

## Evidence Requirements

Evidence should be captured throughout the lab and stored under:

`Evidence/`

Recommended evidence includes:

* Linux log screenshots.
* Wazuh dashboard screenshots.
* Authentication events.
* Failed authentication events.
* Successful authentication events.
* `sudo` activity.
* User/account activity.
* Process activity.
* Detection alerts.
* Investigation timelines.
* Detection-rule validation.
* Pre-response state.
* Response actions.
* Post-response state.
* Verification results.
* Troubleshooting results.

Evidence should demonstrate the actual work performed rather than simply showing configuration screens.

---

## Expected Professional Skills

This lab is designed to demonstrate entry-level SOC analyst capabilities in:

### Security Monitoring

Understanding endpoint telemetry and identifying security-relevant events.

### Log Analysis

Reading and interpreting Linux authentication, system, process, and audit information.

### Detection

Creating and validating basic detection logic based on observable security behavior.

### Alert Triage

Determining whether an alert represents normal, suspicious, or malicious activity.

### Investigation

Correlating multiple events to understand what happened, when it happened, and which account or process was involved.

### Incident Response

Performing controlled containment, remediation, recovery, and verification activities.

### Troubleshooting

Identifying whether failures originate from the endpoint, logging configuration, collection pipeline, or detection layer.

### Documentation

Recording evidence, analysis, conclusions, response actions, and verification results in a professional format.

---

## Lab Completion Objective

The final objective of the Linux Security Monitoring Lab is to demonstrate the complete defensive monitoring lifecycle:

**Generate → Collect → Detect → Analyze → Investigate → Respond → Recover → Verify → Document**

The learner should finish the lab with practical evidence showing the ability to monitor a Linux endpoint, investigate security-relevant activity, perform controlled response actions, and verify the effectiveness of those actions using a SOC-oriented workflow.

---

## Related Documentation

The following documentation will expand upon this objective:

* `02-Lab-Setup.md`
* `03-Linux-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-Shell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
