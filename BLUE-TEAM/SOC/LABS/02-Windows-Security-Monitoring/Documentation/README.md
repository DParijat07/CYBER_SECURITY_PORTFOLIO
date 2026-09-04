# Documentation

## Purpose

This directory contains the complete technical documentation for the Windows Security Monitoring lab.

It documents how Windows security telemetry is generated, collected, monitored, analyzed, detected, investigated, and used for incident response within the controlled home lab environment.

## Lab Scope

The scope of this lab is to demonstrate practical security monitoring and SOC investigation capabilities on a Windows endpoint.

### In Scope

* Windows security event logging
* Windows Security, System, and Application logs
* Authentication and logon monitoring
* Account and privilege activity
* Process execution monitoring
* PowerShell activity monitoring
* File and system activity monitoring
* Sysmon telemetry, where configured
* Security event detection
* Alert analysis
* Incident investigation
* Basic incident response
* Detection verification
* Security evidence collection
* SOC documentation and reporting

### Out of Scope

The following activities are outside the primary scope of this lab:

* Production Windows infrastructure
* Unauthorized systems or networks
* Destructive malware deployment
* Real-world attacks against external systems
* Advanced malware reverse engineering
* Enterprise-scale SIEM architecture
* Paid cloud infrastructure
* Full digital forensics investigations

All security testing must be performed within the authorized home lab environment.

## Windows Security Monitoring Workflow

The lab follows a practical SOC workflow for monitoring and investigating security activity on Windows endpoints.

```text
Windows Activity / Security Event
            ↓
     Event Generation
            ↓
     Event Log Collection
            ↓
    Security Telemetry
            ↓
     Detection / Rules
            ↓
        SOC Alert
            ↓
      Alert Analysis
            ↓
   Incident Investigation
            ↓
      Response Action
            ↓
       Verification
            ↓
      Documentation
```

## Monitoring Sources

The lab focuses on security-relevant Windows telemetry, including:

* Windows Security Event Logs
* System Event Logs
* Application Event Logs
* PowerShell activity
* Process creation events
* Authentication events
* Account and privilege activity
* File and system activity
* Sysmon telemetry, where configured

## Key Windows Security Events

The lab may investigate events such as:

* Successful and failed logons
* Account creation and modification
* Privilege-related activity
* Process creation
* PowerShell execution
* Service activity
* Security policy changes
* File or system changes
* Other suspicious endpoint activity

Event IDs should be documented alongside the corresponding investigation when applicable.

## Scenario-Based Monitoring

The lab uses controlled scenarios to demonstrate practical Windows security monitoring.

Examples include:

### Failed Authentication

```text
Repeated Failed Logons
        ↓
Windows Security Event
        ↓
Event Log Collection
        ↓
Detection
        ↓
Alert Analysis
        ↓
Source / Account Investigation
        ↓
Determine Suspicious Activity
        ↓
Response
        ↓
Verification
```

### Suspicious Process Execution

```text
Process Execution
        ↓
Windows / Sysmon Event
        ↓
Telemetry Collection
        ↓
Detection
        ↓
Alert
        ↓
Process / Parent Process Analysis
        ↓
Command-Line Investigation
        ↓
Determine Risk
        ↓
Response
        ↓
Verification
```

### PowerShell Activity

```text
PowerShell Execution
        ↓
Windows / PowerShell Telemetry
        ↓
Event Collection
        ↓
Detection
        ↓
Alert Analysis
        ↓
Command / User / Host Investigation
        ↓
Determine Legitimate or Suspicious Activity
        ↓
Response
        ↓
Verification
```

## Core Analyst Investigation Model

Each Windows monitoring scenario follows:

```text
DETECT
  ↓
VALIDATE
  ↓
ANALYZE
  ↓
INVESTIGATE
  ↓
RESPOND
  ↓
VERIFY
  ↓
DOCUMENT
```

The objective is to demonstrate practical Windows security monitoring and SOC investigation skills rather than simply collecting event logs.

## Required Documentation Files

The following documentation files define the complete scope of the Windows Security Monitoring lab:

1. `01-Lab-Objective.md` — Defines the purpose, goals, learning outcomes, and success criteria.
2. `02-Lab-Setup.md` — Documents the Windows monitoring environment, virtual machines, network configuration, and required components.
3. `03-Windows-Event-Logging.md` — Explains Windows event logging and the security-relevant event sources used in the lab.
4. `04-Security-Monitoring-Configuration.md` — Documents the configuration required to enable and monitor Windows security telemetry.
5. `05-Log-Collection.md` — Documents how Windows logs and telemetry are collected for analysis.
6. `06-Detection-Rules.md` — Documents detection logic and security rules used to identify suspicious activity.
7. `07-Alert-Analysis.md` — Defines the process for reviewing, validating, and analyzing Windows security alerts.
8. `08-Authentication-Monitoring.md` — Covers successful and failed authentication, account activity, and related monitoring.
9. `09-Process-Monitoring.md` — Covers process creation, parent-child relationships, command-line activity, and suspicious process analysis.
10. `10-PowerShell-Monitoring.md` — Covers PowerShell telemetry, execution monitoring, and suspicious PowerShell activity.
11. `11-Incident-Investigation.md` — Documents the investigation methodology used to analyze Windows security incidents.
12. `12-Incident-Response.md` — Documents containment, response, remediation, and recovery activities.
13. `13-Scenarios.md` — Contains controlled scenario-based exercises used to validate the monitoring workflow.
14. `14-Troubleshooting.md` — Documents common configuration, logging, collection, and detection problems and their solutions.
15. `15-Lessons-Learned.md` — Records findings, limitations, improvements, and lessons learned from the lab.

## Documentation Structure

The documentation is organized using the following sequence:

```text
01-Lab-Objective.md
02-Lab-Setup.md
03-Windows-Event-Logging.md
04-Security-Monitoring-Configuration.md
05-Log-Collection.md
06-Detection-Rules.md
07-Alert-Analysis.md
08-Authentication-Monitoring.md
09-Process-Monitoring.md
10-PowerShell-Monitoring.md
11-Incident-Investigation.md
12-Incident-Response.md
13-Scenarios.md
14-Troubleshooting.md
15-Lessons-Learned.md
```

## Documentation Standards

* Document activities actually performed in the lab.
* Use technically accurate Windows terminology.
* Include relevant Event IDs where applicable.
* Record useful timestamps, users, hosts, processes, and other investigation details.
* Explain the purpose of important Windows security events.
* Link findings to supporting evidence.
* Keep procedures reproducible.
* Use controlled and authorized lab activity only.
* Never include passwords, credentials, tokens, or other sensitive information.

## Relationship With Other Lab Directories

```text
Documentation/
    ↓
Technical procedures, monitoring methods, investigations, and findings

Evidence/
    ↓
Screenshots, event logs, alerts, and technical proof

Reports/
    ↓
Professional analysis, findings, and conclusions
```

## Objective

The objective of this documentation is to demonstrate practical Windows endpoint security monitoring capabilities, including:

**Event Generation → Collection → Detection → Analysis → Investigation → Response → Verification → Documentation**
