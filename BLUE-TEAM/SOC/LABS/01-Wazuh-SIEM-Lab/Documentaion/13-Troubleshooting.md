# Wazuh SIEM Lab — Troubleshooting

## 1. Purpose

This document provides a practical troubleshooting guide for common issues encountered while operating the Wazuh SIEM laboratory.

The objective is to help identify, isolate, and resolve problems affecting:

- Wazuh Manager
- Wazuh Dashboard
- Wazuh Agents
- Log collection
- Event processing
- Alert generation
- File Integrity Monitoring
- Sysmon telemetry
- Laboratory network connectivity

Troubleshooting should be performed systematically and only on authorized laboratory systems.

---

## 2. Troubleshooting Methodology

Use the following troubleshooting workflow:

**Identify → Verify → Isolate → Investigate → Correct → Test → Document**

Avoid making multiple unrelated changes at the same time.

---

## 3. Initial Troubleshooting Checklist

Before investigating a specific issue, verify:

- [ ] Wazuh Manager is running.
- [ ] Wazuh Dashboard is accessible.
- [ ] Required agents are connected.
- [ ] Network connectivity is available.
- [ ] System time is synchronized.
- [ ] Required log sources are active.
- [ ] Expected events are being generated.
- [ ] Wazuh configuration is valid.
- [ ] Sufficient disk space is available.
- [ ] No recent configuration changes caused the issue.

---

## 4. Problem Classification

First identify which layer is affected.

| Layer | Example Problem |
|---|---|
| Infrastructure | VM or network unavailable |
| Manager | Wazuh service not running |
| Dashboard | Dashboard inaccessible |
| Agent | Agent disconnected |
| Collection | Logs not being received |
| Detection | Rule not generating an alert |
| Investigation | Events difficult to correlate |
| Evidence | Screenshots/logs not available |

Correctly identifying the layer reduces troubleshooting time.

---

## 5. Wazuh Manager Not Running

### Symptoms

- Dashboard does not show expected data.
- Agents cannot communicate with the Manager.
- Security events are not being processed.

### Checks

Verify:

- Manager service status.
- Manager logs.
- System resources.
- Recent configuration changes.

### General Procedure

1. Check whether the Manager service is running.
2. Review relevant Manager logs.
3. Check for configuration errors.
4. Verify available disk space.
5. Check CPU and memory utilization.
6. Restart the affected service only after identifying the likely cause.
7. Verify that event processing resumes.

---

## 6. Wazuh Dashboard Not Accessible

### Symptoms

- Browser cannot open the dashboard.
- Connection refused.
- Dashboard loads incorrectly.
- Security data is not displayed.

### Checks

Verify:

- Dashboard service.
- Network connectivity.
- Listening service.
- Browser connectivity.
- Server resources.
- Relevant dashboard logs.

### Procedure

1. Verify the Wazuh server is reachable.
2. Verify the dashboard service.
3. Check network connectivity.
4. Review dashboard logs.
5. Verify that required backend services are available.
6. Correct the identified issue.
7. Reload the dashboard.

---

## 7. Agent Disconnected

### Symptoms

An endpoint appears disconnected or inactive in Wazuh.

### Possible Causes

- Agent service stopped.
- Network connectivity problem.
- Incorrect Manager address.
- Firewall restriction.
- Incorrect agent configuration.
- VM network change.
- System shutdown.

### Procedure

1. Verify the endpoint is powered on.
2. Check endpoint network connectivity.
3. Check the Wazuh Agent service.
4. Verify the configured Manager address.
5. Check firewall rules.
6. Review agent logs.
7. Correct the identified issue.
8. Confirm that the agent reconnects.
9. Verify that new events are received.

---

## 8. Agent Connected but No Events

### Symptoms

The agent appears connected, but expected security events are not visible.

### Possible Causes

- Incorrect log collection configuration.
- Incorrect log path.
- Event source disabled.
- Insufficient permissions.
- Incorrect configuration.
- Event not generated.
- Processing delay.

### Procedure

1. Confirm the event actually occurred.
2. Check the local log source.
3. Verify the Wazuh Agent configuration.
4. Verify permissions.
5. Review agent logs.
6. Check Manager-side processing.
7. Generate another controlled test event.
8. Verify event reception.

---

## 9. Windows Logs Not Appearing

### Symptoms

Expected Windows security events are missing.

### Checks

Verify:

- Windows Event Log service.
- Relevant event channels.
- Wazuh Agent configuration.
- Agent connectivity.
- Event generation.

### Procedure

1. Confirm Windows Event Logging is operational.
2. Generate a controlled event.
3. Confirm the event exists locally.
4. Verify Wazuh collection configuration.
5. Check the Wazuh Agent logs.
6. Verify the event reaches the Manager.
7. Check whether a detection rule matches the event.

---

## 10. Linux Logs Not Appearing

### Symptoms

Expected Linux authentication or system events are missing.

### Checks

Verify:

- Logging service.
- Relevant log files.
- Wazuh Agent configuration.
- File permissions.
- Agent connectivity.

### Procedure

1. Identify the expected Linux log source.
2. Confirm the log file exists.
3. Generate a controlled test event.
4. Confirm the event is written locally.
5. Verify Wazuh collection.
6. Review Agent logs.
7. Verify the event reaches the Manager.

---

## 11. Sysmon Events Not Appearing

### Symptoms

Sysmon is installed, but expected telemetry is not visible.

### Possible Causes

- Sysmon service not running.
- Incorrect configuration.
- Incorrect Wazuh collection configuration.
- Event channel issue.
- Agent problem.

### Procedure

1. Verify Sysmon is installed.
2. Verify the Sysmon service.
3. Confirm Sysmon events exist locally.
4. Review the Sysmon event channel.
5. Verify Wazuh collection configuration.
6. Confirm the Agent is connected.
7. Generate a controlled test process.
8. Verify that the event reaches Wazuh.

---

## 12. File Integrity Monitoring Not Triggering

### Symptoms

A monitored file is modified but no expected event appears.

### Possible Causes

- File is not included in monitoring.
- Configuration is incorrect.
- Agent is disconnected.
- Monitoring interval has not elapsed.
- File event was not generated as expected.

### Procedure

1. Confirm the file is configured for monitoring.
2. Verify the Agent configuration.
3. Modify an authorized test file.
4. Wait for the monitoring interval.
5. Check for the resulting event.
6. Review Agent logs.
7. Verify the alert in Wazuh.

---

## 13. Alert Not Generated

### Symptoms

An event is visible, but no alert is generated.

### Possible Causes

- No matching rule.
- Rule condition not satisfied.
- Decoder did not parse the event correctly.
- Rule configuration problem.
- Event source is incomplete.

### Procedure

1. Confirm the raw event exists.
2. Review the event structure.
3. Determine whether a rule should match it.
4. Check the relevant rule configuration.
5. Validate the detection logic.
6. Test with another controlled event.
7. Review the resulting alert.

---

## 14. Custom Detection Rule Not Working

### Symptoms

A custom rule has been created but does not generate the expected alert.

### Troubleshooting Steps

1. Confirm the underlying event is being collected.
2. Review the event fields.
3. Verify the rule syntax.
4. Verify the rule ID.
5. Check rule conditions.
6. Confirm the rule is loaded.
7. Restart required services if appropriate.
8. Generate the test event again.
9. Verify the resulting alert.
10. Document the final result.

---

## 15. False Positive Alerts

### Symptoms

A legitimate activity repeatedly generates an alert.

### Procedure

1. Identify the triggering rule.
2. Determine why the rule matched.
3. Confirm the activity is legitimate.
4. Review the event context.
5. Determine whether the alert should be tuned.
6. Modify detection logic only when justified.
7. Retest the rule.
8. Document the tuning decision.

Avoid weakening detection logic simply to eliminate alerts.

---

## 16. Duplicate Alerts

### Symptoms

The same activity produces multiple alerts.

### Possible Causes

- Multiple collection paths.
- Multiple rules matching the same event.
- Duplicate event sources.
- Configuration overlap.

### Procedure

1. Compare alert timestamps.
2. Compare rule IDs.
3. Compare event contents.
4. Identify whether multiple rules are responsible.
5. Check collection configuration.
6. Determine whether the duplication is expected.
7. Tune the configuration if appropriate.

---

## 17. Delayed Events

### Symptoms

An event occurs but appears in Wazuh after a delay.

### Possible Causes

- Collection interval.
- Network latency.
- Processing load.
- Endpoint resource constraints.
- Manager resource constraints.

### Procedure

1. Record the event generation time.
2. Record the Wazuh reception time.
3. Compare timestamps.
4. Check endpoint resources.
5. Check Manager resources.
6. Review network connectivity.
7. Determine whether the delay is expected.

---

## 18. Time Synchronization Problems

### Symptoms

Events appear out of chronological order.

### Possible Causes

- Different system clocks.
- Incorrect timezone.
- Clock drift.
- Incorrect timestamp interpretation.

### Procedure

1. Check the time on the Manager.
2. Check the time on each Agent.
3. Verify timezone settings.
4. Synchronize system clocks.
5. Generate another test event.
6. Verify the resulting timestamps.

Accurate time is essential for incident investigation.

---

## 19. Network Connectivity Problems

### Symptoms

- Agent disconnected.
- Dashboard inaccessible.
- Events not reaching the Manager.

### Checks

Verify:

- VM network adapter.
- IP configuration.
- Routing.
- Firewall.
- Host-to-VM connectivity.
- Manager-to-Agent connectivity.

### Procedure

1. Check IP addresses.
2. Test connectivity between required systems.
3. Check routing.
4. Check firewall configuration.
5. Verify Wazuh communication settings.
6. Retest the connection.

---

## 20. Virtual Machine Problems

Because the laboratory may run inside virtual machines, verify:

- VM is powered on.
- Correct network adapter is selected.
- IP address is correct.
- VM resources are sufficient.
- Snapshots have not reverted important changes.
- Host system has sufficient resources.

Document significant VM configuration changes.

---

## 21. Disk Space Problems

### Symptoms

- Services fail.
- Logs stop being written.
- Performance decreases.
- Events are not processed correctly.

### Procedure

1. Check available disk space.
2. Identify large log files.
3. Review log-retention requirements.
4. Remove only unnecessary laboratory data.
5. Avoid deleting required evidence.
6. Verify service operation afterward.

Evidence required for the portfolio should be preserved before cleanup.

---

## 22. Performance Problems

### Symptoms

- Dashboard is slow.
- Alerts appear late.
- VM becomes unresponsive.
- Events take longer to process.

### Checks

Review:

- CPU usage
- Memory usage
- Disk usage
- Network usage
- Number of monitored endpoints
- Event volume

### Procedure

1. Identify the resource bottleneck.
2. Reduce unnecessary workload.
3. Verify VM resource allocation.
4. Review event volume.
5. Retest system performance.

---

## 23. Configuration Changes

When troubleshooting requires a configuration change:

1. Record the original configuration.
2. Identify the reason for the change.
3. Make the smallest required change.
4. Test the result.
5. Record the new configuration.
6. Verify normal operation.
7. Document the outcome.

Avoid undocumented configuration changes.

---

## 24. Troubleshooting Evidence

Capture evidence when troubleshooting significant problems.

Useful evidence includes:

- Error messages
- Service status
- Agent status
- Relevant logs
- Configuration excerpts
- Dashboard screenshots
- Before/after results
- Final verification

Store sanitized evidence in the `Evidence/` directory.

---

## 25. Troubleshooting Record

Use the following format:

| Field | Value |
|---|---|
| Issue ID | |
| Date | |
| Component | |
| Problem | |
| Symptoms | |
| Initial Hypothesis | |
| Investigation | |
| Root Cause | |
| Corrective Action | |
| Verification | |
| Final Status | |
| Evidence | |

---

## 26. Troubleshooting Decision Tree

Use this simplified process:

**Problem Detected**

↓

**Is the Component Running?**

- No → Investigate Service
- Yes → Continue

↓

**Is Network Connectivity Working?**

- No → Investigate Network
- Yes → Continue

↓

**Is the Event Generated?**

- No → Investigate Event Source
- Yes → Continue

↓

**Is the Event Collected?**

- No → Investigate Agent/Collection
- Yes → Continue

↓

**Is the Event Parsed?**

- No → Investigate Decoder/Format
- Yes → Continue

↓

**Does a Rule Match?**

- No → Investigate Detection Logic
- Yes → Continue

↓

**Is the Alert Visible?**

- No → Investigate Processing/Dashboard
- Yes → Continue

↓

**Issue Resolved**

---

## 27. Common Mistakes

### Changing Everything at Once

This makes the root cause difficult to identify.

### Ignoring Logs

Logs often provide the most useful troubleshooting information.

### Ignoring Time

Timestamp problems can make a working system appear broken.

### Assuming the Detection Rule Is the Problem

Always verify that the underlying event is actually being collected first.

### Deleting Evidence

Do not remove evidence simply to clean the laboratory.

### Not Documenting Changes

Undocumented changes make future troubleshooting harder.

---

## 28. Troubleshooting Checklist

### Infrastructure

- [ ] VM operational.
- [ ] Network adapter verified.
- [ ] IP configuration verified.
- [ ] Resources sufficient.

### Wazuh

- [ ] Manager operational.
- [ ] Dashboard operational.
- [ ] Agents connected.
- [ ] Relevant logs reviewed.

### Telemetry

- [ ] Event source operational.
- [ ] Event generated.
- [ ] Event collected.
- [ ] Event parsed.

### Detection

- [ ] Rule identified.
- [ ] Rule conditions verified.
- [ ] Alert generation tested.
- [ ] False positives evaluated.

### Resolution

- [ ] Root cause identified.
- [ ] Corrective action performed.
- [ ] System retested.
- [ ] Evidence captured.
- [ ] Troubleshooting documented.

---

## 29. Final Troubleshooting Standard

The laboratory troubleshooting process should follow:

**Observe → Verify → Isolate → Analyze → Correct → Validate → Document**

The goal is not simply to make the system work.

The goal is to understand:

- What failed?
- Why did it fail?
- How was it identified?
- What evidence supported the diagnosis?
- What corrective action was taken?
- How was the solution validated?

---

## 30. Final Outcome

Completion of this troubleshooting process demonstrates the ability to maintain and diagnose a practical SIEM laboratory.

This is an important SOC skill because analysts must be able to distinguish between:

- A genuine security event
- A monitoring failure
- A telemetry problem
- A detection problem
- A system problem
- A configuration problem

A reliable monitoring environment is necessary for reliable security analysis.

---

## 31. Next Step

After completing the Troubleshooting documentation, continue with:

14-Lessons-Learned.md

This final document will capture the technical lessons, SOC skills developed, challenges encountered, improvements identified, and future enhancements for the Wazuh SIEM laboratory.
