# Network Device Monitoring

> **Blue Team → SOC → Security Monitoring → Network Device Monitoring**

Network devices are a critical telemetry source for a SOC because they provide visibility into communication between systems, users, applications, servers, and the Internet.

A SOC analyst uses network-device telemetry to answer:

> **Who communicated with whom, over which protocol and port, when did it happen, and was the communication expected?**

Network monitoring typically combines:

```text
Firewalls
+
Routers
+
Switches
+
VPN Gateways
+
IDS/IPS
+
DNS
+
Proxy
+
NetFlow
+
Packet Capture
+
SIEM
```

---

# 1. Objectives

After completing this section, you should understand:

* Network-device monitoring fundamentals
* Firewall monitoring
* Router monitoring
* Switch monitoring
* VPN monitoring
* IDS/IPS monitoring
* Network flows
* NetFlow/IPFIX
* DNS monitoring
* Proxy monitoring
* Network authentication
* Network anomalies
* Scanning detection
* C2 indicators
* Data-exfiltration indicators
* Network-device logs
* SIEM correlation
* Practical network-monitoring investigations

---

# 2. Network Monitoring Architecture

A typical enterprise architecture:

```text
                         INTERNET
                            │
                            ↓
                       FIREWALL
                            │
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
           ROUTER         VPN          IDS/IPS
             │              │              │
             └──────────────┼──────────────┘
                            ↓
                         SWITCH
                            │
            ┌───────────────┼───────────────┐
            ↓               ↓               ↓
        Endpoints         Servers         Wi-Fi
            │               │               │
            └───────────────┼───────────────┘
                            ↓
                       Network Logs
                            ↓
                          SIEM
                            ↓
                         SOC
```

---

# 3. Why Network Device Monitoring Matters

Endpoint logs tell you what happened on a system.

Network telemetry tells you:

```text
Source
Destination
Port
Protocol
Direction
Volume
Timing
```

This can reveal:

```text
Scanning
Brute Force
Lateral Movement
Malware Communication
Command & Control
Data Exfiltration
Unauthorized Access
Policy Violations
```

---

# 4. Major Network Telemetry Sources

| Source         | Primary Visibility       |
| -------------- | ------------------------ |
| Firewall       | Allowed/blocked traffic  |
| Router         | Routing/network activity |
| Switch         | LAN activity             |
| VPN            | Remote access            |
| IDS/IPS        | Threat detection         |
| DNS            | Domain queries           |
| Proxy          | Web activity             |
| NetFlow        | Traffic metadata         |
| Packet Capture | Packet-level evidence    |

A mature SOC correlates multiple sources rather than depending on only one.

---

# 5. Firewall Monitoring

Firewalls are among the most important network telemetry sources.

Typical firewall events include:

```text
Connection Allowed
Connection Blocked
NAT
VPN
Policy Change
Authentication
Threat Detection
```

Important fields:

```text
Source IP
Destination IP
Source Port
Destination Port
Protocol
Action
Rule
Timestamp
Interface
User
```

---

# 6. Allowed vs Blocked Traffic

A firewall may produce:

```text
ALLOW
```

or:

```text
DENY
DROP
REJECT
```

Example:

```text
10.10.10.50
      ↓
203.0.113.10:443
      ↓
ALLOW
```

The connection is allowed.

But:

```text
10.10.10.50
      ↓
203.0.113.20:4444
      ↓
DENY
```

The firewall blocked it.

Neither event is automatically malicious.

Context matters.

---

# 7. Important Firewall Questions

When investigating firewall activity:

```text
Who initiated the connection?
What is the source?
What is the destination?
Which port?
Which protocol?
Was it allowed?
Which firewall rule allowed it?
How frequently did it occur?
Was the destination expected?
```

---

# 8. Repeated Blocked Connections

A pattern such as:

```text
Blocked
Blocked
Blocked
Blocked
Blocked
Blocked
```

may indicate:

```text
Scanning
Malware
Misconfiguration
Unauthorized Application
Policy Violation
```

Investigate:

```text
Source
Destination
Ports
Frequency
Time Window
```

---

# 9. Port Scanning Detection

Port scanning may produce multiple connection attempts against different ports.

Example:

```text
10.10.10.50
      │
      ├── :21
      ├── :22
      ├── :23
      ├── :25
      ├── :80
      ├── :443
      └── :445
```

Potential indicators:

```text
Many Ports
+
Same Source
+
Short Time Window
```

This can indicate reconnaissance.

---

# 10. Horizontal Scanning

Horizontal scanning targets the same port across multiple hosts.

Example:

```text
10.10.10.50
    │
    ├── 10.10.10.1:445
    ├── 10.10.10.2:445
    ├── 10.10.10.3:445
    ├── 10.10.10.4:445
    └── 10.10.10.5:445
```

This may indicate:

```text
SMB Discovery
Service Discovery
Lateral Movement Preparation
```

---

# 11. Vertical Scanning

Vertical scanning targets many ports on a single host.

Example:

```text
10.10.10.50
     │
     ├── :21
     ├── :22
     ├── :23
     ├── :25
     ├── :80
     ├── :139
     ├── :445
     └── :3389
```

This can indicate service enumeration.

---

# 12. Lateral Movement

Network telemetry can help identify movement between internal systems.

Example:

```text
Compromised Workstation
        ↓
Internal Server
        ↓
Domain Controller
```

Monitor:

```text
Internal Source
Internal Destination
Administrative Ports
Authentication
Frequency
```

Common ports of interest include:

```text
22
23
80
443
135
139
445
3389
5985
5986
```

Port numbers alone do not prove malicious activity.

---

# 13. Remote Administration Monitoring

Common remote administration protocols include:

```text
SSH
RDP
WinRM
SMB
VPN
```

A SOC analyst should establish:

```text
Who normally uses them?
From where?
To which systems?
During which hours?
```

Unexpected administrative access should be investigated.

---

# 14. VPN Monitoring

VPN telemetry is important because it provides remote access into enterprise environments.

Monitor:

```text
User
Source IP
VPN Gateway
Login
Logout
Authentication Result
MFA Result
Session Duration
Assigned IP
```

---

# 15. Suspicious VPN Activity

Example:

```text
User
 ↓
VPN Login
 ↓
Unknown Geography / IP
 ↓
Unusual Time
 ↓
Internal Access
```

Possible explanations include:

```text
Compromised Credentials
Legitimate Travel
VPN Infrastructure
False Positive
```

Therefore, investigate rather than immediately declaring compromise.

---

# 16. VPN Authentication Failures

Repeated VPN failures can indicate:

```text
Brute Force
Password Spraying
Credential Abuse
Misconfiguration
```

Correlate:

```text
Failed Login
+
Source IP
+
Target User
+
Successful Login
+
Internal Activity
```

---

# 17. IDS and IPS

### IDS

Intrusion Detection System:

```text
Detects
+
Alerts
```

### IPS

Intrusion Prevention System:

```text
Detects
+
Blocks / Prevents
```

IDS/IPS can detect patterns associated with:

```text
Scanning
Exploitation
Malware
C2
Policy Violations
Known Attack Signatures
```

---

# 18. IDS/IPS Alert Investigation

When an IDS/IPS alert occurs, examine:

```text
Signature
Source
Destination
Port
Protocol
Timestamp
Severity
Action
Payload / Context
```

Do not treat every IDS alert as a confirmed compromise.

Determine:

```text
True Positive
False Positive
Benign Trigger
Suspicious Activity
```

---

# 19. Signature-Based Detection

Traditional IDS/IPS systems can use signatures.

Example:

```text
Known Attack Pattern
        ↓
Signature Match
        ↓
Alert
```

Advantages:

```text
Fast
Known Threat Detection
Easy to Understand
```

Limitations:

```text
Unknown Threats
Evasion
Encrypted Traffic
Novel Attacks
```

---

# 20. Network Flow Monitoring

Network flow records provide metadata about communication.

Typical information:

```text
Source IP
Destination IP
Source Port
Destination Port
Protocol
Bytes
Packets
Start Time
End Time
```

Flow telemetry does not necessarily contain full packet contents.

---

# 21. NetFlow / IPFIX

Common flow technologies include:

```text
NetFlow
IPFIX
sFlow
```

These help identify traffic patterns at scale.

Example:

```text
Host A
   ↓
Host B
   ↓
443
   ↓
2 GB
   ↓
3 Hours
```

This may be legitimate or suspicious depending on the environment.

---

# 22. Beaconing

Malware may communicate with an external destination periodically.

Example:

```text
10:00 → 203.0.113.10
10:05 → 203.0.113.10
10:10 → 203.0.113.10
10:15 → 203.0.113.10
```

Potential indicator:

```text
Regular
+
Repeated
+
Unexpected
```

This pattern is sometimes associated with command-and-control beaconing.

---

# 23. Command and Control Monitoring

Possible network indicators include:

```text
Periodic Connections
Unknown External Domains
Rare Destinations
Unusual Ports
Encrypted Connections
DNS Anomalies
Unexpected Protocols
```

Correlation with endpoint telemetry is important.

Example:

```text
powershell.exe
      ↓
HTTPS
      ↓
Rare External Domain
```

This is more useful than looking at the network connection alone.

---

# 24. DNS Monitoring

DNS is a critical detection source.

Monitor:

```text
Query
Client
Domain
Response
Frequency
Query Type
```

Potential indicators:

```text
Suspicious Domain
DGA
DNS Tunneling
Rare Domain
Large Number of Queries
Newly Observed Domain
```

---

# 25. DNS Tunneling

DNS can sometimes be abused to transfer information.

Conceptually:

```text
Internal Host
     ↓
Encoded Data
     ↓
DNS Queries
     ↓
Attacker-Controlled Domain
```

Potential indicators:

```text
Long Subdomains
High Query Volume
Random-Looking Strings
Repeated Queries
Unusual Record Types
```

Detection requires baselining because legitimate applications can also generate unusual DNS traffic.

---

# 26. Proxy Monitoring

Enterprise proxies can provide web visibility.

Useful fields:

```text
User
Source IP
URL
Domain
HTTP Method
Response
Bytes
User Agent
Timestamp
```

This can support:

```text
Malware Investigation
Phishing Investigation
Data Loss Investigation
Web Policy Monitoring
Threat Hunting
```

---

# 27. HTTP/HTTPS Monitoring

Monitor:

```text
Domain
URL
Method
Status Code
User Agent
Source
Destination
```

For HTTPS, visibility depends heavily on the organization's architecture and whether TLS inspection is deployed.

Do not assume that full URL/content visibility is available.

---

# 28. Suspicious Web Activity

Potential indicators:

```text
Unexpected Domain
Malware Infrastructure
Suspicious File Download
Rare User Agent
Unusual HTTP Method
Large Upload
Repeated Requests
```

Example:

```text
User
 ↓
Unknown Website
 ↓
Executable Download
 ↓
Endpoint Execution
```

This becomes much stronger when endpoint and proxy telemetry correlate.

---

# 29. Data Exfiltration Monitoring

Network monitoring can identify unusual outbound data transfer.

Example:

```text
Internal Server
      ↓
External Destination
      ↓
Large Data Volume
      ↓
Unusual Time
```

Investigate:

```text
Source
Destination
Volume
Protocol
Application
User
Time
```

Potential channels include:

```text
HTTPS
DNS
Cloud Storage
FTP
SSH
Email
```

---

# 30. Data Exfiltration Baseline

A large transfer is not automatically malicious.

For example:

```text
Backup Server
 ↓
Cloud Storage
 ↓
500 GB
```

may be completely legitimate.

Therefore compare:

```text
Current Transfer
vs
Historical Baseline
```

---

# 31. Network Device Configuration Monitoring

Network-device configuration changes should be monitored.

Examples:

```text
Firewall Rule
Router Configuration
ACL
VPN Configuration
NAT
Routing
DNS
Switch Configuration
```

Potentially suspicious:

```text
Unexpected Rule
+
Unexpected Administrator
+
Unusual Time
```

---

# 32. Firewall Rule Changes

A new firewall rule can create a major security risk.

Example:

```text
ALLOW
Internet
   ↓
Internal Server
   ↓
Port 3389
```

This should be reviewed.

Questions:

```text
Who created it?
Why?
When?
Was it approved?
What system is exposed?
How long should it remain?
```

---

# 33. Router Monitoring

Routers can provide:

```text
Interface Events
Routing Changes
Authentication
Configuration Changes
ACL Events
Traffic Metadata
```

Potential indicators:

```text
Unexpected Configuration
New Route
Interface Failure
Authentication Anomaly
Unexpected Administrative Access
```

---

# 34. Switch Monitoring

Switches can provide visibility into LAN infrastructure.

Monitor:

```text
Port Status
MAC Address Changes
Authentication
VLAN Changes
Configuration
Spanning Tree Events
```

Potential security concerns include:

```text
Unexpected Device
Unauthorized Port
VLAN Manipulation
MAC Flapping
```

---

# 35. Network Authentication

Enterprise networks may use:

```text
802.1X
RADIUS
TACACS+
VPN Authentication
Directory Services
```

Monitor:

```text
User
Device
Source
Authentication Result
Method
Time
```

Repeated failures may indicate credential attacks.

---

# 36. Network Anomaly Detection

Anomaly detection looks for deviations from normal behavior.

Example:

```text
Normal:
Workstation → 10 internal servers
```

Anomaly:

```text
Workstation → 500 internal hosts
```

Potential explanation:

```text
Network Scanner
Compromised Host
IT Discovery Tool
Vulnerability Scanner
```

Context determines the conclusion.

---

# 37. Network Monitoring Investigation Flow

```text
Alert
 ↓
Identify Source
 ↓
Identify Destination
 ↓
Identify User / Device
 ↓
Check Port / Protocol
 ↓
Check Frequency
 ↓
Check Historical Baseline
 ↓
Correlate Endpoint Data
 ↓
Correlate Identity Data
 ↓
Determine Intent
 ↓
Classify Alert
```

---

# 38. Practical Lab — Firewall Investigation

## Objective

Understand firewall telemetry.

Generate controlled traffic between your lab machines.

Record:

```text
Source
Destination
Port
Protocol
Action
Timestamp
```

Compare:

```text
Allowed Traffic
vs
Blocked Traffic
```

Document the difference.

---

# 39. Practical Lab — Port Scanning Detection

Use your isolated lab network.

Perform controlled scanning against your own VM.

Observe:

```text
Multiple Ports
Multiple Connections
Source
Destination
Time
```

Build a detection concept:

```text
One Source
+
Many Destination Ports
+
Short Time Window
```

Document:

```text
Scan
Evidence
Detection
Conclusion
```

---

# 40. Practical Lab — Horizontal Scan

In your isolated lab:

```text
Scanner
   ↓
Host 1 : Port X
Host 2 : Port X
Host 3 : Port X
Host 4 : Port X
```

Observe network telemetry.

Determine:

```text
Source
Targets
Port
Frequency
```

---

# 41. Practical Lab — VPN Monitoring

If your home lab includes a VPN service, generate controlled authentication activity.

Observe:

```text
Successful Login
Failed Login
Source IP
User
Session
```

Build a timeline.

---

# 42. Practical Lab — DNS Investigation

Generate normal DNS queries from your lab machines.

Observe:

```text
Client
Domain
Query Type
Timestamp
Frequency
```

Then compare:

```text
Normal DNS
vs
Unusual DNS Pattern
```

---

# 43. Practical Lab — Network Flow Analysis

Collect flow information from your lab network where supported.

Analyze:

```text
Top Sources
Top Destinations
Top Ports
Top Protocols
Highest Bytes
Longest Sessions
```

Use the results to establish a baseline.

---

# 44. Practical Lab — Suspicious Outbound Connection

Create a controlled test connection from a lab endpoint.

Investigate:

```text
Source Host
Process
Destination
Port
Protocol
Time
Bytes
```

Then correlate endpoint telemetry.

Goal:

```text
Network Event
      ↓
Endpoint Process
      ↓
User
      ↓
Intent
```

---

# 45. Practical Lab — Firewall Rule Change

Inside your lab:

```text
Create Test Rule
      ↓
Generate Traffic
      ↓
Observe Effect
      ↓
Review Logs
      ↓
Remove Rule
```

Document:

```text
Rule
Purpose
Administrator
Traffic
Evidence
Result
```

---

# 46. Practical Lab — Network Attack Timeline

Build a complete investigation:

```text
Port Scan
   ↓
Successful Connection
   ↓
Authentication
   ↓
Internal Movement
   ↓
Suspicious Outbound Connection
```

Correlate:

```text
Firewall
+
Endpoint
+
Authentication
+
DNS
```

This is closer to real SOC work than analyzing a single log.

---

# 47. Network Monitoring Detection Matrix

| Activity            | Telemetry             | Investigation         |
| ------------------- | --------------------- | --------------------- |
| Port Scan           | Firewall / Flow       | Source + ports        |
| Horizontal Scan     | Flow                  | Source + many hosts   |
| Brute Force         | Firewall + Auth       | Attempts + success    |
| Lateral Movement    | Firewall + Endpoint   | Internal connections  |
| C2                  | Flow + DNS + Endpoint | Beaconing             |
| DNS Tunneling       | DNS                   | Query patterns        |
| Exfiltration        | Flow / Proxy          | Volume + destination  |
| VPN Abuse           | VPN                   | User + source         |
| Firewall Change     | Firewall Audit        | Administrator         |
| Router Change       | Router Logs           | Admin + configuration |
| Unauthorized Device | Switch                | MAC + port            |
| IDS Alert           | IDS/IPS               | Signature + context   |

---

# 48. Network Investigation Questions

### Source

```text
Who or what initiated the connection?
```

### Destination

```text
What system received it?
```

### Protocol

```text
Why was this protocol used?
```

### Port

```text
Is the port expected?
```

### Frequency

```text
How often did it happen?
```

### Volume

```text
How much data moved?
```

### Identity

```text
Which user or device was involved?
```

### Context

```text
Is this normal for this host?
```

---

# 49. Network Monitoring Blind Spots

Common weaknesses include:

```text
No centralized network logging
Insufficient firewall logging
No DNS visibility
No NetFlow
No IDS/IPS
No VPN logging
Poor log retention
Encrypted traffic without appropriate visibility
No endpoint correlation
No baseline
```

A SOC should understand these limitations.

---

# 50. Network Monitoring with Wazuh

Wazuh can ingest and correlate selected network/security telemetry depending on the architecture.

A practical home-lab design:

```text
Kali
Windows
Linux
   │
   ↓
Network Traffic
   │
   ├── Firewall Logs
   ├── DNS
   ├── Sysmon
   └── Linux Logs
          │
          ↓
        Wazuh
          │
          ↓
         SIEM
          │
          ↓
       Detection
```

For deeper packet analysis, use a dedicated network-analysis tool alongside Wazuh.

---

# 51. Network Monitoring + Wireshark

Wireshark provides packet-level visibility.

Use it when you need to investigate:

```text
Protocol
Packet
Handshake
DNS
HTTP
TCP
UDP
TLS
```

Example workflow:

```text
SIEM Alert
    ↓
Identify Connection
    ↓
Retrieve Packet Capture
    ↓
Filter Traffic
    ↓
Inspect Protocol
    ↓
Extract Evidence
```

---

# 52. Network Monitoring + Nmap

Nmap is useful for controlled asset and service discovery.

In a SOC lab:

```text
Nmap Scan
   ↓
Firewall Logs
   ↓
Network Flow
   ↓
IDS Detection
   ↓
SIEM Alert
```

This demonstrates how offensive activity appears from a defensive monitoring perspective.

Only scan systems you own or are explicitly authorized to test.

---

# 53. Interview Scenario

> **A SOC alert reports that one workstation contacted 200 internal IP addresses on port 445 within five minutes. How would you investigate?**

Start with:

```text
Source Host
 ↓
User
 ↓
Destination Hosts
 ↓
Port 445
 ↓
Connection Count
 ↓
Time Window
 ↓
Process
 ↓
Authentication
```

Possible explanations:

```text
SMB Discovery
Vulnerability Scanner
Administrative Tool
Compromised Host
Lateral Movement
```

Correlate endpoint and identity telemetry before classifying the alert.

---

# 54. Interview Scenario — Possible C2

> **A workstation makes an HTTPS connection to the same external IP every five minutes. What would you check?**

Investigate:

```text
Destination Reputation
        ↓
DNS History
        ↓
Process
        ↓
User
        ↓
Connection Frequency
        ↓
TLS / Domain Context
        ↓
Historical Baseline
```

If the process is unexpected:

```text
Endpoint Investigation
+
Network Investigation
```

should proceed together.

---

# 55. Portfolio Deliverables

For this section, create:

```text
01-Firewall-Monitoring/
02-Port-Scan-Detection/
03-Horizontal-Scan/
04-VPN-Monitoring/
05-DNS-Investigation/
06-Network-Flow-Analysis/
07-Suspicious-Outbound-Connection/
08-Firewall-Rule-Monitoring/
09-Network-Attack-Timeline/
```

Each lab should contain:

```text
README.md
Evidence/
Screenshots/
Detection/
Investigation.md
Conclusion.md
```

---

# 56. Evidence Checklist

For every investigation capture:

```text
Source IP
Destination IP
Source Port
Destination Port
Protocol
Action
Timestamp
User
Hostname
Process
Bytes
Packets
Rule / Signature
Alert
Screenshot
Timeline
Conclusion
```

---

# 57. Key Takeaways

```text
1. Network devices provide visibility beyond individual endpoints.

2. Firewalls provide important connection and policy telemetry.

3. IDS/IPS can identify known suspicious patterns.

4. NetFlow provides scalable traffic metadata.

5. DNS is a valuable security telemetry source.

6. VPN monitoring is essential for remote-access security.

7. Port scanning can be identified through connection patterns.

8. Lateral movement often generates internal network activity.

9. C2 may reveal periodic communication patterns.

10. Data exfiltration can produce unusual outbound traffic.

11. Configuration changes to network devices must be monitored.

12. Baselines are necessary to distinguish anomalies from legitimate activity.

13. Network telemetry becomes significantly more powerful when correlated with endpoint and identity data.

14. Wireshark provides packet-level investigation capability.

15. The SOC objective is to convert network activity into an understandable security narrative.
```

---

# 58. Final Mental Model

```text
                    NETWORK ENVIRONMENT
                           │
        ┌──────────────────┼──────────────────┐
        ↓                  ↓                  ↓
     Firewall            Router             Switch
        │                  │                  │
        ├──────────────────┼──────────────────┤
        ↓                  ↓                  ↓
       VPN              IDS/IPS             DNS
        │                  │                  │
        └──────────────────┼──────────────────┘
                           ↓
                    Network Telemetry
                           │
              ┌────────────┼────────────┐
              ↓            ↓            ↓
            Flow         Logs        Packets
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
                    Timeline / Report
```

> **Network-device monitoring is not simply watching firewall logs. It is the ability to reconstruct communication patterns across the environment and correlate them with identity, endpoint, and application telemetry to detect threats.**
