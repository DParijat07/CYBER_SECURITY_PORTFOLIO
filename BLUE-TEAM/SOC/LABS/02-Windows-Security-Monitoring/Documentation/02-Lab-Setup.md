# Lab Setup

## Purpose

This document describes the technical environment required to perform the Windows Security Monitoring Lab.

The setup provides a controlled Windows endpoint environment where security events can be generated, collected, monitored, analyzed, and investigated using defensive security tools.

---

## Lab Environment

The lab is designed as a virtualized home-lab environment.

The primary components are:

* Windows 11 host system
* VMware Workstation
* Windows virtual machine
* Kali Linux virtual machine(s)
* Wazuh SIEM environment
* Virtual network for communication between lab systems

The environment should remain isolated from unauthorized systems and should only be used for authorized security testing.

---

## Lab Architecture

The basic architecture is:

```
Windows 11 Host
       │
       │
VMware Workstation
       │
       ├───────────────┐
       │               │
       ▼               ▼
Windows VM         Kali Linux VM
Security           Testing/
Monitoring         Analysis
Endpoint
       │
       │
       ▼
  Wazuh Server
  / SIEM
  Monitoring
```

The Windows VM acts as the primary monitored endpoint.

The Wazuh environment is used to collect and analyze security telemetry when integrated into the lab.

Kali Linux may be used to generate controlled and authorized network or endpoint activity for monitoring exercises.

---

## Core Components

### 1. Windows Host

The physical Windows 11 system provides the virtualization platform for the laboratory.

Responsibilities:

* Run VMware Workstation
* Host virtual machines
* Provide computing resources
* Maintain the isolated lab environment

---

### 2. Windows Monitoring Endpoint

The Windows virtual machine is the primary endpoint being monitored.

It is used to generate and observe security telemetry such as:

* Authentication events
* Account activity
* Process creation
* PowerShell activity
* System events
* File activity
* Security policy events

The Windows endpoint should have sufficient resources to operate normally while generating monitoring telemetry.

---

### 3. Wazuh SIEM

Wazuh provides centralized security monitoring and analysis capabilities.

It can be used to:

* Collect Windows logs
* Monitor endpoint activity
* Generate security alerts
* Apply detection rules
* Investigate events
* Correlate security information
* Support incident investigation

The Wazuh server should be reachable from the Windows monitoring endpoint over the lab network.

---

### 4. Kali Linux

Kali Linux is used as an authorized testing and activity-generation system.

Potential uses include:

* Generating controlled network activity
* Testing monitoring visibility
* Simulating selected security scenarios
* Validating detection rules
* Supporting investigation exercises

Kali Linux must only interact with systems inside the authorized lab environment.

---

## Virtual Network

All required virtual machines should be connected through a controlled VMware virtual network.

Example:

```
Windows VM
    │
    ├──────── Lab Virtual Network ────────┐
    │                                     │
    ▼                                     ▼
Wazuh Server                         Kali Linux
```

The exact IP addresses may vary depending on the local VMware configuration.

Document the actual addresses used during the lab in the relevant evidence or investigation report.

---

## Required Software

The following software/components may be used:

* Windows 11
* Windows monitoring endpoint
* VMware Workstation
* Wazuh
* Kali Linux
* Windows Event Viewer
* PowerShell

Additional defensive tools may be introduced when required for a specific monitoring scenario.

---

## Windows Monitoring Endpoint Preparation

Before beginning monitoring exercises, verify that the Windows endpoint:

1. Boots successfully.
2. Has network connectivity to the required lab systems.
3. Has Windows Event Viewer available.
4. Has PowerShell available.
5. Generates normal Windows security events.
6. Can communicate with the Wazuh environment when Wazuh integration is enabled.
7. Has sufficient storage for collected logs and evidence.

---

## Wazuh Connectivity Verification

When Wazuh is included in the monitoring workflow, verify:

* Wazuh server is running.
* Wazuh agent is installed on the Windows endpoint.
* The Windows endpoint is visible to the Wazuh server.
* The agent is connected.
* Windows security logs are being collected.
* Events are appearing in the Wazuh interface.

The exact Wazuh configuration should be documented separately in:

`04-Security-Monitoring-Configuration.md`

---

## Windows Event Logging Verification

Open Windows Event Viewer and verify access to relevant event logs.

Important sources include:

* Windows Security log
* Windows System log
* Windows Application log
* PowerShell-related logs
* Microsoft-Windows-Sysmon/Operational, when Sysmon is installed
* Other security-relevant Windows operational logs

The availability of individual logs depends on the Windows configuration and monitoring components installed.

---

## Initial Setup Verification

Before starting security scenarios, perform the following checks.

### System Check

* Windows VM is running.
* VMware networking is functioning.
* Required virtual machines are available.
* Lab network is reachable.

### Monitoring Check

* Event Viewer opens successfully.
* Security logs contain events.
* PowerShell logging is available where configured.
* Process telemetry is available where configured.
* Wazuh agent is running when Wazuh is used.

### Evidence Check

Create a baseline record of:

* Windows version
* Hostname
* IP address
* Wazuh agent status
* Monitoring tools installed
* Relevant logging configuration
* Initial system state

---

## Baseline Activity

Before generating suspicious or controlled security activity, observe normal endpoint behavior.

Examples:

* Normal user login
* Normal application execution
* Normal PowerShell usage
* Normal system activity
* Normal network communication

This baseline helps distinguish normal behavior from potentially suspicious activity during later investigations.

---

## Lab Isolation and Safety

The laboratory must remain within an authorized environment.

Follow these principles:

* Use only systems owned or explicitly authorized for testing.
* Keep security testing inside the lab network.
* Do not intentionally target public systems.
* Avoid exposing vulnerable laboratory systems directly to the Internet.
* Take VM snapshots before major configuration changes.
* Maintain backups of important evidence.
* Remove temporary test artifacts when exercises are complete.

---

## Configuration Documentation

All important configuration changes should be documented.

Examples include:

* Windows audit policy changes
* PowerShell logging configuration
* Sysmon configuration
* Wazuh agent configuration
* Log collection configuration
* Detection rule configuration
* Network configuration

Configuration details should be documented in:

`04-Security-Monitoring-Configuration.md`

---

## Evidence Collection

During setup, collect evidence demonstrating that the monitoring environment is operational.

Possible evidence:

* Windows system information
* Windows Event Viewer
* Security log
* PowerShell logging configuration
* Sysmon status
* Wazuh agent status
* Wazuh endpoint visibility
* Network connectivity
* Baseline events

Store supporting evidence in:

`../Evidence/`

---

## Setup Completion Criteria

The lab setup is considered complete when:

* The Windows monitoring endpoint is operational.
* The required virtual network is functioning.
* Windows security logs are accessible.
* Required monitoring telemetry is available.
* Wazuh integration is operational when used.
* Baseline activity can be observed.
* Evidence of the setup has been collected.
* The environment is ready for controlled security scenarios.

---

## Scope

This setup is intended exclusively for the authorized Windows Security Monitoring Lab.

The environment supports defensive monitoring, detection, investigation, incident response, and security documentation.

---

## Related Documentation

The next documentation files build on this setup:

* `03-Windows-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `09-Process-Monitoring.md`
* `10-PowerShell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
