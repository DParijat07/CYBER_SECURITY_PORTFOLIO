# 08 — Authentication Monitoring

## 1. Purpose

Authentication monitoring is the process of observing and analyzing login-related activity on a Linux system.

In this lab, authentication monitoring is performed on an **Ubuntu 22.04 LTS Linux endpoint** connected to a **Wazuh Server through the Wazuh Agent**.

The purpose of this documentation is to learn how a SOC analyst can:

* Monitor successful and failed logins.
* Identify suspicious authentication activity.
* Review SSH login events.
* Monitor privileged access through `sudo`.
* Correlate authentication events with local Linux logs.
* Validate authentication alerts in the Wazuh Dashboard.
* Document authentication-related security events.

---

## 2. Lab Environment

| Component                | Details                              |
| ------------------------ | ------------------------------------ |
| Operating System         | Ubuntu 22.04 LTS                     |
| Architecture             | 64-bit x86_64                        |
| Virtualization           | VMware Workstation Player            |
| Endpoint Role            | Linux Security Monitoring Endpoint   |
| Security Agent           | Wazuh Agent                          |
| Central Platform         | Wazuh Manager, Indexer and Dashboard |
| Main Log File            | `/var/log/auth.log`                  |
| Additional Log Source    | `systemd-journald`                   |
| Main Protocol Monitored  | SSH                                  |
| Main Privileged Activity | `sudo`                               |

### Authentication Monitoring Flow

Ubuntu Linux Endpoint
→ Authentication Event
→ Linux Authentication Log
→ Wazuh Agent
→ Wazuh Manager
→ Wazuh Detection Engine
→ Wazuh Alert
→ Wazuh Dashboard
→ SOC Analyst Investigation

---

## 3. What Is Authentication?

Authentication is the process of verifying the identity of a user or system.

Examples include:

* Entering a username and password.
* Logging in through SSH.
* Using an SSH key.
* Authenticating before executing a privileged command.
* Opening a local Linux session.

### Example

A user attempts to log in to Ubuntu through SSH.

```
Username: parijat
Password: ********
```

The Linux system checks whether the supplied credentials are valid.

Possible results include:

* Authentication successful.
* Authentication failed.
* Invalid username.
* Account locked.
* Authentication denied by policy.

---

## 4. Authentication vs Authorization

Authentication and authorization are different concepts.

| Concept        | Meaning                         | Example                       |
| -------------- | ------------------------------- | ----------------------------- |
| Authentication | Verifies who the user is        | User logs in with a password  |
| Authorization  | Determines what the user can do | User is allowed to run `sudo` |

### Example

A user successfully logs in to Ubuntu.

This confirms authentication.

The same user then executes:

```bash
sudo whoami
```

The system checks whether the user is authorized to perform the privileged action.

---

## 5. Why Authentication Monitoring Matters in a SOC

Authentication monitoring helps a SOC analyst identify:

* Repeated failed login attempts.
* Unauthorized login attempts.
* Login attempts against invalid usernames.
* Successful logins after multiple failures.
* Unexpected privileged access.
* Suspicious login sources.
* Unexpected account activity.
* Possible credential compromise.
* Unauthorized access to Linux systems.

Authentication events are important because attackers may need to authenticate before accessing a system or performing privileged actions.

A single failed login is not automatically malicious. The analyst must review the event together with its context.

---

## 6. Linux Authentication Log Sources

### 6.1 `/var/log/auth.log`

On Ubuntu, authentication and authorization-related events are commonly recorded in:

```
/var/log/auth.log
```

This file may contain:

* SSH login attempts.
* Successful logins.
* Failed password attempts.
* Invalid users.
* `sudo` activity.
* Session opening and closing.
* Account-related activity.
* Authentication service messages.

View the latest entries:

```bash
sudo tail -n 50 /var/log/auth.log
```

Monitor the file in real time:

```bash
sudo tail -f /var/log/auth.log
```

---

### 6.2 systemd-journald

Ubuntu also records system events in the systemd journal.

View recent journal entries:

```bash
sudo journalctl --since "10 minutes ago"
```

View SSH-related journal entries:

```bash
sudo journalctl -u ssh --no-pager
```

Follow new journal events:

```bash
sudo journalctl -f
```

---

### 6.3 SSH Logs

SSH authentication events may include:

* Successful password authentication.
* Failed password authentication.
* Invalid usernames.
* Public-key authentication.
* Connection attempts.
* Session opening.
* Session closing.

SSH events are especially important because SSH is commonly used for remote Linux administration.

---

### 6.4 Sudo Logs

The `sudo` command is used to execute commands with elevated privileges.

Search for `sudo` activity:

```bash
sudo grep "sudo:" /var/log/auth.log
```

Example command:

```bash
sudo whoami
```

Expected output:

```text
root
```

The command may generate an authentication or authorization-related log entry.

---

### 6.5 Account-Related Logs

Account-related activity may include:

* User creation.
* User deletion.
* Password changes.
* Group membership changes.
* Account locking.
* Account unlocking.
* Changes to account permissions.

These events should be reviewed carefully because account changes can affect system access.

---

## 7. Important Authentication Event Categories

### 7.1 Failed Login

A user attempts to log in but authentication fails.

Example search pattern:

```
Failed password
```

Possible reasons include:

* Incorrect password.
* User mistake.
* Expired credentials.
* Unauthorized login attempt.
* Automated password guessing.

A single failed login is not automatically malicious.

---

### 7.2 Successful Login

A user successfully authenticates.

Example search pattern:

```
Accepted
```

A successful login should be reviewed in context.

Questions to ask:

* Was the login expected?
* Was the username correct?
* Was the source IP expected?
* Was the login during normal working hours?
* Were there previous failed attempts?

---

### 7.3 Invalid User

An authentication attempt is made using a username that does not exist on the system.

Search for invalid users:

```bash
sudo grep "Invalid user" /var/log/auth.log
```

Possible explanations include:

* Typing mistake.
* Misconfigured automation.
* Unauthorized login attempt.
* Username enumeration.
* Password-guessing activity.

---

### 7.4 Root Login

A root login provides direct administrative access.

Root authentication should be reviewed carefully because the root account has extensive privileges.

Questions to ask:

* Was root access expected?
* Was it performed locally or remotely?
* Was the source IP trusted?
* Was the activity part of maintenance?
* Were other suspicious events observed?

---

### 7.5 Sudo Use

A user authenticates or uses authorization to execute a privileged command.

Example:

```bash
sudo whoami
```

Important investigation details include:

* Username.
* Command executed.
* Time of execution.
* Whether the user normally requires privileged access.
* Whether the command was expected.

---

### 7.6 Session Opened and Closed

Linux may record when a user session starts and ends.

Session events help the analyst understand:

* When the user accessed the system.
* How long the session remained active.
* Whether a session was properly closed.
* Whether multiple sessions existed.

---

### 7.7 Password Changes

Password changes may be legitimate or suspicious.

Questions to ask:

* Who changed the password?
* Which account was affected?
* Was the change expected?
* Was it performed after a suspicious login?
* Was the account a privileged account?

---

### 7.8 Account Changes

Account changes may include:

* Creating a user.
* Deleting a user.
* Adding a user to a group.
* Removing a user from a group.
* Locking an account.
* Unlocking an account.

These events should be documented because they may change access permissions.

---

### 7.9 SSH Key Authentication

Some Linux systems use SSH keys instead of passwords.

SSH key authentication may appear as a successful SSH authentication event.

The analyst should record:

* Username.
* Authentication method.
* Source IP.
* Time.
* Whether the key-based login was expected.

---

## 8. Useful Authentication Monitoring Commands

### View Recent Authentication Logs

```bash
sudo tail -n 50 /var/log/auth.log
```

### Monitor Authentication Logs in Real Time

```bash
sudo tail -f /var/log/auth.log
```

### Search Failed Password Attempts

```bash
sudo grep "Failed password" /var/log/auth.log
```

### Search Successful Authentication

```bash
sudo grep "Accepted" /var/log/auth.log
```

### Search Invalid Users

```bash
sudo grep "Invalid user" /var/log/auth.log
```

### Search Sudo Activity

```bash
sudo grep "sudo:" /var/log/auth.log
```

### View SSH Journal Events

```bash
sudo journalctl -u ssh --no-pager
```

### View Recent Journal Activity

```bash
sudo journalctl --since "10 minutes ago"
```

### View Previous Login History

```bash
last
```

The `last` command displays previous successful login sessions.

---

### View Failed Login History

```bash
sudo lastb
```

The `lastb` command reads failed login records.

It may require:

* `sudo` permissions.
* The `/var/log/btmp` file.
* The file to be present and readable.

If the command does not return information, record the result as part of troubleshooting.

---

### View Currently Logged-In Users

```bash
who
```

### View Logged-In Users and Activity

```bash
w
```

### View Current User Identity

```bash
id
```

---

## 9. Authentication Monitoring Scope

This beginner lab focuses on the following authentication activities:

| Monitoring Area            | Example                          |
| -------------------------- | -------------------------------- |
| Failed SSH login           | Incorrect password               |
| Successful SSH login       | Valid password or SSH key        |
| Invalid username           | Login attempt using unknown user |
| Sudo activity              | `sudo whoami`                    |
| Session activity           | Login and logout                 |
| Login history              | `last`                           |
| Failed login history       | `lastb`                          |
| Current sessions           | `who` and `w`                    |
| Account activity           | Controlled test account changes  |
| Authentication correlation | Failed login followed by success |

---

## 10. Wazuh Authentication Monitoring

The Wazuh Agent collects selected Linux log sources and sends the information to the Wazuh Manager.

The Wazuh Manager processes the collected events and checks them against available detection rules.

### Wazuh Authentication Monitoring Flow

```
SSH Login Attempt
        |
        v
Linux Authentication Service
        |
        v
/var/log/auth.log or systemd journal
        |
        v
Wazuh Agent
        |
        v
Wazuh Manager
        |
        v
Detection Rules
        |
        v
Wazuh Alert
        |
        v
Wazuh Dashboard
        |
        v
SOC Analyst
```

Authentication monitoring depends on three important activities:

1. The Linux system must generate the event.
2. The Wazuh Agent must collect the event.
3. Wazuh must process and display the event correctly.

---

## 11. Authentication Collection Configuration Reference

Authentication log collection is configured in the Wazuh Agent configuration file:

```
/var/ossec/etc/ossec.conf
```

The Ubuntu authentication log is commonly collected through a `localfile` configuration.

Example:

```xml
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/auth.log</location>
</localfile>
```

Before making changes, check the existing configuration:

```bash
sudo grep -n "auth.log" /var/ossec/etc/ossec.conf
```

Do not add duplicate configuration entries without checking the existing file.

Create a backup before editing:

```bash
sudo cp /var/ossec/etc/ossec.conf /var/ossec/etc/ossec.conf.backup
```

After a valid configuration change, restart the agent:

```bash
sudo systemctl restart wazuh-agent
```

Check the agent status:

```bash
sudo systemctl status wazuh-agent
```

The detailed collection configuration is covered in:

* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`

---

## 12. Basic Authentication Monitoring Preparation

Before testing authentication activity, confirm that:

* The Ubuntu VM is running.
* The Wazuh Agent is installed.
* The Wazuh Agent is active.
* The Ubuntu endpoint is visible in the Wazuh Dashboard.
* SSH is available for the controlled test.
* The authentication log exists.
* The test is performed only against the user's own lab system.

Check the Wazuh Agent:

```bash
sudo systemctl is-active wazuh-agent
```

Expected result:

```text
active
```

Check the authentication log:

```bash
sudo test -f /var/log/auth.log && echo "auth.log exists"
```

Check recent authentication events:

```bash
sudo tail -n 20 /var/log/auth.log
```

---

## 13. Controlled Authentication Test 1 — Failed SSH Login

### Objective

Generate one controlled failed SSH authentication event.

### Safety Rule

Perform only one or a small number of intentional failed attempts.

Do not perform password guessing, brute-force testing, or repeated automated login attempts.

### Procedure

1. Open the Ubuntu terminal.
2. Identify the Ubuntu VM IP address.
3. From an authorized lab machine, start an SSH connection.
4. Use a valid test username.
5. Enter an incorrect password once.
6. Close the connection.
7. Review the authentication log.

Search for failed authentication:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Review the latest entries:

```bash
sudo tail -n 30 /var/log/auth.log
```

### Record the Following Details

* Date and time.
* Username.
* Source IP address.
* Destination Ubuntu endpoint.
* Authentication result.
* Reason for failure, if visible.
* Related Wazuh alert, if generated.

---

## 14. Controlled Authentication Test 2 — Successful SSH Login

### Objective

Generate one successful SSH authentication event.

### Procedure

1. Start an SSH connection to the Ubuntu VM.
2. Use an authorized test account.
3. Enter the correct password or use an authorized SSH key.
4. Confirm that the login succeeds.
5. Exit the SSH session.

Search for successful authentication:

```bash
sudo grep "Accepted" /var/log/auth.log
```

Review recent entries:

```bash
sudo tail -n 30 /var/log/auth.log
```

### Record the Following Details

* Date and time.
* Username.
* Source IP address.
* Authentication method.
* Destination endpoint.
* Session start time.
* Whether the login was expected.
* Related Wazuh alert, if generated.

---

## 15. Controlled Authentication Test 3 — Sudo Activity

### Objective

Generate a controlled privileged activity event.

### Procedure

Run:

```bash
sudo whoami
```

Expected output:

```text
root
```

Search for the related activity:

```bash
sudo grep "sudo:" /var/log/auth.log
```

Review the latest authentication log entries:

```bash
sudo tail -n 30 /var/log/auth.log
```

### Record the Following Details

* Date and time.
* Username.
* Command executed.
* Result of the command.
* Whether the activity was expected.
* Related Wazuh alert, if generated.

Do not execute destructive commands during this test.

---

## 16. Controlled Authentication Test 4 — Session Information

### Objective

Review current and previous Linux sessions.

### View Current Sessions

```bash
who
```

```bash
w
```

### View Current User Information

```bash
id
```

### View Previous Login History

```bash
last
```

### View Failed Login History

```bash
sudo lastb
```

### Record the Following Details

* Current logged-in username.
* Login terminal or session.
* Login time.
* Source information, if available.
* Previous login sessions.
* Failed login records, if available.

---

## 17. Optional Controlled Authentication Test 5 — Test Account Activity

This test is optional.

Perform it only if a separate test account is available and the activity is authorized.

Do not modify the main administrator account.

Possible safe activities include:

* Creating a temporary test account.
* Reviewing the account.
* Removing the temporary test account after the test.

Example:

```bash
sudo adduser labtest
```

Review the account:

```bash
id labtest
```

After completing the test, remove the temporary account only if it is no longer required:

```bash
sudo deluser labtest
```

Review authentication and account-related logs:

```bash
sudo tail -n 50 /var/log/auth.log
```

Record:

* Account name.
* Account creation time.
* Account removal time.
* Commands executed.
* Whether the activity was expected.
* Related Wazuh event or alert.

If the account test is not required, skip it and document:

```
Test skipped because no temporary account was required.
```

---

## 18. Exact Wazuh Authentication Validation Procedure

### Step 1 — Check the Wazuh Agent

Run on Ubuntu:

```bash
sudo systemctl is-active wazuh-agent
```

The expected result is:

```text
active
```

If the agent is not active, start it:

```bash
sudo systemctl start wazuh-agent
```

Check the service:

```bash
sudo systemctl status wazuh-agent
```

---

### Step 2 — Check the Local Authentication Log

Search for failed authentication:

```bash
sudo grep "Failed password" /var/log/auth.log
```

Search for successful authentication:

```bash
sudo grep "Accepted" /var/log/auth.log
```

Search for invalid users:

```bash
sudo grep "Invalid user" /var/log/auth.log
```

Search for privileged activity:

```bash
sudo grep "sudo:" /var/log/auth.log
```

---

### Step 3 — Check the Wazuh Agent Log

Review the latest Wazuh Agent log entries:

```bash
sudo tail -n 50 /var/ossec/logs/ossec.log
```

Look for signs of:

* Agent communication.
* Log collection.
* Configuration problems.
* Permission problems.
* Connection errors.

---

### Step 4 — Open the Wazuh Dashboard

1. Open the Wazuh Dashboard.
2. Navigate to the security events or alerts section.
3. Select the Ubuntu monitoring agent.
4. Set a recent time range, such as **Last 15 minutes**.
5. Search for authentication-related events.
6. Locate the event generated during the controlled test.
7. Open the event details.

---

### Step 5 — Record Alert or Event Details

Record the following information:

* Event timestamp.
* Wazuh agent name.
* Hostname.
* Rule ID, if displayed.
* Rule description.
* Rule level, if displayed.
* Source IP address.
* Username.
* Authentication result.
* Authentication method.
* Event data.
* Related process or service.
* Analyst interpretation.

Do not guess a rule ID if it is not displayed.

---

### Step 6 — Compare Wazuh With the Local Log

Compare the Wazuh event with the Ubuntu authentication log.

Check:

* Whether the timestamps are similar.
* Whether the username matches.
* Whether the source IP matches.
* Whether the authentication result matches.
* Whether the event description is correct.
* Whether any important information is missing.

---

## 19. Authentication Analysis Questions

For every authentication event, ask:

### Identity

* Which username was involved?
* Was the account valid?
* Was the account privileged?

### Time

* When did the event occur?
* Was it during expected activity hours?
* Were there multiple events close together?

### Source

* Which IP address or system initiated the activity?
* Was the source expected?
* Was the source part of the lab environment?

### Result

* Was authentication successful?
* Was authentication unsuccessful?
* Was the username invalid?
* Was access denied?

### Context

* Was the activity expected?
* Was there a maintenance task?
* Was there a previous failed login?
* Was there a later successful login?
* Was `sudo` used after the login?
* Was a suspicious process started after authentication?

### Impact

* Did the event provide access?
* Did the user obtain elevated privileges?
* Did the event affect another account?
* Is further investigation required?

---

## 20. Basic Authentication Detection Patterns

The following patterns may require additional investigation.

### 20.1 Repeated Failed Logins

Example pattern:

```
Failed login
Failed login
Failed login
```

Possible explanations:

* User forgot a password.
* Incorrect configuration.
* Unauthorized login attempts.
* Password-guessing activity.

---

### 20.2 Failed Login Followed by Success

Example pattern:

```
Failed login
Failed login
Successful login
```

This pattern deserves attention because it may indicate:

* A user eventually entered the correct password.
* A legitimate user made typing mistakes.
* An attacker successfully guessed or obtained credentials.

The analyst must review the username, source IP, time and surrounding events.

---

### 20.3 Invalid Username Attempts

Example pattern:

```
Invalid user admin
Invalid user test
Invalid user guest
```

Possible explanations:

* Misconfigured automation.
* Username enumeration.
* Unauthorized access attempts.

---

### 20.4 Unexpected Privileged Activity

Example pattern:

```
Successful login
        |
        v
sudo command
        |
        v
Privileged system activity
```

The analyst should verify whether the user was authorized to perform the activity.

---

### 20.5 Unexpected Account Activity

Examples include:

* New user creation.
* Unexpected password change.
* Unexpected group membership change.
* Account unlocking.
* Account deletion.

Account-related activity should be correlated with the user, time and change request.

---

## 21. False Positives

A false positive occurs when an event appears suspicious but is later confirmed to be legitimate.

Examples:

* A user entered the wrong password.
* An administrator logged in during maintenance.
* A test account was intentionally created.
* A monitoring tool used an invalid credential.
* A user ran `sudo` for a valid administrative task.

When an event is confirmed as legitimate, document the reason.

Example:

```
Authentication event reviewed.
The failed login was caused by an intentional lab test.
No unauthorized activity was identified.
```

---

## 22. Basic Authentication Investigation Record

Use the following template for each important authentication event.

### Authentication Event Record

| Field                 | Value |
| --------------------- | ----- |
| Event ID              |       |
| Date                  |       |
| Time                  |       |
| Hostname              |       |
| Wazuh Agent           |       |
| Username              |       |
| Source IP             |       |
| Authentication Type   |       |
| Authentication Result |       |
| Event Description     |       |
| Rule ID               |       |
| Rule Level            |       |
| Related Process       |       |
| Related Command       |       |
| Expected Activity?    |       |
| Analyst Decision      |       |
| Evidence Location     |       |
| Additional Notes      |       |

---

## 23. Example Authentication Investigation

### Scenario

A failed SSH login is followed by a successful SSH login from the same source IP.

### Investigation

1. Review the failed login event.
2. Record the username.
3. Record the source IP address.
4. Record the timestamp.
5. Review the successful login event.
6. Compare the usernames.
7. Compare the source IP addresses.
8. Check whether `sudo` was used afterward.
9. Check whether suspicious processes were started.
10. Decide whether the activity was expected.

### Example Analyst Conclusion

```
A failed SSH authentication was followed by a successful login
for the same authorized lab account. The source IP belonged to
the controlled lab environment. A subsequent sudo command was
intentionally executed as part of the authentication monitoring
test. No unauthorized activity was identified.
```

---

## 24. Evidence Requirements

Capture evidence for the authentication monitoring lab.

Recommended evidence includes:

* Screenshot of the Ubuntu VM.
* Screenshot of the Wazuh Agent status.
* Screenshot of `/var/log/auth.log`.
* Screenshot of a failed authentication event.
* Screenshot of a successful authentication event.
* Screenshot of `sudo` activity.
* Screenshot of `last` output.
* Screenshot of `who` or `w` output.
* Screenshot of the Wazuh Dashboard.
* Screenshot of the Wazuh event details.
* Authentication investigation record.
* Final lab report.

Store evidence under:

```
Evidence/
```

Use clear filenames, for example:

```
evidence-01-wazuh-agent-active.png
evidence-02-failed-ssh-login.png
evidence-03-successful-ssh-login.png
evidence-04-sudo-activity.png
evidence-05-wazuh-authentication-alert.png
evidence-06-authentication-investigation-record.md
```

Do not capture or publish real passwords, private SSH keys or sensitive personal information.

---

## 25. Basic Troubleshooting

### Problem 1 — `/var/log/auth.log` Does Not Exist

Check the file:

```bash
ls -l /var/log/auth.log
```

Check the journal:

```bash
sudo journalctl --since "10 minutes ago"
```

Check SSH events:

```bash
sudo journalctl -u ssh --no-pager
```

---

### Problem 2 — No Authentication Event Appears

Check whether the test was performed correctly.

Review:

```bash
sudo tail -n 50 /var/log/auth.log
```

Check SSH status:

```bash
sudo systemctl status ssh
```

Check the Wazuh Agent:

```bash
sudo systemctl is-active wazuh-agent
```

---

### Problem 3 — Wazuh Agent Is Not Active

Check the service:

```bash
sudo systemctl status wazuh-agent
```

Start the service:

```bash
sudo systemctl start wazuh-agent
```

Review the agent log:

```bash
sudo tail -n 50 /var/ossec/logs/ossec.log
```

---

### Problem 4 — Local Event Exists but Wazuh Shows Nothing

Check:

* The Wazuh Agent is active.
* The Ubuntu endpoint is connected.
* `/var/log/auth.log` is configured for collection.
* The Wazuh Agent configuration has no errors.
* The Dashboard time range includes the test time.
* The correct Ubuntu agent is selected.

Restart the agent after a valid configuration change:

```bash
sudo systemctl restart wazuh-agent
```

---

### Problem 5 — `lastb` Does Not Work

Check the command:

```bash
sudo lastb
```

Possible reasons include:

* Missing `/var/log/btmp`.
* Insufficient permissions.
* No failed login records.
* The system does not currently maintain the file.

Record the result in the troubleshooting evidence.

---

## 26. Authentication Monitoring Checklist

* [ ] Ubuntu 22.04 LTS endpoint is running.
* [ ] Wazuh Agent is installed.
* [ ] Wazuh Agent is active.
* [ ] Ubuntu endpoint is visible in Wazuh Dashboard.
* [ ] `/var/log/auth.log` exists.
* [ ] Recent authentication logs were reviewed.
* [ ] One controlled failed SSH login was tested.
* [ ] One controlled successful SSH login was tested.
* [ ] One controlled `sudo` command was tested.
* [ ] Current sessions were reviewed using `who` or `w`.
* [ ] Login history was reviewed using `last`.
* [ ] Failed login history was reviewed using `lastb`, if available.
* [ ] Local logs were compared with Wazuh events.
* [ ] Authentication event details were recorded.
* [ ] Evidence was saved.
* [ ] Authentication investigation record was completed.

---

## 27. Authentication Monitoring Completion Criteria

This documentation is complete when:

1. Authentication concepts are understood.
2. Ubuntu authentication log sources are identified.
3. SSH authentication events are generated safely.
4. Successful and failed authentication events are reviewed.
5. Sudo activity is observed.
6. Current and previous sessions are checked.
7. Wazuh Agent collection is validated.
8. Authentication events are located in the Wazuh Dashboard.
9. Local logs are compared with Wazuh events.
10. At least one authentication investigation record is completed.
11. Evidence is stored in the lab repository.
12. The results are explained in beginner-friendly SOC language.

---

## 28. SOC Learning Outcome

After completing this activity, the learner should be able to explain:

* What authentication means.
* The difference between authentication and authorization.
* Why authentication events matter in a SOC.
* Where Ubuntu stores authentication logs.
* How SSH login activity is recorded.
* How `sudo` activity is monitored.
* How to identify failed and successful logins.
* How to use `last`, `lastb`, `who` and `w`.
* How Wazuh collects authentication events.
* How to validate authentication events in the Wazuh Dashboard.
* How to correlate local Linux logs with Wazuh alerts.
* How to document an authentication investigation.

---

## 29. Success Criteria

The lab is successful when the learner can:

* Generate a controlled failed SSH authentication event.
* Generate a controlled successful SSH authentication event.
* Generate a controlled `sudo` activity event.
* Locate the events in `/var/log/auth.log`.
* Confirm that the Wazuh Agent is active.
* Locate the related event or alert in Wazuh.
* Record the username, timestamp and source IP.
* Explain whether the activity was expected.
* Identify the difference between an event and a security alert.
* Produce a clear authentication monitoring evidence package.

---

## 30. Related Documentation

* `01-Lab-Objective.md`
* `02-Lab-Setup.md`
* `03-Linux-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
* `06-Detection-Rules.md`
* `07-Alert-Analysis.md`
* `09-Process-Monitoring.md`
* `10-Shell-Monitoring.md`
* `11-Incident-Investigation.md`
* `12-Incident-Response.md`
* `13-Scenarios.md`
* `14-Troubleshooting.md`
* `15-Lessons-Learned.md`
