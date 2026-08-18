# Incident Containment

## 1. Introduction

Incident Containment is the process of limiting the spread, impact, and persistence of a cybersecurity incident while preserving the organization's ability to investigate and recover.

Containment is performed after an incident has been identified and sufficiently investigated.

The primary objective is:

> Stop the attacker from causing additional damage while maintaining enough evidence and business continuity to support the investigation.

The basic workflow is:

    Detection
       ↓
    Triage
       ↓
    Investigation
       ↓
    Incident Confirmation
       ↓
    Containment
       ↓
    Eradication
       ↓
    Recovery


---

## 2. Objectives of Containment

The main objectives are to:

- Stop ongoing malicious activity
- Prevent further compromise
- Limit lateral movement
- Protect critical systems
- Protect sensitive data
- Prevent additional unauthorized access
- Preserve important evidence
- Reduce business impact
- Prepare the environment for eradication and recovery


---

## 3. Why Containment Matters

Without containment, an attacker may continue to:

- Execute commands
- Steal credentials
- Move laterally
- Establish persistence
- Access sensitive systems
- Exfiltrate data
- Deploy malware
- Disrupt business services

Example:

    Compromised Endpoint
           ↓
    Attacker Access
           ↓
    Lateral Movement
           ↓
    Additional Hosts
           ↓
    Data Access
           ↓
    Larger Incident

Containment attempts to break this chain as early as possible.


---

## 4. Containment vs Eradication

These two activities are different.

### Containment

Stops or limits the attack.

Example:

    Isolate compromised endpoint

### Eradication

Removes the underlying threat.

Example:

    Remove malware and persistence

Therefore:

    Containment
        ↓
    Stop the Threat
        ↓
    Eradication
        ↓
    Remove the Threat


---

## 5. Containment Strategy

A containment strategy should consider:

- Incident severity
- Asset criticality
- Scope
- Attacker activity
- Business impact
- Evidence preservation
- Availability requirements
- Regulatory requirements
- Recovery options


Example:

    Critical Server
         ↓
    Immediate Isolation?
         ↓
    Business Impact Assessment
         ↓
    Controlled Containment


Containment should be proportional to the risk.


---

## 6. Short-Term Containment

Short-term containment focuses on immediately limiting the attack.

Examples:

- Isolate endpoint
- Disable compromised account
- Block malicious IP
- Block malicious domain
- Terminate malicious process
- Disable compromised credentials
- Block malicious email
- Revoke active sessions


Workflow:

    Active Threat
        ↓
    Immediate Action
        ↓
    Limit Attacker Access
        ↓
    Prevent Further Damage


---

## 7. Long-Term Containment

Long-term containment provides a more stable environment for investigation and remediation.

Examples:

- Network segmentation
- Temporary firewall rules
- Temporary account restrictions
- Application isolation
- Increased monitoring
- Temporary access restrictions
- Moving critical workloads to protected infrastructure


Short-term containment stops immediate activity.

Long-term containment reduces the chance of continued compromise while eradication is performed.


---

## 8. Endpoint Isolation

Endpoint isolation is one of the most common containment actions.

Example:

    Compromised Endpoint
          ↓
    EDR Isolation
          ↓
    Network Access Restricted
          ↓
    Attacker Communication Limited
          ↓
    Investigation Continues


The endpoint may still remain accessible to security tools depending on the isolation mechanism.


---

## 9. Account Containment

If an account is suspected to be compromised:

- Disable account
- Reset password
- Revoke sessions
- Revoke tokens
- Revoke API keys
- Remove unauthorized MFA devices
- Review privilege assignments


Example:

    Compromised Account
          ↓
    Disable / Restrict
          ↓
    Revoke Sessions
          ↓
    Reset Credentials
          ↓
    Investigate


Credential changes should be coordinated carefully to avoid disrupting legitimate services.


---

## 10. Network Containment

Network containment may involve:

- Firewall blocks
- ACL changes
- VLAN isolation
- Network segmentation
- Proxy blocking
- DNS blocking
- Egress filtering


Example:

    Malicious Destination
          ↓
    Firewall Rule
          ↓
    Connection Blocked


---

## 11. IP Blocking

A malicious IP can be blocked at appropriate security controls.

Example:

    Internal Host
          ↓
    Malicious IP
          ↓
    Firewall
          ↓
    BLOCK


Before blocking, validate:

- Reputation
- Ownership
- Business relevance
- Historical activity
- Whether multiple systems depend on the address


Avoid blindly blocking shared infrastructure.


---

## 12. Domain Blocking

Malicious domains can be blocked through:

- DNS security
- Secure web gateway
- Firewall
- Proxy
- Endpoint security
- Email security


Example:

    Malicious Domain
          ↓
    DNS Security
          ↓
    Query Blocked


Domain blocking should be combined with endpoint investigation.


---

## 13. Process Containment

A malicious process may be terminated when appropriate.

Example:

    Malicious Process
          ↓
    Identify PID
          ↓
    Validate Activity
          ↓
    Terminate Process
          ↓
    Monitor


Process termination should be performed carefully because it can destroy volatile evidence or trigger attacker behavior.


---

## 14. Malware Containment

For malware incidents:

    Malware Detected
          ↓
    Isolate Endpoint
          ↓
    Block IoCs
          ↓
    Stop Malicious Activity
          ↓
    Search Environment
          ↓
    Identify Additional Hosts


The objective is to prevent malware from spreading while preparing for eradication.


---

## 15. Phishing Containment

Phishing containment may include:

- Remove malicious emails
- Block sender
- Block malicious domain
- Block URLs
- Quarantine attachments
- Reset compromised credentials
- Revoke sessions
- Investigate affected endpoints


Workflow:

    Phishing Email
          ↓
    Identify Recipients
          ↓
    Remove Email
          ↓
    Block IoCs
          ↓
    Investigate Users
          ↓
    Protect Accounts


---

## 16. Ransomware Containment

Ransomware requires rapid containment.

Possible actions:

- Isolate affected endpoints
- Disable compromised accounts
- Block malicious communication
- Segment affected network areas
- Protect backups
- Prevent further file encryption
- Identify additional affected systems


Example:

    Ransomware Detection
          ↓
    Endpoint Isolation
          ↓
    Network Segmentation
          ↓
    Account Protection
          ↓
    Backup Protection
          ↓
    Scope Assessment


Do not assume that the first infected system is the only affected system.


---

## 17. Lateral Movement Containment

If lateral movement is suspected:

- Isolate affected systems
- Restrict remote administration
- Protect privileged accounts
- Reset compromised credentials
- Block suspicious source/destination paths
- Increase authentication monitoring


Example:

    Host A
       ↓
    Stolen Credential
       ↓
    Host B
       ↓
    Host C

Containment should attempt to break the movement path.


---

## 18. Data Exfiltration Containment

When data exfiltration is suspected:

- Block destination
- Restrict outbound communication
- Isolate affected endpoint
- Disable compromised account
- Protect sensitive repositories
- Preserve network evidence
- Identify affected data


Example:

    Sensitive Data
          ↓
    Unauthorized Transfer
          ↓
    Destination Block
          ↓
    Endpoint Isolation
          ↓
    Investigation


---

## 19. Cloud Containment

Cloud containment may involve:

- Disable compromised identity
- Revoke access keys
- Revoke sessions
- Remove unauthorized permissions
- Restrict security groups
- Block suspicious IPs
- Protect affected resources
- Increase audit monitoring


Example:

    Compromised Cloud Identity
          ↓
    Revoke Credentials
          ↓
    Revoke Sessions
          ↓
    Remove Unauthorized Access
          ↓
    Investigate


---

## 20. Email Account Containment

For a compromised mailbox:

- Reset password
- Revoke sessions
- Revoke tokens
- Remove malicious forwarding rules
- Remove unauthorized delegates
- Check sent messages
- Check mailbox access
- Investigate related accounts


Example:

    Compromised Mailbox
          ↓
    Session Revocation
          ↓
    Rule Removal
          ↓
    Credential Reset
          ↓
    Email Investigation


---

## 21. Privileged Account Containment

Privileged account compromise should receive high priority.

Possible actions:

- Disable account temporarily
- Revoke sessions
- Reset credentials
- Remove unauthorized privilege
- Review administrative activity
- Investigate other privileged accounts


Example:

    Domain Admin Compromise
           ↓
    Immediate Containment
           ↓
    Credential Protection
           ↓
    Privilege Review
           ↓
    Environment-Wide Search


---

## 22. Network Segmentation

Segmentation can limit attacker movement.

Example:

    Corporate Network
          ↓
    Security Boundary
          ↓
    Critical Systems

If one segment is compromised:

    Compromised Segment
          X
    Critical Segment


Segmentation is particularly important for protecting:

- Domain controllers
- Databases
- Production servers
- Backup systems
- Security infrastructure


---

## 23. Protecting Backup Infrastructure

During destructive incidents such as ransomware, backup systems are critical.

Containment should consider:

- Backup credentials
- Backup servers
- Backup repositories
- Backup connectivity
- Immutable backups
- Offline backups


Example:

    Ransomware
        ↓
    Production Systems
        ↓
    Backup Infrastructure
        ↓
    Protect Immediately


An attacker who compromises backups may significantly increase the impact of an incident.


---

## 24. Evidence Preservation During Containment

Containment can alter the environment.

Potentially affected evidence includes:

- Running processes
- Network connections
- Memory
- Temporary files
- Active sessions
- Logs


Therefore, before destructive containment actions, consider whether volatile evidence should be captured.

Example:

    Suspicious Host
          ↓
    Evidence Assessment
          ↓
    Volatile Evidence?
          ↓
    Capture if Required
          ↓
    Containment


The correct approach depends on incident severity, organizational procedures, and forensic requirements.


---

## 25. Volatile Evidence

Volatile evidence may disappear when a system is shut down.

Examples:

- Running processes
- Active network connections
- Logged-in users
- Memory
- Temporary data
- Active sessions


A security team should determine whether collecting such evidence is necessary before shutting down or isolating a system.


---

## 26. Containment Decision Matrix

A practical decision model:

| Situation | Possible Containment |
|---|---|
| Malware on endpoint | Endpoint isolation |
| Compromised user | Disable account / revoke sessions |
| Malicious IP | Firewall block |
| Malicious domain | DNS / proxy block |
| Ransomware | Isolation + segmentation |
| Data exfiltration | Egress restriction |
| Cloud account compromise | Revoke credentials |
| Privileged account compromise | Immediate privilege protection |
| Phishing | Remove email + block IoCs |
| Lateral movement | Network restriction + credential protection |

Actions should always be adapted to the environment.


---

## 27. Containment Priority

A useful prioritization model is:

    Threat Severity
          +
    Asset Criticality
          +
    Attacker Activity
          +
    Business Impact
          +
    Scope
          ↓
    Containment Priority


Example:

    Critical Server
        +
    Active Attacker
        +
    Data Exfiltration
        ↓
    Immediate Containment


---

## 28. Business Impact Considerations

Containment can affect business operations.

Before major actions, consider:

- Production impact
- Service availability
- Customer impact
- Critical dependencies
- Regulatory requirements
- Safety implications
- Recovery requirements


Example:

    Isolate Production Server?
           ↓
    Security Risk
           +
    Business Impact
           ↓
    Incident Commander Decision


Emergency actions may still be necessary when the risk of continued compromise is greater than the operational impact.


---

## 29. Containment Authorization

Depending on organizational procedures, actions may require approval.

Potential decision-makers include:

- SOC Analyst
- Incident Responder
- Security Lead
- Incident Commander
- IT Operations
- System Owner
- Management


Clearly defined authorization prevents confusion during high-pressure incidents.


---

## 30. Containment Communication

Important containment actions should be communicated to relevant teams.

Example:

    Security Team
         ↓
    Incident Lead
         ↓
    IT Operations
         ↓
    System Owner
         ↓
    Management


Communication should include:

- What happened
- What was contained
- Why it was contained
- Expected impact
- Required actions
- Next steps


---

## 31. Containment Documentation

Record:

    Incident ID
    Date / Time
    Analyst
    Action
    System
    User
    Reason
    Authorization
    Evidence
    Result
    Business Impact
    Next Step


Example:

    14:20
    Host: WIN-CLIENT01
    Action: Endpoint isolated
    Reason: Confirmed malware activity
    Result: External communication stopped
    Next Step: Malware eradication


---

## 32. Containment Verification

After containment, verify that the action worked.

Example:

    Firewall Block
         ↓
    Test Connection
         ↓
    Connection Failed
         ↓
    Verify SIEM Logs
         ↓
    No Further Communication
         ↓
    Containment Confirmed


Containment should not be assumed to be successful without validation.


---

## 33. Environment-Wide IOC Search

After containing the initial system, search for the same indicators across the environment.

Example:

    Known Malicious Hash
          ↓
    Search EDR
          ↓
    Search SIEM
          ↓
    Search Email
          ↓
    Search DNS
          ↓
    Search Proxy
          ↓
    Identify Additional Hosts


This prevents containment from being limited to the first detected system.


---

## 34. Containment Validation

A successful containment should answer:

- Is the attacker still connected?
- Are malicious processes still running?
- Are malicious destinations still reachable?
- Can compromised credentials still authenticate?
- Has lateral movement stopped?
- Has data transfer stopped?
- Are additional systems affected?


---

## 35. Common Containment Mistakes

### Mistake 1 — Isolating Only the First Host

The attacker may already have compromised additional systems.

### Mistake 2 — Blocking Only One IOC

Attackers may use multiple domains, IPs, or infrastructure.

### Mistake 3 — Ignoring Credentials

Network containment does not remove stolen credentials.

### Mistake 4 — Destroying Evidence

Immediate destructive actions may remove valuable forensic evidence.

### Mistake 5 — Ignoring Business Impact

Poorly planned containment can create unnecessary operational disruption.

### Mistake 6 — Failing to Verify

A containment action should be validated.

### Mistake 7 — Not Documenting Actions

Unrecorded actions make investigation and auditing difficult.


---

## 36. Automation in Containment

Automation can execute predefined containment actions.

Example:

    High-Confidence Alert
          ↓
    Automation
          ↓
    Extract IOC
          ↓
    Validate
          ↓
    Isolate Endpoint
          ↓
    Block IOC
          ↓
    Create Ticket
          ↓
    Notify Analyst


Automation should be carefully controlled, especially for destructive or business-critical actions.


---

## 37. SOAR-Based Containment

A SOAR workflow can coordinate multiple actions.

Example:

    SIEM Alert
        ↓
    SOAR
        ↓
    Threat Intelligence
        ↓
    Risk Assessment
        ↓
    EDR Isolation
        ↓
    Firewall Block
        ↓
    Ticket Creation
        ↓
    Analyst Notification


This reduces response time and improves consistency.


---

## 38. AI-Assisted Containment

AI can assist with:

- Summarizing incident evidence
- Recommending containment actions
- Identifying affected systems
- Prioritizing containment
- Generating response checklists
- Explaining potential business impact


Example:

    Incident Data
         ↓
    AI Analysis
         ↓
    Suggested Containment
         ↓
    Human Validation
         ↓
    Authorized Action


AI should not independently perform high-impact containment without appropriate controls and authorization.


---

## 39. Containment Playbook Example

### Scenario

A Windows endpoint is confirmed to be communicating with malicious infrastructure.

### Detection

    EDR Alert
         ↓
    Suspicious Network Connection


### Investigation

    Process
      ↓
    Network Connection
      ↓
    IOC Reputation
      ↓
    Malicious Destination


### Containment

    1. Isolate endpoint
    2. Block malicious destination
    3. Preserve relevant evidence
    4. Search environment for IOC
    5. Investigate user account
    6. Monitor for additional activity


### Validation

    Endpoint Isolation → Confirmed
    IOC Block → Confirmed
    Additional Hosts → Investigated


---

## 40. Ransomware Containment Example

### Detection

    Multiple File Encryption Events
             ↓
    Ransomware Alert


### Immediate Containment

    Affected Endpoint
          ↓
    Isolate
          ↓
    Identify Other Affected Hosts
          ↓
    Segment Network
          ↓
    Protect Backups
          ↓
    Protect Privileged Accounts


### Follow-Up

    Scope Investigation
          ↓
    Evidence Collection
          ↓
    Eradication Planning


---

## 41. Account Compromise Containment Example

### Detection

    Suspicious Authentication
          ↓
    Account Compromise Suspected


### Containment

    Disable / Restrict Account
          ↓
    Revoke Sessions
          ↓
    Reset Credentials
          ↓
    Revoke Tokens
          ↓
    Review MFA
          ↓
    Investigate Access


### Validation

    Active Sessions Removed
          ↓
    New Authentication Controlled
          ↓
    Suspicious Activity Reduced


---

## 42. Containment Checklist

    [ ] Confirm incident
    [ ] Determine scope
    [ ] Identify affected assets
    [ ] Identify affected accounts
    [ ] Assess business impact
    [ ] Determine containment priority
    [ ] Preserve required evidence
    [ ] Isolate affected systems
    [ ] Protect compromised accounts
    [ ] Block malicious infrastructure
    [ ] Restrict lateral movement
    [ ] Protect critical systems
    [ ] Protect backups
    [ ] Search environment for IoCs
    [ ] Verify containment
    [ ] Document actions
    [ ] Communicate with relevant teams
    [ ] Prepare for eradication


---

## 43. Professional Containment Workflow

A mature containment process is:

    Incident Confirmation
          ↓
    Scope Assessment
          ↓
    Risk Assessment
          ↓
    Evidence Preservation
          ↓
    Containment Decision
          ↓
    Authorization
          ↓
    Execute Containment
          ↓
    Verify Action
          ↓
    Environment-Wide IOC Search
          ↓
    Monitor
          ↓
    Eradication


---

## 44. Key Takeaways

Effective containment should:

- Stop active threats
- Limit attacker movement
- Protect critical assets
- Protect credentials
- Protect sensitive data
- Preserve important evidence
- Minimize business disruption
- Be documented
- Be verified
- Prepare the environment for eradication


The key principle is:

> **Contain the threat without unnecessarily destroying evidence or causing avoidable business disruption.**


---

## 45. Final Containment Model

The complete containment model is:

    Detect
      ↓
    Confirm
      ↓
    Scope
      ↓
    Assess Risk
      ↓
    Preserve Evidence
      ↓
    Choose Containment
      ↓
    Authorize
      ↓
    Execute
      ↓
    Verify
      ↓
    Search Environment
      ↓
    Monitor
      ↓
    Eradicate


---

## 46. Conclusion

Incident containment is the critical transition between investigation and eradication.

A professional security team must balance:

    Security Risk
         +
    Evidence Preservation
         +
    Business Continuity
         +
    Response Speed
         ↓
    Containment Decision


The ultimate objective is to prevent the attacker from causing additional damage while creating a controlled environment in which the threat can be fully removed.

Effective containment therefore requires a combination of **technical controls, incident response procedures, evidence awareness, business context, automation, and human decision-making**.
