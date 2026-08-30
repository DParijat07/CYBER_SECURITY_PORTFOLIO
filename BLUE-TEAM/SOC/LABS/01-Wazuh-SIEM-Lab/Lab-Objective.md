# Wazuh SIEM Lab — Lab Objective

## 1. Lab Overview

This laboratory is designed to build practical experience with Wazuh as a Security Information and Event Management (SIEM) and security monitoring platform in a controlled home-lab environment.

The lab focuses on deploying and operating a Wazuh-based monitoring environment, collecting security telemetry from endpoints, generating controlled security events, analyzing alerts, and performing basic SOC investigation workflows.

This lab provides the foundation for subsequent Windows, Linux, endpoint monitoring, threat hunting, incident response, and detection engineering laboratories.

---

## 2. Primary Objective

The primary objective of this laboratory is to understand how a SIEM collects, processes, analyzes, and presents security telemetry for SOC operations.

The practical workflow is:

**Endpoint → Agent → Wazuh Manager → Log Analysis → Detection → Alert → Investigation → Documentation**

---

## 3. Learning Objectives

After completing this laboratory, the learner should be able to:

1. Explain the role of a SIEM in a SOC.
2. Explain the basic architecture of Wazuh.
3. Understand the purpose of Wazuh agents.
4. Deploy a Wazuh server/manager in a controlled lab environment.
5. Connect monitored endpoints to Wazuh.
6. Configure basic endpoint monitoring.
7. Understand how security logs are collected.
8. Identify common security telemetry sources.
9. Generate controlled security events.
10. Observe security events inside Wazuh.
11. Understand Wazuh alerts and severity levels.
12. Perform basic alert triage.
13. Investigate suspicious events.
14. Correlate related events.
15. Identify relevant Indicators of Compromise (IOCs).
16. Document investigation findings.
17. Troubleshoot basic Wazuh monitoring problems.
18. Understand how Wazuh supports SOC analyst workflows.

---

## 4. SIEM Workflow Objective

The lab should demonstrate the following simplified SIEM workflow:

```text
Monitored Endpoint
       ↓
Security Event
       ↓
Log / Telemetry
       ↓
Wazuh Agent
       ↓
Wazuh Manager
       ↓
Analysis & Correlation
       ↓
Detection Rule
       ↓
Wazuh Alert
       ↓
SOC Analyst
       ↓
Triage
       ↓
Investigation
       ↓
Classification
       ↓
Documentation
```

The learner should understand what happens at each stage.

---

## 5. Wazuh Architecture Objectives

The laboratory should provide practical understanding of the major Wazuh components.

### Wazuh Manager

Responsible for receiving and analyzing security data from monitored endpoints.

### Wazuh Agent

Installed on monitored endpoints to collect relevant security information and send telemetry to the Wazuh environment.

### Wazuh Indexer

Stores and indexes security data for searching and analysis.

### Wazuh Dashboard

Provides the interface for viewing security events, alerts, agents, dashboards, and investigation data.

The learner should understand how these components work together.

---

## 6. Endpoint Monitoring Objectives

The lab should demonstrate endpoint monitoring using controlled systems.

Potential monitored endpoints include:

- Windows
- Linux
- Virtual machines
- Other authorized laboratory systems

The learner should understand how endpoint telemetry can include:

- Authentication events
- Process activity
- File activity
- System events
- Configuration changes
- Network-related events
- Security events

---

## 7. Security Event Generation Objectives

Controlled events should be generated to verify that monitoring is working correctly.

Examples may include:

- Failed login attempts
- Successful authentication
- Creation of a test user
- Modification of a test account
- Process execution
- File creation
- File modification
- Service activity
- Configuration changes
- Controlled network activity

All events should be generated only on authorized laboratory systems.

---

## 8. Alert Analysis Objectives

The learner should practice analyzing Wazuh alerts by examining:

- Alert timestamp
- Alert level
- Rule ID
- Rule description
- Source host
- Destination host, where applicable
- Username
- Process
- File
- Source IP
- Destination IP
- Event type
- Raw log data
- Related events

The objective is to understand what the alert means and whether additional investigation is required.

---

## 9. Alert Triage Objectives

The learner should develop a basic SOC alert-triage workflow.

For each alert, determine:

1. What happened?
2. When did it happen?
3. Which endpoint was affected?
4. Which user was involved?
5. What process or service was involved?
6. What generated the alert?
7. Is the activity expected?
8. Is there supporting evidence?
9. Are there related events?
10. Does the event indicate suspicious behavior?
11. Does the event require escalation?

---

## 10. Investigation Objectives

The laboratory should demonstrate how an analyst moves from an alert to an investigation.

The investigation should include:

```text
Alert
  ↓
Initial Triage
  ↓
Collect Context
  ↓
Review Related Events
  ↓
Build Timeline
  ↓
Identify Evidence
  ↓
Assess Risk
  ↓
Classify Activity
  ↓
Document Findings
```

The learner should avoid making conclusions based on a single isolated event when additional telemetry is available.

---

## 11. Event Correlation Objectives

The lab should demonstrate the importance of correlating multiple security events.

Example:

```text
Multiple Failed Logins
          ↓
Successful Login
          ↓
New Process Execution
          ↓
Privilege Change
          ↓
Network Connection
```

The individual events may appear harmless when viewed separately, but their sequence may provide additional context.

The learner should practice constructing an event timeline and identifying relationships between events.

---

## 12. IOC Identification Objectives

During investigation, the learner should identify potentially useful Indicators of Compromise.

Examples include:

- IP addresses
- Domains
- URLs
- File hashes
- File paths
- User accounts
- Process names
- Suspicious command lines
- Registry locations
- Hostnames

IOCs identified during controlled lab exercises should be documented with appropriate context.

---

## 13. Alert Classification Objectives

The learner should classify investigated activity using a simple classification model.

### Benign

Legitimate and expected activity.

### Suspicious

Activity requiring additional investigation.

### Potential Incident

Evidence indicates that the activity may represent a security incident.

### Confirmed Incident

Sufficient evidence exists to determine that a security incident has occurred.

### Inconclusive

Available evidence is insufficient to make a reliable determination.

---

## 14. Documentation Objectives

Every significant investigation should be documented.

The investigation record should contain:

- Investigation title
- Date and time
- Alert information
- Affected endpoint
- User
- Event details
- Relevant telemetry
- Investigation steps
- Evidence
- Timeline
- Findings
- Classification
- Recommended action
- Lessons learned

---

## 15. Troubleshooting Objectives

The learner should develop the ability to identify common monitoring problems.

Potential issues include:

- Agent not connected
- Agent not reporting
- Incorrect agent configuration
- Network connectivity problems
- Authentication problems
- Missing logs
- Incorrect log-source configuration
- Service failures
- Dashboard access problems
- Resource limitations
- Time synchronization issues

The learner should practice troubleshooting methodically rather than making random configuration changes.

---

## 16. SOC Skills Demonstrated

Completion of this laboratory should demonstrate practical capability in:

- SIEM fundamentals
- Wazuh administration
- Endpoint monitoring
- Log collection
- Security telemetry
- Alert monitoring
- Alert triage
- Event analysis
- Event correlation
- IOC identification
- Basic investigation
- Incident classification
- Security documentation
- Basic SOC workflow
- SIEM troubleshooting

---

## 17. Portfolio Evidence

The laboratory should produce practical evidence that can be included in the cybersecurity portfolio.

Potential evidence includes:

- Wazuh architecture diagram
- Wazuh installation screenshots
- Agent registration evidence
- Connected-agent status
- Log collection evidence
- Generated security events
- Wazuh alert screenshots
- Alert investigation notes
- Event timelines
- IOC analysis
- Detection results
- Troubleshooting records
- Final lab findings

Sensitive information should be removed or anonymized before publishing evidence publicly.

---

## 18. Prerequisite Knowledge

Before starting this laboratory, the learner should have basic knowledge of:

- Networking fundamentals
- Linux fundamentals
- Windows fundamentals
- Cybersecurity fundamentals
- Logs and events
- Virtual machines
- Basic SIEM concepts
- Basic command-line usage

Advanced Wazuh knowledge is not required.

---

## 19. Authorization and Safety

All activities in this laboratory must be performed only within an authorized and controlled environment.

The lab should use:

- Personally controlled virtual machines
- Test accounts
- Test data
- Controlled security events
- Isolated or properly segmented laboratory networking

Do not use the laboratory to monitor systems, accounts, networks, or data without authorization.

---

## 20. Success Criteria

The Wazuh SIEM laboratory is considered successfully completed when the learner can:

- [ ] Explain the purpose of a SIEM.
- [ ] Explain the basic Wazuh architecture.
- [ ] Deploy or configure a Wazuh monitoring environment.
- [ ] Connect an authorized endpoint.
- [ ] Verify agent communication.
- [ ] Collect endpoint security telemetry.
- [ ] Generate controlled security events.
- [ ] Identify corresponding Wazuh alerts.
- [ ] Analyze alert details.
- [ ] Perform basic alert triage.
- [ ] Correlate related events.
- [ ] Build an investigation timeline.
- [ ] Identify relevant IOCs.
- [ ] Classify investigated activity.
- [ ] Document investigation findings.
- [ ] Troubleshoot basic monitoring issues.
- [ ] Preserve appropriate evidence.
- [ ] Explain how the lab supports a SOC analyst workflow.

---

## 21. Expected Outcome

After completing this laboratory, the learner should be able to operate a basic Wazuh-based monitoring environment and understand how security telemetry moves from an endpoint into a SIEM.

The learner should be able to demonstrate:

```text
Endpoint
   ↓
Telemetry
   ↓
Wazuh
   ↓
Detection
   ↓
Alert
   ↓
Triage
   ↓
Investigation
   ↓
Evidence
   ↓
Classification
   ↓
Documentation
```

---

## 22. Final Objective

The final objective of this laboratory is to establish practical SIEM and security-monitoring capability using Wazuh.

The learner should finish the laboratory with the ability to:

> **Deploy → Monitor → Collect → Detect → Analyze → Investigate → Correlate → Classify → Document**

This laboratory forms the technical foundation for the subsequent SOC labs covering Windows security monitoring, Linux security monitoring, endpoint telemetry, network analysis, threat intelligence, threat hunting, incident response, digital forensics, detection engineering, vulnerability management, SOC automation, and AI-assisted SOC operations.
