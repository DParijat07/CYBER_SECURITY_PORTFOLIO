# Identity and Access Monitoring

## 1. Introduction

Identity and Access Monitoring is the process of collecting, analyzing, and correlating authentication, authorization, account, privilege, and access-related telemetry to detect unauthorized access, credential compromise, privilege abuse, account takeover, and other identity-based threats.

Identity is one of the most important security monitoring areas because attackers frequently target user accounts before attempting to compromise systems or data.

A typical identity monitoring flow is:

User
  ↓
Authentication
  ↓
Identity Provider / Active Directory
  ↓
Authorization
  ↓
Resource Access
  ↓
Logs
  ↓
SIEM
  ↓
SOC Analyst

---

## 2. Why Identity Monitoring Is Important

Attackers may compromise legitimate credentials and use them to operate inside an environment.

This creates a major challenge for defenders:

> Malicious activity can sometimes look like legitimate user activity.

Identity monitoring helps detect:

- Brute-force attacks
- Password spraying
- Credential stuffing
- Account takeover
- Impossible travel
- Suspicious logins
- Privilege escalation
- Unauthorized administrative activity
- New account creation
- MFA abuse
- Authentication anomalies
- Suspicious service-account activity

---

## 3. Objectives of Identity Monitoring

The main objectives are:

1. Detect unauthorized authentication
2. Identify compromised accounts
3. Detect brute-force attacks
4. Detect password spraying
5. Detect privilege abuse
6. Monitor administrative accounts
7. Detect suspicious account creation
8. Monitor MFA activity
9. Detect abnormal access patterns
10. Correlate identity activity with endpoint and network telemetry

---

## 4. Identity Monitoring Sources

Important identity telemetry sources include:

- Active Directory
- Windows Security Event Logs
- Microsoft Entra ID
- Identity Providers
- VPN authentication systems
- SSO platforms
- MFA systems
- Linux authentication logs
- Cloud IAM systems
- Application authentication logs
- Privileged Access Management systems
- SIEM platforms

Common information includes:

Timestamp
Username
Source IP
Destination
Authentication Method
Authentication Result
Device
Location
Application
Privilege Level
Session
MFA Result

---

## 5. Authentication Monitoring

Authentication determines whether an identity can prove who they are.

Common authentication methods include:

- Password
- MFA
- Smart card
- Certificate
- Security key
- Biometrics
- SSO
- Kerberos
- OAuth
- SAML

SOC analysts should monitor both successful and failed authentication events.

Example:

10:01 → Failed login
10:02 → Failed login
10:03 → Failed login
10:04 → Successful login

This sequence may indicate a successful brute-force or password-guessing attempt.

---

## 6. Successful vs Failed Authentication

A single failed authentication is usually normal.

However:

1 failed login

is very different from:

500 failed logins
      ↓
Successful authentication
      ↓
Sensitive resource access

The second pattern should receive significantly more attention.

---

## 7. Windows Authentication Monitoring

Windows environments generate important authentication telemetry.

Common Windows Security Event IDs include:

| Event ID | Description | Security Relevance |
|---|---|---|
| 4624 | Successful logon | Establishes successful authentication |
| 4625 | Failed logon | Brute-force/password-spray investigation |
| 4634 | Logoff | Session analysis |
| 4647 | User initiated logoff | Session analysis |
| 4648 | Explicit credential use | Possible credential abuse |
| 4672 | Special privileges assigned | Privileged account monitoring |
| 4720 | User account created | Account creation monitoring |
| 4722 | User account enabled | Account modification |
| 4724 | Password reset attempt | Account takeover investigation |
| 4728 | Member added to global security-enabled group | Privilege monitoring |
| 4732 | Member added to local security-enabled group | Privilege monitoring |
| 4740 | Account locked out | Brute-force investigation |
| 4768 | Kerberos authentication ticket requested | Authentication monitoring |
| 4769 | Kerberos service ticket requested | Kerberos activity |
| 4771 | Kerberos pre-authentication failed | Password attack investigation |
| 4776 | Domain controller attempted to validate credentials | Credential monitoring |

Event IDs should always be interpreted within context rather than individually.

---

## 8. Linux Authentication Monitoring

Linux systems commonly record authentication activity in:

/var/log/auth.log

or:

/var/log/secure

depending on the distribution.

Monitor for:

Failed password
Accepted password
Accepted publickey
Invalid user
sudo
su
authentication failure

Example:

Failed password for invalid user admin

Repeated events from the same source may indicate reconnaissance or brute-force activity.

---

## 9. Active Directory Monitoring

Active Directory is a major identity infrastructure component in many enterprise environments.

SOC analysts should monitor:

- User creation
- User deletion
- Group membership changes
- Privileged group changes
- Password resets
- Account lockouts
- Kerberos activity
- Authentication failures
- Domain controller activity
- Service account behavior

Particularly sensitive groups include:

Domain Admins
Enterprise Admins
Administrators
Backup Operators
Account Operators

Unauthorized changes to privileged groups should receive high priority.

---

## 10. Brute-Force Detection

Brute-force attacks involve repeated attempts to guess credentials against an account or service.

Example:

Source IP
    ↓
Login Attempt
    ↓
Failure
    ↓
Failure
    ↓
Failure
    ↓
Failure
    ↓
...

A simple detection rule could be:

IF
single source generates
more than 20 failed logins
within 5 minutes

THEN
generate brute-force alert

Severity:

Medium

However, legitimate applications can also generate repeated failures, so context is important.

---

## 11. Password Spraying

Password spraying differs from traditional brute force.

Instead of:

One account
+
Many passwords

the attacker uses:

One common password
+
Many accounts

Example:

user01 → Password123
user02 → Password123
user03 → Password123
user04 → Password123
...

This technique attempts to avoid account lockout controls.

Detection should therefore examine authentication failures across multiple accounts from the same source or infrastructure.

---

## 12. Credential Stuffing

Credential stuffing uses previously leaked username/password combinations.

Typical pattern:

Many accounts
+
Previously compromised credentials
+
Repeated authentication attempts

Indicators may include:

- Large numbers of authentication attempts
- Multiple usernames
- Distributed source IPs
- Unusual geographic locations
- Successful authentication after repeated failures
- Login attempts against multiple applications

---

## 13. Account Lockout Monitoring

Repeated failed authentication can cause account lockouts.

Example:

Failed Login
     ↓
Failed Login
     ↓
Failed Login
     ↓
Account Lockout

Account lockout events can indicate:

- Brute-force activity
- Password spraying
- Stale credentials
- Misconfigured applications
- Scheduled tasks using old passwords
- Compromised systems

The analyst should determine the cause before concluding that an attack occurred.

---

## 14. Privileged Account Monitoring

Privileged accounts require additional monitoring because they can perform high-impact actions.

Monitor:

- Administrative logins
- Privileged group membership
- Privilege assignment
- Administrative commands
- Remote administration
- Service creation
- Security-policy changes
- Account creation

Example:

Normal User
    ↓
Privilege Change
    ↓
Administrator
    ↓
Remote Login
    ↓
Sensitive System Access

This sequence should be investigated.

---

## 15. Suspicious Account Creation

Unexpected account creation can indicate:

- Persistence
- Insider activity
- Administrative error
- Compromise

Example:

New User Created
      ↓
Added to Administrators
      ↓
Remote Login

This should be treated as highly suspicious unless there is a documented business reason.

---

## 16. MFA Monitoring

Multi-factor authentication provides an additional security layer.

SOC teams should monitor:

- MFA failures
- MFA fatigue attempts
- Repeated push notifications
- MFA enrollment changes
- MFA method changes
- Authentication from unusual devices
- MFA success after suspicious login activity

Example:

10 MFA prompts
      ↓
User finally approves
      ↓
Successful login

This may indicate MFA fatigue or push-bombing behavior.

---

## 17. Impossible Travel

Impossible travel detection identifies authentication events that appear geographically impossible within a short period.

Example:

09:00
Location A
      ↓
09:20
Location B

This could indicate:

- Credential compromise
- VPN/proxy usage
- Cloud infrastructure
- Incorrect geolocation
- Legitimate travel

Therefore, impossible travel is an investigation signal rather than automatic proof of compromise.

---

## 18. Unusual Login Detection

Monitor for authentication behavior outside the user's normal baseline.

Examples:

- First login from new country
- First login from new device
- Login outside normal working hours
- Login to unusual application
- Login to sensitive system
- Login using unusual authentication method

Example:

User:
analyst01

Normal:
Corporate workstation
Normal business hours

Observed:
Unknown device
Unusual IP
03:15

This should be investigated.

---

## 19. Service Account Monitoring

Service accounts often have elevated permissions and may operate without interactive users.

Monitor:

- Interactive logins
- Password changes
- Privilege changes
- New authentication sources
- Unusual authentication frequency
- New services using the account

An interactive login by a service account can be suspicious if it is not expected.

---

## 20. Cloud Identity Monitoring

Cloud environments introduce additional identity telemetry.

Monitor:

Cloud login
MFA
IAM changes
Access key usage
Role assumption
Privilege changes
API activity
New credentials
New users
Policy changes

Example:

User
 ↓
Cloud Console Login
 ↓
IAM Policy Change
 ↓
Administrative Privilege
 ↓
Sensitive Resource Access

This sequence requires investigation.

---

## 21. Identity and Endpoint Correlation

Identity events become much more valuable when correlated with endpoint telemetry.

Example:

Successful Login
      ↓
New Process
      ↓
PowerShell
      ↓
Credential Access
      ↓
Outbound Connection

This can indicate that a compromised account is being used on an endpoint.

---

## 22. Identity and Network Correlation

Example:

Suspicious Login
      ↓
VPN Connection
      ↓
Internal Network Access
      ↓
SMB Connections
      ↓
Multiple Internal Hosts

This may indicate lateral movement.

---

## 23. Identity-Based Attack Chain

A simplified attack chain can look like:

Credential Theft
      ↓
Initial Authentication
      ↓
Privilege Escalation
      ↓
Persistence
      ↓
Lateral Movement
      ↓
Sensitive Resource Access
      ↓
Data Exfiltration

Identity monitoring can provide visibility at almost every stage.

---

## 24. SIEM Correlation

Identity telemetry should be integrated into the SIEM.

Example:

Authentication Logs
        +
Endpoint Logs
        +
VPN Logs
        +
Cloud IAM Logs
        +
Network Logs
        ↓
       SIEM
        ↓
Correlation Rules
        ↓
       Alert
        ↓
   SOC Investigation

---

## 25. Detection Rules

### Rule 1 — Brute Force

IF
one source IP produces
more than 20 failed logins
against one account
within 5 minutes

THEN
generate brute-force alert

Severity:

Medium

---

### Rule 2 — Password Spraying

IF
one source IP produces
failed authentication attempts
against many different accounts

THEN
generate password-spraying alert

Severity:

High

---

### Rule 3 — Privileged Group Modification

IF
a user is added to
a privileged security group

AND
no approved change exists

THEN
generate high-priority alert

Severity:

High

---

### Rule 4 — Suspicious Account Creation

IF
new account is created
AND
account receives administrative privileges

THEN
generate critical investigation alert

Severity:

Critical

---

### Rule 5 — Suspicious Service Account Login

IF
service account performs
interactive authentication

THEN
generate investigation alert

Severity:

Medium

---

### Rule 6 — Successful Login After Multiple Failures

IF
multiple failed authentication attempts
are followed by
successful authentication

THEN
generate suspicious authentication alert

Severity:

High

---

## 26. Example SOC Alert

Alert:
Potential Password Spraying Activity

Severity:
High

Source IP:
10.10.20.15

Target Accounts:
user01
user02
user03
user04
user05
user06

Failed Attempts:
42

Time Window:
5 minutes

Authentication Service:
Active Directory

### Analyst Comment

Multiple authentication failures were observed from a single source against several user accounts within a short period. The distribution of targeted accounts is consistent with a potential password-spraying pattern. Source-host activity, authentication history, VPN activity, and successful logins following the failures should be reviewed to determine whether an account was compromised.

---

## 27. SOC Triage Process

### Step 1 — Identify the Identity

Determine:

Username
Account Type
Privilege Level
Department

### Step 2 — Identify the Source

Check:

Source IP
Device
Hostname
Location
VPN
Application

### Step 3 — Analyze Authentication Pattern

Look for:

Failed attempts
Successful attempts
Number of accounts
Time interval
Authentication method

### Step 4 — Check Account History

Determine:

Normal login locations
Normal devices
Normal login times
Previous authentication behavior

### Step 5 — Check Privilege Changes

Look for:

Group membership
Role changes
New privileges
Password reset
MFA changes

### Step 6 — Check Endpoint Activity

Look for:

Process creation
PowerShell
Command execution
Credential access
Remote connections

### Step 7 — Check Network Activity

Look for:

VPN
SMB
RDP
SSH
Internal scanning
Unusual outbound connections

### Step 8 — Determine Impact

Ask:

Was an account compromised?
Was privilege escalated?
Was lateral movement performed?
Were sensitive resources accessed?
Was persistence established?

### Step 9 — Escalate

Confirmed compromise should be escalated according to the organization's incident-response process.

---

## 28. Identity Monitoring Best Practices

Organizations should:

- Monitor authentication events
- Protect privileged accounts
- Enforce MFA
- Monitor privileged group changes
- Monitor service accounts
- Establish login baselines
- Detect password spraying
- Detect brute-force attacks
- Monitor account creation
- Monitor MFA changes
- Integrate identity logs with SIEM
- Correlate identity and endpoint telemetry
- Review privileged access regularly
- Apply least privilege
- Maintain strong identity governance

---

## 29. Identity Monitoring Investigation Checklist

[ ] Identify username
[ ] Identify account type
[ ] Check privilege level
[ ] Identify source IP
[ ] Identify device
[ ] Check geographic location
[ ] Check authentication method
[ ] Review failed logins
[ ] Review successful logins
[ ] Check password spraying indicators
[ ] Check brute-force indicators
[ ] Check account lockouts
[ ] Check MFA events
[ ] Check account changes
[ ] Check privilege changes
[ ] Check group membership changes
[ ] Check service account activity
[ ] Check endpoint activity
[ ] Check VPN activity
[ ] Check network activity
[ ] Determine whether account compromise occurred
[ ] Determine impact
[ ] Assign severity
[ ] Document findings
[ ] Escalate if required

---

## 30. Key Takeaways

Identity monitoring is a fundamental SOC capability because compromised credentials can allow attackers to operate using legitimate access.

A SOC analyst should understand:

- Authentication
- Authorization
- Active Directory
- Identity providers
- Authentication logs
- Brute force
- Password spraying
- Credential stuffing
- Account takeover
- Privileged accounts
- MFA monitoring
- Service accounts
- Account lifecycle
- Cloud IAM
- Identity-based lateral movement

The core investigation model is:

Identity Event
      ↓
Authentication Analysis
      ↓
Account Context
      ↓
Privilege Analysis
      ↓
Endpoint Correlation
      ↓
Network Correlation
      ↓
Behavior Analysis
      ↓
Impact Assessment
      ↓
Incident Response

**Identity monitoring should not focus only on failed logins. The strongest detections come from understanding the complete identity lifecycle: authentication, authorization, privilege changes, resource access, and subsequent endpoint/network behavior.**
