# PROJECT 4 – LOLBins Process Detection (Suspicious Malware Execution)

##  Overview
This project focuses on detecting and investigating the abuse of **Living-off-the-Land Binaries (LOLBins)** for malicious execution.

LOLBins are legitimate Windows binaries that attackers abuse to execute payloads, evade detection, and perform fileless attacks.

The goal of this project is to simulate real-world attack techniques, detect them using **Sysmon + Microsoft Sentinel (KQL)**, and investigate the activity like a SOC analyst.

---

##  Objectives
- Simulate LOLBins-based attack techniques  
- Detect suspicious process execution using Sysmon logs  
- Analyze command-line behavior  
- Investigate and validate suspicious activity  
- Map activity to MITRE ATT&CK  

---

##  Initial Setup – Sysmon Deployment & Verification

###  Objective
Install Sysmon on a Windows machine and configure it to capture detailed process activity.  
Also verify that logs are successfully sent to Microsoft Sentinel (Log Analytics Workspace).

---

###  Activity Performed
- Installed Sysmon on the Windows endpoint  
- Configured it to capture **process creation events (Event ID 1)**  
- Verified logs were flowing into Microsoft Sentinel  
- Confirmed visibility of events in Log Analytics  

---

###  Why Sysmon Was Used
Sysmon was installed because it provides more detailed visibility than normal Windows logs.

It shows:
- What process was executed  
- How it was executed (command line)  
- What triggered it (parent process)  

---

###  Importance for Detection & Investigation

Without Sysmon:
- You only know that a file was opened or executed  

With Sysmon:
- You can see what exactly ran  
- What command was used  
- What triggered the execution  

This makes it much easier to investigate suspicious or malicious activity.

---

###  Outcome
Sysmon provided the visibility needed to:
- Detect suspicious process execution  
- Investigate LOLBins abuse  
- Perform analysis using Microsoft Sentinel  

---

##  Tools Used
- Microsoft Sentinel  
- Sysmon  
- KQL (Kusto Query Language)  
- Windows Virtual Machine  

---

##  Attack Simulations

### 1. MSHTA – VBScript Execution
- Abuse of `mshta.exe` to execute VBScript  
- Demonstrates fileless script execution  

➡️ [View Use Case](use-cases/mshta-vbscript-execution/README.md)

---

### 2. PowerShell – Encoded Command Execution
- Use of `powershell.exe` with encoded commands  
- Common attacker technique for obfuscation  

➡️ [View Use Case](use-cases/powershell-encoded-command/README.md)

---

### 3. Certutil – LOLBin Abuse 
- Abuse of `certutil.exe` to download or decode payloads  
- Often used by attackers for file transfer and evasion  

➡️ [View Use Case](use-cases/certutil-encoded-command/README.md)

---

##  Detection Approach
Detection was performed using **KQL queries on Sysmon logs**, focusing on:

- Suspicious process execution  
- Command-line anomalies  
- Abuse of trusted Windows binaries  

Each use case includes:
- Detection query  
- Investigation analysis  
- Evidence screenshots  

---

##  SOC Workflow Applied
Each scenario follows a real SOC workflow:

1. Detection  
2. Triage  
3. Investigation  
4. Containment  
5. Remediation  
6. Recovery  
7. Reporting  

---

##  MITRE ATT&CK Mapping

| Technique | Description |
|----------|------------|
| T1218.005 | Mshta |
| T1059.001 | PowerShell |
| T1105 | Ingress Tool Transfer (Certutil) |

---

##  Project Structure

```
PROJECT-4-lolbins-process-detection/
│
├── use-cases/
│   ├── mshta-vbscript-execution/
│   ├── powershell-encoded-command/
│   └── certutil-abuse/
│
├── queries/
│
└── screenshots/
```

---

##  Key Takeaways
- Attackers abuse legitimate tools to evade detection  
- Command-line analysis is critical for detection  
- Sysmon provides deep visibility into system activity  
- KQL enables efficient investigation and threat hunting  

---

##  Status
- MSHTA Detection ✅  
- PowerShell Detection ✅  
- Certutil Simulation ✅  

---


