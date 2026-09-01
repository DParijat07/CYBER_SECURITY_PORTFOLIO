# Wazuh SIEM Lab — Installation

## 1. Purpose

This document covers the installation phase of the Wazuh SIEM laboratory.

The objective is to deploy the required Wazuh components, verify that the services are operational, and prepare the environment for endpoint-agent configuration and security monitoring.

All installation activities should be performed only within the authorized home-lab environment.

---

## 2. Wazuh Components

A complete Wazuh deployment consists of the following major components:

```text
Wazuh Agent
     │
     ▼
Wazuh Manager
     │
     ▼
Wazuh Indexer
     │
     ▼
Wazuh Dashboard
```

### Wazuh Agent

The agent runs on monitored endpoints and collects security telemetry.

### Wazuh Manager

The manager receives and analyzes data from agents and applies detection rules.

### Wazuh Indexer

The indexer stores and indexes security data for searching and analysis.

### Wazuh Dashboard

The dashboard provides the graphical interface used to monitor agents, events, alerts, and security information.

---

## 3. Installation Architecture

For this home laboratory, a single-node deployment is sufficient.

```text
                 Wazuh Dashboard
                        │
                        ▼
                 Wazuh Indexer
                        │
                        ▼
                 Wazuh Manager
                        │
             ┌──────────┴──────────┐
             │                     │
             ▼                     ▼
      Windows Agent          Linux Agent
             │                     │
             ▼                     ▼
       Windows VM              Linux VM
```

This architecture is suitable for learning and small-scale testing.

---

## 4. Prerequisites

Before beginning installation, verify that the following are available:

### Host

- 64-bit CPU
- Hardware virtualization enabled
- Minimum 16 GB RAM recommended
- Sufficient free disk space
- Stable network connectivity

### Virtualization

- VMware Workstation or equivalent virtualization platform

### Server

- Supported Linux operating system
- Administrative privileges
- Static or predictable IP address recommended

### Endpoints

- Windows virtual machine
- Linux virtual machine
- Network connectivity to the Wazuh server

---

## 5. Prepare the Wazuh Server VM

Create a dedicated Linux virtual machine for the Wazuh deployment.

Recommended starting configuration:

| Resource | Recommendation |
|---|---|
| CPU | 4 vCPU or more |
| RAM | 8 GB or more |
| Storage | 50 GB or more |
| Network | Dedicated lab network |
| Hostname | WAZUH-SERVER |

Resource requirements may vary depending on Wazuh version and telemetry volume.

---

## 6. Configure the Server Hostname

Set a clear hostname for the Wazuh server.

Example:

```bash
hostnamectl set-hostname WAZUH-SERVER
```

Verify:

```bash
hostname
```

Expected result:

```text
WAZUH-SERVER
```

A clear hostname makes later investigation and documentation easier.

---

## 7. Identify the Server IP Address

Determine the IP address assigned to the Wazuh server.

For Linux, commands such as the following can be used:

```bash
ip addr
```

or:

```bash
hostname -I
```

Record the address in the lab documentation.

Example:

```text
Wazuh Server IP: 192.168.100.10
```

Use your actual laboratory address rather than the example address.

---

## 8. Update the Operating System

Before installing Wazuh, update the server operating system.

For Debian/Ubuntu-based systems:

```bash
sudo apt update
sudo apt upgrade -y
```

For other supported Linux distributions, use the appropriate package-management commands.

Reboot if required:

```bash
sudo reboot
```

---

## 9. Verify System Resources

Before installation, verify CPU, RAM, storage, and network configuration.

Useful commands include:

```bash
lscpu
```

```bash
free -h
```

```bash
df -h
```

```bash
ip addr
```

Record relevant information in the lab notes.

---

## 10. Install Wazuh

Use the **official Wazuh installation documentation** appropriate for the Wazuh version being deployed.

The installation procedure can change between Wazuh releases, so the commands should always be taken from the current official documentation rather than copied from an outdated tutorial.

The installation process normally involves:

```text
Prepare Linux Server
        ↓
Configure Wazuh Repository / Installer
        ↓
Install Wazuh Components
        ↓
Initialize Wazuh Services
        ↓
Verify Services
        ↓
Access Dashboard
```

---

## 11. Wazuh Installation Assistant

For a new laboratory deployment, the Wazuh installation assistant can be used when supported by the selected Wazuh version.

The general workflow is:

```text
Download Installation Assistant
            ↓
Generate Configuration
            ↓
Install Wazuh Components
            ↓
Start Services
            ↓
Verify Deployment
```

Do not blindly reuse installation commands from previous Wazuh versions.

Always verify the installation procedure against the Wazuh documentation for the version currently being deployed.

---

## 12. Verify Wazuh Services

After installation, verify that the Wazuh services are running.

Useful commands may include:

```bash
sudo systemctl status wazuh-manager
```

```bash
sudo systemctl status wazuh-indexer
```

```bash
sudo systemctl status wazuh-dashboard
```

The exact service names may vary depending on the deployment method and Wazuh version.

---

## 13. Check Running Services

You can inspect running Wazuh-related services with:

```bash
sudo systemctl --type=service | grep wazuh
```

The objective is to confirm that the required services are operational.

---

## 14. Verify Wazuh Manager

The Wazuh manager is responsible for receiving and analyzing security data.

Verify its service state:

```bash
sudo systemctl status wazuh-manager
```

If the service is active, continue with the dashboard and endpoint configuration.

If it fails, inspect the service logs before making configuration changes.

---

## 15. Verify Wazuh Indexer

The Wazuh indexer stores and indexes security information.

Verify its service state:

```bash
sudo systemctl status wazuh-indexer
```

Confirm that the service is active and that there are no obvious configuration or certificate errors.

---

## 16. Verify Wazuh Dashboard

The Wazuh Dashboard provides the graphical interface for monitoring the environment.

Verify:

```bash
sudo systemctl status wazuh-dashboard
```

Then access the dashboard from an authorized browser using the address configured during deployment.

Example:

```text
https://<WAZUH-SERVER-IP>
```

The exact port and URL depend on the installation.

---

## 17. Dashboard Verification

After accessing the dashboard, verify that:

- The login page loads.
- Authentication works.
- The dashboard interface loads correctly.
- No major service errors are displayed.
- The Wazuh application is accessible.

Take a screenshot for the `Evidence/` directory after sensitive information has been removed.

---

## 18. Verify Server Connectivity

From an authorized endpoint, verify that the Wazuh server is reachable.

Example:

```bash
ping <WAZUH-SERVER-IP>
```

On Windows:

```powershell
ping <WAZUH-SERVER-IP>
```

ICMP may be disabled depending on the network configuration, so failure to receive a ping response does not always indicate that the Wazuh service is unavailable.

Use appropriate service/connectivity tests when required.

---

## 19. Firewall Considerations

The Wazuh deployment requires appropriate network connectivity between:

```text
Endpoint
    ↓
Wazuh Agent
    ↓
Wazuh Manager
```

and between the administrator's browser and:

```text
Browser
    ↓
Wazuh Dashboard
```

Only required ports should be permitted.

Do not expose the Wazuh management interface unnecessarily to the public Internet.

---

## 20. Agent Installation Preparation

Once the Wazuh server is operational, prepare the monitored endpoints.

The general workflow is:

```text
Wazuh Server Ready
       ↓
Select Endpoint
       ↓
Install Wazuh Agent
       ↓
Configure Manager Address
       ↓
Register / Authenticate Agent
       ↓
Start Agent
       ↓
Verify Connection
```

Agent installation should be performed using the Wazuh documentation corresponding to the deployed version.

---

## 21. Windows Agent

For the Windows laboratory endpoint:

1. Confirm network connectivity.
2. Download the appropriate Wazuh agent package.
3. Install the agent.
4. Configure the Wazuh manager address.
5. Register the endpoint if required.
6. Start the Wazuh agent service.
7. Verify that the agent appears in the Wazuh Dashboard.

Example endpoint name:

```text
WIN-ENDPOINT
```

---

## 22. Linux Agent

For the Linux laboratory endpoint:

1. Confirm network connectivity.
2. Install the appropriate Wazuh agent package.
3. Configure the Wazuh manager address.
4. Register the endpoint if required.
5. Start the agent service.
6. Verify communication with the Wazuh manager.
7. Confirm the endpoint appears in the Dashboard.

Example endpoint name:

```text
LINUX-ENDPOINT
```

---

## 23. Agent Verification

After installing an agent, verify its service.

On Linux:

```bash
sudo systemctl status wazuh-agent
```

On Windows, verify the Wazuh Agent service through:

```text
Services
    ↓
Wazuh Agent
    ↓
Status: Running
```

The exact service-management procedure may vary by operating-system version.

---

## 24. Verify Agents in Dashboard

Open the Wazuh Dashboard and navigate to the agent-management section.

Verify:

- Agent name
- Agent ID
- Operating system
- IP address
- Connection status
- Last keepalive
- Agent version

Expected state:

```text
Agent
  ↓
Connected
  ↓
Telemetry Available
```

---

## 25. Installation Validation

The installation phase is successful when:

```text
Wazuh Manager
      ↓
Operational

Wazuh Indexer
      ↓
Operational

Wazuh Dashboard
      ↓
Accessible

Endpoint Agent
      ↓
Connected

Security Telemetry
      ↓
Visible
```

---

## 26. Installation Checklist

### Server

- [ ] Linux VM created
- [ ] Hostname configured
- [ ] IP address recorded
- [ ] Operating system updated
- [ ] Wazuh components installed
- [ ] Wazuh Manager running
- [ ] Wazuh Indexer running
- [ ] Wazuh Dashboard running
- [ ] Dashboard accessible

### Windows Endpoint

- [ ] Windows VM available
- [ ] Hostname configured
- [ ] Network connectivity verified
- [ ] Wazuh Agent installed
- [ ] Manager address configured
- [ ] Agent service running
- [ ] Agent visible in Dashboard

### Linux Endpoint

- [ ] Linux VM available
- [ ] Hostname configured
- [ ] Network connectivity verified
- [ ] Wazuh Agent installed
- [ ] Manager address configured
- [ ] Agent service running
- [ ] Agent visible in Dashboard

---

## 27. Evidence to Capture

Recommended evidence for this stage includes:

1. Wazuh server VM information.
2. Server hostname and IP configuration.
3. Wazuh Manager service status.
4. Wazuh Indexer service status.
5. Wazuh Dashboard login page.
6. Wazuh Dashboard main interface.
7. Connected-agent list.
8. Windows agent status.
9. Linux agent status.

Store screenshots in:

```text
01-Wazuh-SIEM-Lab/
└── Evidence/
    └── Installation/
```

Remove or obscure:

- Passwords
- API keys
- Tokens
- Private keys
- Sensitive IP addresses
- Personal information
- Other confidential information

before publishing evidence to a public GitHub repository.

---

## 28. Common Installation Problems

### Dashboard Does Not Load

Check:

```bash
sudo systemctl status wazuh-dashboard
```

Also verify:

- Server IP
- Network connectivity
- Firewall configuration
- Dashboard service logs

---

### Wazuh Manager Is Not Running

Check:

```bash
sudo systemctl status wazuh-manager
```

Then inspect the relevant service logs and configuration files.

Do not repeatedly restart the service without identifying the underlying problem.

---

### Agent Does Not Appear

Check:

- Manager IP address
- Agent configuration
- Agent service status
- Network connectivity
- Registration/authentication
- Firewall rules
- Wazuh Manager status

---

### No Security Events

Verify:

- Agent is connected.
- Relevant log sources are enabled.
- Agent configuration is correct.
- Events are actually being generated.
- Wazuh Manager is receiving data.
- The dashboard is displaying current data.

---

## 29. Installation Notes

Record important information during installation.

Example:

```text
Wazuh Version:
Server OS:
Server IP:
Server Hostname:
Dashboard Status:
Manager Status:
Indexer Status:
Windows Agent:
Linux Agent:
Installation Date:
```

Do not store credentials or secrets in this file.

---

## 30. Completion Criteria

The installation phase is complete when:

- [ ] Wazuh server is operational.
- [ ] Wazuh Manager is running.
- [ ] Wazuh Indexer is running.
- [ ] Wazuh Dashboard is accessible.
- [ ] At least one endpoint agent is installed.
- [ ] Agent communication is established.
- [ ] Agents are visible in the Dashboard.
- [ ] Initial security telemetry is available.
- [ ] Installation evidence has been captured.
- [ ] Sensitive information has been removed from public evidence.

---

## 31. Next Step

After completing the installation, continue with:

**Configuration → Log Collection → Alert Analysis → Investigation → Troubleshooting**

The next documentation file should explain how to configure the Wazuh environment and monitored endpoints for the specific security telemetry required by this laboratory.
