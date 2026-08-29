# Linux Monitoring

> **Blue Team → SOC → Security Monitoring → Linux**

Linux systems are widely used for servers, cloud infrastructure, databases, containers, security appliances, and enterprise applications. For a SOC analyst, Linux monitoring is therefore essential for detecting unauthorized access, privilege escalation, persistence, malware execution, suspicious processes, and abnormal network activity.

A strong Linux monitoring capability combines:

```text
Linux System Logs
+
Authentication Logs
+
systemd journal
+
auditd
+
Process Monitoring
+
Network Monitoring
+
File Integrity Monitoring
+
Service Monitoring
+
Wazuh / SIEM
```

The objective is to answer:

> **Who accessed the system, what did they execute, what changed, what network activity occurred, and what happened afterward?**

---

# 1. Objectives

After completing this section, you should understand:

* Linux logging fundamentals
* `/var/log`
* `auth.log`
* `syslog`
* `journalctl`
* SSH monitoring
* sudo monitoring
* user and group monitoring
* process monitoring
* service monitoring
* scheduled-task monitoring
* `auditd`
* file integrity monitoring
* network monitoring
* Linux malware indicators
* Linux persistence indicators
* Linux monitoring with Wazuh
* practical SOC investigations

---

# 2. Linux Monitoring Architecture

```text
                    LINUX SERVER
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
    System Logs      Authentication      auditd
        │                │                │
        ↓                ↓                ↓
      syslog           SSH/sudo       Audit Events
        │                │                │
        └────────────────┼────────────────┘
                         ↓
                   Wazuh Agent
                         ↓
                  Wazuh Manager
                         ↓
                       SIEM
                         ↓
                    Detection
                         ↓
                       Alert
                         ↓
                   SOC Analyst
```

---

# 3. Linux Logging Fundamentals

Linux systems generate logs from:

```text
Kernel
Services
Authentication
Applications
Users
Network Services
Security Controls
```

Traditional logs are commonly stored under:

```text
/var/log/
```

Modern Linux distributions may also rely heavily on:

```text
systemd-journald
```

---

# 4. Important Linux Log Files

Common files include:

```text
/var/log/auth.log
/var/log/syslog
/var/log/messages
/var/log/kern.log
/var/log/secure
```

The exact files vary by Linux distribution.

For example:

```text
Debian / Ubuntu
→ /var/log/auth.log

RHEL / CentOS
→ /var/log/secure
```

Always verify the logging configuration of the specific system.

---

# 5. `/var/log/auth.log`

On Debian-based systems, authentication-related activity is commonly recorded in:

```text
/var/log/auth.log
```

It may contain:

```text
SSH Login
SSH Failure
sudo
su
Authentication
User Sessions
```

Example:

```text
Failed password for user admin
```

This is highly useful for SOC investigations.

---

# 6. SSH Monitoring

SSH is one of the most important Linux remote-access services.

Monitor:

```text
Successful Login
Failed Login
Username
Source IP
Timestamp
Authentication Method
Session
```

Example:

```text
Internet
   ↓
SSH
   ↓
Multiple Failed Logins
   ↓
Successful Login
```

This could indicate:

```text
Brute Force
Credential Compromise
Password Spraying
```

But legitimate administrative activity must also be considered.

---

# 7. SSH Failed Authentication

Repeated SSH failures are a common detection opportunity.

Example:

```text
Failed
Failed
Failed
Failed
Failed
```

Investigate:

```text
Source IP
Target Account
Time Window
Number of Attempts
Authentication Method
Successful Login After Failures
```

A simple detection concept:

```text
Multiple Failed SSH Logins
+
Same Source
+
Short Time Window
```

---

# 8. SSH Successful Authentication

A successful SSH login should be evaluated against context.

Questions:

```text
Who logged in?
From where?
When?
Which server?
Was the account expected?
Was the source IP known?
What happened afterward?
```

Example:

```text
admin
 ↓
SSH
 ↓
Unknown IP
 ↓
03:00 AM
 ↓
sudo
 ↓
New Process
```

This sequence deserves investigation.

---

# 9. SSH Keys

Linux environments frequently use SSH keys for authentication.

Monitor:

```text
~/.ssh/
authorized_keys
known_hosts
```

Potential security concerns include:

```text
Unexpected Key Added
Unknown Key
Unauthorized Account
Unexpected authorized_keys Modification
```

An attacker who gains access may attempt to establish persistent SSH access.

---

# 10. Sudo Monitoring

`sudo` allows authorized users to execute commands with elevated privileges.

Monitoring should capture:

```text
User
Command
Target User
Timestamp
Host
```

Example:

```text
alice
 ↓
sudo
 ↓
systemctl
```

This may be normal.

But:

```text
unexpected_user
 ↓
sudo
 ↓
new privileged command
```

may require investigation.

---

# 11. `su` Monitoring

The `su` command can switch user context.

Monitor:

```text
Source User
Target User
Timestamp
Success/Failure
```

Potentially important:

```text
Normal User
    ↓
su
    ↓
root
```

This should be correlated with authorization and expected administrative activity.

---

# 12. Linux Users

Monitor user-account changes.

Useful commands for administrators include:

```text
who
w
last
lastlog
id
getent passwd
```

Security monitoring may identify:

```text
New Account
Disabled Account
Unexpected Login
Unexpected Privileged User
```

---

# 13. User Creation

A new account can be legitimate or malicious.

Investigate:

```text
Account Name
Creator
Timestamp
UID
Groups
Home Directory
Shell
```

Potentially suspicious:

```text
Unexpected Account
+
Privileged Group
+
Interactive Login
```

---

# 14. Privileged Users

Linux privilege should be monitored carefully.

Important accounts may include:

```text
root
sudo-enabled users
Service accounts
Administrative accounts
```

Useful context:

```text
UID
Groups
sudo permissions
Login history
Process activity
```

A privileged account compromise can have significant impact.

---

# 15. Linux Groups

Group membership can determine access to sensitive resources.

Monitor changes to:

```text
sudo
adm
docker
wheel
other privileged groups
```

Example:

```text
User
 ↓
Added to privileged group
 ↓
Access increases
```

Unexpected privilege changes deserve investigation.

---

# 16. `journalctl`

Systems using systemd can centralize logs through the journal.

Useful command:

```text
journalctl
```

Examples:

```text
journalctl -u ssh
journalctl -b
journalctl -p warning
```

The journal can provide:

```text
Authentication
Service Activity
Kernel Events
System Events
Application Events
```

---

# 17. Systemd Services

Linux services are important monitoring sources.

Examples:

```text
sshd
nginx
apache2
mysql
docker
cron
```

Monitor:

```text
Service Start
Service Stop
Service Failure
Configuration Change
Unexpected New Service
```

A suspicious new service may indicate persistence.

---

# 18. Service Monitoring

Example investigation:

```text
Unknown Service
      ↓
Started Automatically
      ↓
Runs as root
      ↓
Unknown Binary
```

This should be investigated.

Useful commands:

```text
systemctl list-units
systemctl list-unit-files
systemctl status <service>
```

---

# 19. Scheduled Tasks

Linux scheduling mechanisms include:

```text
cron
crontab
systemd timers
```

Monitor:

```text
New Scheduled Job
Modified Job
Unexpected Script
Execution Frequency
User
```

Potential persistence pattern:

```text
Attacker
   ↓
Cron Job
   ↓
Script
   ↓
Periodic Execution
```

---

# 20. Cron Monitoring

Common locations include:

```text
/etc/crontab
/etc/cron.d/
/etc/cron.hourly/
/etc/cron.daily/
/var/spool/cron/
```

Monitor changes to these locations.

A SOC analyst should ask:

```text
Who changed it?
When?
What command executes?
As which user?
Where is the script?
```

---

# 21. Process Monitoring

Linux processes are fundamental telemetry.

Useful commands:

```text
ps
top
htop
pgrep
pstree
```

Security monitoring should identify:

```text
Process
PID
Parent PID
User
Command Line
Executable
CPU
Memory
Network Activity
```

---

# 22. Process Trees

A process tree helps establish execution relationships.

Example:

```text
sshd
 ↓
bash
 ↓
sudo
 ↓
python
```

Another example:

```text
nginx
 ↓
unexpected shell
```

The second pattern may require investigation.

---

# 23. Suspicious Processes

Potential indicators include:

```text
Unknown Binary
Unexpected Parent
Execution from /tmp
Execution from /dev/shm
Root-Owned Unexpected Process
Hidden Process
Unexpected Network Connection
```

These indicators should be evaluated together.

---

# 24. `/tmp` and `/dev/shm`

Attackers may sometimes execute files from temporary or memory-backed locations.

Examples:

```text
/tmp
/dev/shm
```

Monitoring should look for:

```text
Executable Creation
Execution
Permission Changes
Network Connections
```

However, legitimate applications may also use these locations.

Context is essential.

---

# 25. Network Monitoring

Linux network telemetry can include:

```text
Connections
Listening Ports
DNS
Routing
Interface Activity
Firewall Events
```

Useful commands:

```text
ss
ip
lsof
```

For example:

```text
ss -tulnp
```

can help identify listening services.

---

# 26. Unexpected Listening Services

Example:

```text
Server
 ↓
Expected: 22, 80, 443
```

Suddenly:

```text
Port 4444
```

appears.

The analyst should investigate:

```text
Process
PID
User
Binary
Configuration
Creation Time
Network Connections
```

A new listening port is an indicator, not proof, of compromise.

---

# 27. File Integrity Monitoring

Important files and directories should be monitored for unauthorized changes.

Examples:

```text
/etc/passwd
/etc/shadow
/etc/sudoers
/etc/ssh/
~/.ssh/
Cron directories
Systemd service directories
Application configurations
```

FIM can detect:

```text
File Created
File Modified
File Deleted
Hash Changed
Permission Changed
```

---

# 28. `/etc/passwd`

This file contains account information.

Monitoring changes can help detect:

```text
New User
Modified User
Unexpected Account
```

Do not treat every modification as malicious.

Package installations and administration can legitimately modify system files.

---

# 29. `/etc/sudoers`

Changes to sudo configuration are highly important.

Monitor:

```text
File Modification
New Privilege
Unexpected User
Unexpected Command Permission
```

Example:

```text
User
 ↓
sudoers modification
 ↓
New administrative privileges
```

This may represent privilege escalation or legitimate administration.

---

# 30. SSH Configuration

Monitor important SSH configuration files such as:

```text
/etc/ssh/sshd_config
```

Potential changes include:

```text
Authentication Settings
Port
Root Login
Password Authentication
Access Controls
```

Unexpected changes should be investigated.

---

# 31. Linux Auditd

`auditd` provides kernel-level auditing capabilities.

It can monitor:

```text
System Calls
File Access
User Activity
Privilege Changes
Configuration Changes
```

Example:

```text
User
 ↓
Sensitive File Access
 ↓
auditd
 ↓
Event
```

This can provide deeper forensic context.

---

# 32. Audit Rules

Audit rules can be designed around important assets.

Examples:

```text
/etc/passwd
/etc/shadow
/etc/sudoers
/etc/ssh/
```

The goal is to monitor high-value actions without creating excessive noise.

---

# 33. File Permission Monitoring

Linux security depends heavily on file permissions.

Monitor:

```text
Owner
Group
Mode
SUID
SGID
ACL
```

Potentially suspicious:

```text
Unexpected SUID Binary
Unexpected Permission Change
World-Writable Sensitive File
```

---

# 34. SUID Monitoring

SUID allows a program to execute with the privileges of its owner.

SUID binaries can be legitimate.

However, unexpected SUID changes may indicate privilege-escalation risk.

Monitor:

```text
New SUID File
Modified SUID File
Unknown Binary
Location
Owner
Hash
```

---

# 35. Malware Monitoring

Linux malware may reveal itself through:

```text
Unknown Process
Unexpected Network Connection
Persistence
Modified System Files
Unexpected Binary
High Resource Usage
```

Example:

```text
Unknown Binary
+
External Connection
+
Persistence
```

is much more concerning than any single indicator alone.

---

# 36. Network Connections

Investigate suspicious outbound connections.

Important fields:

```text
Process
PID
User
Destination IP
Destination Port
Protocol
Timestamp
```

Example:

```text
python
 ↓
203.0.113.10:443
```

The analyst should determine:

```text
Why is Python communicating externally?
What script launched it?
Which user owns the process?
Is the destination trusted?
```

---

# 37. DNS Monitoring

Linux servers may generate DNS queries through:

```text
systemd-resolved
dnsmasq
applications
local resolvers
```

Monitor:

```text
Domain
Source
Frequency
Response
```

Potential detections:

```text
Malicious Domain
DNS Tunneling
DGA
Unexpected External Domain
```

---

# 38. Authentication Correlation

Linux authentication events become more useful when correlated.

Example:

```text
Multiple Failed SSH Logins
          ↓
Successful Login
          ↓
sudo
          ↓
New Process
          ↓
Network Connection
```

This is more meaningful than investigating each event separately.

---

# 39. Linux Monitoring Through Wazuh

Your home lab can use:

```text
Linux VM
   │
   ├── auth.log
   ├── syslog
   ├── journald
   ├── auditd
   ├── Process Activity
   └── File Integrity
          │
          ↓
      Wazuh Agent
          ↓
     Wazuh Manager
          ↓
          SIEM
          ↓
       Detection
          ↓
         Alert
```

---

# 40. Wazuh Linux Monitoring

Configure monitoring for:

```text
SSH
sudo
Authentication
User Changes
Group Changes
Critical Files
Processes
Services
Network Activity
File Integrity
Audit Events
```

This creates a practical SOC environment.

---

# 41. Practical Lab — SSH Brute-Force Detection

## Objective

Detect repeated SSH authentication failures.

### Generate controlled failed logins

Use your isolated Linux VM.

### Identify events

Search:

```text
/var/log/auth.log
```

or:

```text
journalctl
```

### Record:

```text
Source IP
Username
Timestamp
Failure Count
Successful Login
```

### Build detection:

```text
Multiple SSH Failures
+
Same Source
+
Short Time Window
```

---

# 42. Practical Lab — Successful SSH Investigation

Generate a legitimate SSH login.

Record:

```text
User
Source IP
Timestamp
Host
Authentication Method
```

Then inspect activity immediately afterward:

```text
who
w
last
journalctl
```

Goal:

```text
Login
 ↓
Session
 ↓
Commands
 ↓
Privilege Use
 ↓
Network Activity
```

---

# 43. Practical Lab — Sudo Monitoring

Perform controlled administrative activity.

Observe:

```text
sudo
```

telemetry.

Document:

```text
User
Command
Timestamp
Host
Result
```

Then identify what normal sudo activity looks like.

---

# 44. Practical Lab — User Creation

Inside the isolated lab:

```text
Create Test User
        ↓
Observe Logs
        ↓
Identify Event
        ↓
Check Groups
        ↓
Remove Test User
```

Document:

```text
Before
Event
After
Detection
Evidence
```

---

# 45. Practical Lab — Cron Monitoring

Create a harmless scheduled task in the isolated lab.

Observe:

```text
Cron Configuration
Execution
Log
```

Document:

```text
User
Schedule
Command
File
Execution Time
```

Then remove the task.

---

# 46. Practical Lab — File Integrity

Monitor:

```text
/etc/passwd
/etc/sudoers
/etc/ssh/
```

Make a controlled change.

Observe:

```text
File Changed
 ↓
Hash / Metadata
 ↓
Wazuh Alert
```

Document:

```text
File
Change
User
Timestamp
Detection
```

---

# 47. Practical Lab — Suspicious Network Connection

Create a harmless test connection from a controlled process.

Identify:

```text
Process
PID
User
Destination
Port
```

Use:

```text
ss
lsof
```

Then correlate the connection with process telemetry.

---

# 48. Linux Attack Chain Monitoring

A useful advanced scenario:

```text
SSH Brute Force
      ↓
Successful Login
      ↓
Privilege Escalation
      ↓
Suspicious Process
      ↓
Persistence
      ↓
Outbound Connection
```

Your goal is to reconstruct this timeline from telemetry.

---

# 49. Linux Investigation Checklist

## Identity

```text
Who?
Which account?
Privileged?
Expected?
```

## Authentication

```text
SSH?
sudo?
su?
Failed attempts?
Successful login?
```

## Process

```text
What executed?
Who owns it?
Parent?
Command?
Binary?
```

## Persistence

```text
Cron?
Systemd?
SSH Keys?
SUID?
Startup files?
```

## Network

```text
Destination?
Port?
Process?
User?
```

## Files

```text
What changed?
Who changed it?
When?
Hash?
Permissions?
```

---

# 50. Linux Detection Mapping

| Detection             | Primary Source             |
| --------------------- | -------------------------- |
| SSH Brute Force       | auth.log / journal         |
| Successful SSH Login  | auth.log / journal         |
| Suspicious sudo       | auth.log / auditd          |
| Account Creation      | Account logs / auditd      |
| Privilege Change      | auditd                     |
| Suspicious Process    | Process telemetry / auditd |
| New Service           | systemd                    |
| Cron Persistence      | cron / FIM                 |
| SSH Key Persistence   | FIM / auditd               |
| Sensitive File Change | FIM / auditd               |
| SUID Change           | FIM                        |
| Suspicious Connection | Network telemetry          |
| Malware               | EDR / FIM / process        |
| Configuration Change  | auditd / FIM               |

---

# 51. Common Linux Monitoring Blind Spots

```text
No centralized logging
Missing SSH telemetry
No auditd
No file integrity monitoring
Weak sudo visibility
No process telemetry
No network visibility
Poor log retention
Unmonitored privileged accounts
Unmonitored cloud Linux instances
```

These gaps reduce detection capability.

---

# 52. Monitoring Baseline

Establish normal behavior.

Example:

```text
Normal:
admin connects through SSH
from corporate IP
during working hours.
```

Anomaly:

```text
admin
 ↓
unknown IP
 ↓
03:00 AM
 ↓
sudo
 ↓
new service
```

The combined behavior deserves investigation.

---

# 53. Evidence Collection

For each investigation, document:

```text
Hostname
IP
Username
Timestamp
Source IP
Event
Process
Command
File
Hash
Network Connection
Detection Rule
Screenshot
Conclusion
```

This creates professional SOC documentation.

---

# 54. Portfolio Structure

Recommended practical structure:

```text
05-Linux-Monitoring.md

Labs/
│
├── 01-SSH-Brute-Force/
│   ├── README.md
│   ├── Evidence/
│   └── Report.md
│
├── 02-SSH-Login-Investigation/
│
├── 03-Sudo-Monitoring/
│
├── 04-User-Account-Monitoring/
│
├── 05-Cron-Monitoring/
│
├── 06-File-Integrity-Monitoring/
│
├── 07-Process-Monitoring/
│
└── 08-Network-Connection-Investigation/
```

---

# 55. Interview Questions

### Fundamentals

1. Where are Linux logs commonly stored?
2. What is `/var/log/auth.log`?
3. What is `journalctl`?
4. What is `auditd`?
5. How do you investigate SSH brute force?
6. How do you monitor sudo activity?
7. How can Linux persistence be detected?
8. What is SUID?
9. How do you investigate a suspicious process?
10. How do you monitor Linux file changes?

### Scenario

> **You receive an alert that a Linux server experienced 50 failed SSH logins followed by a successful root login. What do you investigate?**

Approach:

```text
Failed Authentication
        ↓
Source IP
        ↓
Target Account
        ↓
Successful Login
        ↓
Session
        ↓
sudo / root activity
        ↓
Processes
        ↓
Files
        ↓
Persistence
        ↓
Network Connections
```

Then determine:

```text
Brute Force?
Credential Compromise?
Legitimate Admin?
Persistence?
Post-Compromise Activity?
```

---

# 56. Key Takeaways

```text
1. Linux systems generate extensive security telemetry.

2. Authentication logs are critical for SOC investigations.

3. SSH is one of the highest-value Linux monitoring areas.

4. sudo and privileged activity require careful monitoring.

5. systemd provides centralized logging through journald.

6. auditd can provide deeper security auditing.

7. Processes should be analyzed using parent-child relationships.

8. Cron and systemd can be abused for persistence.

9. SSH keys can provide persistent access.

10. File integrity monitoring helps detect unauthorized changes.

11. Network connections should be correlated with processes and users.

12. SUID changes can indicate privilege-escalation risk.

13. Wazuh can centralize Linux telemetry.

14. Baselines help distinguish legitimate administration from anomalies.

15. The goal is to reconstruct activity into a security timeline.
```

---

# 57. Final Mental Model

```text
                    LINUX SYSTEM
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
 Authentication       Processes         Files
        │                │                │
 SSH / sudo          Process Tree       FIM
        │                │                │
        └────────────────┼────────────────┘
                         ↓
                 journald / auditd
                         ↓
                    Wazuh Agent
                         ↓
                  Wazuh Manager
                         ↓
                       SIEM
                         ↓
                    Correlation
                         ↓
                     Detection
                         ↓
                       Alert
                         ↓
                 SOC Investigation
                         ↓
                     Timeline
                         ↓
                      Report
```

> **Linux monitoring is the ability to turn authentication, process, file, service, privilege, and network telemetry into a coherent security timeline.**
