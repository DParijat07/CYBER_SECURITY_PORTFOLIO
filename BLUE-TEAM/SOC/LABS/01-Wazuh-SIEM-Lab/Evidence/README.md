# Evidence

## Purpose

This directory contains the practical evidence collected during the Wazuh SIEM lab.

The evidence demonstrates that the lab was actually performed and supports the findings documented in the `Documentation/` and `Reports/` directories.

## Evidence Types

Examples of evidence that can be stored here:

* Wazuh dashboard screenshots
* Security alert screenshots
* Log/event screenshots
* Detection results
* Investigation results
* Incident response results
* Relevant exported logs
* Relevant JSON/CSV/text evidence
* Screenshots showing configuration or testing results

## Evidence Guidelines

* Evidence should directly support a documented activity or finding.
* Use clear and descriptive filenames.
* Capture relevant timestamps whenever possible.
* Remove passwords, tokens, API keys, personal information, and other sensitive data before committing.
* Avoid uploading unnecessary or duplicate screenshots.
* Evidence should be organized logically and remain easy to trace back to the corresponding documentation or report.

## Recommended Naming Convention

Use descriptive names such as:

* `wazuh-dashboard.png`
* `security-alert.png`
* `failed-login-alert.png`
* `windows-event-log.txt`
* `incident-investigation.png`
* `detection-result.png`

## Evidence and Documentation Relationship

```text
Documentation/
    ↓
Lab activity / procedure / investigation
    ↓
Evidence/
    ↓
Screenshots / logs / technical proof
    ↓
Reports/
    ↓
Final findings and conclusions
```

## Objective

The objective of this directory is to provide verifiable technical proof of the activities, detections, investigations, and responses performed in the Wazuh SIEM lab.
