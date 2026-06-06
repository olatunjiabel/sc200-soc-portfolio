# Project 2: False Positive Analysis - Brute Force Detection

##  Incident Summary

| Field | Details |
|---|---|
| Analyst | Olatunji Abel |
| Date | March 2025 |
| Platform | Microsoft Sentinel |
| Event ID | 4625 (Failed Logon) |
| Source IP | 127.0.0.1 |
| Logon Type | 7 (Workstation Unlock) |
| Verdict | False Positive |
| Severity | Informational |

---

##  Overview

In this project I simulated multiple failed login attempts on a Windows machine and used Microsoft Sentinel to detect and investigate the activity.

The goal was to determine whether the behavior represented a real brute force attack or normal user activity, a critical SOC skill for Identifying False Positives

---
##  What Happened

I intentionally entered incorrect passwords multiple times while trying to unlock my Windows VM. This generated several failed login events (Event ID 4625), which were ingested into Microsoft Sentinel and triggered an analytics rule.

---

##  MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Credential Access | Brute Force | T1110 |
| Credential Access | Password Guessing | T1110.001 |

> Note: These techniques describe what the alert appeared to be. Investigation confirmed this was NOT malicious activity.

---
##  Detection Query (KQL)

```kql
SecurityEvent
| where TimeGenerated >= ago(10m)
| where EventID == 4625
| summarize FailedAttempts = count() by 
    IpAddress, 
    Account, 
    LogonType
| where FailedAttempts >= 3
| sort by FailedAttempts desc
```

**What this query does:**
- Looks for accounts with 3+ failed logins within 10 minutes
- it displays the EventID which showed 4625 as failure
- count all failed attempts and project its IP,Account, and Logontype
- Returns result where Failed attempts is greater than or equal to 3
  
---

##  Conclusion

**Verdict: False Positive**

This was not a real brute force attack. The alert was triggered by a user repeatedly entering the wrong password during a workstation unlock.

This taught me that not every alert needs to be escalated. Understanding  what triggered the alert behind the alert fired  is what matters.

**Key lesson:** Always check LogonType and source IP before classifying a failed login alert as malicious.

---

##  Tools Used

- Microsoft Sentinel
- Log Analytics Workspace
- Windows Security Event Logs (Event ID 4625)

---

##  Project Structure

- `/screenshots` — Sentinel incident, query results, event logs
- `/queries` — KQL detection query
- `/analytics-rule` — Rule configuration
- `/attack-simulation` — Simulation steps
- `/investigation` — Full investigation findings and triage details

👉 [View Full Investigation Details](investigation/findings.md)
