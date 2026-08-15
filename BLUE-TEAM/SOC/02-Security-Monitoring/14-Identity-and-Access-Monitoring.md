# Identity and Access Monitoring

## 1. Introduction

Identity and Access Monitoring is the process of collecting, analyzing, and correlating authentication, authorization, account, privilege, and access-related telemetry to detect unauthorized access, credential compromise, privilege abuse, account takeover, and other identity-based threats.

Identity is one of the most important security monitoring areas because attackers frequently target user accounts before attempting to compromise systems or data.

A typical identity monitoring flow is:

```text
User
  ↓
Authentication
  ↓
Identity Provider / Active Directory
  ↓
Authorization
  ↓
Resource Access
  ↓
Logs
  ↓
SIEM
  ↓
SOC Analyst
