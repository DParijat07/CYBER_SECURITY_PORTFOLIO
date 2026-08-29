# Cloud Monitoring

> **Blue Team → SOC → Security Monitoring → Cloud Monitoring**

Cloud environments introduce a different monitoring model from traditional on-premises infrastructure. Instead of monitoring only physical servers and network devices, a SOC must monitor identities, APIs, cloud resources, configurations, workloads, storage, network activity, and control-plane operations.

A cloud SOC therefore needs visibility across:

```text
Identity
+
Cloud Control Plane
+
Compute
+
Storage
+
Network
+
Applications
+
Containers
+
Serverless
+
Security Services
```

The core objective is:

> **Detect unauthorized access, privilege abuse, suspicious API activity, configuration changes, compromised workloads, and data exposure in cloud environments.**

---

# 1. Objectives

After completing this section, you should understand:

* Cloud security monitoring fundamentals
* Cloud control-plane activity
* IAM monitoring
* Authentication monitoring
* API monitoring
* Compute monitoring
* Storage monitoring
* Network monitoring
* Cloud configuration monitoring
* CloudTrail-style audit logging
* Azure Activity Logs
* Google Cloud audit logs
* Cloud-native SIEM concepts
* Cloud security alerts
* Cloud incident investigation
* Practical cloud-monitoring labs

---

# 2. Cloud Monitoring Architecture

A simplified architecture:

```text id="9l3nqv"
                    CLOUD ENVIRONMENT
                           │
        ┌──────────────────┼──────────────────┐
        ↓                  ↓                  ↓
      IAM              Compute             Storage
        │                  │                  │
        ↓                  ↓                  ↓
 Authentication       Workloads          Data Access
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ↓
                     Cloud Audit Logs
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
           Network       APIs       Configuration
              │            │            │
              └────────────┼────────────┘
                           ↓
                         SIEM
                           ↓
                       Detection
                           ↓
                         Alert
                           ↓
                    SOC Investigation
```

---

# 3. Why Cloud Monitoring Matters

Cloud environments are heavily API-driven.

A user may perform:

```text id="tq8j8h"
Login
 ↓
API Call
 ↓
Create Resource
 ↓
Modify IAM
 ↓
Access Storage
 ↓
Transfer Data
```

The SOC needs visibility into this sequence.

Cloud monitoring can help detect:

```text id="e6n3a2"
Account Compromise
Privilege Escalation
Credential Abuse
Data Exposure
Resource Hijacking
Cryptomining
Malicious Configuration Changes
API Abuse
Cloud Persistence
```

---

# 4. Shared Responsibility

Cloud security operates under a shared-responsibility model.

Generally:

```text id="jv7kpg"
Cloud Provider
        +
Customer
```

Both have security responsibilities, although the exact division depends on the service model.

Monitoring therefore needs to cover:

```text id="3n2gqh"
Provider Security Controls
+
Customer Configuration
+
Customer Identities
+
Customer Workloads
+
Customer Data
```

---

# 5. Major Cloud Monitoring Areas

A SOC should monitor:

| Area          | Examples                 |
| ------------- | ------------------------ |
| Identity      | Users, roles, MFA        |
| API           | Control-plane operations |
| Compute       | VMs, containers          |
| Storage       | Object access            |
| Network       | VPC/VNet traffic         |
| Configuration | Security settings        |
| Database      | Queries/access           |
| Serverless    | Function execution       |
| Containers    | Runtime activity         |
| Secrets       | Access and modification  |

---

# 6. Cloud Identity Monitoring

Identity is one of the highest-value cloud monitoring areas.

Monitor:

```text id="1b8c2h"
Login
Logout
MFA
Failed Authentication
Role Assignment
Permission Changes
Access Keys
Service Accounts
Privileged Accounts
```

Example:

```text id="uv8u7r"
User Login
     ↓
MFA Failure
     ↓
Successful Login
     ↓
Privilege Change
```

This should trigger investigation.

---

# 7. IAM Monitoring

Identity and Access Management should be closely monitored.

Important activities include:

```text id="9k6n9d"
User Created
User Deleted
Role Created
Role Assigned
Policy Modified
Permission Increased
Access Key Created
Access Key Deleted
MFA Changed
```

Unexpected IAM changes can indicate:

```text id="h10b1r"
Privilege Escalation
Persistence
Account Compromise
Insider Threat
Misconfiguration
```

---

# 8. Privilege Escalation in Cloud

A suspicious pattern could be:

```text id="3y0d2j"
Compromised User
      ↓
IAM Policy Change
      ↓
Administrative Privileges
      ↓
Sensitive Resource Access
```

Investigate:

```text id="q8x8qp"
Who?
What changed?
Previous permission?
New permission?
Why?
Was it approved?
What happened afterward?
```

---

# 9. Cloud Authentication Monitoring

Monitor:

```text id="ztv3v6"
Successful Login
Failed Login
MFA
Source IP
Device
Location
Authentication Method
Session
```

Potential anomaly:

```text id="g11l4h"
Normal:
User → Office IP → MFA → Cloud
```

Anomaly:

```text id="z5nqbf"
User
 ↓
Unknown IP
 ↓
Unusual Time
 ↓
MFA anomaly
 ↓
Cloud API activity
```

---

# 10. Impossible Travel

Impossible-travel detections identify authentication events that appear geographically or temporally inconsistent.

Example:

```text id="f6uy3n"
09:00
India
 ↓
09:15
Europe
```

This may indicate:

```text id="h8gc5j"
Credential Compromise
VPN
Proxy
Travel
Geo-IP Error
```

Therefore it is an investigation signal, not proof of compromise.

---

# 11. API Monitoring

Cloud infrastructure is heavily controlled through APIs.

Monitor:

```text id="7m7m1n"
API Caller
API Action
Resource
Source IP
Timestamp
Result
Authentication
```

Example:

```text id="l7h2xg"
User
 ↓
Create IAM Policy
 ↓
Assign Privileges
```

This is highly relevant to cloud security.

---

# 12. Control-Plane Monitoring

The cloud control plane manages resources.

Examples:

```text id="hjh4de"
Create VM
Delete VM
Modify Security Group
Create IAM User
Change Storage Policy
Create Access Key
Modify Network
```

Control-plane logging is therefore one of the most important cloud telemetry sources.

---

# 13. AWS CloudTrail

For AWS environments, CloudTrail provides audit visibility into API activity.

Typical information includes:

```text id="2ax2oe"
User / Principal
Event
Service
API Action
Source IP
Timestamp
Resource
Result
```

Example:

```text id="e1y4kl"
IAM User
 ↓
CreateAccessKey
 ↓
Unknown Source IP
```

This may warrant investigation.

---

# 14. Azure Activity Logs

Azure provides Activity Logs for management-plane operations.

They can help monitor:

```text id="8a0o6k"
Resource Creation
Resource Deletion
Role Assignment
Configuration Changes
Administrative Actions
```

Example:

```text id="v8a4xl"
User
 ↓
Role Assignment
 ↓
Privileged Role
```

Investigate unexpected administrative changes.

---

# 15. Google Cloud Audit Logs

Google Cloud provides audit logging for activity within cloud resources.

Monitoring can cover:

```text id="v2z1gi"
Administrative Activity
Data Access
System Events
Policy Changes
```

A SOC should understand the difference between:

```text id="l5m5yo"
Control Plane Activity
vs
Data Access
```

---

# 16. Cloud Compute Monitoring

Compute resources may include:

```text id="p5f8jb"
Virtual Machines
Containers
Kubernetes
Serverless Functions
```

Monitor:

```text id="e2o9kj"
Instance Creation
Instance Modification
Instance Termination
Process Activity
Network Connections
Startup Scripts
Images
Security Groups
```

---

# 17. Suspicious VM Creation

Example:

```text id="3v0e7y"
Compromised Account
      ↓
New VM
      ↓
Unusual Region
      ↓
High CPU
      ↓
External Network Activity
```

Possible explanations include:

```text id="t3n7tw"
Cryptomining
Malicious Workload
Testing
Legitimate Deployment
```

Investigate context.

---

# 18. Cryptomining Detection

Cloud environments can be abused for unauthorized cryptocurrency mining.

Possible indicators:

```text id="g4q0c6"
Unexpected VM
High CPU
Unknown Process
Mining Pool Connection
Unexpected Region
Rapid Resource Creation
```

Example:

```text id="2r9m4y"
Compromised Credentials
 ↓
Create Multiple VMs
 ↓
High CPU
 ↓
Mining Pool
```

This is a high-priority investigation.

---

# 19. Cloud Storage Monitoring

Storage is a major security concern.

Examples:

```text id="0p3l2n"
Object Storage
Blob Storage
Cloud File Systems
Database Storage
```

Monitor:

```text id="t1spq2"
Read
Write
Delete
List
Permission Change
Public Access
Download
```

---

# 20. Public Storage Exposure

A common cloud-security problem is accidental public exposure.

Example:

```text id="rxv8so"
Private Storage
      ↓
Configuration Change
      ↓
Public Access
      ↓
Sensitive Data Exposure
```

Monitor:

```text id="1u4rrh"
Access Policy
ACL
Bucket Policy
Public Permission
Identity
Change Time
```

---

# 21. Sensitive Data Access

Monitor unusual access to:

```text id="r7n8ij"
Customer Data
Credentials
Secrets
Financial Data
Source Code
Backups
Personal Information
```

Investigate:

```text id="1x3xqg"
Who accessed it?
From where?
How much?
Was the access expected?
```

---

# 22. Data Exfiltration

A possible cloud exfiltration pattern:

```text id="k91kdu"
Compromised Account
       ↓
Large Storage Read
       ↓
External Transfer
       ↓
Unknown Destination
```

Useful telemetry:

```text id="qv0d7u"
Identity
Storage Logs
Network Logs
API Logs
Volume
Destination
```

---

# 23. Cloud Network Monitoring

Cloud networks often use:

```text id="w6j3hm"
VPC
VNet
Security Groups
Network ACLs
Load Balancers
Private Endpoints
```

Monitor:

```text id="1e9y3g"
Inbound Traffic
Outbound Traffic
Internal Traffic
Security Group Changes
Network ACL Changes
```

---

# 24. Security Group Monitoring

Security groups control network access in many cloud platforms.

Potentially dangerous change:

```text id="0j8x7p"
SSH
0.0.0.0/0
```

or:

```text id="9t2r3w"
RDP
Internet
```

These changes should be investigated and reviewed against organizational policy.

---

# 25. Cloud Configuration Monitoring

Monitor security-sensitive configuration changes:

```text id="qg2e9f"
IAM
Storage
Network
Logging
Encryption
Firewall
Security Groups
MFA
Secrets
```

A configuration change should answer:

```text id="5q6f9k"
Who changed it?
What changed?
When?
Why?
Was it approved?
```

---

# 26. Cloud Logging Configuration

Attackers may attempt to reduce visibility.

Monitor:

```text id="2z9m0b"
Logging Disabled
Audit Trail Modified
Retention Changed
Security Service Disabled
Alerting Disabled
```

Example:

```text id="7q9t5u"
Attacker
 ↓
Compromised Account
 ↓
Disable Logging
 ↓
Continue Activity
```

This is highly suspicious.

---

# 27. Cloud Persistence

Cloud persistence can involve:

```text id="7av5le"
New IAM User
New Access Key
New Role
Trust Policy Modification
Service Account
Startup Script
Scheduled Function
Automation
```

Example:

```text id="b9y2hm"
Compromised Admin
      ↓
Create Access Key
      ↓
Use Key Later
```

Monitor identity lifecycle events.

---

# 28. Secrets Monitoring

Cloud environments commonly use secret stores.

Monitor:

```text id="x9g8p0"
Secret Read
Secret Created
Secret Modified
Secret Deleted
Access Policy
```

Unexpected secret access may indicate:

```text id="q7u2m8"
Credential Theft
Application Compromise
Insider Activity
Misconfiguration
```

---

# 29. Container Monitoring

Containers introduce additional telemetry.

Monitor:

```text id="s5w1n9"
Container Creation
Image
Registry
Process
Network
Privileges
Volume Mounts
Secrets
```

Potentially suspicious:

```text id="1s8c7a"
Privileged Container
Unknown Image
Unknown Registry
Unexpected Network
Sensitive Host Mount
```

---

# 30. Kubernetes Monitoring

Kubernetes monitoring should include:

```text id="9a7j8x"
API Server
Pods
Deployments
Service Accounts
RBAC
Secrets
Network Policies
Cluster Configuration
```

A suspicious pattern:

```text id="d8h2pq"
Compromised Account
 ↓
Kubernetes API
 ↓
Create Privileged Pod
 ↓
Access Sensitive Resource
```

This requires investigation.

---

# 31. Serverless Monitoring

Serverless environments may use functions triggered by:

```text id="b8m5n2"
HTTP
Events
Queues
Storage
Schedules
```

Monitor:

```text id="v9x3k1"
Function Creation
Function Modification
Execution
Permissions
Environment Variables
Network Access
```

Unexpected function creation can indicate persistence or abuse.

---

# 32. Cloud Security Services

Cloud platforms provide native security services.

Examples include:

```text id="0x9p6c"
Threat Detection
Security Posture Management
Identity Monitoring
WAF
DDoS Protection
Cloud SIEM
```

These alerts should be integrated into the SOC workflow.

---

# 33. Cloud Monitoring + SIEM

A centralized architecture:

```text id="k5m1q8"
AWS / Azure / GCP
        │
        ↓
Cloud Audit Logs
        │
        ├── IAM
        ├── API
        ├── Compute
        ├── Storage
        └── Network
        │
        ↓
       SIEM
        │
        ↓
    Correlation
        │
        ↓
     Detection
        │
        ↓
       Alert
        │
        ↓
   SOC Analyst
```

---

# 34. Cloud Detection Examples

| Detection            | Primary Telemetry           |
| -------------------- | --------------------------- |
| Brute Force          | Authentication              |
| Account Compromise   | IAM + Login                 |
| Privilege Escalation | IAM                         |
| New Access Key       | IAM                         |
| Public Storage       | Storage Config              |
| Large Data Access    | Storage Logs                |
| Suspicious VM        | Control Plane               |
| Cryptomining         | Compute + Network           |
| C2                   | Network + Endpoint          |
| Logging Disabled     | Control Plane               |
| Firewall Change      | Network Config              |
| Secret Access        | Secret Logs                 |
| Container Abuse      | Kubernetes / Container Logs |

---

# 35. Cloud Attack Chain

A useful SOC investigation model:

```text id="l3m2zq"
Credential Compromise
        ↓
Cloud Login
        ↓
API Activity
        ↓
Privilege Escalation
        ↓
Resource Creation
        ↓
Data Access
        ↓
External Transfer
```

The analyst should correlate all stages.

---

# 36. Practical Lab — Cloud IAM Monitoring

Create an isolated cloud test environment.

Perform a controlled IAM change.

Observe:

```text id="0w7s5m"
User
Action
Resource
Timestamp
Source
```

Document:

```text id="0u8j9r"
Before
Change
Log
Detection
After
```

---

# 37. Practical Lab — Cloud Authentication

Generate controlled login attempts.

Observe:

```text id="h5f8s2"
Source IP
User
MFA
Result
Timestamp
```

Create a detection concept:

```text id="9x4r6y"
Multiple Failures
+
Successful Login
+
Unusual Source
```

---

# 38. Practical Lab — Storage Access

Create a test storage resource.

Generate:

```text id="6j4s0n"
Read
Write
Delete
Permission Change
```

Observe the corresponding audit logs.

Document:

```text id="7f4q9m"
User
Action
Object
Timestamp
Source
```

---

# 39. Practical Lab — Security Group Monitoring

Inside a controlled environment:

```text id="9z5b1c"
Create Test Security Group
        ↓
Modify Rule
        ↓
Generate Traffic
        ↓
Review Logs
        ↓
Revert Configuration
```

Document:

```text id="0a7k4w"
Old Rule
New Rule
Administrator
Traffic
Risk
Remediation
```

---

# 40. Practical Lab — Suspicious Resource Creation

Create a controlled VM/resource.

Investigate:

```text id="4j9n8p"
Who Created It?
Which API?
Which Region?
Which Image?
Which Network?
Which IAM Role?
```

Then remove the resource.

This teaches control-plane investigation.

---

# 41. Practical Lab — Cloud Attack Timeline

Create a controlled sequence:

```text id="f3k7q2"
Login
 ↓
IAM Change
 ↓
Resource Creation
 ↓
Storage Access
 ↓
Network Activity
```

Reconstruct the activity from cloud logs.

Your final output should be:

```text id="r9m3x6"
Timeline
+
Evidence
+
Detection
+
Impact
+
Conclusion
+
Recommended Response
```

---

# 42. Cloud Investigation Checklist

## Identity

```text id="j4p7s8"
Who?
Which account?
MFA?
Privileged?
```

## API

```text id="q8k2m5"
What API?
What action?
What resource?
```

## Source

```text id="x5d9n1"
Source IP?
Device?
Location?
```

## Resource

```text id="v3c8q7"
What was created?
Modified?
Deleted?
```

## Data

```text id="w7m2r4"
What was accessed?
How much?
```

## Network

```text id="p6j9t3"
Where did the traffic go?
```

## Timeline

```text id="b4x8n2"
What happened before?
What happened after?
```

---

# 43. Cloud Monitoring Blind Spots

Common weaknesses:

```text id="n8v2s4"
Audit Logging Disabled
Poor Log Retention
Missing IAM Monitoring
No MFA Monitoring
No Storage Monitoring
No Network Visibility
Unmonitored Service Accounts
Unmonitored Access Keys
No Configuration Monitoring
No Cloud SIEM Integration
```

These gaps can significantly reduce cloud detection capability.

---

# 44. Cloud Monitoring Baseline

Establish normal cloud behavior.

Example:

```text id="y7c3m1"
Normal:
Developer
 ↓
Approved Region
 ↓
Deploy Application
 ↓
Expected Resource
```

Anomaly:

```text id="z2k8p5"
Developer
 ↓
Unusual Region
 ↓
Create Multiple VMs
 ↓
Modify IAM
 ↓
Access Sensitive Storage
```

The combined sequence deserves investigation.

---

# 45. Evidence Collection

For cloud investigations, collect:

```text id="a6m3q8"
User / Principal
Account
Source IP
Region
API Action
Resource
Timestamp
Authentication
MFA
Configuration Change
Network Activity
Data Access
Alert
Screenshot
Timeline
Conclusion
```

Never rely on a single cloud event when investigating an incident.

---

# 46. Portfolio Structure

Recommended practical labs:

```text id="p7n4x2"
07-Cloud-Monitoring.md

Labs/
│
├── 01-Cloud-IAM-Monitoring/
│   ├── README.md
│   ├── Evidence/
│   └── Report.md
│
├── 02-Cloud-Authentication/
│
├── 03-Cloud-API-Monitoring/
│
├── 04-Cloud-Storage-Monitoring/
│
├── 05-Security-Group-Monitoring/
│
├── 06-Cloud-Resource-Monitoring/
│
├── 07-Cloud-Logging-Monitoring/
│
└── 08-Cloud-Incident-Timeline/
```

---

# 47. Interview Questions

### Fundamentals

1. What is cloud security monitoring?
2. Why is IAM monitoring important in cloud environments?
3. What is control-plane activity?
4. What is CloudTrail?
5. What are Azure Activity Logs?
6. What are Google Cloud Audit Logs?
7. How would you detect suspicious IAM changes?
8. How would you detect public storage exposure?
9. How would you investigate suspicious cloud resource creation?
10. Why are access keys important to monitor?

### Scenario

> **An employee's cloud account successfully logs in from an unusual IP, creates a new access key, modifies IAM permissions, and accesses a large amount of storage data. How would you investigate?**

Investigation:

```text id="j7x4n8"
Authentication
      ↓
Source IP
      ↓
MFA
      ↓
Access Key Creation
      ↓
IAM Modification
      ↓
Storage Access
      ↓
Data Volume
      ↓
Network Activity
```

Then determine:

```text id="s5k9q2"
Compromised Account?
Insider Activity?
Misconfiguration?
False Positive?
```

---

# 48. Key Takeaways

```text id="e6n4p1"
1. Cloud environments are heavily API-driven.

2. Identity is one of the highest-value cloud monitoring areas.

3. Control-plane logs provide critical visibility.

4. IAM changes can indicate privilege escalation or persistence.

5. Access-key creation should be monitored.

6. Cloud storage requires continuous monitoring.

7. Public exposure can result from configuration changes.

8. Cloud network controls must be monitored.

9. Unexpected resource creation can indicate compromise or abuse.

10. Cryptomining can be detected through compute and network anomalies.

11. Cloud logging itself must be protected.

12. Containers and Kubernetes require specialized telemetry.

13. Serverless functions also require monitoring.

14. Cloud events should be correlated with endpoint, identity, and network telemetry.

15. Cloud SOC investigation is fundamentally a timeline reconstruction problem.
```

---

# 49. Final Mental Model

```text id="v2r8m7"
                    CLOUD ENVIRONMENT
                           │
       ┌───────────────────┼───────────────────┐
       ↓                   ↓                   ↓
      IAM               Control Plane        Workloads
       │                   │                   │
       ↓                   ↓                   ↓
 Authentication           APIs              Compute
       │                   │                   │
       └───────────────────┼───────────────────┘
                           ↓
                    Cloud Audit Logs
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
           Storage       Network      Config
              │            │            │
              └────────────┼────────────┘
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
                    Response / Report
```

> **Cloud monitoring is the ability to turn identity, API, resource, configuration, network, and data-access telemetry into a coherent security narrative.**
