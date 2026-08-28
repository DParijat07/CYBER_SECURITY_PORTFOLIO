# Wazuh SIEM Lab

## 1. Overview

This laboratory focuses on deploying, configuring, and using Wazuh as a Security Information and Event Management (SIEM) and security monitoring platform in a controlled home-lab environment.

The objective is to understand how a SOC analyst collects security telemetry, monitors endpoints, receives alerts, investigates suspicious activity, and documents security findings using Wazuh.

This lab forms the foundation for several later SOC laboratories and projects.

---

## 2. Objectives

The main objectives of this lab are:

- Understand the basic architecture of Wazuh.
- Deploy a Wazuh server.
- Connect endpoint agents to Wazuh.
- Verify agent communication.
- Configure log collection.
- Generate controlled security events.
- Observe collected telemetry.
- Analyze Wazuh alerts.
- Understand Wazuh rules and severity levels.
- Perform basic alert investigation.
- Practice the SOC monitoring workflow.
- Document evidence from investigations.
- Prepare the Wazuh environment for future SOC projects.

---

## 3. SOC Skills Demonstrated

This laboratory demonstrates:

- SIEM deployment
- Security monitoring
- Log collection
- Endpoint monitoring
- Alert analysis
- Event investigation
- Security telemetry analysis
- Basic incident triage
- Evidence collection
- Security documentation
- Home-lab administration

---

## 4. Lab Scenario

A small organization wants centralized security monitoring for its Windows and Linux endpoints.

The SOC analyst needs to:

1. Deploy a centralized Wazuh monitoring server.
2. Connect endpoint systems to the server.
3. Collect security telemetry.
4. Generate controlled security events.
5. Monitor the resulting alerts.
6. Investigate the events.
7. Determine whether the activity is benign or suspicious.
8. Document the findings.

The laboratory simulates this workflow using virtual machines.

---

## 5. Lab Architecture

The initial architecture is:

Windows 11 Host
├── VMware
│   ├── Ubuntu Server
│   │   └── Wazuh Server
│   ├── Windows 7
│   │   └── Wazuh Agent
│   ├── Kali Linux
│   ├── Kali Linux
│   └── Metasploitable 2

The architecture may be expanded as additional monitored endpoints are added.

---

## 6. Lab Components

### 6.1 Wazuh Server

The Wazuh server acts as the centralized security monitoring platform.

Responsibilities include:

- Receiving telemetry
- Processing events
- Applying detection rules
- Generating alerts
- Providing security visibility
- Supporting endpoint monitoring

### 6.2 Wazuh Agent

The Wazuh agent runs on monitored endpoints and forwards relevant security information to the Wazuh infrastructure.

### 6.3 Monitored Endpoints

Potential monitored systems include:

- Windows 7
- Windows 11 where appropriate
- Ubuntu Server
- Other authorized Linux systems

### 6.4 Analyst Workstation

Kali Linux or the Windows host may be used as an analyst workstation for controlled testing and investigation.

---

## 7. Tools and Technologies

### Primary Tools

- Wazuh
- VMware
- Ubuntu Server
- Windows
- Kali Linux

### Supporting Technologies

- Windows Event Logs
- Sysmon
- Linux logs
- Git
- GitHub
- Markdown

Additional tools may be introduced in later laboratories.

---

## 8. Prerequisites

Before starting this laboratory, the following should be available:

- VMware virtualization environment
- Ubuntu Server virtual machine
- Windows virtual machine
- Kali Linux virtual machine
- Working virtual network
- Administrative access to laboratory systems
- Internet connectivity when required for installation
- Sufficient system resources for the virtual machines

All systems must be owned by the learner or explicitly authorized for testing.

---

## 9. Lab Setup

The laboratory should be built in stages.

### Stage 1: Prepare Ubuntu Server

Prepare the Ubuntu Server virtual machine that will host Wazuh.

Tasks include:

- Configure hostname.
- Configure network connectivity.
- Update the operating system.
- Verify IP configuration.
- Verify network connectivity.
- Ensure sufficient resources are available.

Record:

- Hostname
- IP address
- Operating system version
- System resources

### Stage 2: Install Wazuh

Install the appropriate Wazuh server components according to the official Wazuh documentation and the selected version.

Record:

- Wazuh version
- Installation date
- Server IP address
- Hostname
- Installation method

### Stage 3: Access Wazuh Dashboard

Verify that the Wazuh dashboard is accessible from the authorized analyst workstation.

Confirm:

- Dashboard availability
- Authentication
- Server status
- Basic system health

### Stage 4: Deploy an Agent

Install a Wazuh agent on a monitored endpoint.

Record:

- Endpoint hostname
- Operating system
- Agent identifier
- Agent status
- Wazuh server address

### Stage 5: Verify Agent Communication

Confirm that the agent successfully communicates with the Wazuh server.

Expected telemetry flow:

Endpoint
↓
Wazuh Agent
↓
Wazuh Server
↓
Wazuh Dashboard
↓
SOC Analyst

---

## 10. Initial Validation

After deployment, verify:

- Wazuh server is operational.
- Wazuh dashboard is accessible.
- Agent is registered.
- Agent is connected.
- Endpoint telemetry is being received.
- Alerts can be displayed.
- System time is synchronized.
- Network connectivity is stable.

Document any configuration issues encountered during setup.

---

## 11. Log Collection

The next stage is understanding how endpoint telemetry reaches Wazuh.

### Windows Telemetry

Potential sources include:

- Security Event Log
- System Event Log
- Application Event Log
- PowerShell-related events
- Sysmon events where configured

### Linux Telemetry

Potential sources include:

- Authentication logs
- SSH logs
- System logs
- Service logs
- Application logs

The exact logs collected depend on the endpoint and Wazuh configuration.

---

## 12. Generate Controlled Security Events

Security events should be generated only inside the authorized laboratory environment.

Examples include:

- Failed login attempts
- Successful login
- User account activity
- Service activity
- Process execution
- File modification
- Configuration changes
- Controlled network connections

The purpose is to generate telemetry that can be observed and investigated.

---

## 13. Observe Wazuh Alerts

After generating a controlled event:

1. Open the Wazuh dashboard.
2. Locate the relevant endpoint.
3. Review generated alerts.
4. Identify the timestamp.
5. Identify the affected system.
6. Review the rule information.
7. Review the event details.
8. Record relevant evidence.

The analyst should not automatically assume that every alert represents a confirmed security incident.

---

## 14. Alert Triage

The first investigation step is alert triage.

For each selected alert, review:

- Alert timestamp
- Alert severity
- Rule ID
- Rule description
- Hostname
- Agent ID
- Username
- Process
- Source IP
- Destination IP
- Event type
- Raw event information

Then determine:

Alert
↓
Initial Review
↓
Context Collection
↓
Benign / Suspicious
↓
Further Investigation if Required

---

## 15. Alert Severity

Wazuh rule levels indicate the relative importance of alerts.

However, severity alone does not determine whether an event is malicious.

Alert interpretation should consider:

- Severity
- Context
- Asset importance
- User behavior
- Event frequency
- Related events
- Threat intelligence
- Historical activity

---

## 16. Investigation Methodology

Use a structured investigation approach.

### Step 1: Identify the Event

Determine what triggered the alert.

### Step 2: Identify the Asset

Determine which endpoint generated the event.

### Step 3: Identify the User

Determine whether a user account was involved.

### Step 4: Identify the Process

Determine which process or application generated the activity where available.

### Step 5: Review Related Events

Search for events before and after the alert.

### Step 6: Establish a Timeline

Build a simple event timeline.

### Step 7: Determine the Context

Ask:

- Is this expected?
- Is this normal for the user?
- Is this normal for the system?
- Is this a repeated event?
- Are there related alerts?

### Step 8: Determine the Finding

Classify the activity based on available evidence.

Possible outcomes:

- Benign
- Suspicious
- Confirmed malicious
- Inconclusive

---

## 17. Investigation Timeline

Create a timeline for important investigations.

Recommended format:

| Time | Host | User | Event | Observation |
|------|------|------|-------|-------------|
| T1 | Endpoint | User | Event generated | Initial activity |
| T2 | Endpoint | User | Wazuh alert | Detection |
| T3 | Endpoint | User | Related event | Investigation |
| T4 | Endpoint | User | Follow-up event | Context |
| T5 | Endpoint | User | Final state | Conclusion |

Use actual timestamps from laboratory evidence.

---

## 18. Evidence Collection

Evidence should include only information relevant to the investigation.

Examples:

- Wazuh alert screenshot
- Alert details
- Raw event
- Endpoint information
- Related logs
- Investigation timeline
- Relevant queries
- Detection rule information

Store screenshots and supporting files inside the appropriate laboratory directories.

---

## 19. Evidence Directory

Recommended structure:

evidence/
├── screenshots/
├── alerts/
├── logs/
└── notes/

Only create directories that are actually required.

---

## 20. Screenshot Standard

Screenshots should clearly demonstrate the activity being documented.

Useful screenshots may show:

- Alert name
- Timestamp
- Host
- Rule
- Event details
- Relevant investigation context

Avoid screenshots containing unnecessary sensitive information.

---

## 21. Wazuh Rule Investigation

For selected alerts, investigate the associated Wazuh rule.

Document:

- Rule ID
- Rule description
- Severity
- Log source
- Event type
- Detection logic where available
- Relevant MITRE ATT&CK mapping where available

The purpose is to understand why the alert was generated.

---

## 22. False Positive Analysis

Not every alert is malicious.

For selected alerts, determine whether the activity could be legitimate.

Consider:

- Expected administrative activity
- Scheduled tasks
- Normal user behavior
- Software installation
- System maintenance
- Automated services
- Security software activity

Document the reasoning behind the classification.

---

## 23. Basic SOC Workflow

This laboratory demonstrates the basic SOC monitoring cycle:

Telemetry
↓
SIEM
↓
Alert
↓
Triage
↓
Investigation
↓
Analysis
↓
Classification
↓
Response / Escalation
↓
Documentation

This workflow will be reused in later SOC projects.

---

## 24. MITRE ATT&CK Mapping

Where applicable, map observed behavior to MITRE ATT&CK techniques.

Document:

- Technique ID
- Technique Name
- Observed Behavior
- Supporting Evidence

Do not assign a technique simply because it appears related.

The mapping should be supported by actual laboratory evidence.

---

## 25. Threat Intelligence Integration

Threat intelligence is not required for every basic Wazuh alert.

For alerts containing potentially useful indicators, investigation may include:

- IP address enrichment
- Domain enrichment
- Hash enrichment
- Reputation analysis
- TTP research

Threat intelligence should add context rather than replace internal evidence.

---

## 26. Incident Classification

After investigation, classify the event.

Recommended model:

Informational
↓
Benign
↓
Suspicious
↓
Potential Incident
↓
Confirmed Incident

The classification should be based on available evidence.

---

## 27. Analyst Notes

For every investigated alert, maintain concise analyst notes.

Recommended format:

Alert:
Timestamp:
Host:
User:
Severity:
Rule:
Initial Assessment:
Evidence:
Related Events:
Investigation:
Finding:
Recommended Action:

---

## 28. Recommended Actions

### Benign

- Close the alert.
- Document the reasoning.
- Tune the detection if necessary.

### Suspicious

- Continue investigation.
- Collect additional evidence.
- Search for related activity.
- Consider escalation.

### Confirmed Incident

- Escalate according to the incident response process.
- Preserve evidence.
- Contain the affected system when appropriate.
- Investigate scope and impact.
- Document the incident.

---

## 29. Lessons Learned

Document:

- What was learned about Wazuh?
- What telemetry was useful?
- Which alerts were easy to investigate?
- Which alerts lacked sufficient context?
- What configuration problems occurred?
- What detection gaps were identified?
- What should be improved?

---

## 30. Common Troubleshooting Areas

### Agent Not Connected

Check:

- Network connectivity
- Server address
- Agent configuration
- Agent service
- Firewall
- Authentication or registration
- System time

### No Events

Check:

- Log source configuration
- Agent status
- Log generation
- Collection configuration
- Permissions
- Service status

### Dashboard Problems

Check:

- Wazuh services
- Network connectivity
- Authentication
- System resources
- Browser connectivity

Document troubleshooting steps rather than hiding configuration problems.

---

## 31. Lab Deliverables

The completed laboratory should produce:

- Wazuh server
- At least one monitored endpoint
- Verified agent communication
- Working telemetry collection
- Generated security events
- Investigated Wazuh alerts
- Screenshots
- Investigation notes
- Basic timeline
- Findings
- Lessons learned

---

## 32. Recommended Directory Structure

01-Wazuh-SIEM-Lab/
├── README.md
├── screenshots/
├── evidence/
├── logs/
├── queries/
└── scripts/

Only populate directories when evidence or supporting files exist.

---

## 33. Completion Checklist

- [ ] Ubuntu Server prepared.
- [ ] Wazuh installed.
- [ ] Wazuh dashboard accessible.
- [ ] Endpoint agent installed.
- [ ] Agent registered successfully.
- [ ] Agent connected successfully.
- [ ] Endpoint telemetry received.
- [ ] Security events generated.
- [ ] Wazuh alerts observed.
- [ ] At least one alert investigated.
- [ ] Evidence collected.
- [ ] Investigation timeline created.
- [ ] Alert classification completed.
- [ ] MITRE ATT&CK mapping completed where applicable.
- [ ] Lessons learned documented.
- [ ] Screenshots reviewed.
- [ ] Sensitive information removed.
- [ ] GitHub documentation updated.

---

## 34. Skills Demonstrated

After completing this laboratory, the following practical skills should be demonstrated:

- SIEM deployment
- SIEM configuration
- Endpoint onboarding
- Log collection
- Security monitoring
- Alert triage
- Event analysis
- Basic incident investigation
- Evidence collection
- Security documentation
- SOC workflow understanding

---

## 35. Future Expansion

This foundational Wazuh environment will support future laboratories involving:

- Windows Security Monitoring
- Linux Security Monitoring
- Sysmon Endpoint Monitoring
- IOC Investigation
- Threat Intelligence
- Threat Hunting
- Detection Engineering
- Incident Response
- Vulnerability Monitoring
- SOC Automation
- AI-Assisted SOC Operations

The Wazuh laboratory therefore acts as the central monitoring foundation for the broader SOC portfolio.

---

## 36. Portfolio Value

This laboratory demonstrates more than basic Wazuh installation.

It provides evidence that the analyst can:

**Deploy → Monitor → Generate Events → Detect → Investigate → Analyze → Document**

This is an important foundation for an entry-level SOC Analyst portfolio.

---

## 37. Final Outcome

The final goal of this laboratory is to establish a functioning SOC monitoring environment that can be reused for increasingly complex investigations.

The progression is:

Wazuh Deployment
↓
Endpoint Monitoring
↓
Security Telemetry
↓
Alert Detection
↓
Alert Triage
↓
Investigation
↓
Incident Analysis
↓
Incident Response
↓
Threat Hunting
↓
Detection Engineering
↓
SOC Automation

---

## 38. Disclaimer

All activities documented in this laboratory are performed in authorized and controlled environments for educational and defensive cybersecurity purposes.

No unauthorized systems, networks, accounts, or infrastructure should be targeted.

---

## 39. Status

**Status:** In Progress

This laboratory will be updated as the Wazuh environment is configured, tested, investigated, and integrated with subsequent SOC laboratories and projects.
