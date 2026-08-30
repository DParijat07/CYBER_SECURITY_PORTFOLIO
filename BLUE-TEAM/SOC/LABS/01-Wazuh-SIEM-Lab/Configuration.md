# Wazuh SIEM Lab — Configuration

## 1. Purpose

This document covers the configuration phase of the Wazuh SIEM laboratory.

The objective is to configure the Wazuh server and monitored endpoints so that security telemetry can be collected, analyzed, and displayed for SOC monitoring and investigation.

All configuration activities must be performed only within the authorized home-lab environment.

---

## 2. Configuration Workflow

The configuration process follows this workflow:

```text
Wazuh Installation
       ↓
Server Configuration
       ↓
Agent Configuration
       ↓
Log Source Configuration
       ↓
Security Monitoring Configuration
       ↓
Detection Configuration
       ↓
Restart / Reload Services
       ↓
Verify Telemetry
       ↓
Generate Test Events
       ↓
Verify Alerts
```

---

## 3. Configuration Objectives

After completing this phase, the learner should be able to:

- Configure basic Wazuh settings.
- Configure monitored endpoints.
- Configure relevant log sources.
- Configure endpoint monitoring.
- Understand Wazuh configuration files.
- Configure basic file-integrity monitoring.
- Configure security-event collection.
- Configure selected Windows event sources.
- Configure selected Linux log sources.
- Verify agent communication.
- Validate telemetry collection.
- Generate controlled test events.
- Verify that expected alerts are produced.

---

## 4. Configuration Principles

Use the following principles throughout the lab:

1. Change only the configuration required for the exercise.
2. Back up configuration files before modifying them.
3. Make one logical change at a time.
4. Validate configuration after changes.
5. Restart only the required service.
6. Monitor service status after restarting.
7. Document every significant configuration change.
8. Test the configuration before moving to the next stage.

---

## 5. Configuration Backup

Before modifying an important configuration file, create a backup.

Example:

```bash
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.bak
```

The exact configuration path may differ depending on the deployment.

Keep backups outside publicly published portfolio evidence if they contain sensitive information.

---

## 6. Wazuh Manager Configuration

The primary Wazuh Manager configuration is commonly stored in:

```text
/var/ossec/etc/ossec.conf
```

This configuration controls multiple aspects of Wazuh Manager behavior.

Before modifying the file:

```bash
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.bak
```

Review the existing configuration before making changes.

---

## 7. Agent Configuration

The Wazuh agent configuration is commonly stored in:

```text
/var/ossec/etc/ossec.conf
```

on Linux agents.

On Windows, the agent configuration is normally stored within the Wazuh installation directory.

The configuration should specify the Wazuh Manager address and the monitoring settings required for the lab.

---

## 8. Configure Manager Address

Each agent must know which Wazuh Manager it should communicate with.

Conceptually:

```text
Wazuh Agent
     │
     │ Manager Address
     ▼
Wazuh Manager
```

Use the actual IP address or hostname of your Wazuh server.

Example:

```text
WAZUH-SERVER
192.168.100.10
```

Do not copy the example address directly unless it matches your laboratory.

---

## 9. Agent Identity

Use meaningful names for monitored endpoints.

Example:

```text
WIN-ENDPOINT
LINUX-ENDPOINT
```

Clear agent names make it easier to identify systems during alert investigation.

---

## 10. Verify Agent Connectivity

After configuration, verify that the agent is communicating with the manager.

On Linux:

```bash
sudo systemctl status wazuh-agent
```

On Windows:

```text
Services
    ↓
Wazuh Agent
    ↓
Running
```

Then verify the agent from the Wazuh Dashboard.

Expected state:

```text
Agent
  ↓
Connected
  ↓
Active
```

---

## 11. Windows Security Event Monitoring

Windows generates valuable telemetry for SOC investigations.

Relevant event sources may include:

- Security
- System
- Application
- PowerShell
- Microsoft-Windows-Sysmon/Operational

Examples of useful security events include:

- Authentication failures
- Successful logins
- Account creation
- Account changes
- Process creation
- Privilege-related events
- Service activity

Only enable telemetry that is relevant to the laboratory objective.

---

## 12. Windows Event Collection

The Wazuh Windows agent can be configured to collect Windows Event Channels.

The configuration should specify the event channels required for the lab.

Example concept:

```xml
<localfile>
  <location>Security</location>
  <log_format>eventchannel</log_format>
</localfile>
```

Additional channels can be configured when required.

Always verify the syntax against the Wazuh documentation for the installed version.

---

## 13. PowerShell Monitoring

PowerShell can provide valuable security telemetry.

Depending on the laboratory objective, relevant PowerShell event channels may be monitored.

Examples include:

```text
Microsoft-Windows-PowerShell/Operational
```

and, where configured:

```text
Windows PowerShell
```

PowerShell monitoring should be combined with appropriate endpoint telemetry rather than analyzed in isolation.

---

## 14. Sysmon Integration

If Sysmon is installed on the Windows endpoint, its telemetry can provide additional endpoint visibility.

The commonly monitored channel is:

```text
Microsoft-Windows-Sysmon/Operational
```

Potential telemetry includes:

- Process creation
- Network connections
- File creation
- Registry activity
- Driver activity
- Process access
- DNS activity

The exact events depend on the Sysmon configuration.

---

## 15. Linux Authentication Monitoring

Linux authentication logs are valuable for detecting suspicious login activity.

Depending on the Linux distribution, authentication information may be stored in locations such as:

```text
/var/log/auth.log
```

or:

```text
/var/log/secure
```

The correct location depends on the operating system.

---

## 16. Linux System Log Monitoring

Common Linux log sources may include:

```text
/var/log/syslog
/var/log/messages
```

Modern Linux systems may rely heavily on `systemd-journald`.

Determine which logging mechanism is used by the laboratory operating system before configuring collection.

---

## 17. Linux SSH Monitoring

SSH authentication activity is particularly useful for SOC exercises.

Monitor events such as:

- Failed SSH authentication
- Successful SSH authentication
- Invalid users
- Authentication-method changes
- Privilege escalation following login

The goal is to understand authentication behavior rather than perform unauthorized access attempts.

---

## 18. File Integrity Monitoring

Wazuh provides file-integrity monitoring capabilities through its File Integrity Monitoring functionality.

The purpose is to detect changes to selected files and directories.

Potential monitored locations may include:

```text
Important configuration files
System directories
Selected application directories
Selected laboratory files
```

Do not monitor excessively large directories without considering the resulting telemetry volume.

---

## 19. File Integrity Monitoring Workflow

The basic workflow is:

```text
Baseline
   ↓
File / Directory Change
   ↓
Wazuh Detects Change
   ↓
Security Event
   ↓
Alert
   ↓
Analyst Investigation
```

A controlled test file can be used to verify the functionality.

Example:

```bash
sudo touch /path/to/test-file.txt
```

The actual monitored directory should be configured specifically for the laboratory.

---

## 20. Rootcheck and Security Configuration Monitoring

Wazuh includes security-monitoring capabilities that can assist with identifying potentially suspicious system conditions.

These capabilities should be enabled or configured according to the laboratory requirements and supported Wazuh version.

Avoid enabling every possible feature without understanding its purpose and telemetry impact.

---

## 21. Vulnerability Detection

If vulnerability detection is included in the laboratory deployment, configure it according to the capabilities and documentation of the installed Wazuh version.

The purpose is to identify known vulnerabilities affecting monitored systems.

The workflow is:

```text
Asset
  ↓
Software Inventory
  ↓
Vulnerability Matching
  ↓
Vulnerability Finding
  ↓
Risk Assessment
  ↓
Remediation
```

Detailed vulnerability-management activities can be documented separately in:

```text
LABS/12-Vulnerability-Management/
```

---

## 22. Active Response

Wazuh can support automated response actions.

For this beginner laboratory, active response should be used carefully.

Start with:

```text
Detection
   ↓
Alert
   ↓
Manual Investigation
```

Only introduce automated response after understanding the alert and validation workflow.

Potential future use cases include:

- Blocking a malicious IP
- Disabling a test account
- Executing a controlled response script

Any automated response should be tested only against authorized laboratory systems.

---

## 23. Detection Rules

Wazuh uses rules to identify security events and generate alerts.

A simplified workflow is:

```text
Raw Event
    ↓
Decoder
    ↓
Rule Matching
    ↓
Alert
```

The learner should understand that detection depends on:

- Correct telemetry
- Correct parsing
- Appropriate rules
- Relevant event fields
- Appropriate thresholds

---

## 24. Custom Detection Rules

Custom rules can be created when the laboratory requires detection logic not provided by the default rules.

Custom rules should:

- Have a clear purpose.
- Use unique identifiers where appropriate.
- Include useful descriptions.
- Avoid unnecessary duplication.
- Be tested before deployment.
- Be documented.
- Be version-controlled where practical.

Custom rule development can be expanded in:

```text
LABS/11-Detection-Engineering/
```

---

## 25. Rule Testing

A detection rule should be tested using controlled events.

Example workflow:

```text
Detection Requirement
        ↓
Create Rule
        ↓
Generate Test Event
        ↓
Check Wazuh Alert
        ↓
Review Rule Match
        ↓
Tune Rule
        ↓
Retest
```

Never assume that a rule works simply because it has been written.

---

## 26. Severity and Alert Levels

Wazuh alerts include severity information.

During analysis, consider:

- Alert level
- Rule ID
- Rule description
- Event source
- Event context
- Related activity

Severity alone should not determine whether an event is a real incident.

A high-severity alert may be legitimate, while a lower-severity event may become significant when correlated with other activity.

---

## 27. Log Collection Validation

After configuring a log source, verify that data is actually reaching Wazuh.

Validation workflow:

```text
Generate Event
      ↓
Endpoint Log
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Indexer
      ↓
Dashboard
      ↓
Search / Alert
```

If an event is missing, troubleshoot each stage rather than assuming the problem is with the Dashboard.

---

## 28. Configuration Validation

After modifying configuration files:

1. Save the configuration.
2. Validate the configuration if the installed component provides a validation mechanism.
3. Restart the required service.
4. Check service status.
5. Monitor logs for errors.
6. Generate a controlled test event.
7. Verify the expected telemetry.

Example:

```bash
sudo systemctl restart wazuh-manager
```

Then:

```bash
sudo systemctl status wazuh-manager
```

Use the equivalent procedure for the affected service.

---

## 29. Configuration Change Documentation

Maintain a record of significant configuration changes.

Example:

```text
Date:
Component:
Configuration File:
Change:
Reason:
Expected Result:
Actual Result:
Validation:
Rollback Required:
```

This is useful for troubleshooting and demonstrates professional change-management practice.

---

## 30. Recommended Configuration Order

Configure the laboratory in the following order:

```text
1. Verify Wazuh Server
        ↓
2. Verify Dashboard
        ↓
3. Configure Agent Communication
        ↓
4. Connect Windows Endpoint
        ↓
5. Configure Windows Event Collection
        ↓
6. Connect Linux Endpoint
        ↓
7. Configure Linux Log Collection
        ↓
8. Configure Sysmon Telemetry
        ↓
9. Configure File Integrity Monitoring
        ↓
10. Verify Security Events
        ↓
11. Verify Alerts
        ↓
12. Test Detection
```

---

## 31. Configuration Checklist

### Wazuh Server

- [ ] Manager configuration reviewed
- [ ] Configuration backup created
- [ ] Manager address documented
- [ ] Server hostname configured
- [ ] Server IP documented
- [ ] Manager service operational

### Windows Endpoint

- [ ] Agent installed
- [ ] Manager address configured
- [ ] Agent connected
- [ ] Security event collection configured
- [ ] System event collection configured
- [ ] PowerShell telemetry configured where required
- [ ] Sysmon telemetry configured where applicable

### Linux Endpoint

- [ ] Agent installed
- [ ] Manager address configured
- [ ] Agent connected
- [ ] Authentication logs configured
- [ ] System logs configured
- [ ] SSH telemetry verified

### Detection

- [ ] Events generated
- [ ] Events received
- [ ] Rules matched
- [ ] Alerts visible
- [ ] Alert severity reviewed
- [ ] Detection behavior documented

---

## 32. Evidence to Capture

Recommended evidence includes:

1. Wazuh server configuration.
2. Connected-agent status.
3. Windows event collection.
4. Linux log collection.
5. Sysmon telemetry.
6. File-integrity monitoring.
7. Example Wazuh alerts.
8. Detection-rule results.
9. Configuration validation.
10. Successful test-event collection.

Store evidence under:

```text
01-Wazuh-SIEM-Lab/
└── Evidence/
    └── Configuration/
```

Remove sensitive information before publishing screenshots or configuration files.

---

## 33. Troubleshooting During Configuration

If telemetry is missing, check the following sequence:

```text
Is the endpoint running?
        ↓
Is the Wazuh Agent running?
        ↓
Is the agent connected?
        ↓
Is the log source generating events?
        ↓
Is the log source configured?
        ↓
Is the Wazuh Manager receiving data?
        ↓
Is the event being decoded?
        ↓
Is a rule matching the event?
        ↓
Is the alert indexed?
        ↓
Is the Dashboard displaying it?
```

This systematic approach reduces unnecessary configuration changes.

---

## 34. Security Considerations

Do not:

- Publish credentials.
- Publish private keys.
- Publish API tokens.
- Publish sensitive configuration.
- Expose the Wazuh Dashboard unnecessarily.
- Apply experimental configurations to production systems.
- Enable destructive automated responses without testing.
- Monitor unauthorized systems.

Use only authorized laboratory systems.

---

## 35. Completion Criteria

The configuration phase is complete when:

- [ ] Wazuh Manager is operational.
- [ ] Dashboard is accessible.
- [ ] Agents are connected.
- [ ] Windows telemetry is being collected.
- [ ] Linux telemetry is being collected.
- [ ] Sysmon telemetry is available where applicable.
- [ ] File-integrity monitoring is tested.
- [ ] Security events are visible.
- [ ] Alerts are generated.
- [ ] Configuration changes are documented.
- [ ] Evidence has been captured.
- [ ] Sensitive information has been removed from public evidence.

---

## 36. Next Step

After completing configuration, continue with:

**Log Collection → Alert Analysis → Investigation → Troubleshooting**

The next stage should focus on verifying exactly what security telemetry Wazuh is receiving from the monitored endpoints and how that data is used by the SOC analyst.
