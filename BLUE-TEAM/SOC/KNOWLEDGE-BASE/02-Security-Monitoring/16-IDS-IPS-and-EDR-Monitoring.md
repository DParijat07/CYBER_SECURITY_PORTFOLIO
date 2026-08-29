# IDS, IPS and EDR Monitoring

## 1. Introduction

IDS, IPS, and EDR are important security monitoring technologies used by Security Operations Centers (SOCs) to detect, investigate, and respond to malicious activity.

They provide visibility across different parts of the environment:

- IDS monitors and detects suspicious network activity
- IPS detects and can actively block malicious network activity
- EDR monitors endpoint activity and provides investigation and response capabilities

A simplified monitoring architecture is:

Network Traffic
      ↓
IDS / IPS
      ↓
Network Detection
      ↓
SIEM
      ↓
SOC Analyst

Endpoint
      ↓
EDR Agent
      ↓
Process / File / Network Telemetry
      ↓
SIEM / XDR
      ↓
SOC Analyst


---

## 2. IDS

IDS stands for Intrusion Detection System.

An IDS monitors network or system activity and generates alerts when suspicious or malicious behavior is detected.

The primary purpose of an IDS is:

> Detect suspicious activity and notify security teams.

An IDS generally does not block traffic automatically.

Example:

Attacker
   ↓
Malicious Network Traffic
   ↓
IDS
   ↓
Alert
   ↓
SOC Analyst


---

## 3. IPS

IPS stands for Intrusion Prevention System.

An IPS performs detection similar to an IDS but can also take preventive action.

Typical actions include:

- Block traffic
- Drop packets
- Reset connections
- Block source IP
- Update firewall rules

Example:

Attacker
   ↓
Malicious Traffic
   ↓
IPS
   ↓
Detection
   ↓
Traffic Blocked


---

## 4. IDS vs IPS

| Feature | IDS | IPS |
|---|---|---|
| Detection | Yes | Yes |
| Alerting | Yes | Yes |
| Traffic Blocking | Usually No | Yes |
| Network Position | Often Out-of-Band | Usually Inline |
| Risk of False Positive Impact | Lower | Higher |
| Primary Purpose | Detection | Prevention |

An IDS is generally focused on visibility, while an IPS adds active prevention.

---

## 5. Types of IDS

IDS can be broadly categorized into:

### Network-Based IDS

NIDS monitors network traffic.

Examples:

- Snort
- Suricata
- Zeek-based detection systems

Monitor:

- Packets
- Protocols
- Connections
- Source IPs
- Destination IPs
- Ports
- Network signatures


### Host-Based IDS

HIDS monitors activity on individual systems.

Monitor:

- File changes
- Processes
- Authentication
- System calls
- Configuration changes
- Logs

Examples include host-based monitoring capabilities integrated into security agents.

---

## 6. Network-Based Monitoring

A NIDS analyzes traffic flowing through network infrastructure.

Typical telemetry includes:

    Source IP
    Destination IP
    Source Port
    Destination Port
    Protocol
    Packet Information
    Timestamp
    Signature
    Action
    Severity

Example:

    10.10.10.15
         ↓
    10.10.10.20:445
         ↓
    SMB Traffic
         ↓
    Suspicious Pattern
         ↓
    IDS Alert


---

## 7. Signature-Based Detection

Signature-based IDS/IPS detection looks for known patterns associated with attacks.

Examples:

- Known exploit patterns
- Malware signatures
- Command patterns
- Protocol anomalies
- Known malicious payloads

Example:

    Network Traffic
          ↓
    Signature Match
          ↓
    Detection
          ↓
    Alert

Advantages:

- Fast detection
- Easy to understand
- Effective against known threats

Limitations:

- Less effective against unknown attacks
- Can be bypassed by modified payloads
- Requires updated signatures


---

## 8. Anomaly-Based Detection

Anomaly detection identifies behavior that differs from established baselines.

Example:

Normal:

    100 connections/hour

Observed:

    10,000 connections/hour

This could indicate:

- Scanning
- Malware
- Data transfer
- Misconfiguration
- Legitimate workload increase

Anomaly detection can identify previously unknown behavior but may generate more false positives.


---

## 9. Protocol-Based Detection

IDS/IPS systems can inspect network protocols for suspicious behavior.

Examples:

- HTTP
- HTTPS
- DNS
- FTP
- SSH
- SMB
- RDP
- SMTP
- LDAP

Example:

    DNS Query
       ↓
    Unusual Domain
       ↓
    Suspicious Pattern
       ↓
    IDS Alert


---

## 10. IDS/IPS Alert Information

A typical IDS/IPS alert may contain:

    Alert ID
    Timestamp
    Source IP
    Destination IP
    Source Port
    Destination Port
    Protocol
    Signature
    Severity
    Action
    Sensor
    Direction
    Payload Information

SOC analysts should examine these fields during triage.


---

## 11. IDS/IPS Severity

A practical severity model can be:

### Low

Examples:

- Minor protocol anomaly
- Low-confidence scan
- Benign signature match

### Medium

Examples:

- Suspicious network activity
- Possible reconnaissance
- Repeated connection anomalies

### High

Examples:

- Exploit attempt
- Malware communication
- Credential attack
- Command-and-control activity

### Critical

Examples:

- Confirmed exploitation
- Active malware communication
- Successful intrusion
- Critical infrastructure attack


---

## 12. Common IDS/IPS Detection Categories

IDS/IPS systems can detect:

- Port scanning
- Network scanning
- Brute-force attacks
- Exploit attempts
- Malware traffic
- Command and control
- Denial-of-service activity
- Suspicious DNS traffic
- Protocol anomalies
- Data exfiltration patterns
- Lateral movement
- Web attacks


---

## 13. Port Scan Detection

Attackers may scan systems to discover open ports and services.

Example:

    Attacker
       ↓
    10.10.10.10
       ↓
    Port 21
    Port 22
    Port 23
    Port 25
    Port 53
    Port 80
    Port 443
    ...

An IDS may generate:

    Potential Port Scan Detected

The SOC analyst should determine whether the scanning is:

- Authorized
- Internal vulnerability scanning
- Security testing
- Malicious reconnaissance


---

## 14. Brute-Force Detection

IDS/IPS can identify repeated authentication attempts.

Example:

    Source IP
       ↓
    SSH
       ↓
    Failed Login
       ↓
    Failed Login
       ↓
    Failed Login
       ↓
    Failed Login

This may indicate an SSH brute-force attack.

The analyst should correlate network alerts with authentication logs.


---

## 15. Exploit Detection

IDS/IPS may detect known exploit patterns.

Example:

    Attacker
       ↓
    Exploit Payload
       ↓
    Vulnerable Server
       ↓
    IDS
       ↓
    Exploit Alert

The presence of an exploit attempt does not necessarily mean exploitation succeeded.

The SOC analyst must determine:

1. Was the target vulnerable?
2. Did the request reach the target?
3. Was the exploit successful?
4. Was a process created?
5. Was persistence established?
6. Was data accessed?


---

## 16. Command and Control Detection

C2 communication allows compromised systems to communicate with attacker-controlled infrastructure.

Possible indicators include:

- Periodic outbound connections
- Known malicious IP addresses
- Suspicious domains
- DNS tunneling
- Unusual ports
- Encrypted communication
- Beacon-like traffic

Example:

    Compromised Host
          ↓
    Every 60 seconds
          ↓
    External Server
          ↓
    C2 Communication


---

## 17. DNS Monitoring

DNS is frequently used during attacks.

Monitor:

- Unusual domain names
- High query frequency
- Random-looking subdomains
- Newly registered domains
- Suspicious TLDs
- DNS tunneling indicators
- DNS requests to known malicious infrastructure

Example:

    workstation01
          ↓
    Unusual DNS Queries
          ↓
    Suspicious Domain
          ↓
    External Connection

DNS alerts should be correlated with endpoint activity.


---

# 18. EDR

EDR stands for Endpoint Detection and Response.

EDR continuously monitors endpoint activity and provides security telemetry for detection, investigation, and response.

EDR focuses heavily on:

- Processes
- Files
- Registry
- Command execution
- Network connections
- Authentication
- Persistence
- User activity

Example:

    Endpoint
       ↓
    EDR Agent
       ↓
    Telemetry
       ↓
    Detection
       ↓
    SOC


---

## 19. EDR Telemetry

Important EDR telemetry includes:

### Process Information

    Process Name
    Parent Process
    Command Line
    Process ID
    User
    Timestamp

### File Information

    File Name
    Path
    Hash
    Creation
    Modification
    Deletion

### Network Information

    Source IP
    Destination IP
    Port
    Protocol
    Process

### User Information

    Username
    Login
    Session
    Privileges


---

## 20. Process Monitoring

Process monitoring is one of the most important EDR capabilities.

Example:

    winword.exe
         ↓
    powershell.exe
         ↓
    cmd.exe
         ↓
    network connection

This process chain may indicate malicious execution.

The SOC analyst should investigate:

- Parent process
- Command line
- User
- File path
- Hash
- Network activity


---

## 21. Parent-Child Process Analysis

Attackers often abuse legitimate applications to launch malicious processes.

Example:

    winword.exe
         ↓
    powershell.exe
         ↓
    rundll32.exe

This process chain should be reviewed.

Another example:

    outlook.exe
         ↓
    powershell.exe
         ↓
    network connection

This may indicate malicious email attachment or macro-related activity.


---

## 22. Command-Line Monitoring

Command-line arguments can provide valuable evidence.

Examples:

    powershell.exe -enc ...
    cmd.exe /c ...
    certutil.exe ...
    rundll32.exe ...
    mshta.exe ...

Suspicious command-line activity should be investigated together with:

- User
- Parent process
- File path
- Hash
- Network connection
- Execution time


---

## 23. File Monitoring

EDR can detect suspicious file activity.

Monitor:

- File creation
- File modification
- File deletion
- File execution
- File hash
- Temporary files
- Executables
- Scripts

Example:

    User Downloads File
          ↓
    File Created
          ↓
    File Executed
          ↓
    PowerShell Started
          ↓
    External Connection

This sequence should be investigated.


---

## 24. Persistence Monitoring

EDR can detect common persistence mechanisms.

Examples:

- Registry Run Keys
- Scheduled Tasks
- Services
- Startup folders
- Cron jobs
- Systemd services
- Startup scripts
- New user accounts

Example:

    Malware
       ↓
    Registry Run Key
       ↓
    Persistence


---

## 25. Credential Access Monitoring

EDR can detect suspicious access to credentials.

Potential indicators include:

- LSASS access
- Credential dumping tools
- Browser credential access
- Password database access
- Suspicious memory access

Example:

    Suspicious Process
          ↓
    LSASS Access
          ↓
    Credential Theft
          ↓
    Lateral Movement


---

## 26. Lateral Movement Monitoring

EDR can help detect lateral movement across systems.

Common techniques include:

- RDP
- SMB
- WinRM
- SSH
- Remote PowerShell
- PsExec-like activity

Example:

    Host A
      ↓
    Credential Use
      ↓
    Host B
      ↓
    Remote Execution
      ↓
    Host C


---

## 27. EDR Network Monitoring

EDR can associate network connections with individual processes.

Example:

    powershell.exe
          ↓
    10.10.10.15
          ↓
    443
          ↓
    External Server

This is more useful than simply knowing that the endpoint made an outbound connection.

The analyst can investigate:

- Which process created the connection?
- Which user launched the process?
- What command line was used?
- What destination was contacted?


---

## 28. File Hash Analysis

EDR commonly provides file hashes.

Common hash types:

- MD5
- SHA-1
- SHA-256

SHA-256 is commonly preferred for modern file identification.

A suspicious hash can be investigated against approved threat intelligence sources.

Example:

    Suspicious.exe
         ↓
    SHA-256
         ↓
    Threat Intelligence
         ↓
    Known Malware?


---

## 29. IDS/IPS + EDR Correlation

Combining network and endpoint telemetry creates stronger detection.

Example:

    IDS Alert
    Suspicious C2 Traffic
          ↓
    EDR
    PowerShell Process
          ↓
    Same Host
          ↓
    Correlated Alert
          ↓
    SOC Investigation

This is stronger than investigating either alert independently.


---

## 30. Example Correlated Attack

Consider:

    10:00
    IDS detects suspicious exploit attempt
          ↓
    10:01
    EDR detects PowerShell execution
          ↓
    10:02
    EDR detects new scheduled task
          ↓
    10:03
    Endpoint connects to external IP
          ↓
    10:04
    Internal SMB connections detected

This sequence may indicate:

    Initial Access
          ↓
    Execution
          ↓
    Persistence
          ↓
    Command and Control
          ↓
    Lateral Movement


---

## 31. SIEM Integration

IDS, IPS, and EDR alerts should be forwarded to the SIEM.

Example:

    IDS
     +
    IPS
     +
    EDR
     +
    Firewall
     +
    Authentication Logs
     +
    DNS
     ↓
    SIEM
     ↓
    Correlation
     ↓
    SOC Alert


---

## 32. Detection Rules

### Rule 1 — IDS Exploit + EDR Process

    IF
    IDS detects exploit attempt

    AND

    EDR detects suspicious process
    on the same host

    THEN
    generate high-priority alert

Severity:

    High


### Rule 2 — Suspicious PowerShell + Network Connection

    IF
    PowerShell executes

    AND
    establishes an external network connection

    THEN
    generate investigation alert

Severity:

    High


### Rule 3 — EDR C2 Detection

    IF
    endpoint connects periodically
    to suspicious external infrastructure

    THEN
    generate C2 investigation alert

Severity:

    High


### Rule 4 — Credential Access + Lateral Movement

    IF
    suspicious credential access occurs

    AND
    remote authentication follows

    THEN
    generate high-priority alert

Severity:

    Critical


### Rule 5 — Malware Persistence

    IF
    suspicious executable creates
    a scheduled task or service

    THEN
    generate persistence alert

Severity:

    High


---

## 33. Example SOC Alert

Alert:

    Potential Endpoint Compromise

Severity:

    Critical

Host:

    WIN-CLIENT01

Related Events:

    IDS detected exploit traffic
    PowerShell process created
    Suspicious executable created
    External connection established
    Scheduled task created

Timeline:

    11:20 — Exploit attempt detected
    11:21 — PowerShell executed
    11:22 — Suspicious file created
    11:23 — External connection detected
    11:24 — Persistence mechanism created

### Analyst Comment

Multiple correlated security events were observed on the same endpoint. An IDS detected suspicious exploit traffic, followed by PowerShell execution, suspicious file creation, outbound communication, and persistence activity identified by EDR. The sequence is consistent with potential endpoint compromise and should be escalated for immediate containment and investigation.


---

## 34. SOC Triage Process

### Step 1 — Identify the Alert

Determine:

    Detection Source
    Alert Type
    Severity
    Timestamp
    Host

### Step 2 — Identify the Endpoint

Check:

    Hostname
    IP Address
    Operating System
    User
    Asset Criticality

### Step 3 — Analyze Network Activity

Check:

    Source IP
    Destination IP
    Port
    Protocol
    Domain
    Network Direction

### Step 4 — Analyze Process Activity

Check:

    Process Name
    Parent Process
    Command Line
    User
    Process Path
    Hash

### Step 5 — Analyze File Activity

Check:

    File Creation
    File Modification
    File Hash
    File Location
    Execution

### Step 6 — Check Persistence

Look for:

    Scheduled Tasks
    Services
    Registry Run Keys
    Startup Items
    Cron Jobs

### Step 7 — Check Credential Activity

Look for:

    Credential Access
    LSASS Access
    Credential Dumping
    Suspicious Authentication

### Step 8 — Check Lateral Movement

Look for:

    RDP
    SMB
    SSH
    WinRM
    Remote Execution

### Step 9 — Determine Impact

Ask:

    Was exploitation successful?
    Was malware executed?
    Was persistence established?
    Was credential theft performed?
    Was lateral movement performed?
    Was data accessed?

### Step 10 — Response

Depending on severity:

    Isolate Endpoint
    Block IP / Domain
    Kill Malicious Process
    Quarantine File
    Disable Compromised Account
    Reset Credentials
    Escalate Incident


---

## 35. IDS/IPS and EDR Investigation Checklist

    [ ] Identify alert source
    [ ] Identify affected host
    [ ] Identify affected user
    [ ] Check source IP
    [ ] Check destination IP
    [ ] Check destination port
    [ ] Identify protocol
    [ ] Identify IDS/IPS signature
    [ ] Check alert severity
    [ ] Determine whether traffic was blocked
    [ ] Review process tree
    [ ] Review command line
    [ ] Review file activity
    [ ] Check file hash
    [ ] Check persistence mechanisms
    [ ] Check credential access
    [ ] Check network connections
    [ ] Check DNS activity
    [ ] Check lateral movement
    [ ] Correlate with authentication logs
    [ ] Correlate with SIEM alerts
    [ ] Determine compromise status
    [ ] Determine impact
    [ ] Assign severity
    [ ] Document findings
    [ ] Contain if required
    [ ] Escalate if required


---

## 36. IDS/IPS and EDR Best Practices

Organizations should:

- Keep IDS/IPS signatures updated
- Regularly tune detection rules
- Minimize false positives
- Deploy EDR across critical endpoints
- Monitor process execution
- Monitor command lines
- Monitor network connections
- Monitor persistence mechanisms
- Monitor credential access
- Integrate IDS/IPS with SIEM
- Integrate EDR with SIEM
- Correlate network and endpoint telemetry
- Establish endpoint baselines
- Maintain incident response procedures
- Regularly test detection capabilities
- Review detection coverage
- Protect security monitoring infrastructure


---

## 37. Key Takeaways

IDS, IPS, and EDR provide complementary visibility.

IDS focuses primarily on:

    Network Detection
          ↓
    Alerting

IPS adds:

    Detection
          ↓
    Prevention

EDR provides:

    Endpoint Telemetry
          ↓
    Detection
          ↓
    Investigation
          ↓
    Response

The strongest SOC detections come from correlating these technologies.

A typical detection chain is:

    Network Alert
          ↓
    Endpoint Process
          ↓
    File Activity
          ↓
    Network Connection
          ↓
    Persistence
          ↓
    Credential Activity
          ↓
    Lateral Movement
          ↓
    Incident Response

**IDS and IPS provide network-level visibility and control, while EDR provides deep endpoint visibility and response capabilities. A mature SOC combines both to detect and investigate attacks across the complete attack chain.**
