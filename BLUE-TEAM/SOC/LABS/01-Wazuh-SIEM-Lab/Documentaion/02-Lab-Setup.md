# Wazuh SIEM Lab — Lab Setup

## 1. Lab Overview

This document describes the laboratory environment required to deploy, configure, and operate Wazuh for security monitoring and SOC investigation practice.

The environment is designed as a controlled home lab using virtual machines and authorized test systems.

The lab should allow security events to be generated on monitored endpoints and collected by Wazuh for analysis.

---

## 2. Lab Architecture

The basic architecture is:

```text
                    SOC Analyst
                         │
                         ▼
                ┌─────────────────┐
                │ Wazuh Dashboard │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │  Wazuh Server   │
                │     /Manager    │
                └────────┬────────┘
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
       ┌─────────────┐       ┌─────────────┐
       │   Windows   │       │    Linux    │
       │   Endpoint  │       │   Endpoint  │
       │ Wazuh Agent │       │ Wazuh Agent │
       └─────────────┘       └─────────────┘
```

The exact architecture may be expanded later as additional endpoints and security tools are added.

---

## 3. Host Machine

The laboratory can be hosted on a personal computer capable of running multiple virtual machines.

Recommended host requirements:

- 64-bit processor
- Hardware virtualization enabled
- Minimum 16 GB RAM
- Recommended 32 GB RAM
- At least 100 GB available storage
- Stable network connection
- VMware Workstation or another supported virtualization platform

More RAM and storage may be required when running several endpoints simultaneously.

---

## 4. Virtualization Platform

The lab uses virtualization to isolate the security-monitoring environment from the primary operating system.

Example virtualization platform:

- VMware Workstation

Alternative platforms may also be used if they support the required virtual networking and operating systems.

---

## 5. Wazuh Server

The Wazuh server acts as the central security-monitoring component.

The server should provide the services required for:

- Agent communication
- Security-data collection
- Log analysis
- Detection
- Alert generation
- Security-event indexing
- Dashboard access

A Linux-based virtual machine is recommended for the Wazuh server.

---

## 6. Recommended Wazuh Server VM

Suggested starting configuration:

| Resource | Recommended |
|---|---|
| Operating System | Supported Linux distribution |
| CPU | 4 vCPU or more |
| RAM | 8 GB or more |
| Storage | 50 GB or more |
| Network | Lab network |
| Role | Wazuh Server / Manager |

The exact resource requirements depend on the Wazuh version, number of monitored endpoints, and volume of telemetry.

For a small home lab, the resources can be adjusted according to available hardware.

---

## 7. Monitored Endpoints

The laboratory should contain at least one monitored endpoint.

Recommended endpoints:

```text
Windows Endpoint
      +
Linux Endpoint
```

The endpoints can be virtual machines.

The learner should install the Wazuh agent on each endpoint that will be monitored.

---

## 8. Windows Endpoint

A Windows virtual machine can be used to generate and monitor security events.

Potential telemetry includes:

- Windows Security Events
- Authentication activity
- Process activity
- File activity
- Account activity
- System events
- PowerShell activity
- Security configuration changes

The Windows endpoint should contain only test data and authorized accounts.

---

## 9. Linux Endpoint

A Linux virtual machine can be used for Linux security monitoring.

Potential telemetry includes:

- Authentication logs
- SSH activity
- Process activity
- System logs
- User activity
- Service activity
- File activity
- Configuration changes

The Linux endpoint should be configured as a controlled laboratory system.

---

## 10. Network Design

The laboratory should use a dedicated virtual network whenever practical.

Example:

```text
                Host Machine
                     │
              Virtual Network
                     │
       ┌─────────────┼─────────────┐
       │             │             │
       ▼             ▼             ▼
 Wazuh Server    Windows VM    Linux VM
```

A private virtual network provides better isolation for laboratory activities.

If Internet access is required for legitimate updates or package installation, network configuration should be designed so that the lab remains controlled.

---

## 11. Example IP Addressing

A private lab subnet may be used.

Example:

```text
Network:       192.168.100.0/24

Wazuh Server:  192.168.100.10
Windows VM:    192.168.100.20
Linux VM:      192.168.100.30
```

These addresses are examples only.

Use the actual addresses assigned by the virtual network configuration.

---

## 12. Required Components

The basic lab requires:

### Core Components

- Wazuh Server
- Wazuh Dashboard
- Wazuh Indexer
- Wazuh Agent
- Windows or Linux endpoint

### Supporting Components

- Virtualization platform
- Virtual network
- Administrative access
- Terminal/command-line access
- Web browser

---

## 13. Optional Components

The environment can later be expanded with:

- Sysmon
- Wireshark
- Windows Event Forwarding
- Vulnerability scanners
- Threat-intelligence sources
- Python
- Security automation tools
- Additional Linux endpoints
- Additional Windows endpoints

These components should be introduced progressively.

---

## 14. Wazuh Agent Architecture

Each monitored endpoint should communicate with the Wazuh server through its installed agent.

Example:

```text
Windows Endpoint
      │
      │ Wazuh Agent
      ▼
Wazuh Server
```

and:

```text
Linux Endpoint
      │
      │ Wazuh Agent
      ▼
Wazuh Server
```

The agent should be configured to communicate with the correct Wazuh server address.

---

## 15. Time Synchronization

Accurate time is important for security investigations.

All laboratory systems should maintain synchronized system time.

Verify:

- Host time
- Wazuh server time
- Windows endpoint time
- Linux endpoint time

Accurate timestamps make event correlation and timeline construction more reliable.

---

## 16. Hostname Configuration

Use clear hostnames so that endpoints can easily be identified during investigations.

Example:

```text
WAZUH-SERVER
WIN-ENDPOINT
LINUX-ENDPOINT
```

Avoid ambiguous names such as:

```text
PC1
VM1
TEST
```

Clear hostnames make SOC investigations easier to document.

---

## 17. User Accounts

Use dedicated laboratory accounts where possible.

Example:

```text
SOC-ADMIN
SOC-ANALYST
LAB-USER
```

Do not use unnecessary personal credentials or sensitive production credentials inside the laboratory.

---

## 18. Snapshot Strategy

Virtual-machine snapshots are strongly recommended before major configuration changes.

Suggested snapshots:

```text
Clean OS
   ↓
Wazuh Agent Installed
   ↓
Agent Configured
   ↓
Monitoring Verified
   ↓
Lab Ready
```

Snapshots allow the environment to be restored if a configuration change causes problems.

---

## 19. Backup Strategy

Important configuration and investigation evidence should be backed up.

Potential backup items include:

- Wazuh configuration
- Agent configuration
- Detection rules
- Custom rules
- Investigation notes
- Screenshots
- Lab documentation
- Configuration files

Do not publish sensitive credentials, tokens, private keys, or internal network information to a public repository.

---

## 20. Security Isolation

The laboratory should remain separated from production or personal systems whenever practical.

Recommended practices:

- Use virtual machines
- Use a dedicated virtual network
- Use test accounts
- Use test data
- Avoid production credentials
- Avoid sensitive personal information
- Use controlled security events
- Take snapshots before experiments

---

## 21. Browser Access

The Wazuh Dashboard can be accessed through a web browser from an authorized system that can reach the Wazuh server.

Example:

```text
https://<WAZUH-SERVER-IP>
```

The exact URL and port depend on the Wazuh deployment configuration.

---

## 22. Installation Preparation

Before installing Wazuh, verify:

- [ ] Host virtualization is working.
- [ ] Required virtual machines are created.
- [ ] Wazuh server operating system is installed.
- [ ] Endpoint operating systems are installed.
- [ ] Virtual networking is configured.
- [ ] Systems can communicate as required.
- [ ] Hostnames are configured.
- [ ] System time is synchronized.
- [ ] Required resources are available.
- [ ] Snapshots have been created.

---

## 23. Connectivity Verification

Before configuring the Wazuh agent, verify basic connectivity between endpoints and the Wazuh server.

For example, test:

```text
Windows Endpoint
      ↓
Wazuh Server
```

and:

```text
Linux Endpoint
      ↓
Wazuh Server
```

The exact connectivity tests depend on the operating systems and network configuration.

---

## 24. Lab Readiness Checklist

### Host

- [ ] Virtualization enabled
- [ ] Sufficient RAM
- [ ] Sufficient storage
- [ ] VMware or equivalent installed

### Wazuh Server

- [ ] Linux VM created
- [ ] Network configured
- [ ] Hostname configured
- [ ] Time synchronized
- [ ] Wazuh components installed
- [ ] Dashboard accessible

### Windows Endpoint

- [ ] Windows VM available
- [ ] Network configured
- [ ] Hostname configured
- [ ] Test account available
- [ ] Wazuh agent installed
- [ ] Agent connected

### Linux Endpoint

- [ ] Linux VM available
- [ ] Network configured
- [ ] Hostname configured
- [ ] Test account available
- [ ] Wazuh agent installed
- [ ] Agent connected

---

## 25. Recommended Lab Build Order

Build the environment in the following order:

```text
1. Prepare Host
       ↓
2. Configure Virtualization
       ↓
3. Create Wazuh Server VM
       ↓
4. Configure Virtual Network
       ↓
5. Install Wazuh
       ↓
6. Verify Dashboard
       ↓
7. Create Windows Endpoint
       ↓
8. Install Windows Agent
       ↓
9. Verify Windows Telemetry
       ↓
10. Create Linux Endpoint
       ↓
11. Install Linux Agent
       ↓
12. Verify Linux Telemetry
       ↓
13. Generate Controlled Events
       ↓
14. Analyze Alerts
```

---

## 26. Final Lab Architecture

The completed beginner Wazuh lab should resemble:

```text
                         SOC Analyst
                              │
                              ▼
                    ┌─────────────────┐
                    │ Wazuh Dashboard │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ Wazuh Server    │
                    │ / Manager       │
                    │                 │
                    │ Indexer         │
                    └────────┬────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       ┌──────────────┐              ┌──────────────┐
       │ Windows VM   │              │  Linux VM    │
       │              │              │              │
       │ Wazuh Agent  │              │ Wazuh Agent  │
       └──────────────┘              └──────────────┘
              │                             │
              ▼                             ▼
       Windows Events                Linux Logs
              │                             │
              └──────────────┬──────────────┘
                             ▼
                    Wazuh Security Data
                             │
                             ▼
                          Alerts
                             │
                             ▼
                       Investigation
```

---

## 27. Expected Setup Outcome

At the end of the setup phase, the following conditions should be satisfied:

- Wazuh is operational.
- The Dashboard is accessible.
- The Wazuh server is healthy.
- At least one endpoint is connected.
- Endpoint telemetry is being received.
- Security events can be observed.
- Alerts can be generated.
- Events can be investigated.
- Evidence can be documented.

The environment is then ready for the next stages of the laboratory:

**Installation → Configuration → Log Collection → Alert Analysis → Investigation → Troubleshooting**
