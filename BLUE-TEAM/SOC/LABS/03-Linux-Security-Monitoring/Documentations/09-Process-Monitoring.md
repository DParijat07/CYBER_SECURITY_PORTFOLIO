# 09 — Process Monitoring

## 1. Purpose

Process monitoring is the process of observing programs and processes running on a Linux system.

In a SOC environment, process monitoring helps analysts understand:

* Which processes are running.
* Which user started a process.
* Which process is consuming system resources.
* Which command or program was executed.
* Whether a process is expected or suspicious.
* Whether a suspicious process is related to another security event.

In this lab, process monitoring is performed on the **Ubuntu 22.04 LTS Linux endpoint** using Linux process-monitoring commands and the **Wazuh Agent**.

---

## 2. Lab Environment

| Component             | Details                               |
| --------------------- | ------------------------------------- |
| Operating System      | Ubuntu 22.04 LTS                      |
| Architecture          | 64-bit x86_64                         |
| Virtualization        | VMware Workstation Player             |
| Endpoint Role         | Linux Security Monitoring Endpoint    |
| Security Agent        | Wazuh Agent                           |
| Central Platform      | Wazuh Manager, Indexer and Dashboard  |
| Primary Process Tools | `ps`, `top`, `htop`, `pgrep`, `pidof` |
| Main Monitoring Goal  | Process and command activity          |

### Process Monitoring Flow

```
User / System Activity
        |
        v
Process Created
        |
        v
Linux Process Table / Process Information
        |
        v
Wazuh Agent / Security Telemetry
        |
        v
Wazuh Manager
        |
        v
Detection
        |
        v
Alert
        |
        v
Wazuh Dashboard
        |
        v
SOC Analyst
        |
        v
Investigation and Response
```

---

## 3. What Is a Process?

A process is a running instance of a program.

For example, when a user runs:

```bash id="9ajh0s"
whoami
```

Linux creates or uses a process to execute the command.

Examples of processes running on Ubuntu include:

* `systemd`
* `sshd`
* `bash`
* `sudo`
* `cron`
* `rsyslog`
* Wazuh Agent processes
* User applications

Each running process normally has a unique **Process ID (PID)**.

---

## 4. What Is a PID?

PID stands for **Process ID**.

Linux assigns a numerical PID to a running process.

Example:

```
PID     COMMAND
1000    bash
1200    sshd
1500    wazuh-agent
```

The exact PID values will be different on every system.

A PID helps the analyst identify and investigate a specific running process.

---

## 5. Why Process Monitoring Matters in a SOC

Process monitoring can help identify activity such as:

* Unexpected programs.
* Unknown processes.
* Suspicious command execution.
* Programs running under unexpected users.
* Processes launched after a suspicious login.
* Unusual resource consumption.
* Unauthorized administrative activity.
* Suspicious parent-child process relationships.

Process information becomes more useful when correlated with other telemetry.

### Example

```
Successful SSH Login
        |
        v
User Session
        |
        v
New Process
        |
        v
Privileged Command
        |
        v
Security Investigation
```

The individual events may appear normal, but their relationship can provide useful investigation context.

---

## 6. Basic Linux Process Information

Linux provides several commands for viewing running processes.

The main beginner commands used in this lab are:

* `ps`
* `top`
* `htop`
* `pgrep`
* `pidof`
* `pstree`
* `kill`

These commands should be used carefully.

The purpose of this lab is primarily **observation and investigation**, not destructive process manipulation.

---

## 7. View Running Processes with `ps`

The `ps` command displays information about running processes.

Basic command:

```bash id="gk6y8h"
ps
```

A more useful view is:

```bash id="6r6qgb"
ps aux
```

This can display information such as:

* User.
* PID.
* CPU usage.
* Memory usage.
* Start information.
* Command.

Example structure:

```
USER       PID  %CPU  %MEM  COMMAND
root         1   ...   ...  /sbin/init
user      1200   ...   ...  bash
```

The actual values will depend on the Ubuntu VM.

---

## 8. Understanding Important `ps` Fields

When reviewing process information, focus on:

| Field   | Meaning                          |
| ------- | -------------------------------- |
| USER    | User associated with the process |
| PID     | Process ID                       |
| %CPU    | CPU usage                        |
| %MEM    | Memory usage                     |
| STAT    | Process state                    |
| START   | Process start information        |
| TIME    | CPU time used                    |
| COMMAND | Command or program               |

The `COMMAND` field is particularly useful during basic investigation.

---

## 9. Monitor Processes with `top`

The `top` command provides a real-time view of running processes.

Run:

```bash id="j23l0s"
top
```

Important information includes:

* CPU usage.
* Memory usage.
* Process IDs.
* Running users.
* Process names.
* System load.

Press:

```
q
```

to exit `top`.

Do not terminate processes from `top` unless the activity is specifically part of an authorized lab test.

---

## 10. Monitor Processes with `htop`

If `htop` is installed, it provides an easier-to-read process view.

Run:

```bash id="o8j1x3"
htop
```

If it is not installed, do not make installation a requirement for completing this lab.

The `ps` and `top` commands are sufficient for the basic process-monitoring exercises.

Press:

```
q
```

to exit `htop`.

---

## 11. Find a Process with `pgrep`

The `pgrep` command can search for processes by name.

Example:

```bash id="8zq8r6"
pgrep ssh
```

Another example:

```bash id="v9u0po"
pgrep bash
```

The output normally contains matching PIDs.

This is useful when an analyst wants to locate a particular process.

---

## 12. Find a Process with `pidof`

The `pidof` command can return the PID of a specified program.

Example:

```bash id="l0l7fz"
pidof sshd
```

If the program is running, Linux may return one or more PIDs.

If there is no output, the specified process may not currently be running.

---

## 13. View Process Relationships with `pstree`

The `pstree` command displays processes in a hierarchical structure.

Run:

```bash id="h3t1be"
pstree
```

This can help show relationships between processes.

Example concept:

```
systemd
  |
  +-- sshd
       |
       +-- bash
            |
            +-- command
```

The exact process tree will vary depending on the system.

Process relationships can become useful when investigating how a program was launched.

---

## 14. Process Ownership

Every process is associated with a user.

For example:

```
root
parijat
wazuh
```

Process ownership matters because the same command may have very different security significance depending on which user executed it.

### Investigation Question

Ask:

> Why is this process running under this user?

For example:

* A system service running as `root` may be normal.
* A user application running as the logged-in user may be normal.
* An unexpected program running as `root` may require investigation.

Do not assume that a root-owned process is malicious. Many legitimate Linux services run with elevated privileges.

---

## 15. Process and Command Activity

A process may be associated with a command.

Example:

```bash id="dzc08m"
whoami
```

Another controlled command:

```bash id="h3s40f"
id
```

Another example:

```bash id="p5j2kh"
uname -a
```

These commands can be used during the lab to generate normal process activity.

The purpose is to understand how process activity can be observed and correlated with security telemetry.

---

## 16. Basic Process Investigation Questions

When an analyst finds an unfamiliar process, ask:

### What?

* What program is running?
* What command was executed?

### Who?

* Which user owns the process?
* Was the user expected to run it?

### When?

* When did the process start?
* Did it start after another security event?

### Where?

* Which endpoint is running the process?

### Why?

* Is there a legitimate reason for the process?
* Was it started manually?
* Is it part of a normal service?

### Relationship

* What parent process started it?
* Was there a preceding login event?
* Was `sudo` used?
* Did another suspicious event occur nearby?

---

## 17. Process Monitoring and Authentication Correlation

Process monitoring becomes more useful when combined with authentication monitoring.

Example investigation:

```
10:00  Failed SSH Login
         |
10:02  Successful SSH Login
         |
10:03  User Session Created
         |
10:04  New Command Executed
         |
10:05  sudo Activity
```

The SOC analyst can investigate these events together instead of treating each event independently.

This is an example of basic event correlation.

---

## 18. Process Monitoring and Privileged Activity

Privileged commands should be reviewed in context.

For example:

```bash id="yd52ka"
sudo whoami
```

The command returns:

```
root
```

The analyst can then review:

* Which user executed the command.
* When it happened.
* What command was executed.
* Whether the user was expected to have administrative privileges.
* Whether related process activity occurred.

This does not mean every `sudo` command is suspicious.

---

## 19. Wazuh Process Monitoring

The Wazuh Agent provides endpoint security telemetry to the Wazuh Manager.

Depending on the configured monitoring and available telemetry, process-related activity can be used for security monitoring and investigation.

The basic monitoring path is:

```
Linux Process Activity
        |
        v
Security Telemetry
        |
        v
Wazuh Agent
        |
        v
Wazuh Manager
        |
        v
Detection / Alert
        |
        v
Wazuh Dashboard
```

The exact event and alert information depends on the configured Wazuh monitoring and the activity generated on the endpoint.

Do not assume that every Linux process visible in `ps` will automatically appear as a Wazuh alert.

---

## 20. Process Monitoring Configuration Reference

The Wazuh Agent configuration is located at:

```
/var/ossec/etc/ossec.conf
```

Before making any configuration changes, inspect the existing configuration.

Example:

```bash id="c4z9d1"
sudo grep -n "process" /var/ossec/etc/ossec.conf
```

Also check the existing Wazuh configuration before adding new monitoring entries.

Create a backup before making changes:

```bash id="u3d0q2"
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.backup
```

If a valid configuration change is made, restart the Wazuh Agent:

```bash id="5e4f0a"
sudo systemctl restart wazuh-agent
```

Check the service:

```bash id="q7eq3g"
sudo systemctl status wazuh-agent
```

Configuration and collection fundamentals are covered in:

* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`

---

## 21. Controlled Process Monitoring Test 1 — View Running Processes

### Objective

Review the processes currently running on Ubuntu.

Run:

```bash id="h8gh2r"
ps aux
```

Then:

```bash id="2p0k5f"
top
```

Exit `top` using:

```
q
```

### Record

* Number of processes observed.
* Important system processes.
* Wazuh-related processes, if visible.
* Current user processes.
* Any unfamiliar process requiring further review.

Do not label an unfamiliar process as malicious without investigation.

---

## 22. Controlled Process Monitoring Test 2 — Generate Normal Commands

### Objective

Generate simple, safe process and command activity.

Run:

```bash id="d8g8mm"
whoami
```

Then:

```bash id="r5v6a3"
id
```

Then:

```bash id="7q8e8z"
uname -a
```

Review the process list:

```bash id="ez0u2y"
ps aux
```

The purpose is to understand the relationship between commands executed by a user and processes running on the system.

---

## 23. Controlled Process Monitoring Test 3 — Search for SSH Processes

### Objective

Identify SSH-related processes.

Run:

```bash id="m8f9jb"
pgrep ssh
```

Then:

```bash id="4fjvpo"
pidof sshd
```

Review the process information:

```bash id="z9q8l5"
ps aux | grep ssh
```

Be aware that the `grep ssh` command itself may appear in the output.

Record:

* SSH-related PID.
* Process owner.
* Command.
* Whether the process is expected.

---

## 24. Controlled Process Monitoring Test 4 — Review Process Tree

### Objective

Understand basic parent-child process relationships.

Run:

```bash id="1x4k3f"
pstree
```

If the output is large, focus on:

* `systemd`
* `sshd`
* User shells
* Wazuh processes

Record one example of a parent-child process relationship.

Example:

```
Parent Process → Child Process

sshd → bash
```

The exact relationship may differ in the lab.

---

## 25. Controlled Process Monitoring Test 5 — Controlled Privileged Command

### Objective

Generate a safe privileged command and review the related activity.

Run:

```bash id="t0o4q5"
sudo whoami
```

Expected output:

```
root
```

Then review:

```bash id="w5b8nm"
sudo grep "sudo:" /var/log/auth.log
```

Review running processes:

```bash id="c6s1x2"
ps aux
```

The purpose is to correlate:

```
User
  |
  v
sudo
  |
  v
Privileged Command
  |
  v
Process / System Activity
```

Do not execute destructive commands.

---

## 26. Exact Wazuh Process Monitoring Validation

### Step 1 — Check Wazuh Agent

Run:

```bash id="v8s5cl"
sudo systemctl is-active wazuh-agent
```

Expected result:

```
active
```

If necessary:

```bash id="cz6m8u"
sudo systemctl start wazuh-agent
```

---

### Step 2 — Generate Controlled Process Activity

Run safe commands:

```bash id="q5p2va"
whoami
```

```bash id="b8z1a7"
id
```

```bash id="r2m4c9"
uname -a
```

Run:

```bash id="q6n4ew"
ps aux
```

Do not use destructive commands for the test.

---

### Step 3 — Check Local Evidence

Review the system logs:

```bash id="7v8d5n"
sudo tail -n 50 /var/log/auth.log
```

Review recent journal activity:

```bash id="k8j1y4"
sudo journalctl --since "10 minutes ago"
```

If the process activity produces relevant security telemetry, identify the related event.

---

### Step 4 — Check the Wazuh Agent Log

Run:

```bash id="p3g6n2"
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Look for:

* Agent communication.
* Configuration problems.
* Collection errors.
* Permission problems.
* Connection problems.

---

### Step 5 — Open Wazuh Dashboard

1. Open the Wazuh Dashboard.
2. Select the Ubuntu monitoring endpoint.
3. Set a recent time range, such as **Last 15 minutes**.
4. Review security events and alerts.
5. Search for events related to the controlled test.
6. Open a relevant event or alert if available.

---

### Step 6 — Record Event Information

If a relevant Wazuh event or alert is generated, record:

* Timestamp.
* Agent name.
* Hostname.
* Rule ID, if displayed.
* Rule description.
* Rule level, if displayed.
* Username.
* Process or command information.
* Event data.
* Related authentication event.
* Analyst interpretation.

Do not guess a rule ID if Wazuh does not display one.

---

### Step 7 — Compare With Local Evidence

Compare the Wazuh information with the Ubuntu system evidence.

Check:

* Timestamp.
* Hostname.
* Username.
* Process or command.
* Related authentication event.
* Event description.

Document whether the information matches.

---

## 27. Process Monitoring Validation Matrix

| Test                     | Local Observation | Wazuh Observation | Result |
| ------------------------ | ----------------- | ----------------- | ------ |
| Running processes        |                   |                   |        |
| Normal command execution |                   |                   |        |
| SSH process              |                   |                   |        |
| Process tree             |                   |                   |        |
| Sudo command             |                   |                   |        |

Use:

```
PASS — Expected evidence observed
PARTIAL — Some evidence observed
FAIL — Expected evidence not observed
N/A — Test not applicable
```

---

## 28. Process Analysis Example

### Scenario

An analyst notices a process associated with a user session.

### Investigation

First identify the process:

```bash id="6r0c5v"
ps aux
```

Identify the user:

```
USER
```

Identify the PID:

```
PID
```

Identify the command:

```
COMMAND
```

Then review the process relationship:

```bash id="83b0re"
pstree
```

Check whether the user recently authenticated:

```bash id="u7r2k5"
sudo grep "Accepted" /var/log/auth.log
```

Check for privileged activity:

```bash id="v3f8k1"
sudo grep "sudo:" /var/log/auth.log
```

### Analyst Questions

* Was the user expected to log in?
* Was the process expected?
* Was the process started after the login?
* Was `sudo` used?
* Is the process associated with a legitimate application?

---

## 29. Basic Suspicious Process Indicators

The following indicators may require investigation:

### Unknown Process

A process is unfamiliar to the analyst.

### Unexpected User

A process is running under a user who normally should not run it.

### Unexpected Privilege

A process is running with elevated privileges without an obvious reason.

### Unexpected Timing

A process starts immediately after a suspicious authentication event.

### Unexpected Command

A command appears unusual for the system's normal activity.

### High Resource Usage

A process consumes unusually high CPU or memory.

High resource usage alone does not prove malicious activity.

It may also be caused by:

* Software updates.
* System maintenance.
* Legitimate applications.
* Background services.
* Temporary workloads.

---

## 30. False Positive Handling

Not every unusual process is malicious.

Examples of legitimate processes include:

* System services.
* Package management processes.
* Wazuh Agent processes.
* SSH processes.
* User applications.
* Scheduled tasks.

Before classifying a process as suspicious, verify:

1. Process name.
2. Process owner.
3. Command.
4. Parent process.
5. Start time.
6. Related user activity.
7. Related authentication events.
8. Whether the activity was expected.

Document the reason for the final classification.

---

## 31. Basic Troubleshooting

### Problem 1 — `ps` Shows Many Processes

This is normal.

Linux systems run many background processes.

Focus on understanding:

* Process owner.
* PID.
* Command.
* Process purpose.

---

### Problem 2 — A Process Is Not Found

If:

```bash id="4n8t1q"
pgrep <process-name>
```

returns no output, the process may not currently be running.

Check again using:

```bash id="b5k0j9"
ps aux
```

---

### Problem 3 — Wazuh Shows No Process-Related Alert

Check:

1. Wazuh Agent status.
2. Agent connectivity.
3. Wazuh configuration.
4. Local event generation.
5. Dashboard time range.
6. Whether the tested activity is actually configured for collection or detection.

Do not assume that every process visible in `ps` generates a Wazuh alert.

---

### Problem 4 — Wazuh Agent Has Errors

Check:

```bash id="1c8z2r"
sudo systemctl status wazuh-agent
```

Then:

```bash id="u2e9w7"
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Record the error and troubleshooting action in the evidence.

---

### Problem 5 — `htop` Is Not Installed

Continue the lab using:

```bash id="v5j6s0"
ps aux
```

and:

```bash id="m3n7q2"
top
```

`htop` is not required for completing the basic process-monitoring objectives.

---

## 32. Evidence Requirements

Capture evidence for the process-monitoring lab.

Recommended evidence includes:

* Screenshot of `ps aux`.
* Screenshot of `top`.
* Screenshot of SSH process identification.
* Screenshot of `pstree`.
* Screenshot of controlled command execution.
* Screenshot of controlled `sudo` activity.
* Screenshot of Wazuh Agent status.
* Screenshot of Wazuh Dashboard event or alert, if generated.
* Process investigation record.
* Process monitoring validation matrix.

Store evidence under:

```
Evidence/
```

Example filenames:

```
evidence-01-process-list.png
evidence-02-top-process-monitoring.png
evidence-03-ssh-process.png
evidence-04-process-tree.png
evidence-05-sudo-process-activity.png
evidence-06-wazuh-process-event.png
evidence-07-process-investigation-record.md
```

Do not publish sensitive credentials, private keys or unrelated personal information.

---

## 33. Process Monitoring Investigation Record

Use this template when analyzing an important process.

| Field                        | Value |
| ---------------------------- | ----- |
| Investigation ID             |       |
| Date                         |       |
| Time                         |       |
| Hostname                     |       |
| Wazuh Agent                  |       |
| Process Name                 |       |
| PID                          |       |
| Process Owner                |       |
| Command                      |       |
| Parent Process               |       |
| Start Time                   |       |
| CPU Usage                    |       |
| Memory Usage                 |       |
| Related User                 |       |
| Related Authentication Event |       |
| Related Sudo Activity        |       |
| Expected Activity?           |       |
| Analyst Classification       |       |
| Evidence Location            |       |
| Analyst Notes                |       |

---

## 34. Process Monitoring Workflow

The basic SOC workflow for this lab is:

```
Observe
   |
   v
Identify Process
   |
   v
Identify User
   |
   v
Identify Command
   |
   v
Check Parent Process
   |
   v
Check Authentication Events
   |
   v
Check Privileged Activity
   |
   v
Check Wazuh Telemetry
   |
   v
Determine Expected / Suspicious
   |
   v
Document Findings
```

---

## 35. Security and Authorization

All process-monitoring activity in this lab must be performed on systems that the learner owns or is explicitly authorized to test.

Do not:

* Terminate unknown processes on production systems.
* Disable security services without authorization.
* Execute destructive commands.
* Modify system files unnecessarily.
* Attempt to investigate systems outside the lab.
* Perform unauthorized privilege escalation.
* Perform malware execution for testing.

The purpose of this lab is defensive monitoring and investigation.

---

## 36. Process Monitoring Completion Criteria

This documentation is complete when:

1. Linux process concepts are understood.
2. PIDs are understood.
3. Running processes are reviewed using `ps`.
4. Real-time process monitoring is performed using `top`.
5. Process searching is performed using `pgrep` or `pidof`.
6. Process relationships are reviewed using `pstree`.
7. Safe commands are used to generate normal process activity.
8. A controlled privileged command is observed.
9. Wazuh Agent status is validated.
10. Wazuh Dashboard is checked for relevant telemetry.
11. Local and central evidence are compared.
12. At least one process investigation record is completed.
13. Evidence is stored in the lab repository.

---

## 37. SOC Learning Outcome

After completing this activity, the learner should be able to explain:

* What a Linux process is.
* What a PID represents.
* How to view running processes.
* How to identify process ownership.
* How to identify a process command.
* How to find SSH-related processes.
* How to understand basic parent-child process relationships.
* How process activity can support security investigations.
* How process activity can be correlated with authentication events.
* How privileged activity can be investigated.
* How Wazuh can support endpoint monitoring.
* Why every unfamiliar process is not automatically malicious.
* How to document a basic process investigation.

---

## 38. Success Criteria

The lab is successful when the learner can:

* Use `ps aux` to review running processes.
* Use `top` for real-time process monitoring.
* Use `pgrep` or `pidof` to locate processes.
* Use `pstree` to understand process relationships.
* Identify the owner and command of a process.
* Generate safe process and command activity.
* Review a controlled `sudo` activity.
* Check Wazuh Agent status.
* Review Wazuh telemetry in the Dashboard.
* Correlate process activity with authentication activity.
* Explain why a process may be expected or suspicious.
* Complete a professional process-monitoring evidence record.

---

## 39. Related Documentation

* `01-Lab-Objective.md`
* `02-Lab-Setup.md`
* `03-Linux-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `08-Authentication-Monitoring.md`
* `10-Shell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
