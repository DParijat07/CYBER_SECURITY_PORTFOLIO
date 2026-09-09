# Linux Security Monitoring — Lab Setup

## Purpose

The purpose of this document is to describe the basic environment required to perform the Linux Security Monitoring Lab.

The setup uses a Linux virtual machine as the monitored endpoint and Wazuh as the security monitoring platform.

The configuration is designed for a beginner-friendly home lab using freely available tools.

---

# 1. Home Lab Topology

The Linux Security Monitoring Lab is part of the larger cybersecurity home lab.

The existing home-lab environment uses a **Windows 11 physical host with VMware Workstation Player** as the virtualization platform.

### Exact Home-Lab Topology

```
┌─────────────────────────────────────────────────────────────┐
│                    PHYSICAL HOST                            │
│                     Windows 11                              │
│                                                             │
│                  VMware Workstation Player                  │
└─────────────────────────────┬───────────────────────────────┘
                              │
                     VMware Virtual Network
                              │
         ┌────────────────────┼────────────────────┐
         │                    │                    │
         ▼                    ▼                    ▼
  ┌─────────────┐      ┌──────────────┐     ┌──────────────┐
  │ Linux VM    │      │ Wazuh Server │     │ Kali Linux   │
  │ Monitoring  │─────►│ Ubuntu/Linux │     │ VM(s)        │
  │ Endpoint    │      │ Manager +    │     │ Security     │
  │             │      │ Dashboard    │     │ Testing      │
  └─────────────┘      └──────────────┘     └──────────────┘
         │
         │
         ├───────────────────────────────┐
         │                               │
         ▼                               ▼
  ┌─────────────┐                 ┌───────────────┐
  │ Windows 7   │                 │ Metasploitable│
  │ VM          │                 │ 2 VM          │
  │ Victim/Test │                 │ Victim/Test   │
  └─────────────┘                 └───────────────┘
```

For this particular lab, the primary communication path is:

```
Linux Monitoring VM
        │
        │ Wazuh Agent
        ▼
Wazuh Manager / Server
        │
        ▼
Wazuh Dashboard
        │
        ▼
SOC Analyst
```

The other virtual machines belong to the broader home lab and are not required for the basic Linux Security Monitoring Lab.

---

# 2. Components Used in This Lab

| Component                 | Role                                     |
| ------------------------- | ---------------------------------------- |
| Windows 11 Host           | Physical host system                     |
| VMware Workstation Player | Virtualization platform                  |
| Linux VM                  | Monitored Linux endpoint                 |
| Wazuh Server              | Central security monitoring platform     |
| Wazuh Agent               | Collects Linux telemetry                 |
| Wazuh Manager             | Receives and analyzes endpoint telemetry |
| Wazuh Dashboard           | Displays events and alerts               |

### Other Home-Lab Systems

The following systems are part of the broader home lab but are not required for the basic execution of this lab:

| System           | Role                      |
| ---------------- | ------------------------- |
| Kali Linux VM(s) | Security testing/learning |
| Windows 7 VM     | Vulnerable/test endpoint  |
| Metasploitable 2 | Vulnerable/test endpoint  |

These systems should not be used as the primary monitored endpoint for this Linux Security Monitoring Lab.

---

# 3. Lab Architecture

The Linux monitoring path is:

```
Linux VM
   │
   │ Linux security/system activity
   ▼
Linux Logs
   │
   │ Wazuh Agent
   ▼
Wazuh Manager
   │
   ▼
Wazuh Dashboard
   │
   ▼
SOC Analyst
```

The Linux VM generates security-relevant activity.

The Wazuh Agent collects selected Linux telemetry and sends it to the Wazuh Manager.

The Wazuh Dashboard is used to view and investigate the collected events and alerts.

---

# 4. Required Linux VM

A Linux virtual machine is required for this lab.

A beginner-friendly choice is:

* Ubuntu Linux
* Debian Linux
* Kali Linux

Ubuntu or Debian is recommended for this lab because the logging structure is relatively straightforward for learning Linux monitoring.

The Linux VM should have:

* Working network connectivity
* Sufficient disk space
* A normal user account
* `sudo` access
* Wazuh Agent installed

---

# 5. Setup Steps

This section contains only the steps required to prepare the environment.

Validation is performed separately in **Section 6 — Validation Steps**.

---

## Step 1 — Start the Home Lab

Start:

1. Windows 11 host.
2. VMware Workstation Player.
3. Wazuh Server VM.
4. Linux Monitoring VM.

The Kali, Windows 7, and Metasploitable 2 VMs are not required for the basic Linux monitoring setup.

---

## Step 2 — Verify the Linux Operating System

Open a terminal on the Linux VM.

Check the operating system:

```
cat /etc/os-release
```

Check the hostname:

```
hostname
```

Check the current user:

```
whoami
```

Check whether `sudo` is available:

```
sudo -v
```

---

## Step 3 — Identify the Linux IP Address

Run:

```
ip addr
```

Identify the active network interface and its IPv4 address.

Record the address for the lab documentation.

Example:

```
Linux VM IP: 192.168.x.x
```

Use the actual address assigned to your VM.

---

## Step 4 — Identify the Wazuh Server IP

On the Wazuh Server, identify its IP address.

For a Linux-based Wazuh Server:

```
ip addr
```

Record:

```
Wazuh Server IP: __________________
```

The Linux VM must be able to communicate with this address.

---

## Step 5 — Verify Basic Network Connectivity

From the Linux VM:

```
ping <WAZUH_MANAGER_IP>
```

Replace `<WAZUH_MANAGER_IP>` with the actual Wazuh Server IP address.

Do not proceed until basic connectivity has been established.

---

## Step 6 — Install the Wazuh Agent

Install the Wazuh Agent on the Linux monitoring VM using the appropriate Wazuh installation method for the Linux distribution.

During installation/configuration, specify the Wazuh Manager address.

The configuration should point the agent to the Wazuh Server used by the home lab.

---

## Step 7 — Check the Wazuh Agent Service

Check the service:

```
systemctl status wazuh-agent
```

If the service is installed but stopped:

```
sudo systemctl start wazuh-agent
```

Enable automatic startup:

```
sudo systemctl enable wazuh-agent
```

---

## Step 8 — Configure the Wazuh Agent Connection

The Wazuh Agent configuration is stored in:

```
/var/ossec/etc/ossec.conf
```

Check the configuration:

```
sudo nano /var/ossec/etc/ossec.conf
```

Confirm that the Wazuh Manager address is configured correctly.

Do not modify unrelated configuration sections.

---

## Step 9 — Restart the Wazuh Agent

After configuration:

```
sudo systemctl restart wazuh-agent
```

Check the service:

```
systemctl status wazuh-agent
```

---

## Step 10 — Identify Available Linux Logs

Check the log directory:

```
ls -l /var/log/
```

For Debian/Ubuntu-based systems, check:

```
sudo ls -l /var/log/auth.log

sudo ls -l /var/log/syslog
```

Check the system journal:

```
sudo journalctl -n 20
```

The exact available log sources depend on the Linux distribution.

---

## Step 11 — Prepare the Evidence Directory

The lab evidence will be stored under:

```
Evidence/
```

Recommended initial structure:

```
Evidence/
├── linux-system-information.png
├── linux-network-information.png
├── wazuh-agent-status.png
├── wazuh-agent-connected.png
└── linux-log-sources.png
```

Only create evidence files after the corresponding information has actually been captured.

---

# 6. Validation Steps

This section verifies whether the setup from Section 5 is working correctly.

Validation is different from setup.

**Setup prepares the environment.**

**Validation proves that the environment works.**

---

## Validation 1 — Linux System

Run:

```
hostname

whoami

ip addr
```

Expected result:

* Linux system responds normally.
* Correct hostname is displayed.
* Current user is displayed.
* Linux VM has an IP address.

---

## Validation 2 — Network Connectivity

Run:

```
ping <WAZUH_MANAGER_IP>
```

Expected result:

The Linux VM can reach the Wazuh Server.

If this fails, the Wazuh Agent connection should not be investigated yet. First resolve the basic network problem.

---

## Validation 3 — Wazuh Agent Service

Run:

```
systemctl status wazuh-agent
```

Expected result:

The Wazuh Agent service is active/running.

---

## Validation 4 — Wazuh Agent Connection

Open the Wazuh Dashboard from the home-lab environment.

Locate the Linux endpoint.

Verify:

* Agent name
* Agent status
* Agent IP address
* Last communication time

Expected result:

The Linux VM appears as a connected/active Wazuh agent.

---

## Validation 5 — Authentication Logging

Generate a normal authentication event by logging into the Linux system normally.

Then check:

```
sudo tail -n 20 /var/log/auth.log
```

If the distribution does not use `/var/log/auth.log`, use:

```
sudo journalctl -n 20
```

Expected result:

Authentication-related activity is recorded locally.

---

## Validation 6 — Sudo Activity

Run:

```
sudo whoami
```

Expected output:

```
root
```

Then check:

```
sudo tail -n 20 /var/log/auth.log
```

Expected result:

The administrative activity is recorded in the appropriate Linux security log.

---

## Validation 7 — Process Activity

Run harmless commands:

```
whoami

pwd

ls

ps
```

Check running processes:

```
ps aux
```

Expected result:

Normal process and command activity is visible on the Linux endpoint.

---

## Validation 8 — System Journal

Run:

```
sudo journalctl -n 30
```

Expected result:

Recent system events are displayed if the system uses `systemd`.

---

## Validation 9 — Centralized Telemetry

Open the Wazuh Dashboard and search for events generated by the Linux endpoint.

Verify that the endpoint is producing telemetry centrally.

Expected result:

Linux activity can be observed through the Wazuh monitoring platform.

The exact dashboard fields and search interface may vary according to the Wazuh version and configuration.

---

# 7. Lab Information Record

Record the following information after the setup and validation steps:

| Information             | Value                     |
| ----------------------- | ------------------------- |
| Linux Distribution      |                           |
| Linux Version           |                           |
| Hostname                |                           |
| Linux IP Address        |                           |
| Wazuh Agent Version     |                           |
| Wazuh Server IP         |                           |
| Wazuh Manager Version   |                           |
| VMware Network Type     |                           |
| Virtualization Platform | VMware Workstation Player |

Do not include passwords, private keys, API tokens, or other credentials in the documentation.

---

# 8. Validation Checklist

| Check                            | Expected Result         | Status |
| -------------------------------- | ----------------------- | ------ |
| Linux VM starts                  | Successful              | ☐      |
| Linux has IP address             | Yes                     | ☐      |
| Linux can reach Wazuh Server     | Yes                     | ☐      |
| Wazuh Agent installed            | Yes                     | ☐      |
| Wazuh Agent running              | Yes                     | ☐      |
| Wazuh Agent connected            | Yes                     | ☐      |
| Authentication logging available | Yes                     | ☐      |
| System logging available         | Yes                     | ☐      |
| `journalctl` available           | Yes, if systemd is used | ☐      |
| `sudo` works                     | Yes                     | ☐      |
| Linux telemetry visible in Wazuh | Yes                     | ☐      |
| Initial evidence captured        | Yes                     | ☐      |

---

# 9. Basic Troubleshooting

## Wazuh Agent Is Not Running

Check:

```
systemctl status wazuh-agent
```

If necessary:

```
sudo systemctl restart wazuh-agent
```

Then check the status again.

---

## Linux Cannot Reach Wazuh Server

Check the Linux IP:

```
ip addr
```

Test the server:

```
ping <WAZUH_MANAGER_IP>
```

Check:

* VMware network configuration
* Linux network interface
* Wazuh Server IP address
* Wazuh Server status
* Firewall configuration

---

## Wazuh Agent Is Running but Not Connected

Check the agent configuration:

```
sudo nano /var/ossec/etc/ossec.conf
```

Confirm that the configured Wazuh Manager address is correct.

Then restart:

```
sudo systemctl restart wazuh-agent
```

Check:

```
systemctl status wazuh-agent
```

---

## Authentication Log Does Not Exist

Some Linux distributions do not use:

```
/var/log/auth.log
```

Check:

```
ls -l /var/log/
```

Then check:

```
sudo journalctl
```

The correct log source depends on the Linux distribution.

---

## Journal Is Empty or Unavailable

Check the process running as PID 1:

```
ps -p 1 -o comm=
```

If `systemd` is being used, try:

```
sudo journalctl -n 20
```

---

# 10. Evidence Requirements

Evidence should be captured during the validation process and stored under:

```
Evidence/
```

Recommended evidence:

* Linux system information
* Linux IP address
* Wazuh Agent status
* Wazuh endpoint connection
* Authentication log
* Sudo activity
* System journal
* Centralized Wazuh telemetry

Evidence should demonstrate that the setup actually works rather than simply showing configuration screens.

---

# 11. Safety and Authorization

All monitoring and testing activities in this lab must be performed only against authorized virtual machines in the home lab.

Use harmless and controlled activity while validating the monitoring setup.

Do not intentionally attack external systems or generate unauthorized traffic.

Do not place credentials or other sensitive information inside screenshots, GitHub documentation, or evidence files.

---

# 12. Setup Completion Criteria

The **setup** is complete when:

1. Linux VM is operational.
2. Linux VM has network connectivity.
3. Wazuh Agent is installed.
4. Wazuh Agent configuration points to the correct Wazuh Server.
5. Wazuh Agent service is running.
6. Required Linux logging sources are available.

---

# 13. Validation Completion Criteria

The **validation** is complete when:

1. Linux can communicate with the Wazuh Server.
2. Wazuh Agent is running.
3. Linux endpoint appears in Wazuh.
4. Authentication activity is recorded locally.
5. Sudo activity is recorded locally.
6. System activity is available through Linux logging.
7. Linux telemetry is visible centrally in Wazuh.
8. Initial evidence has been captured.

Once both setup and validation are complete, the environment is ready for the next stage: understanding Linux event logging.

---

## Related Documentation

* `01-Lab-Objective.md`
* `03-Linux-Event-Logging.md`
* `04-Security-Monitoring-Configuration.md`
* `05-Log-Collection.md`
