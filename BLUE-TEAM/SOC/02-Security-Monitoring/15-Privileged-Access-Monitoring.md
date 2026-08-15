# Privileged Access Monitoring

## 1. Introduction

Privileged Access Monitoring is the process of monitoring, analyzing, and correlating activities performed by privileged accounts, administrators, service accounts, and other identities with elevated permissions.

Privileged accounts have greater access than standard users. If compromised or misused, they can be used to modify security controls, access sensitive information, create persistence, disable defenses, or move laterally across an environment.

A typical privileged access monitoring workflow is:

User
  ↓
Privileged Authentication
  ↓
Privilege Assignment
  ↓
Administrative Activity
  ↓
Resource Access
  ↓
Logs
  ↓
SIEM
  ↓
SOC Analyst
  ↓
Investigation / Response

---

## 2. What Is Privileged Access?

Privileged access refers to permissions that allow an identity to perform administrative or high-impact operations.

Examples include:

- Creating or deleting users
- Modifying security policies
- Installing software
- Changing firewall rules
- Accessing sensitive databases
- Managing servers
- Changing Active Directory settings
- Modifying cloud IAM policies
- Accessing security infrastructure

Common privileged identities include:

- Domain Administrators
- Local Administrators
- Root
- Cloud Administrators
- Database Administrators
- Security Administrators
- Network Administrators
- Service Accounts
- Emergency / Break-Glass Accounts

---

## 3. Why Privileged Access Monitoring Is Important

Privileged accounts are attractive targets for attackers because they provide broad access.

A compromised privileged account can potentially allow an attacker to:

- Disable security controls
- Create new accounts
- Modify permissions
- Access confidential data
- Execute commands remotely
- Establish persistence
- Move laterally
- Deploy malware
- Modify logs
- Change network configuration

Therefore:

> Privileged activity should receive stronger monitoring than ordinary user activity.

---

## 4. Objectives of Privileged Access Monitoring

The main objectives are:

1. Detect unauthorized administrative activity
2. Monitor privileged authentication
3. Detect privilege escalation
4. Monitor privileged group membership
5. Detect suspicious administrative commands
6. Detect unauthorized account creation
7. Monitor service accounts
8. Detect abnormal privileged access
9. Correlate privileged activity with endpoint and network telemetry
10. Reduce the risk of privileged account compromise

---

## 5. Types of Privileged Accounts

### 5.1 Domain Administrator

Domain Administrators have extensive control over an Active Directory domain.

Monitor:

- Domain Admin logins
- Group membership changes
- Remote authentication
- Administrative commands
- Account creation
- Policy changes

---

### 5.2 Local Administrator

Local administrators have administrative privileges on individual systems.

Monitor:

- Interactive logins
- Remote logins
- Local group membership
- Software installation
- Security configuration changes
- PowerShell activity

---

### 5.3 Root Account

Linux root accounts have unrestricted privileges.

Monitor:

- SSH authentication
- sudo usage
- su activity
- Command execution
- Configuration changes
- File modifications

---

### 5.4 Cloud Administrator

Cloud administrators can modify cloud infrastructure and IAM controls.

Monitor:

- Console login
- API activity
- IAM changes
- Role assignments
- Access key creation
- Security group changes
- Storage access

---

### 5.5 Database Administrator

Database administrators can access and modify sensitive data.

Monitor:

- Database logins
- Privilege changes
- SQL queries
- User creation
- Data exports
- Schema changes
- Administrative commands

---

### 5.6 Service Accounts

Service accounts are typically used by applications or services.

Monitor:

- Authentication sources
- Interactive logins
- Password changes
- Privilege changes
- New applications using the account
- Unusual activity

Interactive authentication by a service account can be suspicious if it is not expected.

---

## 6. Privileged Authentication Monitoring

Authentication events involving privileged accounts should receive higher scrutiny.

Example:

Admin Account
     ↓
Successful Login
     ↓
New Device
     ↓
Unusual Location
     ↓
Administrative Activity

This should trigger an investigation.

Important attributes include:

- Username
- Source IP
- Hostname
- Device
- Location
- Authentication method
- Timestamp
- Login type
- Session
- MFA status

---

## 7. Windows Privileged Access Monitoring

Windows Security Event Logs provide important information about privileged activity.

Important Event IDs include:

| Event ID | Description | Monitoring Purpose |
|---|---|---|
| 4624 | Successful logon | Privileged authentication |
| 4625 | Failed logon | Brute-force investigation |
| 4648 | Explicit credential use | Credential abuse |
| 4672 | Special privileges assigned | Privileged session detection |
| 4688 | Process creation | Administrative command analysis |
| 4720 | User account created | Persistence detection |
| 4728 | Member added to global security group | Privilege escalation |
| 4732 | Member added to local security group | Privilege escalation |
| 4756 | Member added to universal security group | Privilege monitoring |
| 7045 | New service installed | Persistence / administrative activity |

Event IDs should always be correlated with user, host, process, and network context.

---

## 8. Linux Privileged Access Monitoring

Linux privileged access can be monitored through:

- Authentication logs
- sudo logs
- auditd
- SSH logs
- System logs
- Process telemetry

Important activity includes:

    sudo
    su
    ssh
    useradd
    usermod
    passwd
    chmod
    chown
    systemctl
    service
    crontab

Example:

    user01
       ↓
    sudo
       ↓
    systemctl stop security-service

This should be investigated if the user is not authorized to stop the service.

---

## 9. Active Directory Privileged Access Monitoring

Active Directory monitoring should focus heavily on privileged groups.

Important groups include:

    Domain Admins
    Enterprise Admins
    Administrators
    Schema Admins
    Account Operators
    Backup Operators

Monitor:

- User added to privileged group
- User removed from privileged group
- Privileged account creation
- Password reset
- Group membership changes
- Administrative authentication
- Domain controller activity

---

## 10. Privilege Escalation Monitoring

Privilege escalation occurs when an attacker or user obtains permissions beyond what they should normally have.

Example:

Standard User
     ↓
Exploit / Misconfiguration
     ↓
Administrator
     ↓
Sensitive System Access

Possible indicators include:

- New administrator membership
- Suspicious token privileges
- Unexpected sudo usage
- UAC bypass indicators
- Exploitation of vulnerable software
- Abnormal process execution
- Credential theft
- Security policy modification

---

## 11. Privileged Group Modification

Changes to privileged groups should be closely monitored.

Example:

    user01
       ↓
    Added to
    Domain Admins
       ↓
    Administrative Login
       ↓
    Multiple Server Access

This may indicate:

- Legitimate administrative change
- Privilege escalation
- Insider activity
- Compromised administrator account

Always validate against an approved change request.

---

## 12. Administrative Account Creation

Creating a new privileged account can be a persistence mechanism.

Example:

    New Account Created
           ↓
    Added to Administrators
           ↓
    Remote Login
           ↓
    System Changes

This sequence should receive high priority.

Investigate:

- Who created the account?
- Why was it created?
- Who approved it?
- What privileges were assigned?
- From which host was it created?
- Was the account immediately used?

---

## 13. Break-Glass Account Monitoring

Break-glass accounts are emergency administrative accounts used when normal administrative access is unavailable.

Because they are highly privileged, their use should be rare.

Monitor:

- Login events
- MFA events
- Password changes
- Source IP
- Device
- Commands
- Resource access

Any unexpected break-glass account activity should be investigated immediately.

---

## 14. Privileged Remote Access

Remote administrative access is common in enterprise environments.

Examples include:

- RDP
- SSH
- WinRM
- PowerShell Remoting
- Remote management tools
- VPN
- Cloud consoles

Example:

    Administrator
         ↓
    VPN
         ↓
    RDP
         ↓
    Server
         ↓
    PowerShell
         ↓
    Security Configuration Change

The complete chain should be reviewed.

---

## 15. Privileged PowerShell Monitoring

PowerShell is frequently used by administrators but can also be abused by attackers.

Monitor:

- PowerShell process creation
- Encoded commands
- Download activity
- Script execution
- Credential access
- Remote execution
- Administrative configuration changes

Example:

    Administrator Login
          ↓
    powershell.exe
          ↓
    Encoded Command
          ↓
    Network Connection
          ↓
    File Download

This combination is highly suspicious.

---

## 16. Privileged Command Monitoring

Administrative commands should be monitored based on risk.

Examples:

### Windows

    net user
    net localgroup administrators
    whoami
    powershell
    sc.exe
    reg.exe
    wevtutil

### Linux

    sudo
    useradd
    usermod
    passwd
    chmod
    chown
    systemctl
    iptables
    crontab

The command itself does not automatically indicate malicious activity.

Context is critical.

---

## 17. Privileged Account Baselines

Organizations should establish normal behavior for privileged accounts.

A baseline may include:

    Normal Login Time
    Normal Devices
    Normal Source IPs
    Normal Hosts
    Normal Commands
    Normal Applications
    Normal Geographic Locations

Example:

Normal:

    Administrator
    Corporate workstation
    09:00–18:00
    Internal network

Observed:

    Administrator
    Unknown device
    External IP
    03:20
    RDP
    PowerShell

This deviation should be investigated.

---

## 18. Service Account Monitoring

Service accounts can become high-value targets.

Monitor:

- Authentication frequency
- Source systems
- Interactive authentication
- Privilege changes
- Password changes
- New services
- New applications
- Unusual network connections

Example:

    Service Account
          ↓
    New Source Host
          ↓
    Interactive Login
          ↓
    Administrative Command

This may indicate credential compromise.

---

## 19. Cloud Privileged Access Monitoring

Cloud environments require monitoring of privileged IAM activity.

Monitor:

- Administrative console logins
- IAM role changes
- Policy changes
- Access key creation
- Access key deletion
- Role assumption
- Privilege escalation
- Security group changes
- Storage policy changes
- Logging configuration changes

Example:

    Cloud Admin Login
          ↓
    IAM Policy Modification
          ↓
    Logging Disabled
          ↓
    Sensitive Resource Access

This is a high-risk sequence.

---

## 20. Database Privileged Access Monitoring

Database administrators have access to sensitive data.

Monitor:

- DBA authentication
- Administrative queries
- User creation
- Permission changes
- Schema changes
- Bulk exports
- Backup access
- Database configuration changes

Example:

    DBA Login
       ↓
    Permission Change
       ↓
    Large Data Query
       ↓
    Data Export

This should be investigated if unexpected.

---

## 21. Network Device Privileged Access

Network administrators may have access to routers, switches, firewalls, and other infrastructure.

Monitor:

- Administrative login
- Configuration changes
- Firewall rule changes
- ACL changes
- Routing changes
- VPN configuration
- Account changes

Example:

    Network Admin Login
          ↓
    Firewall Rule Change
          ↓
    Internet Exposure
          ↓
    New External Connection

This can create significant security risk.

---

## 22. Privileged Access and Endpoint Correlation

Privileged identity telemetry should be correlated with endpoint activity.

Example:

    Admin Login
        ↓
    New Process
        ↓
    PowerShell
        ↓
    Credential Access
        ↓
    Network Connection

This can indicate a compromised privileged account.

---

## 23. Privileged Access and Network Correlation

Example:

    Admin Login
        ↓
    RDP
        ↓
    Server A
        ↓
    SMB
        ↓
    Server B
        ↓
    Server C

This pattern may indicate lateral movement.

---

## 24. Privileged Access Attack Chain

A possible attack chain is:

    Credential Theft
          ↓
    Privileged Authentication
          ↓
    Privilege Abuse
          ↓
    Security Control Modification
          ↓
    Lateral Movement
          ↓
    Sensitive Data Access
          ↓
    Persistence

Privileged access monitoring can detect activity across this chain.

---

## 25. SIEM Correlation

Privileged access data should be integrated with the SIEM.

Example:

    Authentication Logs
            +
    Privilege Changes
            +
    Endpoint Logs
            +
    Network Logs
            +
    Cloud IAM Logs
            +
    Database Logs
            ↓
           SIEM
            ↓
       Correlation
            ↓
           Alert
            ↓
      SOC Investigation

---

## 26. Detection Rules

### Rule 1 — Privileged Group Addition

    IF
    standard user is added
    to a privileged group

    AND
    no approved change exists

    THEN
    generate high-severity alert

Severity:

    High

---

### Rule 2 — Unusual Administrator Login

    IF
    privileged account logs in
    from a new device or unusual location

    THEN
    generate investigation alert

Severity:

    High

---

### Rule 3 — Service Account Interactive Login

    IF
    service account performs
    interactive authentication

    THEN
    generate investigation alert

Severity:

    Medium

---

### Rule 4 — Break-Glass Account Usage

    IF
    emergency administrative account
    is used

    THEN
    generate high-priority alert

Severity:

    High

---

### Rule 5 — New Privileged Account

    IF
    new account is created
    AND
    administrative privileges are assigned

    THEN
    generate high-severity alert

Severity:

    High

---

### Rule 6 — Privileged Login Followed by Suspicious Process

    IF
    privileged login occurs

    AND
    suspicious process execution follows

    THEN
    generate high-priority alert

Severity:

    High

---

## 27. Example SOC Alert

Alert:

    Unauthorized Privileged Group Modification

Severity:

    High

User:

    administrator01

Action:

    user01 added to Domain Admins

Source Host:

    DC01

Timestamp:

    14:35:21

Change Approval:

    Not Found

Related Activity:

    user01 authenticated to DC01
    shortly after the group membership change.

### Analyst Comment

A standard user account was added to the Domain Admins group without an associated approved change request. The account subsequently authenticated to a domain controller. This activity may indicate unauthorized privilege escalation or account compromise. The originating administrator session, endpoint telemetry, authentication history, and subsequent administrative activity should be reviewed immediately.

---

## 28. SOC Triage Process

### Step 1 — Identify the Privileged Account

Determine:

    Username
    Account Type
    Role
    Privilege Level

### Step 2 — Identify the Source

Check:

    Source IP
    Hostname
    Device
    Location
    VPN
    Authentication Method

### Step 3 — Validate the Activity

Ask:

    Was the action authorized?
    Was there a change ticket?
    Was there maintenance activity?
    Is the account expected to perform this action?

### Step 4 — Review Authentication

Check:

    Successful logins
    Failed logins
    Login location
    Login device
    MFA
    Remote access

### Step 5 — Review Privilege Changes

Check:

    Group membership
    Role assignment
    New accounts
    Password changes
    IAM policies

### Step 6 — Review Endpoint Activity

Check:

    Process creation
    PowerShell
    Command execution
    Remote administration
    Credential access

### Step 7 — Review Network Activity

Check:

    RDP
    SSH
    SMB
    WinRM
    VPN
    Internal scanning
    Lateral movement

### Step 8 — Determine Impact

Ask:

    Was privilege escalated?
    Was a security control changed?
    Was sensitive data accessed?
    Was lateral movement performed?
    Was persistence established?

### Step 9 — Escalate

Escalate confirmed or high-confidence malicious privileged activity according to the organization's incident-response process.

---

## 29. Privileged Access Monitoring Best Practices

Organizations should:

- Apply least privilege
- Use separate administrative accounts
- Enforce MFA
- Monitor privileged authentication
- Monitor privileged group changes
- Monitor service accounts
- Monitor break-glass accounts
- Establish privileged activity baselines
- Use Privileged Access Management
- Rotate privileged credentials
- Remove unnecessary privileges
- Review privileged access regularly
- Restrict administrative access to trusted devices
- Correlate privileged activity with endpoint telemetry
- Correlate privileged activity with network telemetry
- Maintain detailed audit logs

---

## 30. Privileged Access Investigation Checklist

    [ ] Identify privileged account
    [ ] Identify account type
    [ ] Check privilege level
    [ ] Identify source IP
    [ ] Identify source device
    [ ] Check authentication method
    [ ] Check geographic location
    [ ] Review successful logins
    [ ] Review failed logins
    [ ] Check MFA activity
    [ ] Validate change approval
    [ ] Review privileged group changes
    [ ] Review account creation
    [ ] Review password changes
    [ ] Review endpoint activity
    [ ] Review PowerShell activity
    [ ] Review administrative commands
    [ ] Review RDP/SSH activity
    [ ] Review SMB activity
    [ ] Review network connections
    [ ] Review cloud IAM activity
    [ ] Review database activity
    [ ] Determine privilege escalation
    [ ] Determine impact
    [ ] Assign severity
    [ ] Document findings
    [ ] Escalate if required

---

## 31. Key Takeaways

Privileged Access Monitoring is a critical SOC capability because privileged identities can make high-impact changes across an organization's environment.

A SOC analyst should understand:

- Privileged accounts
- Administrative authentication
- Active Directory privileges
- Linux root and sudo activity
- Cloud IAM
- Database privileges
- Network administration
- Privilege escalation
- Privileged group changes
- Service accounts
- Break-glass accounts
- Remote administration
- Administrative commands
- PowerShell monitoring
- Endpoint correlation
- Network correlation
- SIEM detection

The core investigation model is:

    Privileged Identity
          ↓
    Authentication
          ↓
    Authorization
          ↓
    Privileged Action
          ↓
    Endpoint Correlation
          ↓
    Network Correlation
          ↓
    Behavioral Analysis
          ↓
    Impact Assessment
          ↓
    Incident Response

**Privileged access monitoring should focus not only on who has administrative privileges, but also on when, where, how, and why those privileges are being used.**
