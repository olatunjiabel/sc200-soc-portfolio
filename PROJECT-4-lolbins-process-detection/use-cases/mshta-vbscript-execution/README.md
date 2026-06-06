# MSHTA VBScript Execution (LOLBIN Abuse)

##  Attack Simulation
A simulated attack was performed using `mshta.exe` to execute a VBScript payload.

The VBScript used in this simulation displayed a simple message box (`msgbox Test`) to confirm execution. This demonstrates how attackers can abuse legitimate Windows binaries (LOLBins) to execute scripts.

VBScript is executed via `mshta.exe`, a trusted Windows binary commonly abused for script execution.

In a real-world scenario, an attacker could replace this script with a malicious payload to download malware, execute commands, or establish persistence.

---

##  Log Source
- Sysmon (Event ID 1 – Process Creation)

---

##  Detection (KQL Query)

Detection was performed using a targeted KQL query to identify `mshta.exe` executing VBScript from Sysmon logs.

➡️ [View Detection Query](../queries/mshta-vbscript-detection.kql)

```kql
Event
| where Source == "Microsoft-Windows-Sysmon"
| where EventID == 1
| parse EventData with * '<Data Name="CommandLine">' CommandLine '</Data>' *
| parse EventData with * '<Data Name="Image">' Image '</Data>' *
| where Image endswith "mshta.exe"
| where CommandLine has "vbscript"
| project TimeGenerated, Computer, Image, CommandLine
| order by TimeGenerated desc
```

---

###  Detection Result
![MSHTA Detection](../screenshots/mshta-vbscript-detection.png)


---

##  Investigation

- Sysmon logs confirmed execution of `mshta.exe` on the endpoint  
- The command line revealed:

  `"C:\Windows\System32\mshta.exe" vbscript:msgbox Test`

- This confirms that `mshta.exe` executed a VBScript payload  

- Although the script only displayed a message box, this behavior is not typical for normal user activity  

- Analysis highlights:
  - Use of a trusted Windows binary (`mshta.exe`)  
  - Execution of inline VBScript  
  - Potential for fileless or script-based attacks  

- Key insight:  
  This represents a **Living-off-the-Land (LOLBIN)** technique where legitimate tools are abused to evade detection  

- In real-world attacks, this technique can be used to:
  - Execute malicious scripts  
  - Download payloads  
  - Bypass security controls  

---

###  Process Execution Evidence
![MSHTA CommandLine](../screenshots/mshta-vbscript-commandline.png)

---

##  SOC Workflow

**1. Detection**  
- Suspicious execution identified via KQL query  

**2. Triage**  
- Verified affected host and timestamp  

**3. Investigation**  
- Analyzed process command line  
- Confirmed VBScript execution via mshta  

**4. Containment**  
- Isolated endpoint (if malicious)  
- Terminated mshta process  

**5. Remediation**  
- Removed malicious scripts or artifacts  
- Performed antivirus scan  

**6. Recovery**  
- Restored system and monitored for further activity  

**7. Reporting**  
- Documented findings and response actions  

---

##  Response Actions
- Device isolation  
- Process termination  
- Blocking suspicious scripts or execution methods  
- Full endpoint malware scan  

---

##  MITRE ATT&CK Mapping

- Technique: **T1218.005 – Mshta**  
- Tactic: **Defense Evasion / Execution**  

This technique involves abuse of a trusted Windows binary (`mshta.exe`) to execute scripts and evade detection.
