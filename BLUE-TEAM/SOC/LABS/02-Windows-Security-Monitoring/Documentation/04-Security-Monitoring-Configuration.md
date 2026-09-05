# Security Monitoring Configuration

## Purpose

This document defines the Windows security monitoring configuration required to generate useful endpoint telemetry for the lab.

The objective is to configure security-relevant logging so that authentication, account, process, PowerShell, system, and other endpoint activities can be observed and investigated.

---

## Configuration Objectives

The monitoring configuration should provide visibility into:

* Successful and failed authentication
* Account management
* Privileged activity
* Process creation
* PowerShell execution
* Security policy changes
* System activity
* Relevant endpoint behavior
* Security events required for detection and investigation

The configuration should provide sufficient telemetry without generating unnecessary noise.

---

## Configuration Workflow

The configuration follows this process:

```
Identify Monitoring Requirements
          ↓
Configure Windows Auditing
          ↓
Configure Process Auditing
          ↓
Configure PowerShell Logging
          ↓
Configure Sysmon (Optional)
          ↓
Configure Wazuh Collection
          ↓
Generate Test Activity
          ↓
Verify Telemetry
          ↓
Document Configuration
```

---

## Windows Audit Policy

Windows Audit Policy determines which security-related activities are recorded in the Security event log.

Audit policies can be reviewed using:

`secpol.msc`

Navigate to:

`Security Settings → Advanced Audit Policy Configuration`

The exact available policies depend on the Windows edition and configuration.

---

## Recommended Audit Categories

For this lab, focus on audit categories relevant to SOC monitoring.

### Account Logon

Useful for monitoring authentication-related activity.

Monitor:

* Credential validation
* Authentication activity
* Account logon events

---

### Logon/Logoff

Useful for monitoring user sessions.

Monitor:

* Logon
* Logoff
* Account lockout
* Other relevant session activity

These events are particularly useful for identifying repeated authentication failures and unusual login behavior.

---

### Account Management

Useful for monitoring changes to accounts.

Monitor activities such as:

* User account creation
* User account modification
* User account deletion
* Account enable/disable
* Group membership changes

---

### Detailed Tracking

Detailed tracking can provide additional visibility into endpoint activity.

Where required, enable auditing for:

* Process creation
* Process termination

Process creation auditing is especially important for investigating suspicious execution.

---

### Policy Change

Policy-change auditing can help identify modifications to security configuration.

Monitor:

* Audit policy changes
* Authentication policy changes
* Privilege-related policy changes
* Other security policy modifications

---

### Privilege Use

Privilege-use auditing can provide visibility into certain privileged operations.

It should be enabled where appropriate for the monitoring objectives of the lab.

---

### System

System-level auditing can assist with investigating:

* System startup
* System shutdown
* Security-related system changes
* Service-related activity

---

## Process Creation Auditing

Process creation logging is important for endpoint monitoring.

The primary Windows Security event associated with process creation is:

`Event ID 4688 — A new process has been created`

Process monitoring becomes more useful when command-line information is included.

### Recommended Configuration

Enable:

`Audit Process Creation`

Where supported, also enable:

`Include command line in process creation events`

This provides additional context about how a process was executed.

Example:

```
Process Name
      +
Parent Process
      +
Command Line
      +
User
      +
Timestamp
      ↓
Process Investigation
```

---

## PowerShell Logging

PowerShell should be configured to provide useful security telemetry.

Recommended logging capabilities include:

* Module Logging
* Script Block Logging
* PowerShell operational logging

Important PowerShell Event IDs include:

* `4103` — Module Logging
* `4104` — Script Block Logging
* `400` — PowerShell engine started
* `403` — PowerShell engine stopped

---

## Script Block Logging

Script Block Logging provides visibility into PowerShell script blocks executed on the endpoint.

It can be particularly useful when investigating suspicious PowerShell behavior.

The configuration should be enabled only within the authorized lab environment and used for defensive monitoring.

---

## Module Logging

Module Logging provides visibility into PowerShell module activity.

It can help analysts understand which PowerShell functionality was used during execution.

---

## PowerShell Operational Log

PowerShell operational events can be reviewed through Event Viewer.

Typical location:

`Applications and Services Logs → Microsoft → Windows → PowerShell`

The exact channels available depend on the Windows version and PowerShell configuration.

---

## Sysmon Configuration

Sysmon is an optional but valuable endpoint telemetry source.

When installed, Sysmon can provide enhanced visibility into:

* Process creation
* Network connections
* File creation
* Registry activity
* DNS queries
* Process access
* Other endpoint behavior

The primary Sysmon event channel is:

`Microsoft-Windows-Sysmon/Operational`

Sysmon configuration should be appropriate for the lab's monitoring objectives.

Avoid enabling excessive telemetry without a specific monitoring requirement because unnecessary events can increase noise.

---

## Wazuh Agent Configuration

When Wazuh is used, the Windows endpoint should have a Wazuh agent configured to collect relevant telemetry.

The monitoring workflow becomes:

```
Windows Endpoint
      ↓
Windows Event Logs
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Detection Rules
      ↓
Alerts
      ↓
SOC Investigation
```

The exact Wazuh configuration should reflect the log sources required by the lab.

---

## Monitoring Sources

The configured monitoring environment should prioritize the following sources:

| Source          | Primary Purpose                      |
| --------------- | ------------------------------------ |
| Security Log    | Authentication, accounts, privileges |
| System Log      | System and service activity          |
| Application Log | Application-related events           |
| PowerShell Logs | PowerShell execution                 |
| Sysmon          | Enhanced endpoint telemetry          |
| Wazuh           | Centralized collection and detection |

Not every source is required for every scenario.

---

## Configuration Verification

After configuration, verify that the expected telemetry is actually being generated.

### Authentication Verification

Perform controlled authentication activity and check for:

* Successful logon events
* Failed logon events
* Logoff events
* Account lockout events where applicable

---

### Process Verification

Perform a normal process execution and verify:

* Process creation event
* Process name
* User
* Timestamp
* Process ID
* Parent process
* Command line, when configured

---

### PowerShell Verification

Execute a benign PowerShell command in the authorized lab environment.

Verify that the appropriate PowerShell telemetry is generated.

Check for:

* PowerShell process
* PowerShell operational events
* Script Block Logging events
* Module logging events where enabled

---

### Sysmon Verification

If Sysmon is installed, verify that expected events appear under:

`Microsoft-Windows-Sysmon/Operational`

Check that the configured telemetry is being generated correctly.

---

### Wazuh Verification

If Wazuh is integrated:

1. Confirm the Wazuh agent is running.
2. Confirm the endpoint is connected.
3. Generate controlled test activity.
4. Confirm the event reaches Wazuh.
5. Confirm relevant alerts are generated when detection rules match.
6. Compare the Wazuh alert with the original Windows event.

---

## Configuration Baseline

Record the monitoring configuration before conducting major scenarios.

Recommended baseline information:

* Windows version
* Hostname
* IP address
* Audit policies enabled
* Process auditing status
* Command-line auditing status
* PowerShell logging status
* Sysmon status
* Wazuh agent status
* Wazuh connectivity
* Relevant event channels

This baseline helps identify configuration changes during later troubleshooting.

---

## Avoiding Excessive Logging

Security monitoring requires useful telemetry, not unlimited telemetry.

Excessive logging can create:

* High event volume
* Increased storage requirements
* Alert fatigue
* Difficult investigations
* Unnecessary noise

Therefore, monitoring configuration should follow the principle:

**Collect what is required to answer security questions.**

---

## Configuration Testing

Configuration should be validated using controlled activities.

Example:

```
Configure Logging
      ↓
Generate Benign Activity
      ↓
Check Windows Events
      ↓
Check Wazuh Telemetry
      ↓
Validate Detection
      ↓
Record Evidence
```

Do not assume that a logging policy is working simply because it has been enabled.

Always verify the resulting telemetry.

---

## Evidence Requirements

Capture evidence showing that the monitoring configuration is operational.

Useful evidence includes:

* Audit Policy configuration
* Process auditing configuration
* Command-line auditing configuration
* PowerShell logging configuration
* Sysmon status/configuration
* Wazuh agent status
* Windows Event Viewer results
* Wazuh event/alert results

Store evidence in:

`../Evidence/`

---

## Troubleshooting

If expected telemetry is missing, check:

* Audit policy configuration
* Group Policy settings
* Windows Event Log service
* Correct Event Viewer channel
* PowerShell logging configuration
* Sysmon status
* Wazuh agent status
* Wazuh collection configuration
* Network connectivity
* Event filtering

Detailed troubleshooting procedures are documented in:

`14-Troubleshooting.md`

---

## Security Considerations

All configuration and testing must be performed within the authorized laboratory.

Important principles:

* Use only authorized systems.
* Do not deploy monitoring configurations to systems without permission.
* Keep vulnerable test systems isolated.
* Avoid exposing the lab directly to the public Internet.
* Protect collected security logs and evidence.
* Do not include passwords, tokens, or other credentials in screenshots or reports.

---

## Success Criteria

The configuration is considered successful when:

* Required Windows audit policies are enabled.
* Authentication events are generated.
* Process creation telemetry is available.
* Command-line information is available where configured.
* PowerShell telemetry is generated.
* Sysmon telemetry is available when Sysmon is used.
* Wazuh receives the configured telemetry when integrated.
* Controlled test activity can be observed.
* Evidence of the configuration is collected.

---

## Professional SOC Relevance

A SOC analyst must understand how telemetry is produced before attempting to analyze alerts.

Correct monitoring configuration enables analysts to:

* Improve endpoint visibility
* Investigate authentication activity
* Analyze process execution
* Investigate PowerShell activity
* Build accurate timelines
* Reduce blind spots
* Validate detection rules
* Support incident response

---

## Conclusion

Security monitoring depends on reliable telemetry.

The Windows endpoint should therefore be configured to capture the security events required for the lab's detection and investigation objectives.

The complete monitoring chain is:

**Configure → Generate → Collect → Detect → Analyze → Investigate → Respond → Verify**

The next stage is to document how the configured Windows telemetry is collected and centralized.

Related documentation:

`05-Log-Collection.md`
