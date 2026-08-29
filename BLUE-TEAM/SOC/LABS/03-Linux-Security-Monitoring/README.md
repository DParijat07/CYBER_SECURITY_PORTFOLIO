# Linux Security Monitoring Lab

## 1. Overview

This laboratory focuses on monitoring Linux systems from a Security Operations Center (SOC) perspective.

The objective is to understand Linux security telemetry, identify important Linux logs, monitor authentication and system activity, collect telemetry into a SIEM, investigate suspicious events, and perform basic SOC alert triage.

The lab uses an authorized Linux virtual machine and integrates Linux telemetry with the SOC monitoring environment.

---

## 2. Objectives

The main objectives of this lab are:

- Understand Linux security monitoring.
- Identify important Linux log sources.
- Understand Linux authentication logs.
- Monitor user activity.
- Monitor privilege-related activity.
- Monitor process activity.
- Monitor service activity.
- Monitor system activity.
- Monitor network-related activity.
- Collect Linux telemetry using Wazuh.
- Generate controlled security events.
- Investigate Linux security events.
- Perform basic SOC alert triage.
- Correlate multiple events.
- Build an investigation timeline.
- Document evidence and findings.

---

## 3. SOC Skills Demonstrated

This laboratory demonstrates:

- Linux security monitoring
- Linux log analysis
- Authentication monitoring
- User activity monitoring
- Privilege monitoring
- Process monitoring
- Service monitoring
- Network monitoring
- SIEM monitoring
- Alert triage
- Event correlation
- Basic threat investigation
- Evidence collection
- Security documentation

---

## 4. Lab Scenario

A SOC analyst is responsible for monitoring Linux servers within an organization.

The analyst needs visibility into:

- User authentication
- Failed authentication
- Successful authentication
- Privilege escalation
- User account activity
- Process execution
- Service activity
- System events
- Network activity
- Administrative activity

The laboratory simulates these activities on an authorized Linux virtual machine.

---

## 5. Lab Architecture

The laboratory uses the following general architecture:

Windows 11 Host
│
├── VMware
│   ├── Ubuntu Server
│   │   └── Wazuh Server
│   │
│   ├── Linux Endpoint
│   │   └── Wazuh Agent
│   │
│   ├── Kali Linux
│   │
│   ├── Windows 7
│   │
│   └── Metasploitable 2
│
└── Analyst Workstation

Linux Endpoint
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

### 6.1 Linux Endpoint

The Linux virtual machine acts as the monitored endpoint.

Depending on the Linux distribution and configuration, relevant telemetry may include:

- Authentication logs
- System logs
- Service logs
- Kernel logs
- Application logs
- Audit logs
- Process information
- Network information

### 6.2 Wazuh Agent

The Wazuh agent collects relevant Linux telemetry and forwards it to the Wazuh infrastructure.

### 6.3 Wazuh Server

The Wazuh server receives, processes, analyzes, and presents security events and alerts.

### 6.4 Analyst Workstation

The analyst workstation is used to:

- Generate controlled activity
- Review logs
- Review alerts
- Investigate events
- Collect evidence
- Document findings

---

## 7. Tools and Technologies

### Primary Tools

- Linux
- Wazuh
- VMware
- Ubuntu Server

### Supporting Tools

- Linux terminal
- journalctl
- systemctl
- ps
- ss
- who
- last
- lastb
- grep
- awk
- sed
- Git
- GitHub
- Markdown

---

## 8. Prerequisites

Before starting this laboratory, ensure that:

- A Linux virtual machine is available.
- Wazuh server is operational.
- Wazuh agent is installed.
- Linux endpoint is connected to Wazuh.
- Network connectivity is working.
- Administrative access is available for the laboratory.
- System time is synchronized.
- Relevant Linux logging services are enabled.

All activities must be performed on systems that are owned or explicitly authorized for testing.

---

## 9. Linux Logging Fundamentals

Linux systems generate logs for different types of activity.

Depending on the distribution, important locations and services may include:

- `/var/log/auth.log`
- `/var/log/secure`
- `/var/log/syslog`
- `/var/log/messages`
- `/var/log/kern.log`
- `/var/log/audit/`
- systemd journal

The exact log location depends on the Linux distribution and configuration.

---

## 10. Authentication Monitoring

Authentication monitoring is one of the most important Linux SOC activities.

Monitor:

- Successful logins
- Failed logins
- SSH authentication
- Usernames
- Source IP addresses
- Authentication timestamps
- Privileged authentication
- Session activity

Questions for the analyst:

- Who authenticated?
- When?
- From where?
- Was authentication successful?
- Was the activity expected?
- Were there repeated failures?
- Did a successful authentication follow multiple failures?

---

## 11. SSH Monitoring

SSH is commonly used for remote administration of Linux systems.

Security monitoring should consider:

- Successful SSH authentication
- Failed SSH authentication
- Source IP
- Destination host
- Username
- Authentication method
- Time
- Frequency of attempts

Repeated failed authentication attempts may require investigation depending on context.

---

## 12. Failed Authentication Monitoring

Failed authentication events may occur because of:

- Incorrect credentials
- User mistakes
- Expired credentials
- Misconfigured applications
- Automated services
- Password spraying
- Brute-force activity

A single failed login should not automatically be classified as malicious.

Analyze:

- Number of attempts
- Time interval
- Source address
- Target accounts
- Authentication method
- Related successful logins
- Other endpoint activity

---

## 13. Successful Authentication Monitoring

Successful authentication events should also be monitored.

Investigate unusual successful authentication such as:

- Unexpected source
- Unusual time
- Unexpected account
- Privileged account login
- Login following repeated authentication failures

Always consider normal administrative activity before classifying the event as malicious.

---

## 14. User Activity Monitoring

Linux systems should be monitored for important user activity.

Useful commands include:

- `who`
- `w`
- `last`
- `lastb`
- `id`
- `users`

These commands can help identify:

- Current sessions
- Logged-in users
- Previous sessions
- Failed login history
- User identity

Use the commands only within the authorized laboratory environment.

---

## 15. Privilege Monitoring

Linux privilege escalation and administrative activity are important SOC concerns.

Monitor:

- `sudo` activity
- Root sessions
- Privileged commands
- Changes to privileged users
- Changes to sudo configuration
- Administrative authentication

Questions:

- Which user performed the action?
- What privilege was obtained?
- What command was executed?
- Was the action authorized?
- What happened afterward?

---

## 16. Sudo Monitoring

The `sudo` mechanism allows authorized users to execute commands with elevated privileges.

Security monitoring should record:

- User
- Timestamp
- Command
- Target privilege
- Result
- Related activity

Unexpected sudo activity should be investigated in context.

---

## 17. Process Monitoring

Process activity can provide valuable endpoint visibility.

Monitor:

- Process name
- Process ID
- Parent process
- User
- Command line
- Process path
- Start time where available

Useful command:

`ps aux`

Additional process information may be obtained through:

- `ps`
- `top`
- `htop`
- `/proc`

Process information should be correlated with other security telemetry.

---

## 18. Network Monitoring

Linux network activity may be investigated using tools such as:

- `ss`
- `ip`
- `netstat` where available
- Wazuh telemetry
- Network monitoring tools

Monitor:

- Listening ports
- Active connections
- Source addresses
- Destination addresses
- Connection state
- Associated processes where available

Unexpected network connections should be investigated.

---

## 19. Service Monitoring

Linux services can be monitored using systemd and related tools.

Useful commands include:

- `systemctl status`
- `systemctl list-units`
- `systemctl list-unit-files`

Monitor:

- Service creation
- Service startup
- Service shutdown
- Service failures
- Configuration changes
- Unexpected services

Investigate services that are:

- Unknown
- Newly introduced
- Running unexpectedly
- Associated with unusual processes

---

## 20. System Monitoring

Important system events may include:

- System startup
- System shutdown
- Service failures
- Kernel events
- Configuration changes
- Resource-related events
- Hardware-related events

These events can provide context during incident investigations.

---

## 21. Journalctl

On systemd-based Linux distributions, `journalctl` can be used to review system logs.

Examples:

`journalctl`

`journalctl -b`

`journalctl -u ssh`

`journalctl --since "1 hour ago"`

Use appropriate commands to investigate the laboratory system.

The exact available options depend on the Linux distribution and systemd configuration.

---

## 22. Authentication Log Analysis

Review the authentication log appropriate to the Linux distribution.

For example:

`/var/log/auth.log`

or:

`/var/log/secure`

Look for:

- Authentication failures
- Successful authentication
- SSH activity
- sudo activity
- Account changes
- Session activity

---

## 23. Wazuh Linux Monitoring

After the Linux endpoint is connected to Wazuh:

1. Generate a controlled Linux event.
2. Confirm the event is recorded locally.
3. Confirm the Wazuh agent receives the telemetry.
4. Review the Wazuh dashboard.
5. Identify the Linux endpoint.
6. Locate the corresponding event or alert.
7. Review the event details.
8. Compare the Wazuh event with the original Linux log.
9. Document the result.

This validates the complete telemetry pipeline.

---

## 24. Controlled Failed SSH Login Exercise

### Objective

Generate controlled failed SSH authentication attempts and observe the resulting Linux telemetry.

### Procedure

1. Use the authorized Linux laboratory environment.
2. Attempt authentication using an intentionally incorrect test credential.
3. Review the relevant authentication log.
4. Identify the timestamp.
5. Identify the username.
6. Identify the source information.
7. Review the event in Wazuh.
8. Compare the local log with the SIEM event.
9. Document the findings.

### Expected Learning

The analyst should understand:

- How failed SSH authentication appears.
- Which log contains the event.
- How the event reaches Wazuh.
- What information is useful during triage.

---

## 25. Controlled Successful SSH Login Exercise

### Objective

Observe a normal successful SSH authentication event.

### Procedure

1. Authenticate using an authorized laboratory account.
2. Review the authentication log.
3. Identify the corresponding event.
4. Record the timestamp.
5. Identify the user.
6. Identify the source.
7. Review the event in Wazuh.
8. Compare the local event with the SIEM event.

### Expected Learning

The analyst should understand normal SSH authentication telemetry.

---

## 26. Sudo Investigation Exercise

### Objective

Observe authorized privilege-related activity.

### Procedure

1. Use an authorized test account.
2. Execute a permitted command through `sudo`.
3. Review the authentication log or system journal.
4. Identify the user.
5. Identify the command.
6. Record the timestamp.
7. Locate related Wazuh telemetry.
8. Document the event.

### Expected Learning

The analyst should understand how administrative activity can appear in Linux telemetry.

---

## 27. Process Investigation Exercise

### Objective

Understand Linux process telemetry.

### Procedure

1. Start a benign process.
2. Identify the process using `ps`.
3. Record the process name.
4. Record the PID.
5. Identify the user.
6. Review related telemetry where available.
7. Document the observation.

---

## 28. Service Investigation Exercise

### Objective

Understand Linux service monitoring.

### Procedure

1. Select an authorized test service.
2. Review its status.
3. Start or stop the service as appropriate for the laboratory.
4. Review system logs.
5. Check Wazuh telemetry.
6. Record the event.
7. Document the result.

Do not modify production or unauthorized systems.

---

## 29. Network Connection Investigation

### Objective

Understand active network connections from a Linux endpoint.

### Procedure

1. Review active connections using an appropriate command such as `ss`.
2. Identify listening services.
3. Identify established connections.
4. Record relevant addresses and ports.
5. Identify the associated process where possible.
6. Correlate with other telemetry.
7. Document the result.

---

## 30. Wazuh Alert Investigation

For a selected Linux alert, record:

Alert:
Timestamp:
Hostname:
Agent:
Rule ID:
Rule Description:
Severity:
Username:
Source:
Destination:
Process:
Event:
Initial Assessment:

Then investigate related events.

---

## 31. Alert Triage

Use the following process:

**Alert**

↓

**Identify Host**

↓

**Identify User**

↓

**Identify Event**

↓

**Review Timestamp**

↓

**Review Source**

↓

**Review Related Events**

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

## 32. Event Correlation

A single Linux event may not provide enough information.

Correlate:

- Authentication events
- SSH events
- sudo events
- Process events
- Service events
- Network events
- System events
- User activity

Example:

Repeated SSH Failures
↓
Successful SSH Login
↓
Sudo Activity
↓
New Process
↓
Network Connection

A sequence of related events may provide stronger investigative context.

---

## 33. Investigation Timeline

Create a timeline for selected investigations.

Recommended format:

| Time | Source | User | Event | Activity | Observation |
|------|--------|------|-------|----------|-------------|
| T1 | SSH Log | User | Failed Auth | Authentication failure | Initial activity |
| T2 | SSH Log | User | Failed Auth | Repeated failure | Pattern observed |
| T3 | SSH Log | User | Successful Auth | Authentication succeeded | Access established |
| T4 | Auth Log | User | sudo | Privileged command | Follow-up activity |
| T5 | Process | User | Process | Process execution | Investigation |
| T6 | Network | User | Connection | Network activity | Correlation |

Use actual laboratory timestamps.

---

## 34. Evidence Collection

Evidence may include:

- Linux log screenshots
- Wazuh alerts
- Wazuh event details
- Authentication logs
- System journal output
- Process information
- Network connection information
- Investigation timeline
- Analyst notes

Recommended structure:

evidence/
├── screenshots/
├── alerts/
└── logs/

---

## 35. Screenshot Documentation

Useful screenshots include:

- Linux authentication log
- Wazuh alert
- Wazuh event details
- Terminal investigation
- Process information
- Network connections
- Service status

Screenshots should contain only relevant information.

---

## 36. False Positive Analysis

Linux events can have legitimate explanations.

Examples include:

- Incorrect password
- Automated service authentication
- System administration
- Scheduled tasks
- Software updates
- Monitoring systems
- Backup systems
- Configuration management

The analyst should explain why the event was considered benign or suspicious.

---

## 37. MITRE ATT&CK Mapping

Where appropriate, map observed behaviors to relevant MITRE ATT&CK techniques.

Recommended format:

| Behavior | Technique | Evidence |
|----------|-----------|----------|
| Observed behavior | Relevant ATT&CK technique | Supporting evidence |

Only map techniques that are supported by the investigation evidence.

---

## 38. Investigation Questions

For important Linux security events, ask:

1. What happened?
2. When did it happen?
3. Which Linux host was affected?
4. Which user was involved?
5. What was the source?
6. Was authentication successful?
7. Was privilege escalation involved?
8. What process executed?
9. What network activity occurred?
10. Was the activity expected?
11. Are there related events?
12. Is there evidence of compromise?
13. What should the analyst do next?

---

## 39. Recommended Response

### Benign Event

- Document the event.
- Close the alert where appropriate.
- Consider detection tuning.

### Suspicious Event

- Continue investigation.
- Search for related activity.
- Collect additional telemetry.
- Consider escalation.

### Confirmed Incident

- Escalate according to the incident-response process.
- Preserve evidence.
- Contain the affected system where appropriate.
- Investigate scope.
- Document the incident.

---

## 40. Lessons Learned

Document:

- Which Linux logs were most useful?
- Which commands were useful during investigation?
- Was Wazuh receiving the expected telemetry?
- Which events generated alerts?
- Which events required manual analysis?
- What visibility gaps were discovered?
- What detection improvements are required?

---

## 41. Recommended Lab Directory

03-Linux-Security-Monitoring/
├── README.md
├── screenshots/
├── evidence/
├── logs/
├── queries/
└── scripts/

Only create directories that are required by the actual laboratory.

---

## 42. Lab Deliverables

The completed laboratory should contain:

- Working Linux monitoring
- Connected Wazuh agent
- Verified Linux telemetry
- Authentication log analysis
- Failed authentication investigation
- Successful authentication investigation
- Privilege activity analysis
- Process monitoring
- Service monitoring
- Network monitoring
- Wazuh alert investigation
- Alert triage
- Event correlation
- Investigation timeline
- Evidence screenshots
- Analyst notes
- Lessons learned

---

## 43. Completion Checklist

- [ ] Linux endpoint prepared.
- [ ] Wazuh agent installed.
- [ ] Wazuh agent connected.
- [ ] Linux telemetry received.
- [ ] Authentication logs reviewed.
- [ ] System logs reviewed.
- [ ] Journal logs reviewed where applicable.
- [ ] Failed authentication event generated.
- [ ] Successful authentication event generated.
- [ ] SSH activity analyzed.
- [ ] sudo activity observed.
- [ ] Process activity analyzed.
- [ ] Service activity analyzed.
- [ ] Network activity reviewed.
- [ ] Wazuh alert reviewed.
- [ ] Alert triaged.
- [ ] Related events correlated.
- [ ] Investigation timeline created.
- [ ] Evidence collected.
- [ ] False-positive considerations documented.
- [ ] MITRE ATT&CK mapping completed where applicable.
- [ ] Lessons learned documented.
- [ ] Sensitive information removed.
- [ ] GitHub documentation updated.

---

## 44. Skills Demonstrated

After completing this laboratory, the following practical capabilities should be demonstrated:

- Linux endpoint monitoring
- Linux log analysis
- Authentication monitoring
- SSH monitoring
- Privilege activity monitoring
- Process monitoring
- Service monitoring
- Network monitoring
- SIEM monitoring
- Wazuh alert analysis
- Event correlation
- Basic incident triage
- Investigation timeline creation
- Evidence collection
- Security documentation

---

## 45. Portfolio Value

This laboratory provides practical evidence that the analyst can monitor and investigate Linux security telemetry.

The progression demonstrated is:

**Linux Event → Log Collection → SIEM → Alert → Triage → Investigation → Evidence → Documentation**

This laboratory also provides a foundation for more advanced:

- Threat Hunting
- Detection Engineering
- Incident Response
- Digital Forensics
- Vulnerability Management
- SOC Automation

projects.

---

## 46. Future Expansion

This laboratory can later be expanded with:

- Linux auditd
- Advanced SSH monitoring
- File Integrity Monitoring
- Process anomaly detection
- Privilege escalation detection
- Persistence detection
- Network anomaly detection
- Threat hunting
- Detection engineering
- Incident response
- Digital forensics
- AI-assisted Linux log analysis

---

## 47. Disclaimer

All activities documented in this laboratory are performed in authorized and controlled environments for educational, defensive, and portfolio-development purposes.

No unauthorized systems, networks, accounts, applications, or infrastructure should be targeted.

---

## 48. Status

**Status:** In Progress

This laboratory will be updated as Linux monitoring, Wazuh integration, endpoint telemetry analysis, alert investigation, threat hunting, and SOC investigation capabilities are developed.
