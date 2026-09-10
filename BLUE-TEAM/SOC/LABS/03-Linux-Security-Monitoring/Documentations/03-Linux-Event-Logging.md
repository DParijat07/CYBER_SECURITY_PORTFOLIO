# Linux Event Logging

## 1. Purpose

This document explains the basic Linux event and logging mechanisms used in the **Linux Security Monitoring Lab**.

The objective is to understand:

* What a Linux security event is
* How Linux generates and records events
* The difference between an event and a log
* Where important Linux security logs are stored
* How to inspect Linux logs manually
* How authentication, privilege, process, and system activity appear in logs
* Why Linux logs are important for SOC monitoring
* How local logging connects to centralized monitoring with Wazuh

This document focuses on understanding the **Linux logging layer** before moving to centralized log collection and detection.

---

## 2. Linux Event vs Linux Log

### 2.1 What Is a Linux Event?

A Linux event is an activity or occurrence that happens on a Linux system.

Examples:

* A user logs in
* A user enters an incorrect password
* A user executes a `sudo` command
* A new user account is created
* A process starts
* A process stops
* A service starts or stops
* A configuration file is modified
* An SSH connection is established
* A system error occurs

A security event does not automatically mean that an attack occurred.

For example:

```text
User logs in successfully
```

This is a normal event.

However:

```text
Multiple failed SSH login attempts from the same source IP
```

may indicate suspicious activity.

---

### 2.2 What Is a Linux Log?

A log is a recorded representation of an event.

For example, a Linux system may record an SSH authentication event similar to:

```text
Failed password for testuser from 192.168.56.20
```

The actual format can vary depending on the service, configuration, and logging system.

The important idea is:

```text
Activity
   ↓
Event
   ↓
Logging System
   ↓
Log Record
```

---

## 3. Why Linux Event Logging Matters in a SOC

A SOC analyst needs evidence to understand what happened on an endpoint.

Without logs, it becomes difficult to answer questions such as:

* Who attempted to log in?
* Was the login successful?
* When did the activity occur?
* Which service generated the event?
* Which user executed a privileged command?
* What process was running?
* Was there a sequence of suspicious events?
* What happened before and after an alert?

Linux logs provide the raw security telemetry required for:

```text
Event
  ↓
Log
  ↓
Collection
  ↓
Detection
  ↓
Alert
  ↓
Investigation
  ↓
Response
```

This lab begins at the **Event → Log** stage.

---

# 4. Linux Logging Architecture

At a beginner level, Linux security logging can be understood as:

```text
User / Application / Service / System Activity
                    ↓
              Event Generated
                    ↓
        Linux Logging Mechanisms
          ┌─────────┴─────────┐
          ↓                   ↓
      journald            syslog/rsyslog
          ↓                   ↓
      Journal             Log Files
                              ↓
                  /var/log/*.log
                              ↓
                    Security Monitoring
                              ↓
                       Wazuh Collection
```

Different Linux components may use different logging mechanisms.

The most important components for this lab are:

* `systemd-journald`
* `syslog` / `rsyslog`
* Authentication logs
* System logs
* `auditd` logs when auditd is installed and configured

---

# 5. systemd-journald

## 5.1 What Is journald?

`systemd-journald` is a logging service used by systems based on `systemd`.

Ubuntu 22.04 uses `systemd`.

It collects messages from different sources, including:

* System services
* Kernel messages
* Applications
* Authentication-related services
* Service startup and shutdown events

The main command used to view the journal is:

```bash
journalctl
```

---

## 5.2 View Recent Journal Entries

Run:

```bash
sudo journalctl -n 20
```

This displays the most recent 20 journal entries.

Example structure:

```text
DATE TIME HOST SERVICE[PID]: MESSAGE
```

The exact output depends on the system.

---

## 5.3 View Current Boot Logs

To view logs from the current system boot:

```bash
sudo journalctl -b
```

This is useful when investigating what happened after the system was started.

---

## 5.4 Follow New Events in Real Time

Run:

```bash
sudo journalctl -f
```

The command continues displaying new events as they are generated.

This is useful for observing events while performing controlled activities in the lab.

For example:

```text
Terminal 1:
sudo journalctl -f

Terminal 2:
Perform a controlled activity

Terminal 1:
Observe the new event
```

Press:

```text
Ctrl + C
```

to stop following the log.

---

## 5.5 View Recent Time-Based Events

For example:

```bash
sudo journalctl --since "10 minutes ago"
```

This helps limit the output to recent events.

This is particularly useful during lab exercises because it reduces the amount of unrelated log data.

---

# 6. Linux Log Files

Ubuntu commonly stores important logs under:

```text
/var/log/
```

Two important log files for this lab are:

```text
/var/log/auth.log
/var/log/syslog
```

---

# 7. Authentication Log

## 7.1 `/var/log/auth.log`

The authentication log contains security-related activity associated with authentication and privilege operations.

It can contain events related to:

* SSH authentication
* Login attempts
* Failed authentication
* Successful authentication
* `sudo` activity
* Authentication services

View the most recent entries:

```bash
sudo tail -n 20 /var/log/auth.log
```

---

## 7.2 Follow Authentication Events

Run:

```bash
sudo tail -f /var/log/auth.log
```

This displays new authentication-related log entries as they appear.

Stop the command with:

```text
Ctrl + C
```

---

## 7.3 Search for Failed SSH Authentication

A common search is:

```bash
sudo grep "Failed password" /var/log/auth.log
```

This can help identify failed SSH password authentication events.

Example pattern:

```text
Failed password for username from SOURCE_IP
```

The exact message may differ depending on the SSH configuration and authentication method.

---

## 7.4 Search for Successful SSH Authentication

Run:

```bash
sudo grep "Accepted" /var/log/auth.log
```

This can help locate successful SSH authentication events.

A typical pattern may contain:

```text
Accepted password for username from SOURCE_IP
```

Again, the exact message depends on the authentication method.

---

# 8. System Log

## 8.1 `/var/log/syslog`

The system log can contain messages generated by:

* System services
* Applications
* Background processes
* Networking components
* General system activity

View recent entries:

```bash
sudo tail -n 20 /var/log/syslog
```

---

## 8.2 Follow System Events

Run:

```bash
sudo tail -f /var/log/syslog
```

Then perform a controlled activity on the Ubuntu VM and observe whether new events appear.

Stop with:

```text
Ctrl + C
```

---

# 9. auditd and Audit Logs

Linux can also use the Linux Audit framework.

The audit system can provide detailed security-related records about activities such as:

* User activity
* Privilege usage
* System calls
* File access
* Process activity
* Security-relevant configuration changes

When `auditd` is installed and configured, audit logs are commonly stored at:

```text
/var/log/audit/audit.log
```

Check whether the audit service exists:

```bash
systemctl status auditd
```

If auditd is not installed or enabled, do not assume that this log file will exist.

For this beginner lab, the main focus is on understanding the logging concept rather than creating custom audit rules.

---

# 10. Important Linux Security Event Categories

The Linux Security Monitoring Lab focuses on several important event categories.

## 10.1 Authentication Events

Examples:

```text
Failed login
Successful login
SSH connection
Authentication failure
```

Security relevance:

```text
Repeated failures
        ↓
Possible brute-force activity
```

---

## 10.2 Privilege Events

Examples:

```text
sudo command
Privilege escalation attempt
Administrative command execution
```

A typical `sudo` log may contain information about:

* User
* Terminal
* Working directory
* Command executed

A useful search is:

```bash
sudo grep "sudo:" /var/log/auth.log
```

---

## 10.3 User and Account Events

Examples:

```text
New user created
User modified
User deleted
Group membership changed
```

These events are important because attackers may attempt to create or modify accounts for persistence.

---

## 10.4 Process Events

Examples:

```text
Process started
Process terminated
Suspicious command executed
```

Process activity may not always appear in the normal system logs with enough detail for security investigation.

Additional monitoring mechanisms may therefore be required later in the lab.

The important beginner concept is:

```text
Process Activity
       ↓
Security Telemetry
       ↓
Detection / Investigation
```

---

## 10.5 Service Events

Examples:

```text
SSH service started
Web service stopped
Unexpected service restart
```

Service activity can be useful during troubleshooting and incident investigation.

For example:

```bash
sudo journalctl -u ssh
```

can be used to inspect journal entries for the SSH service when that service is present on the system.

---

# 11. Common Linux Log Fields

A log entry may contain several useful pieces of information.

| Field             | Meaning                                 |
| ----------------- | --------------------------------------- |
| Timestamp         | When the event occurred                 |
| Hostname          | System that generated the event         |
| Service / Process | Component that generated the event      |
| PID               | Process ID, when available              |
| Username          | User associated with the activity       |
| Source IP         | Source address, when applicable         |
| Severity          | Importance of the event, when available |
| Message           | Description of the event                |

For example:

```text
Timestamp
    ↓
Hostname
    ↓
Service / Process
    ↓
User / Source
    ↓
Event Description
```

A SOC analyst uses these fields to reconstruct what happened.

---

# 12. Syslog Severity Levels

Syslog-based systems commonly use severity levels.

| Level         | Meaning                          |
| ------------- | -------------------------------- |
| Emergency     | System is unusable               |
| Alert         | Immediate action may be required |
| Critical      | Critical condition               |
| Error         | Error condition                  |
| Warning       | Warning condition                |
| Notice        | Significant normal condition     |
| Informational | General information              |
| Debug         | Detailed debugging information   |

Not every log file will display the severity level in the same way.

For beginner-level monitoring, the main goal is to understand that log messages can have different levels of importance.

---

# 13. Useful Beginner Commands

The following commands are useful during this lab.

### View recent journal entries

```bash
sudo journalctl -n 20
```

### View current boot logs

```bash
sudo journalctl -b
```

### Follow journal events

```bash
sudo journalctl -f
```

### View recent authentication logs

```bash
sudo tail -n 20 /var/log/auth.log
```

### Follow authentication logs

```bash
sudo tail -f /var/log/auth.log
```

### View recent system logs

```bash
sudo tail -n 20 /var/log/syslog
```

### Follow system logs

```bash
sudo tail -f /var/log/syslog
```

### Search failed SSH authentication

```bash
sudo grep "Failed password" /var/log/auth.log
```

### Search successful authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

### Search sudo activity

```bash
sudo grep "sudo:" /var/log/auth.log
```

### View recent events

```bash
sudo journalctl --since "10 minutes ago"
```

### View SSH-related journal events

```bash
sudo journalctl -u ssh --no-pager
```

The exact service name may differ depending on the installed SSH configuration.

---

# 14. Hands-On Logging Exercise

The following exercise should be performed only on the authorized Ubuntu VM used for this lab.

## Step 1 — Check Current Logs

Run:

```bash
sudo journalctl -n 20
```

Then:

```bash
sudo tail -n 20 /var/log/auth.log
```

Record what types of events you can see.

---

## Step 2 — Generate a Normal User Activity Event

Perform a normal activity such as:

```bash
whoami
```

or:

```bash
id
```

Then inspect the logs again.

The objective is to understand that not every command necessarily produces a useful authentication log entry.

---

## Step 3 — Generate a Controlled Failed SSH Attempt

From an authorized lab machine, attempt an SSH login to the Ubuntu VM using an intentionally incorrect password.

Example:

```text
Lab Machine
     ↓
SSH
     ↓
Ubuntu 22.04
     ↓
Incorrect Password
     ↓
Authentication Failure
     ↓
auth.log / journal
```

Then inspect:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Do not perform this against systems that you do not own or have permission to test.

---

## Step 4 — Generate a Successful Authentication Event

Perform a normal authorized SSH login to the Ubuntu VM.

Then check:

```bash
sudo grep "Accepted" /var/log/auth.log
```

Compare the successful and failed authentication events.

---

## Step 5 — Generate a Sudo Event

Run a harmless administrative command such as:

```bash
sudo whoami
```

Then inspect:

```bash
sudo grep "sudo:" /var/log/auth.log
```

Identify:

* Username
* Command
* Time
* Other available information

---

## Step 6 — Observe Events in Real Time

Open one terminal and run:

```bash
sudo journalctl -f
```

Then perform a normal activity in another terminal.

Observe whether new events appear.

This demonstrates real-time event monitoring.

---

# 15. Event Observation Worksheet

Record observations in the Evidence directory.

| Activity               | Expected Event         | Log Source       | Observed? |
| ---------------------- | ---------------------- | ---------------- | --------- |
| Normal system activity | System event           | journal/syslog   | ☐         |
| Failed SSH login       | Authentication failure | auth.log/journal | ☐         |
| Successful SSH login   | Authentication success | auth.log/journal | ☐         |
| Sudo command           | Privilege activity     | auth.log/journal | ☐         |
| Service activity       | Service event          | journal/syslog   | ☐         |

The exact event source may vary depending on the system configuration.

---

# 16. Event vs Collection vs Detection

These concepts must not be confused.

## Event

Something happened on the endpoint.

Example:

```text
SSH login failed
```

## Log

The event was recorded.

Example:

```text
auth.log contains a failed authentication entry
```

## Collection

The log data is transferred to the central monitoring system.

Example:

```text
Ubuntu
   ↓
Wazuh Agent
   ↓
Wazuh Server
```

## Detection

A security rule identifies potentially suspicious activity.

Example:

```text
Many failed SSH logins
        ↓
Detection Rule
        ↓
Security Alert
```

Therefore:

```text
Event
  ↓
Log
  ↓
Collection
  ↓
Detection
  ↓
Alert
```

Understanding this distinction is essential for SOC work.

---

# 17. Linux Logging and Wazuh

The Ubuntu endpoint generates local security telemetry.

The Wazuh Agent can later be configured to collect relevant Linux log sources and send the telemetry to the Wazuh server.

The overall architecture is:

```text
Ubuntu 22.04 LTS
        │
        ├── journald
        │
        ├── /var/log/auth.log
        │
        ├── /var/log/syslog
        │
        └── Other configured security logs
                │
                ↓
          Wazuh Agent
                │
                ↓
         Wazuh Server
                │
                ↓
        Detection / Alerts
                │
                ↓
          SOC Analysis
```

The next documentation stage will focus on configuring the security monitoring layer.

---

# 18. Evidence Requirements

Capture evidence showing that Linux events can be observed locally.

Recommended evidence:

### Evidence 01 — Journal Logs

Screenshot showing:

```bash
sudo journalctl -n 20
```

### Evidence 02 — Authentication Logs

Screenshot showing:

```bash
sudo tail -n 20 /var/log/auth.log
```

### Evidence 03 — Failed Authentication

Screenshot showing the controlled failed SSH authentication event.

### Evidence 04 — Successful Authentication

Screenshot showing the successful authentication event.

### Evidence 05 — Sudo Activity

Screenshot showing the controlled `sudo` event.

### Evidence 06 — Real-Time Monitoring

Screenshot showing:

```bash
sudo journalctl -f
```

with a new event appearing.

Do not capture or publish passwords, private keys, tokens, or other sensitive information.

---

# 19. Basic Troubleshooting

## Problem 1 — `/var/log/auth.log` Does Not Exist

Check:

```bash
ls -l /var/log/
```

Then check the journal:

```bash
sudo journalctl -n 50
```

Logging configuration can differ between systems.

---

## Problem 2 — No New Event Appears

Check the journal:

```bash
sudo journalctl --since "10 minutes ago"
```

Also verify that the relevant service is running.

For SSH:

```bash
systemctl status ssh
```

---

## Problem 3 — Permission Denied

Some logs require administrative privileges.

Use:

```bash
sudo
```

For example:

```bash
sudo tail -n 20 /var/log/auth.log
```

---

## Problem 4 — Too Many Log Entries

Limit the output:

```bash
sudo journalctl -n 20
```

or:

```bash
sudo journalctl --since "10 minutes ago"
```

This makes beginner-level analysis easier.

---

# 20. Security and Authorization

All event-generation activities in this lab must be performed only against:

* The user's own Ubuntu VM
* Other explicitly authorized lab systems
* The user's isolated home-lab network

The failed authentication exercise is intended only to demonstrate how a controlled security event appears in logs.

Do not perform password-guessing or unauthorized authentication attempts against external systems.

---

# 21. Validation Checklist

## Linux Logging Understanding

* [ ] I understand what a Linux event is.
* [ ] I understand what a Linux log is.
* [ ] I understand the difference between an event and a log.
* [ ] I understand why logs are important for a SOC.
* [ ] I understand the basic role of journald.
* [ ] I understand the purpose of `/var/log/`.
* [ ] I can identify `/var/log/auth.log`.
* [ ] I can identify `/var/log/syslog`.
* [ ] I understand that audit logs may exist when auditd is installed/configured.

## Practical Validation

* [ ] I viewed journal entries.
* [ ] I viewed authentication logs.
* [ ] I viewed system logs.
* [ ] I observed a controlled failed authentication event.
* [ ] I observed a successful authentication event.
* [ ] I observed a sudo event.
* [ ] I used real-time log monitoring.
* [ ] I recorded evidence.

## SOC Understanding

* [ ] I understand Event → Log.
* [ ] I understand Log → Collection.
* [ ] I understand Collection → Detection.
* [ ] I understand Detection → Alert.
* [ ] I understand why authentication logs are useful during investigations.

---

# 22. Success Criteria

This documentation stage is complete when the learner can:

1. Explain the difference between a Linux event and a Linux log.
2. Identify the major Linux logging mechanisms used in the lab.
3. Locate important Ubuntu authentication and system logs.
4. Use `journalctl` to inspect Linux events.
5. Use basic commands to inspect `/var/log/auth.log`.
6. Identify controlled failed and successful authentication events.
7. Identify a sudo-related event.
8. Explain how local Linux logs eventually become security telemetry for Wazuh.
9. Capture basic evidence of observed Linux events.

---

# 23. Learning Outcome

After completing this stage, the learner should understand the basic relationship between Linux activity and security telemetry:

```text
User / System Activity
          ↓
      Linux Event
          ↓
      Linux Log
          ↓
   Security Telemetry
          ↓
   Central Collection
          ↓
      Detection
          ↓
        Alert
          ↓
     Investigation
```

This provides the foundation for the next stage of the Linux Security Monitoring Lab.

---

# 24. Related Documentation

* `01-Lab-Objective.md`
* `02-Lab-Setup.md`
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
