# 10 — Shell Monitoring

## 1. Purpose

Shell monitoring is the process of observing command-line activity performed through a Linux shell.

In a SOC environment, shell activity can provide important context about what a user or process is doing on a Linux endpoint.

In this lab, shell monitoring is performed on the **Ubuntu 22.04 LTS Linux endpoint** using normal Linux commands, authentication logs, system logs, process information, and the **Wazuh Agent**.

The purpose of this documentation is to learn how a SOC analyst can:

* Understand Linux shell activity.
* Identify common Linux shells.
* Observe command execution.
* Correlate shell activity with user sessions.
* Correlate shell activity with authentication events.
* Identify potentially unusual command activity.
* Validate relevant security telemetry in Wazuh.
* Document shell-related investigation findings.

---

## 2. Lab Environment

| Component          | Details                              |
| ------------------ | ------------------------------------ |
| Operating System   | Ubuntu 22.04 LTS                     |
| Architecture       | 64-bit x86_64                        |
| Virtualization     | VMware Workstation Player            |
| Endpoint Role      | Linux Security Monitoring Endpoint   |
| Security Agent     | Wazuh Agent                          |
| Central Platform   | Wazuh Manager, Indexer and Dashboard |
| Primary Shell      | Bash                                 |
| Main Log Sources   | `/var/log/auth.log`, systemd journal |
| Process Monitoring | `ps`, `top`, `pstree`                |

### Shell Monitoring Flow

```
User
  |
  v
Shell
  |
  v
Command Execution
  |
  v
Linux Process / Event
  |
  v
Log / Security Telemetry
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
  |
  v
SOC Analyst
  |
  v
Analysis and Documentation
```

---

## 3. What Is a Shell?

A shell is a program that provides a command-line interface for interacting with an operating system.

A user can enter commands into the shell to:

* View files.
* Check system information.
* Manage processes.
* View network information.
* Manage users.
* Run programs.
* Perform administrative tasks.

The shell interprets the command and requests the operating system to perform the required operation.

---

## 4. Bash Shell

Bash stands for:

```
Bourne Again Shell
```

Bash is commonly available on Linux systems and is the primary shell used for the basic exercises in this lab.

Check the current shell:

```bash id="2x9q3n"
echo $SHELL
```

Example output:

```text id="u3e6m1"
/bin/bash
```

The exact output depends on the user's configured shell.

---

## 5. Shell vs Terminal

A terminal and a shell are not the same thing.

### Terminal

The terminal provides the interface through which the user interacts with the system.

### Shell

The shell interprets commands entered by the user.

Simple relationship:

```
User
  |
  v
Terminal
  |
  v
Shell
  |
  v
Linux Operating System
```

For example, when a user opens a terminal and enters:

```bash id="7t1m8b"
whoami
```

the shell interprets the command and executes it.

---

## 6. Why Shell Monitoring Matters in a SOC

Attackers who gain access to a Linux system may use the command line to:

* Explore the system.
* Identify users.
* Check system information.
* Review network configuration.
* Search for files.
* Execute programs.
* Change configurations.
* Create persistence.
* Attempt privilege escalation.

However, these commands can also be completely legitimate.

For example:

```bash id="8p4x1z"
whoami
```

may be executed by:

* A normal user checking their identity.
* An administrator troubleshooting a system.
* A SOC analyst performing an investigation.
* A student performing this lab.

Therefore, command activity must always be analyzed in context.

---

## 7. Shell Activity Categories

Basic shell activity can be grouped into several categories.

### 7.1 System Information

Examples:

```bash id="1x6w9r"
uname -a
```

```bash id="6m2z8q"
whoami
```

```bash id="4c9p7k"
id
```

---

### 7.2 User and Session Information

Examples:

```bash id="7h3n5v"
who
```

```bash id="0q8s2m"
w
```

```bash id="2b6k4t"
last
```

---

### 7.3 Process Information

Examples:

```bash id="9v5r3x"
ps aux
```

```bash id="6n8c1p"
top
```

---

### 7.4 File and Directory Activity

Examples:

```bash id="4m7y2q"
pwd
```

```bash id="3f8k6w"
ls
```

```bash id="5j1p9n"
ls -la
```

These are common administrative commands and are not automatically suspicious.

---

### 7.5 Privileged Commands

Example:

```bash id="8z2m5c"
sudo whoami
```

Privileged commands should be reviewed according to the user's role and the context of the activity.

---

## 8. Command Execution and Processes

When a user executes a command, Linux may create a process to execute it.

Example:

```bash id="4w7q9s"
uname -a
```

Basic relationship:

```
Shell
  |
  v
Command
  |
  v
Process
  |
  v
Result
```

This is why shell monitoring and process monitoring are closely related.

Process monitoring is documented in:

```
09-Process-Monitoring.md
```

---

## 9. Shell History

Bash commonly maintains command history for interactive sessions.

A user can view the current shell history using:

```bash id="1g5t8v"
history
```

This can help a user review commands entered during a session.

However, shell history should **not** be treated as a complete security log.

Reasons include:

* Not every command is necessarily stored.
* History can depend on shell configuration.
* Different shells may behave differently.
* Commands may be executed by non-interactive processes.
* History can be modified or deleted.

Therefore, a SOC analyst should correlate shell-related information with other available telemetry.

---

## 10. Viewing Recent Shell History

Run:

```bash id="5d8m2x"
history
```

To view a smaller portion:

```bash id="7q4n9b"
history 10
```

This displays recent commands from the current shell history.

The exact output will depend on commands previously executed in the Ubuntu VM.

---

## 11. Shell History File

For Bash, command history is commonly stored in:

```
~/.bash_history
```

Check whether the file exists:

```bash id="3r6k8p"
ls -la ~/.bash_history
```

View the file:

```bash id="9w2c5m"
cat ~/.bash_history
```

Do not modify or delete the history file during this lab.

The purpose is observation and understanding.

---

## 12. Important Limitation of Shell History

Shell history is useful but should not be considered equivalent to centralized security logging.

For example, a SOC analyst should not conclude:

> "The command is not in `.bash_history`, therefore it was never executed."

That conclusion is unsafe.

A better approach is:

```
Shell History
      +
Authentication Logs
      +
Process Information
      +
Wazuh Telemetry
      +
Other Available Evidence
```

This provides stronger investigation context.

---

## 13. Useful Shell Monitoring Commands

### Identify Current Shell

```bash id="6j3p8v"
echo $SHELL
```

### Identify Current User

```bash id="2k7n5m"
whoami
```

### View User Identity and Groups

```bash id="9c4w1x"
id
```

### View Current Directory

```bash id="5r8q2z"
pwd
```

### List Files

```bash id="3m7v6k"
ls
```

### List Detailed Files

```bash id="8p1d4y"
ls -la
```

### View Command History

```bash id="4x9n2c"
history
```

### View Recent History

```bash id="7m3k5v"
history 10
```

### View System Information

```bash id="1q8w6r"
uname -a
```

### View Current Sessions

```bash id="6c4p9x"
who
```

### View Current User Activity

```bash id="2v7m1n"
w
```

### View Running Processes

```bash id="5k9r3z"
ps aux
```

---

## 14. Shell Activity and Authentication Monitoring

Shell activity should be correlated with authentication events.

Example:

```
Successful SSH Login
        |
        v
User Session
        |
        v
Bash Shell
        |
        v
Commands Executed
        |
        v
Process Activity
        |
        v
Privileged Activity
```

This allows the analyst to understand what happened after a user authenticated.

---

## 15. Shell Activity and Sudo

A user may execute privileged commands through `sudo`.

Example:

```bash id="8f2m7q"
sudo whoami
```

Expected result:

```
root
```

Review related authentication activity:

```bash id="5n9x3c"
sudo grep "sudo:" /var/log/auth.log
```

The analyst should record:

* Username.
* Time.
* Command.
* Result.
* Whether the activity was expected.

---

## 16. Shell Activity and Process Monitoring

Shell commands are closely related to process activity.

For example:

```bash id="3k7p1m"
ps aux
```

The command itself runs through the shell and may appear as a process while it executes.

Review the process list:

```bash id="9v4c6x"
ps aux
```

Review the process tree:

```bash id="2m8q5r"
pstree
```

The exact output will vary depending on the system.

---

## 17. Wazuh and Shell Monitoring

The Wazuh Agent collects configured endpoint security telemetry and sends it to the Wazuh Manager.

Shell activity may be represented through different types of telemetry depending on the Linux configuration and monitoring capabilities enabled in the lab.

Basic flow:

```
Shell Activity
      |
      v
Linux Event / Process Activity
      |
      v
Wazuh Agent
      |
      v
Wazuh Manager
      |
      v
Detection
      |
      v
Alert / Event
      |
      v
Wazuh Dashboard
```

Important:

**Do not assume that every command entered into Bash will automatically generate a Wazuh alert.**

The exact visibility depends on:

* What telemetry is being collected.
* How the Wazuh Agent is configured.
* What detection rules apply.
* Whether the activity produces a detectable security event.

---

## 18. Shell Monitoring Configuration Reference

The Wazuh Agent configuration file is:

```
/var/ossec/etc/ossec.conf
```

Before making any configuration changes, inspect the existing configuration.

Example:

```bash id="7x3m9q"
sudo grep -n "localfile" /var/ossec/etc/ossec.conf
```

Create a backup before making changes:

```bash id="4n8p2c"
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.backup
```

If a valid configuration change is made, restart the agent:

```bash id="6r1k5v"
sudo systemctl restart wazuh-agent
```

Check the agent:

```bash id="9m4q7x"
sudo systemctl status wazuh-agent
```

Basic configuration and log collection are covered in:

* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`

---

## 19. Controlled Shell Monitoring Test 1 — Identify the Shell

### Objective

Identify the shell used by the current user.

Run:

```bash id="3w6p8n"
echo $SHELL
```

Record:

* Shell path.
* Current username.
* Date and time.

Example:

```
Shell: /bin/bash
```

The exact result may differ.

---

## 20. Controlled Shell Monitoring Test 2 — Normal Commands

### Objective

Generate normal shell activity.

Run:

```bash id="8q2m5v"
whoami
```

Then:

```bash id="5x7n1c"
id
```

Then:

```bash id="9r3k6p"
pwd
```

Then:

```bash id="4m8w2z"
uname -a
```

Review shell history:

```bash id="7c1p5x"
history 10
```

Record the commands and execution time.

These are normal administrative commands and are used only to understand shell activity.

---

## 21. Controlled Shell Monitoring Test 3 — File and Directory Activity

### Objective

Observe basic shell interaction with the filesystem.

Run:

```bash id="2v6k9m"
pwd
```

Then:

```bash id="8n3r5q"
ls
```

Then:

```bash id="1x7p4c"
ls -la
```

Review the history:

```bash id="5m9w2z"
history 10
```

No files need to be modified for this test.

---

## 22. Controlled Shell Monitoring Test 4 — Process Activity

### Objective

Correlate shell commands with process monitoring.

Run:

```bash id="6q2k8v"
ps aux
```

Then:

```bash id="3r7m1x"
pgrep bash
```

Then:

```bash id="9p4c5n"
pstree
```

Record:

* Current shell.
* Shell PID, if identified.
* User.
* Parent process.
* Child processes, if visible.

---

## 23. Controlled Shell Monitoring Test 5 — Privileged Shell Activity

### Objective

Generate one safe privileged command.

Run:

```bash id="7w5n2q"
sudo whoami
```

Expected output:

```
root
```

Then review the authentication log:

```bash id="4k8m3x"
sudo grep "sudo:" /var/log/auth.log
```

Review recent events:

```bash id="2c6p9v"
sudo tail -n 30 /var/log/auth.log
```

Do not execute destructive commands.

---

## 24. Controlled Shell Monitoring Test 6 — Session Correlation

### Objective

Understand the relationship between user sessions and shell activity.

Run:

```bash id="8m4r7q"
who
```

Then:

```bash id="5x1c9p"
w
```

Then:

```bash id="3n6k2v"
last
```

Review:

```bash id="7p8m4x"
history 10
```

Record:

* Current user.
* Session information.
* Login time, if visible.
* Recent shell commands.
* Relationship between the session and the shell.

---

## 25. Exact Wazuh Shell Monitoring Validation

### Step 1 — Check the Wazuh Agent

Run:

```bash id="9c2v6m"
sudo systemctl is-active wazuh-agent
```

Expected result:

```
active
```

If necessary:

```bash id="4r7n1x"
sudo systemctl start wazuh-agent
```

---

### Step 2 — Generate Controlled Shell Activity

Run the safe commands used in this lab:

```bash id="6m8p3q"
whoami
```

```bash id="1x5c9v"
id
```

```bash id="7n2r4k"
uname -a
```

```bash id="3q6m8p"
ps aux
```

```bash id="8v1c5x"
sudo whoami
```

---

### Step 3 — Review Local Evidence

Review authentication events:

```bash id="5r9k2m"
sudo tail -n 50 /var/log/auth.log
```

Review recent journal events:

```bash id="6p3x8v"
sudo journalctl --since "10 minutes ago"
```

Review shell history:

```bash id="2m7c5n"
history 10
```

The analyst should compare these sources rather than relying on only one source.

---

### Step 4 — Check Wazuh Agent Logs

Run:

```bash id="9q4r1x"
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Look for:

* Communication problems.
* Configuration errors.
* Collection problems.
* Permission errors.
* Other relevant agent messages.

---

### Step 5 — Open the Wazuh Dashboard

1. Open the Wazuh Dashboard.
2. Select the Ubuntu monitoring endpoint.
3. Set a recent time range, such as **Last 15 minutes**.
4. Review relevant security events.
5. Search for events related to the controlled activity.
6. Open a relevant event or alert, if available.

---

### Step 6 — Record Event Details

If a relevant event or alert is available, record:

* Timestamp.
* Wazuh agent.
* Hostname.
* Username.
* Process or command information.
* Event description.
* Rule ID, if displayed.
* Rule level, if displayed.
* Related authentication activity.
* Analyst interpretation.

Do not guess values that are not displayed.

---

### Step 7 — Compare Evidence

Compare:

```
Shell History
      |
      +
Authentication Logs
      |
      +
Process Information
      |
      +
Wazuh Events / Alerts
```

Check whether:

* The timestamps are consistent.
* The username matches.
* The endpoint matches.
* The activity was expected.
* Related privileged activity is present.

---

## 26. Shell Monitoring Validation Matrix

| Test                    | Local Evidence | Wazuh Evidence | Result |
| ----------------------- | -------------- | -------------- | ------ |
| Shell identification    |                |                |        |
| Normal command activity |                |                |        |
| File/directory commands |                |                |        |
| Process commands        |                |                |        |
| Sudo command            |                |                |        |
| Session correlation     |                |                |        |

Use:

```
PASS — Expected evidence observed
PARTIAL — Some evidence observed
FAIL — Expected evidence not observed
N/A — Test not applicable
```

---

## 27. Basic Shell Investigation Questions

When reviewing shell activity, ask:

### Who?

* Which user executed the activity?
* Was the user expected to access the system?

### What?

* What command was executed?
* What process was created?
* Was the command administrative or normal?

### When?

* When did the activity occur?
* Did it happen shortly after authentication?

### Where?

* Which endpoint was involved?
* Was the activity performed locally or through an SSH session?

### Why?

* Was there a legitimate reason?
* Was the activity part of maintenance or troubleshooting?

### What Happened Next?

* Was `sudo` used?
* Was a new process created?
* Were configuration changes made?
* Did another security event occur?

---

## 28. Basic Suspicious Shell Activity Indicators

The following situations may require additional investigation:

### Unexpected User

A user performs shell activity on a system they do not normally access.

### Unexpected Login

Shell activity follows an unexpected successful login.

### Unexpected Privileged Command

A user executes privileged commands without an obvious reason.

### Unusual Command

A command is inconsistent with the user's normal activity.

### Suspicious Sequence

Example:

```
Successful Login
      |
      v
Shell Session
      |
      v
System Discovery
      |
      v
Privileged Activity
```

This sequence does not automatically prove compromise.

The analyst must investigate the context.

---

## 29. False Positives

Many shell commands that appear unusual may be legitimate.

Examples:

```bash id="4q7m1x"
ps aux
```

```bash id="8n2c5v"
uname -a
```

```bash id="6p9r3k"
who
```

These commands can be used by:

* Administrators.
* Developers.
* Security analysts.
* Students.
* Monitoring tools.

Therefore, the command name alone should not determine whether an event is malicious.

---

## 30. Shell Monitoring Investigation Example

### Scenario

An Ubuntu endpoint records a successful SSH login followed by several shell commands and a `sudo` command.

### Investigation Steps

1. Identify the username.
2. Identify the source IP.
3. Record the successful login timestamp.
4. Review the shell activity.
5. Review process information.
6. Check the `sudo` activity.
7. Review Wazuh telemetry.
8. Determine whether the activity was part of the authorized lab.
9. Document the result.

### Example Analyst Conclusion

```
A successful SSH login was followed by normal shell activity
and an authorized sudo command on the Ubuntu monitoring endpoint.
The activity originated from the controlled lab environment and
was generated intentionally for security monitoring validation.
No unauthorized activity was identified.
```

---

## 31. Basic Troubleshooting

### Problem 1 — `history` Does Not Show a Command

Possible reasons include:

* The command was executed in another shell.
* History configuration differs.
* The command was executed non-interactively.
* The shell session has not written history yet.

Use other evidence sources such as:

```bash id="5c8m2q"
sudo tail -n 50 /var/log/auth.log
```

and:

```bash id="7r3n9x"
ps aux
```

Do not assume that missing history means a command was never executed.

---

### Problem 2 — `.bash_history` Is Missing

Check:

```bash id="1m6p8v"
ls -la ~/.bash_history
```

The file may not exist for every user or environment.

Continue using the current shell's:

```bash id="9q2c5r"
history
```

---

### Problem 3 — Wazuh Shows No Shell Event

Check:

1. Wazuh Agent status.
2. Agent connectivity.
3. Wazuh configuration.
4. Local event generation.
5. Dashboard time range.
6. Whether the activity produces telemetry that Wazuh is configured to collect or detect.

Remember:

**Not every shell command automatically generates a Wazuh alert.**

---

### Problem 4 — Wazuh Agent Has Errors

Check:

```bash id="6v4n8m"
sudo systemctl status wazuh-agent
```

Then:

```bash id="3x7p1q"
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Record the observed error and troubleshooting action.

---

## 32. Evidence Requirements

Capture evidence for the shell-monitoring lab.

Recommended evidence includes:

* Screenshot showing current shell.
* Screenshot of `history`.
* Screenshot of normal shell commands.
* Screenshot of process activity.
* Screenshot of `sudo` activity.
* Screenshot of current session information.
* Screenshot of Wazuh Agent status.
* Screenshot of relevant Wazuh event or alert, if generated.
* Shell investigation record.
* Shell monitoring validation matrix.

Store evidence under:

```
Evidence/
```

Example filenames:

```
evidence-01-shell-identification.png
evidence-02-shell-history.png
evidence-03-normal-command-activity.png
evidence-04-process-correlation.png
evidence-05-sudo-shell-activity.png
evidence-06-wazuh-shell-event.png
evidence-07-shell-investigation-record.md
```

Do not publish:

* Passwords.
* Private SSH keys.
* Sensitive tokens.
* Personal information.
* Unrelated system information.

---

## 33. Shell Monitoring Investigation Record

Use this template when documenting an important shell activity event.

| Field                  | Value |
| ---------------------- | ----- |
| Investigation ID       |       |
| Date                   |       |
| Time                   |       |
| Hostname               |       |
| Wazuh Agent            |       |
| Username               |       |
| Source IP              |       |
| Session Type           |       |
| Shell                  |       |
| Command                |       |
| Process                |       |
| PID                    |       |
| Parent Process         |       |
| Authentication Event   |       |
| Sudo Activity          |       |
| Expected Activity?     |       |
| Wazuh Event / Alert    |       |
| Analyst Classification |       |
| Evidence Location      |       |
| Analyst Notes          |       |

---

## 34. Shell Monitoring Workflow

The basic SOC workflow for this lab is:

```
Authentication
     |
     v
User Session
     |
     v
Shell
     |
     v
Command
     |
     v
Process
     |
     v
Log / Telemetry
     |
     v
Wazuh
     |
     v
Alert / Event
     |
     v
Analysis
     |
     v
Documentation
```

This workflow helps the analyst understand what happened before, during and after shell activity.

---

## 35. Security and Authorization

All shell-monitoring activity must be performed on systems that the learner owns or is explicitly authorized to test.

Do not:

* Execute destructive commands.
* Modify system files unnecessarily.
* Delete logs.
* Clear shell history to hide activity.
* Disable security monitoring without authorization.
* Attempt unauthorized privilege escalation.
* Execute malicious payloads.
* Investigate systems outside the authorized lab.

The purpose of this exercise is defensive monitoring and security investigation.

---

## 36. Shell Monitoring Completion Criteria

This documentation is complete when:

1. Linux shell concepts are understood.
2. Bash is identified on the Ubuntu endpoint.
3. Shell activity is observed.
4. Shell history is reviewed.
5. Normal commands are executed safely.
6. Process activity is correlated with shell activity.
7. A controlled `sudo` command is observed.
8. User session information is reviewed.
9. Wazuh Agent status is validated.
10. Wazuh Dashboard is checked for relevant telemetry.
11. Local evidence is compared with Wazuh evidence.
12. At least one shell investigation record is completed.
13. Evidence is stored in the lab repository.

---

## 37. SOC Learning Outcome

After completing this activity, the learner should be able to explain:

* What a Linux shell is.
* What Bash is.
* The difference between a terminal and a shell.
* How shell commands create or interact with processes.
* How to view shell history.
* Why shell history is not a complete security log.
* How shell activity relates to authentication.
* How shell activity relates to process monitoring.
* How privileged shell activity can be investigated.
* How Wazuh can support Linux endpoint monitoring.
* Why individual commands must be analyzed in context.
* How to document basic shell-monitoring findings.

---

## 38. Success Criteria

The lab is successful when the learner can:

* Identify the current shell.
* Identify the current user.
* Review shell history.
* Execute safe Linux commands.
* Observe related process activity.
* Review session information.
* Generate and review controlled `sudo` activity.
* Check authentication logs.
* Check Wazuh Agent status.
* Review Wazuh Dashboard telemetry.
* Correlate shell, authentication and process information.
* Explain whether activity is expected or requires investigation.
* Complete a professional shell-monitoring evidence record.

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
* `09-Process-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
