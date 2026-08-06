# IOC, IOA & TTP

> **SOC L1 → L2 Fundamental**

SOC analysts investigate threats using three closely related concepts:

* **IOC — Indicator of Compromise**
* **IOA — Indicator of Attack**
* **TTP — Tactics, Techniques & Procedures**

Understanding the difference is essential for alert triage, threat intelligence, detection engineering, threat hunting, and incident response.

---

# 1. The Big Picture

```text
                 ATTACKER ACTIVITY
                        │
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
        IOC            IOA           TTP
     Evidence        Behavior       Method
```

A simple way to remember:

```text
IOC → What evidence was left behind?

IOA → What suspicious behavior is happening?

TTP → How does the attacker operate?
```

---

# 2. What Is an IOC?

An **Indicator of Compromise (IOC)** is a piece of evidence that may indicate a system has been compromised or associated with malicious activity.

Common IOCs include:

```text
IP Addresses
Domains
URLs
File Hashes
Malicious Files
Email Addresses
Registry Keys
File Paths
Mutexes
Malware Names
Command-and-Control Infrastructure
```

---

# 3. Common IOC Types

## IP Address

Example:

```text
203.0.113.50
```

A security analyst may investigate whether the IP is associated with:

* Malware
* C2 infrastructure
* Scanning
* Phishing
* Brute-force attacks
* Botnets

---

## Domain

Example:

```text
example-malicious-domain.com
```

Investigate:

```text
Domain Reputation
DNS Records
Registration Information
Historical Resolution
Related IPs
Threat Intelligence
```

---

## URL

Example:

```text
https://example.com/payload.exe
```

URLs can be associated with:

* Phishing
* Malware delivery
* Exploit delivery
* Command-and-control

---

## File Hash

Common hash types:

```text
MD5
SHA-1
SHA-256
```

Example:

```text
SHA256:
<example-hash>
```

Hashes are useful for identifying known files.

However:

> A hash alone does not prove that a file is malicious.

Context matters.

---

# 4. IOC Investigation

Suppose a SIEM alert contains:

```text
Source IP:
203.0.113.50
```

The analyst may perform:

```text
IOC
 ↓
Threat Intelligence
 ↓
Reputation Check
 ↓
Historical SIEM Search
 ↓
Related DNS Events
 ↓
Endpoint Activity
 ↓
Determine Risk
```

Possible result:

```text
Known Malicious
Suspicious
Unknown
Benign
```

---

# 5. IOC Limitations

IOCs are useful but have weaknesses.

### IP addresses can change

Attackers may rotate infrastructure.

### Domains can change

Attackers may register new domains.

### File hashes can change

A modified malware sample produces a different hash.

### Infrastructure can be shared

A malicious IP may host multiple services.

Therefore:

> **IOC-based detection alone is not sufficient for modern threat detection.**

This leads to behavioral detection.

---

# 6. What Is an IOA?

An **Indicator of Attack (IOA)** focuses on suspicious behavior associated with an attack rather than a specific artifact.

Examples:

```text
PowerShell spawning from an unusual process
Credential dumping behavior
Mass file encryption
Suspicious privilege escalation
Abnormal lateral movement
Unexpected remote administration
Encoded command execution
```

---

# 7. IOC vs IOA

| IOC                          | IOA                          |
| ---------------------------- | ---------------------------- |
| Focuses on evidence/artifact | Focuses on behavior          |
| Often static                 | More behavioral              |
| IP address                   | Suspicious network behavior  |
| File hash                    | Suspicious process execution |
| Malicious domain             | Credential dumping behavior  |
| Malware file                 | Mass file encryption         |

Example:

```text
IOC:
Known malicious IP

IOA:
Endpoint suddenly establishes repeated outbound
connections after suspicious PowerShell execution.
```

---

# 8. Why IOAs Matter

Attackers can change:

```text
IP
Domain
Hash
Filename
```

But changing their entire attack behavior can be much harder.

For example:

```text
Malware Hash
     ↓
Change Malware
     ↓
New Hash
     ↓
IOC Detection May Fail
```

But:

```text
Malicious Behavior
     ↓
PowerShell
     ↓
Credential Access
     ↓
Network Connection
```

may still be detectable.

This is why modern detection increasingly focuses on **behavior and TTPs**.

---

# 9. What Are TTPs?

TTP stands for:

```text
Tactics
Techniques
Procedures
```

TTPs describe how threat actors conduct operations.

They are strongly associated with the **MITRE ATT&CK** framework.

---

# 10. Tactics

A **tactic** represents the attacker's objective.

Examples include:

```text
Initial Access
Execution
Persistence
Privilege Escalation
Defense Evasion
Credential Access
Discovery
Lateral Movement
Collection
Command and Control
Exfiltration
Impact
```

Think:

> **"Why is the attacker doing this?"**

---

# 11. Techniques

A **technique** describes how the attacker achieves a tactical objective.

Example:

```text
Tactic:
Execution

Technique:
Command and Scripting Interpreter
```

Another:

```text
Tactic:
Credential Access

Technique:
OS Credential Dumping
```

Think:

> **"How is the attacker achieving the objective?"**

---

# 12. Procedures

A **procedure** describes the specific way a threat actor implements a technique.

Conceptually:

```text
Tactic
  ↓
Technique
  ↓
Procedure
```

Example:

```text
Execution
   ↓
PowerShell
   ↓
Attacker executes a malicious PowerShell command
```

The procedure is the practical implementation.

---

# 13. TTP Example

Consider a phishing attack.

```text
TACTIC
Initial Access
      ↓
TECHNIQUE
Phishing
      ↓
PROCEDURE
Attacker sends a malicious email containing
a credential-harvesting link.
```

Another example:

```text
TACTIC
Execution
      ↓
TECHNIQUE
PowerShell
      ↓
PROCEDURE
Attacker executes an encoded PowerShell command
to download and execute a payload.
```

---

# 14. IOC → IOA → TTP

These concepts can be connected.

Example:

```text
                 ATTACK
                   │
          ┌────────┼────────┐
          ↓        ↓        ↓
         IOC      IOA      TTP
          │        │        │
          ↓        ↓        ↓
       Malicious  Suspicious  PowerShell
          IP      execution
```

Example investigation:

```text
IOC:
203.0.113.50

IOA:
PowerShell connects to external infrastructure

TTP:
Execution → PowerShell
Command & Control → Application Layer Protocol
```

This gives the analyst multiple perspectives.

---

# 15. IOC Investigation Workflow

```text
IOC
 ↓
Validate
 ↓
Enrich
 ↓
Search Environment
 ↓
Find Related Events
 ↓
Identify Affected Assets
 ↓
Determine Scope
 ↓
Assess Risk
 ↓
Document
 ↓
Escalate / Close
```

---

# 16. IOC Enrichment

Suppose you discover:

```text
IP:
203.0.113.50
```

Enrichment may include:

```text
Threat Intelligence
DNS
WHOIS
Geolocation
Reputation
Historical Activity
Passive DNS
Related Domains
Related Infrastructure
```

The objective is to add context.

---

# 17. IOC Searching in a SIEM

A SOC analyst might search:

```text
Source IP
Destination IP
Domain
URL
Hash
Username
Hostname
```

Example:

```text
Search:
destination.ip = "203.0.113.50"
```

Then investigate:

```text
How many hosts contacted it?
When?
Which users?
Which processes?
What happened before?
What happened after?
```

---

# 18. IOC Correlation

One IOC may reveal additional indicators.

Example:

```text
Malicious IP
     ↓
DNS Query
     ↓
Malicious Domain
     ↓
Downloaded File
     ↓
File Hash
     ↓
Process Execution
     ↓
Additional Network Connection
```

This produces an:

> **IOC cluster**

rather than a single IOC.

---

# 19. IOA Investigation

Suppose an alert detects:

```text
Encoded PowerShell
```

Instead of immediately searching for a known malicious hash, investigate the behavior:

```text
Parent Process
      ↓
PowerShell Command
      ↓
Command Arguments
      ↓
User Context
      ↓
Network Connection
      ↓
Child Processes
      ↓
Files Created
```

This helps determine intent.

---

# 20. Example: Suspicious PowerShell

### Event

```text
powershell.exe
```

This alone is not necessarily malicious.

### Additional context

```text
powershell.exe
      ↓
Encoded Command
      ↓
Launched by Word
      ↓
Downloads File
      ↓
Executes File
      ↓
External Connection
```

Now the behavior is significantly more suspicious.

The analyst can map it to relevant ATT&CK techniques.

---

# 21. Example: Credential Dumping

Possible behavioral evidence:

```text
Suspicious process access
       +
Credential-related memory access
       +
Unexpected privileged process
```

Potential TTP:

```text
Tactic:
Credential Access

Technique:
OS Credential Dumping
```

The analyst should then investigate:

```text
Which account?
Which host?
Which process?
Who initiated it?
Was the activity authorized?
Were credentials exposed?
What happened afterward?
```

---

# 22. IOC vs IOA vs TTP — Practical Comparison

| Question                           | Concept   |
| ---------------------------------- | --------- |
| What malicious IP was used?        | IOC       |
| What file hash was observed?       | IOC       |
| What suspicious behavior occurred? | IOA       |
| How did the attacker execute code? | TTP       |
| What was the attacker's objective? | Tactic    |
| What technique was used?           | Technique |
| How was the technique implemented? | Procedure |

---

# 23. Detection Strategy

A mature SOC should use multiple layers:

```text
             Detection
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
      IOC       IOA       TTP
       │         │         │
       ↓         ↓         ↓
   Artifact   Behavior   Technique
```

This provides stronger detection coverage.

---

# 24. IOC-Based Detection

Example:

```text
IF destination_ip == known_malicious_ip
THEN generate alert
```

Advantages:

* Simple
* Fast
* Useful for known threats

Limitations:

* Easily changed
* Can become outdated
* May produce false positives

---

# 25. Behavior-Based Detection

Example concept:

```text
IF
PowerShell
+
Encoded Command
+
Suspicious Parent Process
+
External Network Connection

THEN
Generate High-Severity Alert
```

This can detect previously unknown infrastructure.

---

# 26. TTP-Based Detection

Instead of detecting:

```text
Known malware hash
```

detect:

```text
Behavior associated with
Credential Access
+
Suspicious process behavior
+
Privilege escalation
```

This can provide broader detection coverage.

---

# 27. MITRE ATT&CK Connection

Your SOC investigation can follow:

```text
IOC
 ↓
Observed Behavior
 ↓
IOA
 ↓
MITRE ATT&CK Technique
 ↓
Detection
 ↓
Investigation
 ↓
Response
```

Example:

```text
PowerShell
   ↓
Suspicious execution
   ↓
IOA
   ↓
MITRE ATT&CK:
Command and Scripting Interpreter: PowerShell
   ↓
Detection Rule
   ↓
SOC Alert
```

---

# 28. Practical Home Lab Exercise

Use your existing lab:

```text
Kali Linux
     +
Windows VM
     +
Sysmon
     +
Wazuh
```

Generate controlled activity such as:

```text
PowerShell Execution
Failed Logins
Suspicious Process Execution
DNS Requests
Network Connections
```

Then collect:

```text
Windows Logs
Sysmon Logs
Wazuh Alerts
Network Data
```

---

# 29. Investigation Exercise

For each activity document:

```text
1. Event
2. IOC
3. IOA
4. TTP
5. Detection
6. Alert
7. Investigation
8. Evidence
9. MITRE ATT&CK Mapping
10. Conclusion
```

Example:

```text
Event:
PowerShell execution

IOC:
Destination IP

IOA:
Encoded PowerShell + external connection

TTP:
Execution → PowerShell

Detection:
Suspicious PowerShell rule

Alert:
High severity

Conclusion:
Potential malicious execution
```

---

# 30. Portfolio Evidence

Create a practical report:

```text
IOC-IOA-TTP-Investigation/
│
├── README.md
├── Scenario.md
├── Evidence/
├── Timeline.md
├── IOC-List.md
├── IOA-Analysis.md
├── MITRE-Mapping.md
├── Detection.md
├── Investigation-Report.md
└── Screenshots/
```

This is much stronger evidence than simply writing:

> "I learned IOC and MITRE ATT&CK."

---

# 31. Interview Questions

You should be able to answer:

### Fundamentals

1. What is an IOC?
2. What is an IOA?
3. What are TTPs?
4. What is the difference between IOC and IOA?
5. What is the difference between tactic and technique?
6. Why are behavioral detections important?

### SOC

7. How would you investigate a suspicious IP?
8. How would you investigate a malicious hash?
9. How would you enrich an IOC?
10. How do you correlate multiple IOCs?
11. How would you map an alert to MITRE ATT&CK?

### Practical

12. Give an example of an IOC.
13. Give an example of an IOA.
14. Give an example of a TTP.
15. How would you investigate suspicious PowerShell?
16. How can an attacker bypass IOC-based detection?

---

# 32. Key Takeaway

```text
IOC
↓
Evidence

IOA
↓
Suspicious Behavior

TTP
↓
Attacker Method

TACTIC
↓
Attacker Objective

TECHNIQUE
↓
How the objective is achieved

PROCEDURE
↓
Specific implementation
```

The SOC analyst's job is not simply to collect IOCs.

The real objective is to connect:

```text
Evidence
   ↓
Behavior
   ↓
Technique
   ↓
Attack Story
   ↓
Risk
   ↓
Response
```

> **IOC tells you what to look for. IOA tells you what suspicious behavior to recognize. TTP tells you how the attacker operates.**
