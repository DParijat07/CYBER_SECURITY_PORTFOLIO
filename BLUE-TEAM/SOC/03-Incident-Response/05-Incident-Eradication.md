# Incident Eradication

## 1. Introduction

Incident Eradication is the process of removing the root cause, malware, persistence mechanisms, compromised credentials, unauthorized access, and other attacker-controlled components from an affected environment.

Eradication begins after the incident has been sufficiently contained.

The objective is not simply to stop the attack temporarily, but to remove the attacker's ability to continue or regain access.

The basic workflow is:

    Detection
       ↓
    Triage
       ↓
    Investigation
       ↓
    Containment
       ↓
    Eradication
       ↓
    Recovery
       ↓
    Lessons Learned


---

## 2. Objectives of Eradication

The main objectives are to:

- Remove malware
- Remove persistence
- Remove unauthorized accounts
- Reset compromised credentials
- Remove malicious processes
- Remove malicious files
- Remove unauthorized access
- Remediate exploited vulnerabilities
- Correct security misconfigurations
- Remove attacker infrastructure from affected systems
- Prevent reinfection
- Prepare systems for safe recovery


---

## 3. Containment vs Eradication

Containment limits the attack.

Eradication removes the threat.

Example:

    Malware Detected
          ↓
    Endpoint Isolated
          ↓
    CONTAINMENT
          ↓
    Malware Removed
          ↓
    Persistence Removed
          ↓
    Vulnerability Fixed
          ↓
    ERADICATION


A system may remain contained until eradication has been completed and validated.


---

## 4. Eradication Principles

A professional eradication process should be:

### Complete

Remove all known attacker access and persistence.

### Evidence-Based

Use investigation findings to determine what needs to be removed.

### Controlled

Avoid unnecessary changes to unaffected systems.

### Repeatable

Use documented procedures and playbooks.

### Verified

Confirm that malicious activity has actually been removed.

### Preventive

Fix the weakness that allowed the incident to occur.


---

## 5. Eradication Lifecycle

A structured eradication process is:

    01. Review Investigation
          ↓
    02. Identify Root Cause
          ↓
    03. Identify Persistence
          ↓
    04. Identify Compromised Credentials
          ↓
    05. Remove Malware
          ↓
    06. Remove Persistence
          ↓
    07. Remediate Vulnerabilities
          ↓
    08. Harden Systems
          ↓
    09. Validate Eradication
          ↓
    10. Prepare Recovery


---

## 6. Root Cause

Eradication should address the root cause whenever possible.

Common root causes include:

- Phishing
- Weak credentials
- Unpatched software
- Exposed services
- Misconfiguration
- Excessive privileges
- Vulnerable applications
- Compromised third-party software
- Insecure cloud configuration
- Poor access controls


Example:

    Compromise
       ↓
    Vulnerable Web Application
       ↓
    Unpatched Software
       ↓
    Root Cause
       ↓
    Patch / Remediate
       ↓
    Prevent Recurrence


---

## 7. Malware Removal

Malware eradication may include:

- Delete malicious files
- Remove malicious processes
- Remove malware services
- Remove persistence
- Remove scheduled tasks
- Remove malicious scripts
- Quarantine infected files
- Reimage compromised systems when necessary


Example:

    Malware
       ↓
    Identify
       ↓
    Preserve Evidence
       ↓
    Remove
       ↓
    Scan
       ↓
    Validate


---

## 8. Malware Reimaging

In some incidents, rebuilding a compromised system is safer than attempting to clean it manually.

Reimaging may be appropriate when:

- System integrity cannot be trusted
- Root-level compromise occurred
- Persistence is extensive
- Malware removal cannot be reliably verified
- Critical system files were modified


Workflow:

    Compromised System
          ↓
    Evidence Collection
          ↓
    Secure Rebuild
          ↓
    Patch
          ↓
    Harden
          ↓
    Restore
          ↓
    Validate


---

## 9. Persistence Removal

Persistence mechanisms allow attackers to regain access.

Investigate and remove:

- Scheduled tasks
- Services
- Startup items
- Registry run keys
- Cron jobs
- SSH keys
- Web shells
- Startup scripts
- Unauthorized accounts
- Cloud access keys
- API tokens


Example:

    Malware Removed
         ↓
    Persistence Remains
         ↓
    Attacker Returns
         ↓
    Reinfection


Therefore, malware removal alone is not sufficient.


---

## 10. Windows Persistence

Common areas to investigate include:

- Scheduled Tasks
- Services
- Registry Run Keys
- Startup folders
- PowerShell profiles
- WMI persistence
- Startup scripts
- Unauthorized local accounts


Example:

    Suspicious Service
          ↓
    Identify Binary
          ↓
    Validate
          ↓
    Disable
          ↓
    Remove
          ↓
    Verify


---

## 11. Linux Persistence

Common areas include:

- Cron jobs
- Systemd services
- Startup scripts
- SSH authorized keys
- Shell profiles
- User accounts
- SUID/SGID abuse
- Web shells


Example:

    Unauthorized SSH Key
          ↓
    Identify User
          ↓
    Validate Key
          ↓
    Remove
          ↓
    Reset Credentials
          ↓
    Monitor


---

## 12. Account Eradication

If an account is compromised:

- Reset password
- Revoke sessions
- Revoke tokens
- Revoke API keys
- Remove unauthorized MFA devices
- Remove unauthorized privileges
- Review group membership
- Review account activity


Example:

    Compromised Account
          ↓
    Credential Reset
          ↓
    Session Revocation
          ↓
    Token Revocation
          ↓
    Privilege Review
          ↓
    Monitoring


---

## 13. Credential Eradication

Credential compromise may extend beyond one user.

Investigate:

- User passwords
- Administrative passwords
- Service account credentials
- API keys
- Cloud access keys
- SSH keys
- Tokens
- Certificates


Credential rotation should prioritize accounts that may have been exposed during the incident.


---

## 14. Privilege Eradication

Remove unauthorized privileges.

Review:

- Administrator groups
- Domain groups
- IAM roles
- Cloud permissions
- Service permissions
- Database privileges
- Application roles


Example:

    Attacker
       ↓
    Unauthorized Privilege
       ↓
    Identify
       ↓
    Remove
       ↓
    Verify


---

## 15. Vulnerability Remediation

If a vulnerability was exploited:

    Identify Vulnerability
          ↓
    Determine Affected Systems
          ↓
    Patch
          ↓
    Test
          ↓
    Deploy
          ↓
    Verify


Other remediation options include:

- Configuration changes
- Workarounds
- Service removal
- Access restrictions
- Network segmentation
- Application upgrades


---

## 16. Misconfiguration Remediation

Security incidents may result from insecure configurations.

Examples:

- Public cloud storage
- Open firewall ports
- Weak authentication
- Excessive permissions
- Disabled security controls
- Insecure remote access
- Poor network segmentation


Eradication should correct the configuration that enabled the attack.


---

## 17. Web Shell Eradication

Web shells can provide persistent access to compromised servers.

Investigation may identify:

- Suspicious files
- Recently modified scripts
- Unexpected commands
- Unusual web requests
- Unknown administrator activity


Eradication should include:

    Identify Web Shell
          ↓
    Preserve Evidence
          ↓
    Remove
          ↓
    Identify Initial Vulnerability
          ↓
    Patch
          ↓
    Search Other Servers
          ↓
    Validate


---

## 18. Cloud Eradication

Cloud incidents may require:

- Revoking access keys
- Rotating credentials
- Removing unauthorized IAM users
- Removing unauthorized roles
- Removing persistence
- Correcting security groups
- Fixing storage permissions
- Removing malicious resources


Example:

    Compromised Cloud Account
          ↓
    Revoke Credentials
          ↓
    Remove Unauthorized Access
          ↓
    Remove Persistence
          ↓
    Correct Misconfiguration
          ↓
    Validate


---

## 19. Email Account Eradication

For compromised email accounts:

- Reset credentials
- Revoke sessions
- Remove malicious forwarding rules
- Remove unauthorized delegates
- Remove suspicious application access
- Review mailbox changes
- Investigate sent messages
- Revoke tokens


This helps prevent continued attacker access.


---

## 20. Ransomware Eradication

Ransomware eradication requires careful planning.

Potential activities:

- Identify affected systems
- Preserve evidence
- Remove malware
- Rebuild compromised systems
- Reset exposed credentials
- Patch exploited vulnerabilities
- Remove persistence
- Verify backups
- Search for additional infections


Example:

    Ransomware
       ↓
    Containment
       ↓
    Evidence Collection
       ↓
    Scope
       ↓
    Malware Removal / Rebuild
       ↓
    Credential Reset
       ↓
    Vulnerability Remediation
       ↓
    Validation


---

## 21. Lateral Movement Eradication

If lateral movement occurred:

- Identify compromised systems
- Identify reused credentials
- Reset exposed credentials
- Remove unauthorized remote access
- Review administrative accounts
- Patch exploited systems
- Search for persistence


Example:

    Host A
      ↓
    Credential Theft
      ↓
    Host B
      ↓
    Host C

Eradication must address the entire movement path.


---

## 22. Data Exfiltration Eradication

If data exfiltration occurred:

- Remove attacker access
- Revoke credentials
- Remove persistence
- Secure affected repositories
- Correct access controls
- Investigate affected data
- Review external connections


Eradication should focus on preventing continued access to sensitive data.


---

## 23. Endpoint Eradication

Endpoint eradication may include:

    Identify Compromise
          ↓
    Preserve Evidence
          ↓
    Remove Malware
          ↓
    Remove Persistence
          ↓
    Patch
          ↓
    Reset Credentials
          ↓
    Security Scan
          ↓
    Validate


For highly compromised endpoints, rebuilding may be preferred.


---

## 24. Server Eradication

Server eradication requires additional care because of service dependencies.

Consider:

- Application availability
- Database dependencies
- Network dependencies
- Backup availability
- Configuration backups
- Maintenance windows


Possible workflow:

    Contained Server
          ↓
    Evidence Collection
          ↓
    Service Assessment
          ↓
    Malware / Persistence Removal
          ↓
    Patch
          ↓
    Harden
          ↓
    Validate
          ↓
    Recovery


---

## 25. Database Eradication

For database-related incidents:

- Remove unauthorized accounts
- Reset credentials
- Revoke excessive permissions
- Remove malicious procedures
- Investigate unauthorized queries
- Patch database software
- Correct configuration


Example:

    Suspicious Database Access
          ↓
    Identify Account
          ↓
    Identify Queries
          ↓
    Review Privileges
          ↓
    Remove Unauthorized Access
          ↓
    Patch / Harden


---

## 26. Network Eradication

Network eradication may include:

- Remove unauthorized firewall rules
- Remove malicious routes
- Remove rogue devices
- Correct insecure configurations
- Remove unauthorized VPN access
- Update IDS/IPS rules
- Remove malicious infrastructure references


---

## 27. IoC Cleanup

After identifying IoCs:

- Remove malicious files
- Block malicious domains
- Block malicious IPs
- Remove malicious URLs
- Remove unauthorized accounts
- Remove persistence mechanisms


However, IoC removal should not be confused with complete eradication.

An attacker may have changed or hidden indicators.


---

## 28. Environment-Wide Eradication

A mature response does not clean only the first affected machine.

Workflow:

    Known IOC
       ↓
    Search SIEM
       ↓
    Search EDR
       ↓
    Search DNS
       ↓
    Search Email
       ↓
    Search Network
       ↓
    Identify All Affected Systems
       ↓
    Eradicate


---

## 29. Threat Hunting During Eradication

Threat hunting can identify missed attacker activity.

Search for:

- Known IoCs
- Similar process behavior
- Similar command lines
- Same persistence
- Same network connections
- Same account activity
- Similar file hashes


Example:

    Confirmed Compromise
          ↓
    Extract TTPs
          ↓
    Hunt Environment
          ↓
    Identify Additional Activity
          ↓
    Expand Eradication Scope


---

## 30. Eradication Validation

Eradication should be validated.

Questions include:

- Is malware gone?
- Is persistence gone?
- Are compromised credentials reset?
- Are unauthorized accounts removed?
- Are vulnerabilities fixed?
- Are malicious connections gone?
- Are unauthorized privileges removed?
- Are security controls working?


Example:

    Eradication
       ↓
    Scan
       ↓
    Search Logs
       ↓
    Search IoCs
       ↓
    Test Controls
       ↓
    No Malicious Activity
       ↓
    Eradication Confirmed


---

## 31. Post-Eradication Monitoring

After eradication, increased monitoring is useful.

Monitor:

- Authentication
- Network traffic
- Endpoint activity
- Privileged accounts
- IoCs
- Vulnerability status
- Security alerts


Example:

    Eradicated System
          ↓
    Enhanced Monitoring
          ↓
    No Recurrence
          ↓
    Recovery


---

## 32. Recovery Readiness

Before moving to recovery, confirm:

    Threat Removed
        +
    Persistence Removed
        +
    Credentials Protected
        +
    Vulnerability Fixed
        +
    Security Controls Validated
        ↓
    Recovery Ready


---

## 33. Eradication Documentation

Document:

    Incident ID
    Affected Systems
    Malware
    Persistence
    Compromised Accounts
    Vulnerabilities
    Root Cause
    Eradication Actions
    Evidence
    Validation
    Remaining Risks
    Recovery Recommendation


---

## 34. Eradication Checklist

    [ ] Review investigation findings
    [ ] Confirm incident scope
    [ ] Identify root cause
    [ ] Identify malware
    [ ] Identify persistence
    [ ] Identify compromised credentials
    [ ] Remove malware
    [ ] Remove persistence
    [ ] Remove unauthorized accounts
    [ ] Reset compromised credentials
    [ ] Revoke sessions and tokens
    [ ] Remove unauthorized privileges
    [ ] Patch exploited vulnerabilities
    [ ] Correct security misconfigurations
    [ ] Search environment for remaining IoCs
    [ ] Perform threat hunting
    [ ] Validate eradication
    [ ] Enable enhanced monitoring
    [ ] Document actions
    [ ] Confirm recovery readiness


---

## 35. Common Eradication Mistakes

### Mistake 1 — Removing Malware Without Finding Persistence

The attacker may return after reboot.

### Mistake 2 — Cleaning Only One Endpoint

Additional compromised systems may remain.

### Mistake 3 — Forgetting Credentials

The attacker may still possess valid credentials.

### Mistake 4 — Ignoring Root Cause

The same vulnerability may be exploited again.

### Mistake 5 — Skipping Validation

A system may appear clean while remaining compromised.

### Mistake 6 — Restoring Too Quickly

Recovery before complete eradication can lead to reinfection.

### Mistake 7 — Failing to Monitor

Residual attacker activity may remain undetected.


---

## 36. Automation in Eradication

Automation can assist with repetitive remediation tasks.

Examples:

- IOC searches
- Endpoint scanning
- Account disabling
- Credential rotation workflows
- Malware quarantine
- Vulnerability checks
- Configuration validation
- Compliance verification


Example:

    Incident
       ↓
    Automation
       ↓
    Identify Affected Hosts
       ↓
    Search IoCs
       ↓
    Generate Remediation List
       ↓
    Analyst Approval
       ↓
    Remediation
       ↓
    Validation


High-impact remediation should have appropriate approval and safeguards.


---

## 37. AI-Assisted Eradication

AI can assist with:

- Identifying likely persistence mechanisms
- Summarizing affected systems
- Prioritizing remediation
- Generating remediation checklists
- Analyzing configuration differences
- Creating documentation


Example:

    Investigation Data
          ↓
    AI Analysis
          ↓
    Potential Persistence
          ↓
    Analyst Validation
          ↓
    Remediation Plan
          ↓
    Authorized Action


AI should support analyst decision-making rather than independently making destructive changes.


---

## 38. Eradication Playbook Example

### Scenario

A Windows endpoint has confirmed malware and persistence.

### Findings

    Malicious File
        +
    Scheduled Task
        +
    Compromised User
        +
    Unpatched Application


### Eradication

    1. Preserve required evidence
    2. Remove malware
    3. Remove scheduled task
    4. Reset compromised credentials
    5. Patch vulnerable application
    6. Search environment for same IoCs
    7. Perform security scan
    8. Validate system


### Result

    Malware → Removed
    Persistence → Removed
    Credentials → Protected
    Vulnerability → Remediated
    Environment → Searched


---

## 39. Rebuild vs Clean

A decision should be made based on confidence in system integrity.

### Clean

May be appropriate when:

- Compromise is limited
- System integrity can be established
- Malware and persistence are well understood
- Cleaning can be reliably validated


### Rebuild

May be preferable when:

- Root-level compromise occurred
- System integrity is uncertain
- Persistence is extensive
- Critical components were modified
- Reliable eradication cannot be demonstrated


---

## 40. Professional Eradication Workflow

A mature process is:

    Incident Investigation
          ↓
    Root Cause
          ↓
    Scope
          ↓
    Persistence Identification
          ↓
    Credential Assessment
          ↓
    Remediation Plan
          ↓
    Evidence Preservation
          ↓
    Eradication
          ↓
    Validation
          ↓
    Threat Hunting
          ↓
    Enhanced Monitoring
          ↓
    Recovery


---

## 41. Key Takeaways

Effective eradication should:

- Remove the actual threat
- Remove persistence
- Protect credentials
- Correct vulnerabilities
- Fix misconfigurations
- Search the wider environment
- Validate remediation
- Monitor for recurrence
- Prepare systems for recovery


The key principle is:

> **Do not declare eradication complete until there is sufficient evidence that the attacker can no longer maintain or regain access through the identified compromise path.**


---

## 42. Final Eradication Model

The complete eradication model is:

    Investigate
       ↓
    Identify Root Cause
       ↓
    Identify Persistence
       ↓
    Identify Credentials
       ↓
    Preserve Evidence
       ↓
    Remove Malware
       ↓
    Remove Persistence
       ↓
    Reset Credentials
       ↓
    Patch / Harden
       ↓
    Search Environment
       ↓
    Validate
       ↓
    Monitor
       ↓
    Recovery


---

## 43. Conclusion

Incident Eradication removes the technical and access mechanisms that allow an attacker to continue operating.

A professional eradication process goes beyond deleting malware.

It addresses:

    Malware
      +
    Persistence
      +
    Credentials
      +
    Privileges
      +
    Vulnerabilities
      +
    Misconfigurations
      +
    Root Cause
      ↓
    Complete Eradication


The ultimate objective is to return the environment to a trusted state where the threat has been removed, the attack path has been addressed, and the organization is ready to safely begin recovery.
