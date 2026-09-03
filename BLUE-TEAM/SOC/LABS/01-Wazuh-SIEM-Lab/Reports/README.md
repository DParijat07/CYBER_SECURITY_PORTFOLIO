## Report Naming Convention

All reports should follow a consistent naming convention to make them easy to identify, sort, and reference.

### Standard Format

```text
YYYY-MM-DD_Report-Type_Scenario-Name.md
```

### Naming Components

**YYYY-MM-DD**

The date on which the report was created or the investigation was completed.

**Report-Type**

Describes the purpose of the report.

Recommended report types:

* `Alert-Investigation`
* `Incident-Investigation`
* `Incident-Response`
* `Detection-Validation`
* `Security-Assessment`
* `Monitoring-Assessment`
* `Threat-Analysis`
* `Post-Incident-Review`

**Scenario-Name**

A short, descriptive name representing the security scenario.

Use:

* Title Case
* Hyphens instead of spaces
* No special characters
* Short but meaningful names

### Examples

```text
2026-09-03_Alert-Investigation_Failed-Login.md
2026-09-04_Incident-Investigation_Suspicious-Process.md
2026-09-05_Incident-Response_Brute-Force-Attempt.md
2026-09-06_Detection-Validation_File-Integrity.md
2026-09-07_Threat-Analysis_Suspicious-Network-Activity.md
```

### Evidence References

Reports should reference the corresponding evidence files using the same scenario terminology whenever possible.

Example:

```text
Report:
2026-09-03_Alert-Investigation_Failed-Login.md

Related Evidence:
failed-login-alert.png
failed-login-events.json
investigation-timeline.png
```

### Naming Rules

* Use lowercase or uppercase consistently; this lab uses `Title-Case` for report types and scenario names.
* Use ISO date format: `YYYY-MM-DD`.
* Use hyphens instead of spaces.
* Do not use vague names such as `report1.md`, `final-report.md`, or `test.md`.
* Do not include passwords, credentials, tokens, or sensitive information in filenames.
* Keep filenames concise and descriptive.
* Use `.md` for Markdown reports.
* Use the same scenario name when creating related documentation and evidence where practical.

### Objective

The naming convention ensures that reports remain organized, searchable, traceable, and professionally presented as the Wazuh lab grows.
