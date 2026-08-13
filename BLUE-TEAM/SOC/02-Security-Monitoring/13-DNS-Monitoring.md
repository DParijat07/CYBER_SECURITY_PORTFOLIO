# DNS Monitoring

## 1. Introduction

DNS monitoring is the process of collecting, analyzing, and correlating Domain Name System (DNS) activity to identify suspicious domains, malicious communication, malware behavior, command-and-control (C2) activity, data exfiltration, DNS tunneling, and other security threats.

DNS is a critical security telemetry source because almost every Internet-connected system relies on DNS to resolve domain names.

From a SOC perspective, DNS monitoring helps answer:

* Which host made the DNS request?
* Which domain was requested?
* What IP address was returned?
* How frequently was the domain queried?
* Is the domain known to be malicious?
* Is the requested domain unusual for the organization?
* Does the behavior indicate malware or C2 communication?

Typical flow:

```text
Endpoint
   ↓
DNS Query
   ↓
DNS Resolver
   ↓
Internet DNS
   ↓
DNS Response
   ↓
Security Monitoring / SIEM
   ↓
SOC Analyst
```

---

## 2. Why DNS Monitoring Is Important

Attackers frequently abuse DNS during different stages of an attack.

DNS can provide visibility into:

* Malware communication
* Command-and-control infrastructure
* Phishing campaigns
* Malicious domains
* Domain generation algorithms
* DNS tunneling
* Data exfiltration
* Malware beaconing
* Reconnaissance
* Compromised endpoints

Even when encrypted protocols are used for application traffic, DNS metadata may still provide useful detection signals.

---

## 3. Objectives of DNS Monitoring

The main objectives are:

1. Detect malicious domains
2. Identify suspicious DNS queries
3. Detect malware C2 communication
4. Detect DNS tunneling
5. Identify domain generation algorithm activity
6. Detect DNS-based data exfiltration
7. Monitor unusual DNS volume
8. Identify compromised endpoints
9. Correlate DNS activity with endpoint and network telemetry
10. Support incident investigation

---

## 4. DNS Monitoring Sources

Important DNS telemetry sources include:

* Internal DNS servers
* DNS resolvers
* Windows DNS Server
* Linux DNS services
* Firewall DNS logs
* Secure DNS gateways
* Endpoint DNS telemetry
* Network sensors
* SIEM platforms
* DNS security services

Common DNS-related information includes:

```text
Timestamp
Source IP
Hostname
Requested Domain
Record Type
Response Code
Resolved IP
Query Frequency
Query Length
DNS Server
User
```

---

## 5. Important DNS Record Types

SOC analysts should understand common DNS record types.

### A Record

Maps a domain name to an IPv4 address.

```text
example.com → 192.0.2.10
```

### AAAA Record

Maps a domain name to an IPv6 address.

```text
example.com → 2001:db8::10
```

### CNAME

Creates an alias for another domain.

### MX

Identifies mail servers for a domain.

### NS

Identifies authoritative name servers.

### TXT

Contains text information and is commonly used for domain verification and email-security mechanisms.

### PTR

Used for reverse DNS lookups.

---

## 6. Important DNS Log Fields

A SOC analyst should examine:

```text
Timestamp
Source IP
Hostname
Requested Domain
Record Type
Response Code
Response IP
DNS Server
Query Length
User
Process
```

Example:

```text
Timestamp: 2026-08-14 11:10:31
Source: 10.10.10.25
Hostname: WIN-CLIENT-01
Query: suspicious-example.com
Type: A
Response: 198.51.100.20
Status: NOERROR
```

The domain should be investigated using reputation and contextual information.

---

## 7. DNS Response Codes

Common DNS response codes include:

| Code     | Meaning               | Security Relevance                       |
| -------- | --------------------- | ---------------------------------------- |
| NOERROR  | Successful response   | Normal or suspicious depending on domain |
| NXDOMAIN | Domain does not exist | High volume may indicate malware/DGA     |
| SERVFAIL | Server failure        | May indicate DNS infrastructure issues   |
| REFUSED  | Query refused         | May indicate policy restrictions         |

A high volume of `NXDOMAIN` responses from a single endpoint can be suspicious.

---

## 8. Malicious Domain Detection

SOC analysts can identify suspicious domains using:

* Threat intelligence
* Domain reputation
* Domain age
* DNS history
* WHOIS information
* Passive DNS
* Security vendor verdicts
* Internal allowlists/blocklists
* Domain characteristics

Potential indicators include:

```text
Recently registered domain
Random-looking domain
Look-alike domain
Suspicious TLD
Known malicious infrastructure
Rarely observed domain
Domain associated with malware
```

Example:

```text
Normal:
google.com

Potentially suspicious:
g00gle-login-security-example.com
```

A suspicious-looking domain is not automatically malicious; additional evidence is required.

---

## 9. DNS Beaconing

Malware may periodically communicate with its C2 infrastructure.

Example:

```text
10:00:00 → malicious-domain.example
10:05:00 → malicious-domain.example
10:10:00 → malicious-domain.example
10:15:00 → malicious-domain.example
```

Repeated DNS requests at regular intervals can indicate beaconing.

SOC analysts should correlate the DNS activity with:

* Process execution
* Network connections
* Endpoint alerts
* User activity
* Firewall logs

---

## 10. DNS Tunneling

DNS tunneling abuses DNS queries or responses to transport data.

Conceptually:

```text
Compromised Host
      ↓
Encoded Data
      ↓
DNS Query
      ↓
Attacker-Controlled Domain
      ↓
C2 Infrastructure
```

Example:

```text
aj39dkf92ks0.example.com
```

A single long subdomain is not enough to confirm tunneling.

Potential indicators include:

* Very long DNS queries
* High query frequency
* Random-looking subdomains
* High-entropy labels
* Repeated queries to one unusual domain
* Large volumes of TXT queries
* Consistent encoded-looking data

---

## 11. DNS Data Exfiltration

Attackers may encode stolen information into DNS queries.

Conceptual example:

```text
Sensitive Data
     ↓
Encoding
     ↓
DNS Query
     ↓
Attacker Domain
     ↓
Attacker DNS Server
```

Possible indicators:

```text
Large number of queries
Long subdomain labels
High entropy
Frequent TXT requests
Unusual external domain
Regular transmission pattern
```

DNS-based exfiltration requires careful investigation because legitimate applications can also generate unusual DNS traffic.

---

## 12. Domain Generation Algorithms

Some malware uses Domain Generation Algorithms (DGAs) to generate large numbers of possible domains for C2 communication.

Example pattern:

```text
xj29akd91.com
kq82md02.net
p8s2kd91.org
z91ks02a.com
```

Potential indicators:

* Large numbers of random domains
* High NXDOMAIN rate
* Similar domain structures
* Repeated queries from the same endpoint
* Short-lived domains

DGA detection is particularly useful for identifying malware families that dynamically generate C2 domains.

---

## 13. DNS-Based Malware Detection

A compromised endpoint may generate unusual DNS activity.

Example:

```text
User opens malicious document
        ↓
Malware executes
        ↓
DNS query
        ↓
C2 domain resolved
        ↓
Outbound connection
```

SOC analysts should correlate:

```text
DNS
+
Process Creation
+
Network Connection
+
EDR Alert
```

This combination can significantly increase confidence that the endpoint is compromised.

---

## 14. Internal DNS Monitoring

Internal DNS activity can also reveal suspicious behavior.

Monitor:

* Internal hostnames
* Reverse lookups
* DNS server access
* Unusual internal queries
* Failed lookups
* Attempts to resolve restricted domains
* Unexpected DNS servers

Example:

```text
Normal:
Client → Corporate DNS

Suspicious:
Client → External DNS Server
```

Direct external DNS queries may indicate:

* Malware
* DNS-policy bypass
* Misconfiguration
* Unauthorized software

Investigation is required to determine the cause.

---

## 15. DNS Monitoring in a SOC

DNS telemetry should be integrated into the SIEM.

Example:

```text
Endpoint
   ↓
DNS Query
   ↓
DNS Resolver
   ↓
DNS Logs
   ↓
Log Collector
   ↓
SIEM
   ↓
Detection Rules
   ↓
SOC Analyst
```

The SIEM can correlate DNS activity with:

* Endpoint logs
* Authentication logs
* Firewall logs
* Proxy logs
* WAF logs
* EDR alerts
* Threat intelligence

---

## 16. DNS Threat Intelligence Correlation

Threat intelligence can enrich DNS events.

Example:

```text
DNS Query
    ↓
Domain Reputation
    ↓
Known Malicious?
    ↓
YES
    ↓
Correlate Endpoint
    ↓
Generate Alert
```

Useful enrichment includes:

```text
Domain reputation
IP reputation
Malware association
Threat actor association
First-seen date
Domain age
Known C2 status
```

Threat intelligence should support investigation rather than replace analyst judgment.

---

## 17. DNS Detection Rules

### Rule 1 — Known Malicious Domain

```text
IF
DNS query matches
known malicious domain

THEN
generate high-priority alert
```

Severity:

```text
High
```

---

### Rule 2 — Excessive NXDOMAIN Responses

```text
IF
single endpoint generates
more than 100 NXDOMAIN responses
within 5 minutes

THEN
generate suspicious DNS activity alert
```

Severity:

```text
Medium
```

---

### Rule 3 — DNS Tunneling Indicator

```text
IF
DNS queries contain
long/high-entropy subdomains
AND
query frequency is unusually high

THEN
generate DNS tunneling investigation alert
```

Severity:

```text
High
```

---

### Rule 4 — Periodic DNS Beaconing

```text
IF
same endpoint queries
same unusual domain
at regular intervals

THEN
generate potential C2 beaconing alert
```

Severity:

```text
High
```

---

### Rule 5 — Unauthorized DNS Server

```text
IF
endpoint sends DNS queries
directly to unauthorized external DNS server

THEN
generate policy violation alert
```

Severity:

```text
Medium
```

---

## 18. Example SOC Alert

```text
Alert:
Potential DNS C2 Communication

Severity:
High

Hostname:
WIN-CLIENT-07

Source IP:
10.10.10.37

Domain:
x9a83kd.example

Queries:
143

Time Period:
10 minutes

Pattern:
Long randomized subdomains

Response:
198.51.100.25

Threat Intelligence:
Suspicious
```

### Analyst Comment

```text
Repeated DNS queries containing randomized subdomains were
observed from WIN-CLIENT-07 over a short period. The queried
domain has a suspicious reputation and the query pattern is
inconsistent with normal DNS activity. Endpoint process
telemetry, network connections, and threat-intelligence
information should be reviewed to determine whether the host
is communicating with a command-and-control infrastructure.
```

---

## 19. SOC Triage Process

### Step 1 — Identify the Endpoint

Determine:

```text
Hostname
Source IP
User
Operating System
```

### Step 2 — Analyze the Domain

Check:

```text
Domain reputation
Domain age
Threat intelligence
Resolved IP
Domain structure
```

### Step 3 — Analyze Query Behavior

Check:

```text
Query frequency
Query length
Subdomain structure
Record type
Response code
```

### Step 4 — Check Endpoint Activity

Look for:

```text
New processes
Suspicious scripts
Unknown executables
Browser activity
Scheduled tasks
Persistence mechanisms
```

### Step 5 — Check Network Activity

Determine whether the endpoint established connections to:

```text
Resolved IP
Other external IPs
Known malicious infrastructure
Unusual ports
```

### Step 6 — Correlate

Review:

```text
DNS logs
Firewall logs
Proxy logs
EDR alerts
Authentication logs
Process creation events
```

### Step 7 — Determine Impact

Ask:

```text
Was malware executed?
Was C2 communication established?
Was data transferred?
Is persistence present?
Are additional systems affected?
```

### Step 8 — Escalate

If compromise is confirmed, follow the organization's incident-response process.

---

## 20. Example Attack Timeline

```text
09:30
User opens malicious document
        ↓
09:31
PowerShell process starts
        ↓
09:31
DNS query to suspicious domain
        ↓
09:31
Domain resolves to external IP
        ↓
09:32
Endpoint establishes outbound connection
        ↓
09:35
Repeated DNS requests begin
        ↓
09:40
SIEM correlates DNS + endpoint + network events
        ↓
SOC Alert
```

This type of correlation provides much stronger evidence than a single suspicious DNS query.

---

## 21. DNS Monitoring Best Practices

Organizations should:

* Centralize DNS logging
* Monitor internal DNS resolvers
* Restrict unauthorized DNS traffic
* Monitor high-volume NXDOMAIN activity
* Monitor newly observed domains
* Integrate DNS threat intelligence
* Detect DNS tunneling
* Detect periodic beaconing
* Monitor suspicious TXT queries
* Establish normal DNS baselines
* Integrate DNS logs with SIEM
* Correlate DNS and endpoint telemetry
* Retain DNS logs according to organizational requirements

---

## 22. Common DNS Monitoring Tools

### SIEM

Examples:

* Wazuh
* Splunk
* Microsoft Sentinel
* IBM QRadar

### Network Monitoring

Examples:

* Wireshark
* Zeek

### DNS Security

Examples:

* Cisco Umbrella
* Cloudflare Gateway
* Microsoft Defender DNS-related security capabilities

### Threat Intelligence

Examples:

* VirusTotal
* AbuseIPDB
* AlienVault OTX

---

## 23. DNS Monitoring Investigation Checklist

```text
[ ] Identify hostname
[ ] Identify source IP
[ ] Identify user
[ ] Identify requested domain
[ ] Check DNS record type
[ ] Check response code
[ ] Check resolved IP
[ ] Check domain reputation
[ ] Check domain age
[ ] Check threat intelligence
[ ] Analyze query frequency
[ ] Analyze query length
[ ] Check subdomain structure
[ ] Check for high-entropy domains
[ ] Check for excessive NXDOMAIN responses
[ ] Check for DNS tunneling indicators
[ ] Check endpoint process activity
[ ] Check network connections
[ ] Check firewall logs
[ ] Check proxy logs
[ ] Determine whether C2 communication occurred
[ ] Determine potential data exfiltration
[ ] Assign severity
[ ] Document findings
[ ] Escalate if required
```

---

## 24. Key Takeaways

DNS monitoring provides valuable visibility into the behavior of endpoints and users across an organization.

A SOC analyst should understand:

* DNS fundamentals
* DNS record types
* DNS logs
* Malicious domain detection
* DNS beaconing
* DNS tunneling
* DNS-based exfiltration
* DGA behavior
* Threat-intelligence enrichment
* Endpoint correlation
* Network correlation
* SIEM detection

The core investigation model is:

```text
DNS Query
   ↓
Domain Analysis
   ↓
Threat Intelligence
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
```

**DNS monitoring is especially valuable for detecting malware and command-and-control activity because DNS often occurs before an endpoint establishes the actual network connection. A SOC analyst should therefore treat unusual DNS behavior as an important source of early warning rather than analyzing DNS events in isolation.**
