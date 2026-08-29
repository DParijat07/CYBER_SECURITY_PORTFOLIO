# Database Monitoring

## 1. Introduction

Database monitoring is the process of continuously observing database activity, performance, access patterns, authentication events, queries, and security-related changes to detect abnormal behavior, misuse, attacks, and operational issues.

From a SOC perspective, database monitoring helps security analysts identify:

* Unauthorized database access
* Failed and suspicious authentication attempts
* Privilege escalation
* Creation or modification of database accounts
* Sensitive data access
* Unusual query activity
* Data modification or deletion
* SQL injection activity
* Database configuration changes
* Insider threats
* Data exfiltration
* Malware or compromised hosts accessing databases

Database monitoring is an important part of **Security Monitoring, Threat Detection, Incident Response, and Data Protection**.

---

## 2. Why Database Monitoring Is Important

Databases commonly contain highly sensitive information such as:

* Personally Identifiable Information (PII)
* Credentials
* Financial information
* Customer records
* Business information
* Authentication data
* Application data
* Confidential corporate information

If an attacker compromises an application server or user account, the database may become the next target.

A SOC analyst therefore needs visibility into both:

```text
User/Application
       ↓
Application Server
       ↓
Database
       ↓
Sensitive Data
```

Monitoring the database layer provides additional evidence that may not be visible from endpoint or network logs alone.

---

## 3. Database Monitoring Objectives

The main objectives are:

1. Detect unauthorized access
2. Monitor authentication activity
3. Identify privilege abuse
4. Detect suspicious queries
5. Monitor sensitive data access
6. Detect unauthorized changes
7. Identify possible data exfiltration
8. Correlate database events with endpoint and network telemetry
9. Support incident investigation
10. Maintain audit and compliance visibility

---

## 4. Types of Database Monitoring

### 4.1 Authentication Monitoring

Monitor:

* Successful logins
* Failed logins
* Login attempts from unusual IP addresses
* Login attempts outside normal working hours
* Multiple failed attempts
* Authentication from unusual locations
* Privileged account authentication

Example:

```text
20 failed login attempts
        ↓
Successful login
        ↓
Same source IP
        ↓
Database access
```

This could indicate a possible brute-force attack.

---

### 4.2 Authorization Monitoring

Monitor changes involving:

* User privileges
* Roles
* Permissions
* Database ownership
* Administrative privileges
* Access-control policies

Suspicious example:

```sql
GRANT ALL PRIVILEGES ON database_name TO user1;
```

If this occurs unexpectedly, a SOC analyst should investigate the source, user, and reason for the change.

---

### 4.3 Query Monitoring

Monitor abnormal SQL queries and query patterns.

Examples:

```sql
SELECT * FROM users;
```

```sql
SELECT * FROM credit_cards;
```

```sql
DROP TABLE customers;
```

```sql
UPDATE users SET role='admin';
```

A query is not automatically malicious. The SOC analyst must evaluate the:

* User
* Source system
* Time
* Database
* Query
* Frequency
* Targeted table
* Previous behavior

---

### 4.4 Sensitive Data Access Monitoring

Organizations should monitor access to sensitive tables and records.

Examples:

```text
Customer database
Employee database
Financial database
Healthcare database
Credential database
Payment information
```

A user who normally accesses 20 customer records suddenly querying hundreds of thousands of records may represent suspicious activity.

---

### 4.5 Database Account Monitoring

Monitor:

* New account creation
* Account deletion
* Password changes
* Privilege changes
* Role assignments
* Disabled/enabled accounts
* Administrative accounts

Example:

```sql
CREATE USER attacker IDENTIFIED BY 'password';
```

Unexpected account creation should be treated as a potentially high-risk event.

---

### 4.6 Database Configuration Monitoring

Monitor changes to:

* Authentication configuration
* Audit settings
* Network exposure
* Encryption settings
* Database permissions
* Logging configuration
* Security policies

Attackers may modify configurations to weaken security controls or hide their activity.

---

## 5. Important Database Security Events

A SOC analyst should pay particular attention to:

| Event                           | Security Significance          |
| ------------------------------- | ------------------------------ |
| Failed login                    | Possible brute force           |
| Successful login after failures | Possible account compromise    |
| New user created                | Possible persistence           |
| Privilege escalation            | Possible account abuse         |
| Role modification               | Possible authorization abuse   |
| Sensitive table access          | Possible data theft            |
| Large SELECT query              | Possible data collection       |
| UPDATE/DELETE operation         | Possible data manipulation     |
| DROP operation                  | Potential destructive activity |
| Configuration change            | Possible defense evasion       |
| Audit logging disabled          | Possible defense evasion       |
| Remote administrative login     | Requires investigation         |
| Unusual query volume            | Possible automated activity    |

---

## 6. Common Database Attack Indicators

### 6.1 SQL Injection

SQL injection occurs when an attacker manipulates application input to execute unintended SQL commands.

Example malicious input:

```text
' OR '1'='1
```

Potential indicators include:

* SQL syntax errors
* Unusual database queries
* Repeated malformed requests
* Unexpected database errors
* Queries originating from web application accounts
* Large numbers of similar queries

SOC analysts should correlate:

```text
Web Server Logs
       +
WAF Logs
       +
Database Logs
```

---

### 6.2 Credential Brute Force

Indicators:

```text
Multiple failed logins
        ↓
Same username
        ↓
Same source IP
        ↓
Successful authentication
```

This should trigger investigation, especially for privileged accounts.

---

### 6.3 Privilege Escalation

Possible indicators:

```text
Normal user
     ↓
Role modification
     ↓
Administrative privileges
     ↓
Sensitive database access
```

This may indicate compromised credentials or insider abuse.

---

### 6.4 Data Exfiltration

Possible indicators:

* Large SELECT operations
* Access to many records
* Repeated queries
* Database dumps
* Unusual outbound traffic
* Access outside normal hours
* New external database connections

Example:

```text
Normal:
100 records/hour

Observed:
2,000,000 records/hour
```

This should be investigated immediately.

---

## 7. Database Logs

Different database platforms generate different logs.

Common log categories include:

### Authentication Logs

Record:

```text
Login
Logout
Failed authentication
Authentication method
Source address
Username
```

### Audit Logs

Record:

```text
User activity
Database operations
Privilege changes
Object access
Administrative actions
```

### Query Logs

Record SQL statements or query-related activity.

### Error Logs

Record:

```text
Database errors
Connection failures
Configuration problems
Authentication failures
Service problems
```

---

## 8. Important Fields in Database Logs

A SOC analyst should extract important fields such as:

```text
Timestamp
Username
Source IP
Destination IP
Database
Application
Query
Action
Object/Table
Result
Authentication Status
Privilege
Session ID
Process ID
```

Example event:

```text
Timestamp: 2026-06-20 02:14:51
User: admin
Source IP: 10.10.10.25
Database: customer_db
Action: SELECT
Table: customers
Rows: 850000
Status: SUCCESS
```

The large number of accessed records and unusual time should be investigated.

---

## 9. Database Monitoring in a SOC

Database telemetry should be integrated with the organization's SIEM.

Example architecture:

```text
Database
   │
   ├── Authentication Logs
   ├── Audit Logs
   ├── Query Logs
   └── Error Logs
          │
          ↓
      Log Collector
          │
          ↓
         SIEM
          │
          ↓
    Detection Rules
          │
          ↓
      SOC Analyst
          │
          ↓
    Investigation
          │
          ↓
    Incident Response
```

---

## 10. Wazuh Database Monitoring

Wazuh can be used as part of a database security monitoring architecture by collecting relevant database logs from monitored systems and correlating them with endpoint and security telemetry.

Example:

```text
Database Server
      ↓
Database Logs
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Wazuh Dashboard
      ↓
SOC Analyst
```

The exact log collection method depends on the database platform and deployment architecture.

Common sources can include:

* MySQL/MariaDB logs
* PostgreSQL logs
* Microsoft SQL Server logs
* Oracle database audit logs
* Operating system authentication logs
* Application logs

---

## 11. Example Detection Scenario

### Scenario

An employee normally accesses a database between:

```text
09:00 – 18:00
```

At:

```text
02:15 AM
```

the same account performs a very large query.

Observed:

```text
User: analyst01
Time: 02:15
Source IP: 10.10.10.25
Query: SELECT * FROM customers
Rows: 850000
```

### Initial Assessment

Potential indicators:

* Unusual time
* Large data access
* Sensitive table
* Abnormal query volume

### SOC Investigation

Check:

1. Was the user working at that time?
2. Is the source IP normal?
3. Was the account recently authenticated?
4. Were there previous failed login attempts?
5. Was the user account recently modified?
6. Was the query generated by an application or directly by a user?
7. Were files created on the endpoint?
8. Was there unusual outbound network traffic?
9. Were similar queries executed previously?
10. Are there related endpoint alerts?

---

## 12. Correlation With Other Security Telemetry

Database monitoring becomes much more powerful when correlated with other data sources.

### Example

```text
Windows Event Logs
        +
Sysmon
        +
Web Server Logs
        +
Firewall Logs
        +
Database Logs
        ↓
       SIEM
        ↓
Correlation
        ↓
Incident Investigation
```

Example attack chain:

```text
Internet
   ↓
Web Application
   ↓
SQL Injection
   ↓
Database Access
   ↓
Sensitive Data Query
   ↓
Data Collection
   ↓
Outbound Connection
```

A SOC analyst should investigate the complete attack chain rather than examining the database event in isolation.

---

## 13. Database Monitoring Detection Rules

Example detection logic:

### Rule 1 — Multiple Failed Logins

```text
IF
failed database logins > 10
FROM same source IP
WITHIN 5 minutes

THEN
generate alert
```

Severity:

```text
Medium
```

---

### Rule 2 — Successful Login After Brute Force

```text
IF
multiple failed logins
FOLLOWED BY
successful login

THEN
generate high-priority alert
```

Severity:

```text
High
```

---

### Rule 3 — Privilege Escalation

```text
IF
normal user
RECEIVES administrative database privileges

THEN
generate alert
```

Severity:

```text
High
```

---

### Rule 4 — Sensitive Data Access

```text
IF
user accesses sensitive table
AND
access volume exceeds baseline

THEN
generate alert
```

Severity:

```text
High
```

---

### Rule 5 — Audit Logging Disabled

```text
IF
database audit logging is disabled

THEN
generate critical alert
```

Reason:

An attacker may attempt to disable logging to reduce visibility and hide malicious activity.

---

## 14. Database Monitoring Baseline

A SOC needs to understand normal database behavior.

Establish baselines for:

```text
Normal login times
Normal users
Normal source IPs
Normal applications
Normal query volume
Normal database access
Normal administrative activity
Normal data access volume
```

Example:

```text
Normal:
User = application01
Source = WebServer01
Queries = 5,000/hour

Abnormal:
User = application01
Source = UnknownHost
Queries = 500,000/hour
```

The deviation from the baseline increases the suspicion level.

---

## 15. SOC Triage Process

When a database alert is generated:

### Step 1 — Identify the Event

Determine:

```text
What happened?
When?
Which database?
Which user?
Which source?
```

### Step 2 — Validate the User

Check:

```text
User identity
Role
Department
Privileges
Normal activity
```

### Step 3 — Analyze Source

Determine:

```text
Source IP
Hostname
Device owner
Internal/external
Known/unknown system
```

### Step 4 — Analyze Query

Check:

```text
SQL operation
Target table
Number of records
Query frequency
Query purpose
```

### Step 5 — Correlate

Look for:

```text
Authentication events
Endpoint alerts
Network connections
Web application logs
Firewall events
EDR alerts
```

### Step 6 — Determine Severity

Classify as:

```text
False Positive
Low
Medium
High
Critical
```

### Step 7 — Escalate

Escalate confirmed incidents according to the organization's incident-response procedure.

---

## 16. Example SOC Alert

```text
Alert:
Large Sensitive Database Query

Severity:
High

User:
db_user01

Source IP:
10.10.10.45

Database:
customer_db

Table:
customer_records

Rows Accessed:
950000

Time:
02:13 AM

Status:
Successful
```

### Analyst Comment

```text
A high-volume query was detected against the customer_records
table during unusual hours. The activity is inconsistent with
the user's normal access pattern. Source IP, authentication
history, endpoint telemetry, and outbound network connections
should be investigated to determine whether the activity
represents legitimate administrative activity or possible
data exfiltration.
```

---

## 17. Database Monitoring Best Practices

Organizations should:

* Enable database auditing
* Centralize database logs
* Protect log integrity
* Monitor privileged accounts
* Apply least privilege
* Monitor sensitive data access
* Establish behavioral baselines
* Alert on anomalous queries
* Monitor configuration changes
* Protect database credentials
* Use encryption
* Restrict database network access
* Regularly review database permissions
* Integrate database telemetry with the SIEM
* Retain logs according to organizational requirements

---

## 18. Common Tools

### SIEM

Examples:

* Wazuh
* Splunk
* Microsoft Sentinel
* IBM QRadar

### Database Security / Monitoring

Examples:

* MySQL Audit
* PostgreSQL logging/auditing
* Microsoft SQL Server Audit
* Oracle Audit

### Endpoint / Network

Examples:

* Sysmon
* Windows Event Viewer
* Wireshark
* Firewall logs
* EDR platforms

---

## 19. Database Monitoring Investigation Checklist

```text
[ ] Identify affected database
[ ] Identify affected account
[ ] Check authentication history
[ ] Check source IP
[ ] Check source hostname
[ ] Analyze SQL query
[ ] Identify affected tables
[ ] Determine number of records accessed
[ ] Compare activity with baseline
[ ] Check privilege changes
[ ] Check account creation/modification
[ ] Check endpoint telemetry
[ ] Check network telemetry
[ ] Check application/WAF logs
[ ] Determine whether data was exfiltrated
[ ] Determine severity
[ ] Document findings
[ ] Escalate if required
```

---

## 20. Key Takeaways

Database monitoring gives the SOC visibility into activity occurring at one of the most sensitive layers of an organization's infrastructure.

A SOC analyst should be able to identify:

```text
Authentication
     ↓
Authorization
     ↓
Database Activity
     ↓
Sensitive Data Access
     ↓
Anomalies
     ↓
Correlation
     ↓
Investigation
     ↓
Incident Response
```

The most important skills are:

* Understanding database logs
* Identifying suspicious authentication
* Detecting privilege abuse
* Recognizing abnormal queries
* Monitoring sensitive data access
* Correlating database activity with other telemetry
* Building SIEM detections
* Performing structured SOC triage

**Database monitoring is not simply about monitoring database performance. From a SOC perspective, it is about understanding who is accessing the data, what they are doing, when they are doing it, where the activity originates, and whether the behavior is legitimate.**
