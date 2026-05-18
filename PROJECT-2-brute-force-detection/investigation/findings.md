# Investigation Findings – Project 2: False Positive Analysis

## 📊 What I Found

| Field | Value |
|---|---|
| Account | Administrator |
| Source IP | 127.0.0.1 |
| Logon Type | 7 |
| Failed Attempts | 7 |
| Time Window | < 10 minutes |

---

## 🧩 Investigation & Triage Process

**Step 1 - Alert fired**
Analytics rule triggered after 3+ failed logins detected within 10 minutes.

**Step 2 - Checked source IP**
Source IP was 127.0.0.1 local host loopback address which insinuates that the failed attempts originated from the machine itself, not an external attacker. A real brute force would show an external IP.

**Step 3 - Checked LogonType**
LogonType 7 indicates a workstation unlock attempt. A real brute force attack would show LogonType 3 (network) or LogonType 10 (RDP), not LogonType 7.

**Step 4 - Concluded false positive**
The combination of these findings made me come to the conclusion that it was just the user entering an incorrect password while unlocking their machine.

---

## 🔍 Detailed Analysis

After thorough investigation I was able to discover that the alert was a false positive because the logon type 7 is a session unlock logon. A logon type 10 would have been more suspicious which is RDP. The source IP was 127.0.0.1 local host loopback address which insinuates that the failed attempts originated from the machine itself. The combination of these findings made me come to the conclusion that it was just the user entering an incorrect password while unlocking their machine.

---

## 📸 Evidence

Screenshots of the following are included in the `/screenshots` folder:

 ![Alert Triggered](../screenshots/Alert-triggered.png) (shows alert,logontype,Account,Failedattempts)
 ![Event Log](../screenshots/Event-log.png) (shows KQL rule is usable for analytics rule)

