# Sysmon Endpoint Monitoring Lab

## 1. Overview

This laboratory focuses on using Microsoft Sysmon (System Monitor) to generate detailed endpoint telemetry and integrating that telemetry into a Security Operations Center (SOC) monitoring workflow.

The objective is to understand how Sysmon records security-relevant endpoint activity, how analysts can investigate that telemetry, and how Sysmon data can improve detection, alert triage, threat hunting, and incident response.

This lab is performed in an authorized Windows virtual machine and is designed to complement the Windows Security Monitoring and Wazuh SIEM laboratories.

---

## 2. Objectives

The main objectives of this laboratory are:

- Understand Sysmon and its purpose.
- Install and configure Sysmon in an authorized Windows environment.
- Understand Sysmon event categories.
- Monitor process creation.
- Monitor network connections.
- Monitor file-related activity.
- Monitor process relationships.
- Monitor DNS activity where supported/configured.
- Monitor registry activity where supported/configured.
- Forward Sysmon telemetry to Wazuh.
- Investigate Sysmon events.
- Correlate Sysmon telemetry with Windows Security events.
- Perform basic SOC alert triage.
- Build investigation timelines.
- Identify detection opportunities.
- Document evidence and findings.

---

## 3. SOC Skills Demonstrated

This laboratory demonstrates:

- Endpoint telemetry collection
- Sysmon deployment
- Windows endpoint monitoring
- Process monitoring
- Parent-child process analysis
- Network connection monitoring
- DNS monitoring
- File activity monitoring
- Registry activity monitoring
- SIEM integration
- Alert investigation
- Event correlation
- Detection analysis
- Threat hunting fundamentals
- Evidence collection
- Security documentation

---

## 4. Lab Scenario

A SOC analyst needs deeper visibility into Windows endpoint activity than the default Windows Security logs provide.

The organization deploys Sysmon to collect detailed endpoint telemetry.

The analyst uses Sysmon data to investigate:

- Process execution
- Parent-child process relationships
- Network connections
- DNS activity
- File creation
- Registry activity
- Suspicious execution chains

The telemetry is forwarded to the SIEM for centralized analysis.

---

## 5. Lab Architecture

The laboratory uses the following general architecture:

Windows 11 Host
│
└── VMware
    │
    ├── Windows Endpoint
    │   ├── Sysmon
    │   └── Wazuh Agent
    │
    ├── Ubuntu Server
    │   └── Wazuh Server
    │
    ├── Kali Linux
    │
    └── Metasploitable 2

Windows Endpoint
↓
Sysmon
↓
Windows Event Log
↓
Wazuh Agent
↓
Wazuh Server
↓
Wazuh Dashboard
↓
SOC Analyst

---

## 6. Lab Components

### 6.1 Windows Endpoint

The Windows virtual machine is the monitored endpoint.

Sysmon is installed on this system to generate detailed telemetry.

### 6.2 Sysmon

Sysmon is a Windows system service and device driver that records detailed information about system activity.

Depending on configuration and Sysmon version, useful telemetry can include:

- Process creation
- Process termination
- Network connections
- File creation
- Registry activity
- DNS queries
- Driver activity
- Process access
- Image loading

### 6.3 Wazuh Agent

The Wazuh agent collects selected Windows event telemetry and forwards it to the Wazuh server.

### 6.4 Wazuh Server

The Wazuh server processes and analyzes the telemetry.

### 6.5 Analyst Workstation

The analyst uses the environment to:

- Generate controlled activity
- Review Sysmon logs
- Investigate Wazuh events
- Correlate telemetry
- Document findings

---

## 7. Tools and Technologies

### Primary Tools

- Sysmon
- Wazuh
- Windows
- VMware
- Ubuntu Server

### Supporting Tools

- Windows Event Viewer
- PowerShell
- Command Prompt
- Git
- GitHub
- Markdown

---

## 8. Prerequisites

Before starting this laboratory, ensure that:

- An authorized Windows virtual machine is available.
- Wazuh server is operational.
- Wazuh agent is installed.
- Windows endpoint is connected to Wazuh.
- Administrative privileges are available.
- Network connectivity is working.
- System time is synchronized.
- Windows Event Logging is operational.

All activities must be performed on systems that are owned or explicitly authorized for testing.

---

## 9. Sysmon Installation

Sysmon should be installed only on the authorized laboratory Windows endpoint.

General deployment process:

1. Obtain Sysmon from the official Microsoft Sysinternals distribution.
2. Transfer it to the authorized Windows laboratory machine.
3. Review the configuration before deployment.
4. Install Sysmon.
5. Confirm the Sysmon service is running.
6. Verify that Sysmon events are being generated.
7. Confirm the events appear in Windows Event Viewer.
8. Configure Wazuh to collect the required Sysmon events.

The configuration should be appropriate for the purpose of the laboratory.

---

## 10. Sysmon Event Log Location

Sysmon events are generally available under:

Applications and Services Logs
→ Microsoft
→ Windows
→ Sysmon
→ Operational

The exact location may vary depending on the Windows version and Sysmon configuration.

---

## 11. Important Sysmon Event IDs

Common Sysmon event IDs include:

| Event ID | General Activity |
|----------|------------------|
| 1 | Process creation |
| 2 | File creation time changed |
| 3 | Network connection |
| 5 | Process terminated |
| 6 | Driver loaded |
| 7 | Image loaded |
| 8 | CreateRemoteThread |
| 9 | Raw access read |
| 10 | Process access |
| 11 | File created |
| 12 | Registry object added/deleted |
| 13 | Registry value set |
| 14 | Registry object renamed |
| 15 | File stream created |
| 17 | Named pipe created |
| 18 | Named pipe connected |
| 19 | WMI event filter |
| 20 | WMI event consumer |
| 21 | WMI consumer-to-filter binding |
| 22 | DNS query |
| 23 | File deletion |
| 24 | Clipboard change |
| 25 | Process tampering |
| 26 | File deletion logged |

Availability and behavior may depend on the Sysmon version and configuration.

Event IDs should be interpreted in context.

---

## 12. Process Creation Monitoring

Sysmon Event ID 1 provides detailed process-creation telemetry.

Useful fields may include:

- Process ID
- Image
- Command line
- Parent process
- Parent image
- Parent command line
- User
- Integrity level
- Hashes
- Timestamp

This information is highly useful for endpoint investigations.

---

## 13. Parent-Child Process Analysis

Parent-child relationships can help analysts understand process execution chains.

Example:

explorer.exe
↓
powershell.exe
↓
child_process.exe

The analyst should investigate whether the process relationship is expected.

Important questions:

- Which process launched the child?
- Which user initiated it?
- What command line was used?
- Was the parent process expected?
- What happened afterward?

---

## 14. Network Connection Monitoring

Sysmon Event ID 3 can provide network connection telemetry when network monitoring is enabled.

Useful information may include:

- Source IP
- Source port
- Destination IP
- Destination port
- Protocol
- Process ID
- Process image
- User
- Timestamp

Network telemetry can be correlated with process execution.

---

## 15. DNS Monitoring

Sysmon Event ID 22 can provide DNS query telemetry when enabled.

Useful fields may include:

- Query name
- Query status
- Query results
- Process
- Process ID
- User
- Timestamp

DNS telemetry can provide useful context during investigations.

---

## 16. File Activity Monitoring

Sysmon can provide visibility into file-related activity depending on the enabled event types and configuration.

Examples include:

- File creation
- File deletion
- File timestamp modification
- Alternate data stream creation

File activity should be correlated with:

- Process activity
- User activity
- Network activity
- Authentication events

---

## 17. Registry Monitoring

Sysmon can monitor selected registry activity.

Potential events include:

- Registry key creation
- Registry key deletion
- Registry value modification
- Registry object renaming

Registry telemetry may be useful when investigating configuration changes or persistence-related behavior.

---

## 18. WMI Monitoring

Sysmon can provide telemetry related to Windows Management Instrumentation (WMI).

Relevant events may include:

- WMI event filter creation
- WMI event consumer creation
- Filter-to-consumer binding

These events should be investigated in context because WMI is widely used for legitimate administration and automation.

---

## 19. Process Termination Monitoring

Sysmon Event ID 5 can provide process termination information.

This may help analysts understand:

- How long a process executed
- Which process terminated
- Whether process termination was expected
- Whether termination occurred near other suspicious events

Process creation and termination can be correlated to understand process behavior.

---

## 20. File Creation Exercise

### Objective

Observe Sysmon telemetry for controlled file creation.

### Procedure

1. Use the authorized Windows endpoint.
2. Create a benign test file.
3. Open Windows Event Viewer.
4. Locate the relevant Sysmon event.
5. Identify the event ID.
6. Record the timestamp.
7. Identify the process responsible.
8. Review the corresponding Wazuh telemetry.
9. Document the result.

### Expected Learning

The analyst should understand how endpoint file activity can be observed through Sysmon.

---

## 21. Process Creation Exercise

### Objective

Observe Sysmon process-creation telemetry.

### Procedure

1. Open a benign Windows application.
2. Locate the process creation event.
3. Record the process name.
4. Record the parent process.
5. Review the command line.
6. Identify the user.
7. Review related Wazuh telemetry.
8. Document the event.

---

## 22. Network Connection Exercise

### Objective

Understand process-associated network telemetry.

### Procedure

1. Use a benign authorized application that creates network traffic.
2. Review Sysmon network connection events.
3. Identify the process.
4. Record destination information.
5. Record the timestamp.
6. Correlate with process creation.
7. Review the event in Wazuh.
8. Document the result.

---

## 23. DNS Query Exercise

### Objective

Observe DNS query telemetry.

### Procedure

1. Use an authorized browser or application.
2. Access a permitted domain.
3. Review Sysmon DNS events where enabled.
4. Identify the querying process.
5. Identify the domain.
6. Record the timestamp.
7. Review the event in Wazuh.
8. Document the result.

---

## 24. Registry Activity Exercise

### Objective

Understand registry-event telemetry.

### Procedure

1. Perform a controlled registry change within the laboratory.
2. Record what was changed.
3. Review Sysmon registry events.
4. Identify the process responsible.
5. Identify the user.
6. Record the timestamp.
7. Review corresponding SIEM telemetry.
8. Document the result.

Only make changes that are safe and reversible within the laboratory.

---

## 25. Sysmon and Windows Security Correlation

Sysmon telemetry becomes more useful when correlated with standard Windows Security events.

Example:

Windows Event 4624
↓
Sysmon Event 1
↓
Sysmon Event 3
↓
Sysmon Event 22

Possible interpretation:

Successful authentication
↓
Process execution
↓
Network connection
↓
DNS query

The sequence should be investigated rather than automatically classified as malicious.

---

## 26. Wazuh Sysmon Integration

After Sysmon is operational:

1. Confirm Sysmon events are generated.
2. Confirm events appear in Windows Event Viewer.
3. Configure the Wazuh agent to collect the required event channel.
4. Restart or reload the required Wazuh agent configuration.
5. Generate controlled endpoint activity.
6. Open the Wazuh dashboard.
7. Search for the relevant Sysmon events.
8. Confirm event fields are available.
9. Compare the SIEM event with the original Sysmon event.
10. Document the telemetry pipeline.

---

## 27. Alert Triage

Use the following process:

**Sysmon Alert/Event**

↓

**Identify Endpoint**

↓

**Identify User**

↓

**Identify Process**

↓

**Review Parent Process**

↓

**Review Command Line**

↓

**Review Network/DNS Activity**

↓

**Correlate Windows Events**

↓

**Determine Context**

↓

**Classify**

Possible classifications:

- Benign
- Suspicious
- Potential Incident
- Confirmed Incident
- Inconclusive

---

## 28. Process Investigation

For an interesting Sysmon process event, record:

Process:
PID:
Parent Process:
Parent PID:
User:
Command Line:
Image Path:
Timestamp:
Hash:
Network Activity:
DNS Activity:
Related Events:
Initial Assessment:

---

## 29. Network Investigation

For an interesting Sysmon network event, record:

Process:
PID:
Source IP:
Source Port:
Destination IP:
Destination Port:
Protocol:
Timestamp:
User:
Related DNS:
Related Process Event:
Initial Assessment:

---

## 30. Event Correlation

Correlate multiple telemetry sources.

Potential sources include:

- Sysmon
- Windows Security
- Windows System
- PowerShell
- Wazuh
- Network telemetry

Example:

Authentication
↓
Process Creation
↓
DNS Query
↓
Network Connection
↓
Additional Process Activity

This provides greater investigative context than a single event.

---

## 31. Investigation Timeline

Create a timeline for selected investigations.

Recommended format:

| Time | Source | Event ID | Process/User | Activity | Observation |
|------|--------|----------|--------------|----------|-------------|
| T1 | Security | 4624 | User | Successful Logon | Access established |
| T2 | Sysmon | 1 | User | Process Created | New process |
| T3 | Sysmon | 22 | Process | DNS Query | Domain lookup |
| T4 | Sysmon | 3 | Process | Network Connection | Outbound connection |
| T5 | Analyst | — | — | Investigation | Correlation |

Use actual laboratory timestamps.

---

## 32. Detection Opportunities

Sysmon provides useful telemetry for detection engineering.

Potential detection ideas include:

- Unusual parent-child process relationships
- Suspicious command-line activity
- Unexpected administrative process execution
- Rare network connections
- Unusual DNS activity
- Unexpected registry modifications
- Suspicious file activity
- Abnormal process execution chains

Detections should be based on documented behavior and tested before deployment.

---

## 33. False Positive Analysis

Sysmon generates telemetry for both legitimate and suspicious activities.

Potential legitimate sources include:

- Windows components
- Software updates
- Browsers
- Administrative tools
- Security software
- IT automation
- Backup software
- Monitoring tools

The analyst should understand normal activity before creating detection rules.

---

## 34. Detection Tuning

When an alert generates excessive false positives:

1. Identify the source of the noise.
2. Determine the legitimate behavior.
3. Identify reliable filtering conditions.
4. Modify the detection logic.
5. Test the updated logic.
6. Validate that useful detections still trigger.
7. Document the tuning decision.

---

## 35. Threat Hunting with Sysmon

Sysmon telemetry can support proactive threat hunting.

Example hunting questions:

- Which processes spawned PowerShell?
- Which processes made unusual network connections?
- Which applications generated unusual DNS requests?
- Which users launched administrative tools?
- Which processes executed from unusual paths?
- Which processes have unusual parent-child relationships?

Each hunt should begin with a hypothesis.

---

## 36. MITRE ATT&CK Mapping

Where appropriate, map observed behaviors to MITRE ATT&CK techniques.

Recommended format:

| Observed Behavior | ATT&CK Technique | Evidence |
|--------------------|------------------|----------|
| Observed behavior | Relevant technique | Supporting Sysmon event |

Only map techniques supported by evidence.

---

## 37. Evidence Collection

Evidence may include:

- Sysmon screenshots
- Wazuh alerts
- Windows Event Viewer screenshots
- Event XML/details
- Process information
- Network information
- DNS information
- Investigation timeline
- Analyst notes

Recommended directory:

evidence/
├── screenshots/
├── alerts/
└── events/

---

## 38. Screenshot Documentation

Useful screenshots include:

- Sysmon Operational log
- Event ID 1 process creation
- Event ID 3 network connection
- Event ID 22 DNS query
- Wazuh event
- Process tree
- Investigation timeline

Screenshots should contain only relevant laboratory information.

---

## 39. Investigation Questions

For an important Sysmon event, ask:

1. What happened?
2. When did it happen?
3. Which endpoint generated the event?
4. Which user was involved?
5. Which process generated the event?
6. What was the parent process?
7. What command line was used?
8. Was network activity observed?
9. Was DNS activity observed?
10. Were there related Windows Security events?
11. Was the activity expected?
12. Are there indicators of compromise?
13. What should the analyst investigate next?

---

## 40. Recommended Response

### Benign Event

- Document the event.
- Close the alert where appropriate.
- Tune detection logic if necessary.

### Suspicious Event

- Continue investigation.
- Search for related activity.
- Collect additional telemetry.
- Consider escalation.

### Confirmed Incident

- Escalate according to the incident-response process.
- Preserve evidence.
- Contain the affected endpoint where appropriate.
- Investigate scope.
- Document the incident.

---

## 41. Recommended Lab Directory

04-Sysmon-Endpoint-Monitoring/
├── README.md
├── screenshots/
├── evidence/
├── logs/
└── configs/

Only create directories that are required by the actual laboratory.

---

## 42. Lab Deliverables

The completed laboratory should contain:

- Sysmon installed
- Sysmon configuration documented
- Sysmon service verified
- Sysmon telemetry verified
- Process creation analysis
- Parent-child process analysis
- Network connection analysis
- DNS analysis
- File activity analysis
- Registry activity analysis
- Wazuh integration
- Sysmon alert investigation
- Windows Security event correlation
- Investigation timeline
- Evidence screenshots
- Analyst notes
- Detection opportunities
- Lessons learned

---

## 43. Completion Checklist

- [ ] Authorized Windows endpoint prepared.
- [ ] Sysmon installed.
- [ ] Sysmon service verified.
- [ ] Sysmon configuration reviewed.
- [ ] Sysmon events visible in Event Viewer.
- [ ] Wazuh agent operational.
- [ ] Sysmon telemetry forwarded to Wazuh.
- [ ] Process creation event analyzed.
- [ ] Parent-child relationship analyzed.
- [ ] Network connection event analyzed.
- [ ] DNS event analyzed where enabled.
- [ ] File activity analyzed.
- [ ] Registry activity analyzed.
- [ ] Windows Security event correlation completed.
- [ ] Wazuh event investigated.
- [ ] Alert triage completed.
- [ ] Investigation timeline created.
- [ ] Evidence collected.
- [ ] False-positive analysis documented.
- [ ] Detection opportunities documented.
- [ ] MITRE ATT&CK mapping completed where applicable.
- [ ] Lessons learned documented.
- [ ] Sensitive information removed.
- [ ] GitHub documentation updated.

---

## 44. Skills Demonstrated

After completing this laboratory, the following practical capabilities should be demonstrated:

- Sysmon deployment
- Sysmon configuration
- Windows endpoint monitoring
- Process monitoring
- Parent-child process analysis
- Network connection monitoring
- DNS monitoring
- File activity monitoring
- Registry monitoring
- Wazuh integration
- SIEM event investigation
- Windows event correlation
- Alert triage
- Threat hunting fundamentals
- Detection engineering fundamentals
- Evidence collection
- Security documentation

---

## 45. Portfolio Value

This laboratory demonstrates the ability to collect and investigate detailed Windows endpoint telemetry using Sysmon.

The progression demonstrated is:

**Endpoint Activity → Sysmon Telemetry → Windows Event Log → Wazuh → Alert/Event → Correlation → Investigation → Evidence → Documentation**

This provides a strong technical foundation for:

- SOC Monitoring
- Threat Hunting
- Detection Engineering
- Incident Response
- Digital Forensics
- Endpoint Security

projects.

---

## 46. Future Expansion

This laboratory can later be expanded with:

- Advanced Sysmon configuration
- Sigma detection rules
- Wazuh custom rules
- Process-tree analysis
- PowerShell detection
- Persistence detection
- Suspicious network connection detection
- DNS threat hunting
- Endpoint compromise investigation
- Automated alert enrichment
- SOC automation
- AI-assisted Sysmon investigation

---

## 47. Disclaimer

All activities documented in this laboratory are performed in authorized and controlled environments for educational, defensive, and portfolio-development purposes.

No unauthorized systems, networks, accounts, applications, or infrastructure should be targeted.

---

## 48. Status

**Status:** In Progress

This laboratory will be updated as Sysmon deployment, endpoint telemetry collection, Wazuh integration, event correlation, detection engineering, threat hunting, and SOC investigation capabilities are developed.
