# Wazuh SIEM Lab — Evidence

## 1. Purpose

This document defines the evidence-collection and evidence-management standards for the Wazuh SIEM laboratory.

The purpose of collecting evidence is to demonstrate practical hands-on SOC experience and provide verifiable proof of laboratory activities.

Evidence should support the work documented in the Documentation/ and Reports/ directories.

All evidence must be collected only from authorized laboratory systems.

---

## 2. Evidence Objectives

The evidence collection process should demonstrate the ability to:

1. Capture security alerts.
2. Preserve relevant event information.
3. Document investigation findings.
4. Record security telemetry.
5. Capture screenshots of important activities.
6. Preserve relevant logs.
7. Maintain investigation timelines.
8. Document detection results.
9. Support incident reports.
10. Maintain organized and reproducible proof of work.

---

## 3. Evidence Categories

Evidence for this laboratory should primarily be organized into:

Evidence/
├── Screenshots/
└── Logs/

### Screenshots

Visual proof of:

- Wazuh Dashboard
- Agent status
- Alerts
- Detection results
- Investigation activity
- Monitoring results

### Logs

Relevant security logs and event outputs used during investigation.

---

## 4. Evidence Collection Principles

Follow these principles:

- Collect only relevant evidence.
- Preserve original evidence where practical.
- Do not unnecessarily modify evidence.
- Record timestamps.
- Record the source of evidence.
- Maintain consistent naming.
- Sanitize sensitive information before publication.
- Keep evidence linked to the relevant scenario or report.
- Avoid publishing credentials or private information.

---

## 5. Evidence Naming Convention

Use the following naming convention:

YYYY-MM-DD_<Lab>_<Scenario>_<Evidence-Type>_<Number>

Example:

2026-09-02_Wazuh_AuthenticationAlert_Screenshot_01.png

Log example:

2026-09-02_Wazuh_AuthenticationAlert_Log_01.txt

Use descriptive names rather than generic names such as:

image1.png
test.png
final.png

---

## 6. Screenshot Evidence

Screenshots should capture meaningful information.

Useful screenshots include:

- Wazuh Dashboard
- Alert details
- Rule information
- Agent status
- Event details
- Authentication events
- Process events
- File-integrity alerts
- Investigation timeline
- Detection results

Avoid taking large numbers of redundant screenshots.

---

## 7. Screenshot Standards

A useful screenshot should:

- Clearly show the relevant information.
- Include enough context to understand the event.
- Show the timestamp where relevant.
- Show the host or agent where relevant.
- Avoid exposing passwords or secrets.
- Avoid unnecessary personal information.
- Be readable at normal viewing size.

---

## 8. Alert Evidence

For important alerts, capture:

- Alert timestamp
- Rule ID
- Rule description
- Rule level
- Rule group
- Agent
- Host
- User
- Source information
- Event details

The screenshot should support the written investigation.

---

## 9. Event Evidence

When an event is used during investigation, record:

| Field | Value |
|---|---|
| Timestamp | |
| Host | |
| Agent | |
| User | |
| Event Type | |
| Rule ID | |
| Source | |
| Destination | |
| Process | |
| File | |
| Description | |

Only populate fields relevant to the event.

---

## 10. Log Evidence

Relevant logs may be preserved when they provide important investigation context.

Examples include:

- Authentication logs
- Windows Security logs
- Linux authentication logs
- System logs
- Application logs
- File-integrity events
- Process-related telemetry
- Network-related logs

Store relevant log evidence in:

Evidence/Logs/

---

## 11. Evidence Screenshots Directory

Recommended organization:

Evidence/
└── Screenshots/

Additional subdirectories may be created only when they provide a clear organizational benefit.

---

## 12. Evidence Logs Directory

Recommended organization:

Evidence/
└── Logs/

Use additional categories only when required by the laboratory.

Do not create unnecessary directory structures.

---

## 13. Evidence-to-Scenario Mapping

Every important evidence item should be traceable to a scenario.

Example:

| Evidence | Scenario | Purpose |
|---|---|---|
| Screenshot 01 | Scenario 01 | Authentication alert |
| Screenshot 02 | Scenario 01 | Event details |
| Log 01 | Scenario 01 | Authentication evidence |
| Screenshot 03 | Scenario 04 | File modification |
| Log 02 | Scenario 04 | File-integrity evidence |

This makes the portfolio easier to audit.

---

## 14. Evidence-to-Report Mapping

Evidence should support investigation reports.

Example:

Reports/
└── Investigation-Reports/
    └── Authentication-Investigation.md

Evidence/
└── Screenshots/
    ├── 2026-09-02_Wazuh_AuthenticationAlert_Screenshot_01.png
    └── 2026-09-02_Wazuh_AuthenticationAlert_Screenshot_02.png

The report should reference the relevant evidence.

---

## 15. Evidence Metadata

For significant evidence, maintain basic metadata.

| Field | Value |
|---|---|
| Evidence ID | |
| Date | |
| Time | |
| Scenario | |
| Evidence Type | |
| Source System | |
| Host | |
| Analyst | |
| Description | |
| Related Report | |

---

## 16. Evidence Integrity

Where practical, maintain the integrity of important evidence.

Useful practices include:

- Preserve original files.
- Avoid unnecessary editing.
- Maintain consistent timestamps.
- Use descriptive filenames.
- Record evidence metadata.
- Use file hashes for important exported evidence when appropriate.

Example:

Evidence File → SHA-256 Hash → Evidence Record

Hashing is particularly useful when demonstrating evidence-handling practices.

---

## 17. Evidence Sanitization

Before uploading evidence to GitHub, inspect it for sensitive information.

Remove or obscure:

- Passwords
- API keys
- Tokens
- Private IP addresses where necessary
- Personal information
- Email addresses
- Authentication secrets
- Private hostnames where necessary
- Unrelated confidential information

Never publish credentials even if they were used only in the laboratory.

---

## 18. Evidence Quality

High-quality evidence should answer:

**What happened?**

**When did it happen?**

**Where did it happen?**

**Which system generated the evidence?**

**Why is this evidence relevant?**

Evidence without context is less useful.

---

## 19. Evidence Collection Workflow

Use the following workflow:

Activity → Event → Alert → Evidence Capture → Evidence Verification → Sanitization → Storage → Report Reference

This ensures that evidence is connected to the actual investigation.

---

## 20. Evidence for Detection Rules

For custom detection rules, capture:

1. Detection objective.
2. Test event.
3. Rule information.
4. Generated alert.
5. Alert details.
6. Detection result.
7. False-positive evaluation.
8. Final validation.

This demonstrates that the detection was actually tested.

---

## 21. Evidence for Alert Analysis

For alert-analysis exercises, capture:

- Alert overview
- Rule ID
- Rule level
- Rule description
- Event details
- Host
- User
- Source information
- Analyst classification

The evidence should support the triage decision.

---

## 22. Evidence for Incident Investigation

For investigations, collect evidence such as:

- Initial alert
- Related alerts
- Authentication events
- Process events
- File events
- Network events
- Timeline
- IoCs
- Investigation findings

Only retain evidence that is relevant to the investigation.

---

## 23. Evidence for Incident Response

Where an incident-response scenario is performed, evidence may include:

- Initial detection
- Investigation findings
- Containment action
- Eradication action
- Recovery validation
- Monitoring after recovery
- Final closure

The evidence should demonstrate the response process without exposing sensitive information.

---

## 24. Evidence Checklist

### Collection

- [ ] Relevant alert captured.
- [ ] Event details captured.
- [ ] Relevant logs preserved.
- [ ] Screenshots captured.
- [ ] Timeline documented.
- [ ] Indicators recorded.

### Verification

- [ ] Evidence source identified.
- [ ] Timestamp verified.
- [ ] Host identified.
- [ ] Scenario identified.
- [ ] Evidence is relevant.

### Sanitization

- [ ] Passwords removed.
- [ ] Tokens removed.
- [ ] API keys removed.
- [ ] Personal information removed.
- [ ] Sensitive network information reviewed.

### Organization

- [ ] Consistent filename used.
- [ ] Evidence stored in correct directory.
- [ ] Evidence linked to scenario.
- [ ] Evidence linked to report.

---

## 25. Evidence Collection Record

Use the following template when documenting important evidence:

| Field | Value |
|---|---|
| Evidence ID | |
| Scenario ID | |
| Date | |
| Time | |
| Evidence Type | |
| File Name | |
| Source | |
| Host | |
| Description | |
| Related Alert | |
| Related Report | |
| Sanitized | Yes / No |
| Hash | |
| Notes | |

---

## 26. Portfolio Evidence Standards

The objective is not to upload every screenshot generated during the laboratory.

Instead, select evidence that demonstrates meaningful capability.

Good portfolio evidence should show:

- Real laboratory activity
- Security monitoring
- Detection
- Investigation
- Analysis
- Decision-making
- Documentation
- Professional workflow

Quality is more important than quantity.

---

## 27. Recommended Evidence Per Scenario

For a normal scenario, aim for:

- 1–3 meaningful screenshots
- Relevant log evidence
- Investigation notes
- Timeline where applicable
- Final classification
- Related report where applicable

Complex scenarios may require additional evidence.

Avoid excessive duplication.

---

## 28. GitHub Publication Guidelines

Before publishing evidence:

1. Review every file.
2. Remove sensitive information.
3. Check screenshots for credentials.
4. Check logs for private information.
5. Use descriptive filenames.
6. Confirm that evidence belongs to the laboratory.
7. Link evidence to documentation or reports.
8. Verify that files open correctly on GitHub.

---

## 29. Common Evidence Mistakes

### Too Many Screenshots

Large numbers of repetitive screenshots reduce clarity.

### No Context

A screenshot without explanation may not prove much.

### Sensitive Information

Never publish secrets or credentials.

### Poor Naming

Generic filenames make evidence difficult to understand.

### No Scenario Mapping

Evidence should clearly relate to a specific exercise.

### No Report Reference

Important evidence should support documented findings.

### Editing Original Evidence

Avoid unnecessary modifications to evidence.

---

## 30. Evidence Review Checklist

Before committing evidence to the repository:

- [ ] Evidence is relevant.
- [ ] Evidence is readable.
- [ ] Timestamp is visible where relevant.
- [ ] Source is identifiable.
- [ ] Scenario is identifiable.
- [ ] Sensitive information has been removed.
- [ ] Filename follows the naming convention.
- [ ] Evidence is stored correctly.
- [ ] Related documentation exists.
- [ ] Related report exists where required.

---

## 31. Final Evidence Structure

The practical structure should remain concise:

01-Wazuh-SIEM-Lab/
├── README.md
├── Documentation/
├── Evidence/
│   ├── Screenshots/
│   └── Logs/
└── Reports/

Additional subdirectories should only be introduced when they provide a clear organizational benefit.

---

## 32. Final Outcome

The Evidence section should provide credible proof that the Wazuh SIEM laboratory was actually performed.

The evidence workflow is:

Perform → Observe → Capture → Verify → Sanitize → Organize → Reference

A well-organized evidence repository strengthens the overall cybersecurity portfolio by connecting practical laboratory work with documented technical knowledge and professional investigation reports.

---

## 33. Next Step

After completing the Evidence documentation, continue with:

13-Troubleshooting.md

The next document will cover common Wazuh laboratory problems, diagnostic steps, agent connectivity issues, log-collection problems, alert-generation issues, and practical troubleshooting methodology.
```
