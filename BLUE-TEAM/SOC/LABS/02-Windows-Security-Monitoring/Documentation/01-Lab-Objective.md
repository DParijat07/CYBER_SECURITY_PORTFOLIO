# Lab Objective

## Purpose

The purpose of this lab is to build practical skills in monitoring, detecting, analyzing, and investigating security activity on a Windows endpoint.

The lab simulates a basic SOC environment where Windows security telemetry is collected and analyzed to identify suspicious activity and support incident response.

## Primary Objectives

The lab aims to demonstrate the ability to:

* Understand Windows security telemetry
* Configure Windows security event logging
* Identify important Windows Event IDs
* Monitor authentication activity
* Monitor process execution
* Monitor PowerShell activity
* Monitor system and file activity
* Collect Windows security logs
* Create or apply security detection rules
* Analyze generated alerts
* Investigate suspicious activity
* Perform controlled incident response
* Verify detection and remediation
* Collect supporting evidence
* Document technical findings professionally

## Lab Workflow

The lab follows this security monitoring workflow:

```text
Windows Activity
      ↓
Event Generation
      ↓
Log Collection
      ↓
Security Telemetry
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
      ↓
Verification
      ↓
Documentation
```

## Security Scenarios

The lab will use controlled scenarios to generate realistic Windows security events.

Examples include:

* Repeated failed authentication attempts
* Successful authentication following failed attempts
* Suspicious process execution
* PowerShell execution
* Account-related activity
* Privilege-related activity
* File or system changes
* Other controlled endpoint security events

Each scenario should follow the complete workflow from event generation to verification.

## Learning Outcomes

After completing the lab, the learner should be able to:

1. Explain how Windows generates security telemetry.
2. Identify important Windows security event sources.
3. Interpret relevant Event IDs.
4. Monitor authentication and endpoint activity.
5. Analyze process and PowerShell events.
6. Identify potentially suspicious behavior.
7. Investigate alerts using available telemetry.
8. Determine whether activity is benign, suspicious, or potentially malicious.
9. Perform appropriate response actions within the lab.
10. Validate that monitoring and detection controls work as expected.
11. Collect technical evidence.
12. Produce professional security documentation and reports.

## Success Criteria

The lab will be considered successful when the following outcomes are demonstrated:

* Windows security events are successfully generated.
* Relevant telemetry is successfully collected.
* Security events can be identified and analyzed.
* At least one controlled suspicious activity scenario produces useful telemetry.
* The activity can be investigated using available logs and events.
* Appropriate response or remediation can be performed.
* The original scenario can be retested.
* Supporting evidence is collected.
* Findings are documented clearly.

## Scope

This lab is limited to an authorized Windows home-lab environment.

All security testing must be performed against systems owned or explicitly authorized for testing.

The focus is defensive security monitoring rather than offensive exploitation.

## Lab Setup

The Windows Security Monitoring lab is designed to run inside an isolated home-lab environment.

### Recommended Environment

```text
Windows 11 Host
      │
      └── VMware Workstation
              │
              ├── Windows Monitoring VM
              │       ├── Windows Security Logs
              │       ├── System Logs
              │       ├── Application Logs
              │       ├── PowerShell Logs
              │       └── Sysmon Telemetry
              │
              └── Security Monitoring Infrastructure
                      └── Wazuh
```

### Windows Monitoring Endpoint

The Windows virtual machine acts as the monitored endpoint.

The endpoint should provide access to:

* Windows Event Viewer
* Security Event Logs
* System Event Logs
* Application Event Logs
* PowerShell logging
* Process activity
* File/system activity
* Sysmon telemetry, where configured

### Monitoring Infrastructure

Where applicable, the Windows endpoint forwards security telemetry to the Wazuh monitoring infrastructure.

The monitoring infrastructure is responsible for:

* Receiving endpoint telemetry
* Processing events
* Applying detection rules
* Generating alerts
* Supporting investigation
* Providing security visibility

### Network Configuration

The Windows monitoring VM and monitoring infrastructure should be able to communicate over the isolated lab network.

The lab network should be configured so that testing remains controlled and does not target unauthorized external systems.

## Prerequisites

Before starting the lab, the following prerequisites should be available.

### Hardware

* Computer capable of running virtualization
* Sufficient RAM for the Windows VM and monitoring infrastructure
* Sufficient disk space for Windows logs, telemetry, and evidence

### Virtualization

* VMware Workstation or another supported hypervisor
* Windows virtual machine
* Isolated virtual network

### Windows Knowledge

Basic understanding of:

* Windows operating system administration
* Windows Event Viewer
* Windows users and groups
* Windows services
* File system permissions
* PowerShell
* Basic Windows networking

### Security Knowledge

Basic understanding of:

* Security monitoring
* Authentication events
* Security logs
* Processes
* Network connections
* Indicators of compromise
* Alert triage
* Incident investigation

### Tools and Components

Depending on the scenario, the lab may require:

* Windows Event Viewer
* PowerShell
* Sysmon
* Wazuh Agent
* Wazuh Manager / Server
* Wazuh Dashboard
* VMware networking

Only free or open-source tools and the existing home-lab environment should be used.

## Pre-Lab Verification

Before beginning practical exercises, verify:

```text
[ ] Windows VM starts successfully
[ ] Windows Event Viewer is accessible
[ ] Security logging is enabled
[ ] PowerShell is available
[ ] Required telemetry sources are configured
[ ] Sysmon is installed, if required
[ ] Wazuh Agent is installed, if required
[ ] Windows endpoint can communicate with Wazuh
[ ] Wazuh receives Windows events
[ ] Lab network is isolated and controlled
[ ] Evidence collection is ready
```

## Evidence Requirements

Evidence should demonstrate the practical completion of the lab.

Examples include:

* Windows Event Viewer screenshots
* Relevant Event ID screenshots
* Security event records
* Process monitoring results
* PowerShell monitoring results
* Detection alerts
* Investigation timelines
* Verification results

Evidence should be stored in the lab's `Evidence/` directory.

## Expected Professional Skills

This lab is designed to demonstrate entry-level SOC capabilities relevant to:

* Security Monitoring
* Alert Triage
* Windows Event Analysis
* Endpoint Monitoring
* Threat Detection
* Incident Investigation
* Incident Response
* Security Documentation

## Final Objective

The final objective is to demonstrate the complete ability to monitor and investigate Windows endpoint activity through a practical SOC workflow:

**Generate → Collect → Detect → Analyze → Investigate → Respond → Verify → Document**
