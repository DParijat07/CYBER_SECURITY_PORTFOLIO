# Documentation

## Purpose

This directory contains the complete technical documentation for the Wazuh SIEM lab.

It explains the lab objective, setup, installation, configuration, monitoring, detection, alert analysis, investigation, incident response, testing procedures, troubleshooting, and lessons learned.

## Wazuh Lab Workflow

The lab follows a practical SOC workflow that simulates how a security analyst handles a security event from initial activity through final verification.

```text
Attack / Suspicious Activity
            ↓
      Log Generation
            ↓
       Log Collection
            ↓
      Wazuh Analysis
            ↓
     Detection Rule
            ↓
       SOC Alert
            ↓
      Alert Analysis
            ↓
   Incident Investigation
            ↓
      Incident Response
            ↓
     Remediation / Action
            ↓
       Verification
            ↓
     Lessons Learned
```

## Scenario-Based Workflow Examples

The lab uses controlled scenarios to demonstrate how security events move through the SOC workflow.

### Scenario 1 — Multiple Failed Login Attempts

**Objective:** Detect and investigate repeated authentication failures.

```text
Failed Login Attempts
        ↓
Windows/Linux Authentication Logs
        ↓
Wazuh Agent Collects Events
        ↓
Wazuh Detection Rule
        ↓
Authentication Alert
        ↓
Analyst Reviews Source IP / User / Timestamp
        ↓
Investigate Related Authentication Events
        ↓
Determine Brute-Force or Benign Activity
        ↓
Response / Account Protection
        ↓
Verify Detection
```

**Analyst focus:**

* Number of failed attempts
* Source address
* Target account
* Time pattern
* Successful login after failures
* Related authentication events

### Scenario 2 — Suspicious Process Execution

**Objective:** Detect potentially suspicious process activity on a monitored endpoint.

```text
Suspicious Process Execution
        ↓
Endpoint Generates Process Event
        ↓
Sysmon / Endpoint Telemetry
        ↓
Wazuh Agent
        ↓
Wazuh Analysis
        ↓
Detection Alert
        ↓
Process / Parent Process Analysis
        ↓
User / Command-Line Investigation
        ↓
Determine Malicious or Legitimate Activity
        ↓
Response / Containment
        ↓
Verification
```

**Analyst focus:**

* Process name
* Parent process
* Command line
* Executing user
* Execution time
* Related processes
* Indicators of compromise

### Scenario 3 — File Integrity Change

**Objective:** Detect unauthorized modification of a monitored file.

```text
File Modified
      ↓
Endpoint File Integrity Monitoring
      ↓
Wazuh Agent
      ↓
File Integrity Event
      ↓
Wazuh Detection
      ↓
Alert Generated
      ↓
Analyst Identifies File / User / Timestamp
      ↓
Investigate Related Activity
      ↓
Determine Authorized or Unauthorized Change
      ↓
Remediation
      ↓
Verify File State and Monitoring
```

**Analyst focus:**

* Modified file
* Previous and current state
* User responsible
* Timestamp
* Related processes
* Whether the change was authorized

### Scenario 4 — Suspicious Network Activity

**Objective:** investigate unusual network activity detected from a monitored endpoint.

```text
Suspicious Network Activity
        ↓
Network / Endpoint Event
        ↓
Log Collection
        ↓
Wazuh Analysis
        ↓
Detection
        ↓
SOC Alert
        ↓
Source / Destination Analysis
        ↓
Correlate With Endpoint Events
        ↓
Identify Suspicious Communication
        ↓
Response / Blocking
        ↓
Verify
```

**Analyst focus:**

* Source and destination
* Port and protocol
* Timestamp
* Associated process
* Repeated connections
* Known or suspicious indicators

## Scenario Investigation Model

Each scenario should be documented using the same analyst workflow:

```text
1. Trigger
   ↓
2. Detect
   ↓
3. Validate Alert
   ↓
4. Investigate
   ↓
5. Identify Root Cause
   ↓
6. Respond
   ↓
7. Remediate
   ↓
8. Verify
   ↓
9. Document Findings
```

## Scenario Documentation Requirements

For each scenario, document:

* Scenario objective
* Lab environment
* Triggering activity
* Logs generated
* Wazuh detection
* Alert details
* Investigation steps
* Findings
* Indicators of compromise, if applicable
* Response actions
* Remediation
* Verification results
* Supporting evidence
* Lessons learned

## Documentation Structure

The documentation is organized in a logical sequence:

1. Lab Objective
2. Lab Setup
3. Installation
4. Configuration
5. Log Collection
6. Detection Rules
7. Alert Analysis
8. Incident Investigation
9. Incident Response
10. Procedures
11. Scenarios
12. Evidence
13. Troubleshooting
14. Lessons Learned

## Documentation Standards

* Document practical activities performed in the lab.
* Use clear and technically accurate explanations.
* Include relevant commands, configurations, observations, and results.
* Link technical findings to supporting evidence where appropriate.
* Keep documentation reproducible so another learner can understand and repeat the lab.
* Do not include passwords, API keys, tokens, or other sensitive information.
* Use controlled and authorized lab activity only.
* Clearly distinguish simulated security activity from real-world incidents.

## Relationship With Other Lab Directories

```text
Documentation/
    ↓
What was done and how it was done

Evidence/
    ↓
Technical proof of the activities

Reports/
    ↓
Professional analysis, findings, and conclusions
```

## Objective

The objective of this directory is to maintain a structured, professional, and reproducible record of the Wazuh SIEM lab activities and security operations workflow.

The lab demonstrates practical SOC capabilities through scenario-based exercises:

**Generate → Detect → Analyze → Investigate → Respond → Remediate → Verify → Document**
