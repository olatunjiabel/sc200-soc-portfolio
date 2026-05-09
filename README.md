# 🛡️ Microsoft Sentinel SOC Lab – Security Operations Portfolio

## 🧑‍💻 About Me

Hi, my name is **Olatunji Olubi Abel**.

This portfolio showcases hands-on cybersecurity projects aligned with the **Microsoft SC-200 (Security Operations Analyst)** certification.

It documents my journey toward becoming a **SOC Analyst**, with a strong focus on practical, real-world security operations.

---

## 🎯 Skills Demonstrated

- 🔍 Security Monitoring  
- 🛠️ Detection Engineering  
- 🚨 Security Incident Investigation  
- 🧠 Threat Analysis  
- 📊 Log Analysis  
- ☁️ Microsoft Security Tools  

---

## 🛠️ Tools & Technologies

- **Microsoft Sentinel** (SIEM)  
- **KQL (Kusto Query Language)**  
- **Azure Active Directory (Entra ID)**  
- **Microsoft Defender**  
- **Log Analytics Workspace**  
- **Analytics Rules**  
- **Azure Arc** (Hybrid Environment)  
- **Windows Security Events & Sysmon**
- **Microsoft defender for endpoints**
- **Microsoft defender XDR**
---

## 📂 Portfolio Projects

### 🔹 Project 0: SOC Environment Setup

Foundational project where I built a complete SOC lab environment from scratch.

**What I Did:**
- Configured Microsoft Entra ID (Azure AD) tenant  
- Created Log Analytics Workspace  
- Deployed Microsoft Sentinel (SIEM)  
- Connected Windows Server via Azure Arc  
- Set up data ingestion pipelines  

**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-0-soc-enviroment-setup/README.md)

---

### 🔹 Project 1: Azure AD Brute Force Detection

Detection engineering project using cloud authentication logs.

**What I Did:**
- Analyzed Azure AD sign-in logs for failed authentication patterns  
- Wrote KQL queries to identify suspicious activity  
- Created analytics rule: alert on **10+ failures from same IP within 1 hour**  
- Tested detection using simulated attacks  

**Key Findings:**
- Multiple failed login attempts within a short time window  
- Identified source IP and targeted user account  
- Confirmed brute force attack pattern  

**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-1-detection-engineering/README.md)

---

### 🔹 Project 2: False Positive - Brute Force Detection

Focused on distinguishing real threats from false positives.

**What I Did:**
- Generated failed login events on a Windows workstation  
- Alert triggered for 8+ failed attempts  
- Investigated to validate the alert  

**Investigation Findings:**
- Source: `127.0.0.1` (localhost, not external attacker)  
- Activity: Workstation unlock attempts (**LogonType 7**)  
- Conclusion: User error (incorrect password), not malicious activity  

**Lesson Learned:**
- Not all alerts are real threats  
- Context and investigation are critical in SOC workflows  
- Understanding log data reduces alert fatigue  

**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-2-brute-force-detection/README.md)

---

### 🔹 Project 3: RDP Brute Force Detection & Investigation

Simulated a real-world attack involving multiple failed RDP logins followed by a successful compromise.

**What I Did:**
- Simulated 10+ failed RDP login attempts  
- Successfully logged in after failed attempts  
- Generated Windows Security Events (`4625`, `4624`)  
- Built analytics rule to detect attack pattern  
- Investigated incident using Microsoft Sentinel  

**Key Findings:**
- Failed attempts: **LogonType 3** (network authentication)  
- Successful login: **LogonType 10** (RDP session)  
- Same IP and user account across events  
- Attack occurred within a short time window  

**Outcome:**
- Detection rule successfully triggered  
- Incident created and analyzed in Sentinel  
- Full attack chain visibility achieved  

**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-3-RDP-brute-force-detection/README.md)

---

### 🔹 Project 4: LOLBIN Process Abuse Detection & Investigation

I simulated real-world attacks using different Windows LOLBINs (Living-off-the-Land Binaries) to execute encoded and obfuscated commands, just like how attackers try to hide their activity.

---

### What I Did:
- Simulated attacks using multiple LOLBINs:
  - Certutil (encode, decode, download)
  - PowerShell (encoded commands)
  - MSHTA (script execution)  
- Ran encoded and obfuscated commands to mimic attacker behavior  
- Generated Sysmon logs (Event ID 1 – Process Creation)  
- Wrote KQL detection queries for each LOLBIN technique  
- Investigated process execution and parent-child relationships in Microsoft Sentinel  

---

### Key Findings:
- LOLBINs were executed with suspicious command-line arguments like `-encode`, `-decode`, and encoded PowerShell commands  
- Parent processes included PowerShell, cmd, and mshta, showing how the commands were executed  
- Encoded commands made it harder to immediately understand what was done  
- Different LOLBINs followed similar patterns, which shows how attackers try to evade detection  
- Clear parent-child process relationships were observed during investigation  

---

### Outcome:
- Successfully detected multiple LOLBIN abuse techniques using KQL  
- Identified similar behavior across different binaries, not just one tool  
- Gained better visibility into encoded and obfuscated command execution  
- Built a strong detection approach for identifying defense evasion techniques in a SOC environment
  
**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-4-lolbins-process-detection)

## 🚀 Key Achievements

- Built a functional SOC lab environment from scratch  
- Simulated and detected real-world attack scenarios  
- Developed detection rules using KQL  
- Performed incident investigation and validation  
- Reduced false positives through proper analysis  
- Worked with multiple log sources (Azure AD & Windows Events)  

---

## 🔹 Project 5: CertUtil LOLBin & Ceprolad Investigation

This project focuses on detecting and investigating malicious activity involving **CertUtil (a Windows LOLBin)** and suspicious file execution behavior, including the use of a file named **“ceprolad”**, commonly associated with obfuscated or staged malware activity.

---

### 🧪 What I Did:
- Simulated abuse of **CertUtil.exe** for malicious purposes (download, encode, decode operations)  
- Investigated execution of suspicious file named **“ceprolad”** in command-line activity  
- Generated Windows Security and Sysmon logs (Process Creation events)  
- Built KQL queries to detect CertUtil-based LOLBin misuse  
- Analyzed parent-child process relationships in Microsoft Sentinel  
- Correlated command-line arguments with suspicious execution behavior  

---

### 🎯 Detection Logic Focus:
- CertUtil usage with suspicious flags:
  - `-urlcache`
  - `-encode`
  - `-decode`
- Execution of unknown or non-standard file names (e.g. **ceprolad**)  
- PowerShell or cmd spawning CertUtil processes  
- Encoded or obfuscated command-line activity  
- Abnormal process execution chains  

---

### 🔍 Key Findings:
- CertUtil was used as a LOLBin to simulate file retrieval and encoding abuse  
- Suspicious execution of **ceprolad** identified as potentially malicious or staged payload  
- Encoded command-line activity made direct interpretation difficult  
- Parent processes included PowerShell and cmd.exe, indicating script-based execution  
- Clear LOLBin abuse pattern consistent with defense evasion techniques  

---

### 📊 Outcome:
- Successfully detected CertUtil LOLBin abuse using KQL  
- Identified suspicious execution behavior tied to unknown file activity (ceprolad)  
- Improved ability to detect encoded and obfuscated command execution  
- Strengthened understanding of LOLBin-based attack chains and evasion techniques  

---

**Status:** ✅ Completed  

👉 [View Project Details](PROJECT-5-certutil-lolbin-ceprolad-investigation/README.md)

## 📊 Attack Patterns Detected

| Attack Type               | Project   | Status       |
|--------------------------|----------|-------------|
| Cloud Login Brute Force  | Project 1 | ✅ Complete |
| Local Login Failures     | Project 2 | ✅ Complete |
| RDP Brute Force + Success| Project 3 | ✅ Complete |
| Suspicious Lolbin-Process| Project 4 | ✅ Complete |
| Lolbin Investigation     | Project 5 | ✅ Complete |
---

## 🚀 Coming Next

Planned projects to expand detection coverage:

- **Project 6:** Privilege Escalation Detection  

---

## 🎓 SC-200 Alignment

This portfolio demonstrates hands-on experience with:

- Microsoft Sentinel configuration and deployment  
- Log ingestion and data connectors  
- Analytics rule creation  
- Incident investigation workflows  
- KQL query development  
- Windows Security Event analysis  
- Azure AD authentication monitoring  

---

## 📈 Career Goal

To become a **SOC Analyst / Security Operations Engineer**, specializing in:

- Threat detection and analysis  
- Incident response and investigation  
- SIEM operations (Microsoft Sentinel)  
- Log analysis and correlation  
- Attack pattern identification  

---

## 📌 How To Use This Portfolio

**For learners:**
- Start with **Project 0** (environment setup)  
- Move to **Project 1** (detection logic)  
- Study **Project 2** (false positives)  
- Review **Project 3** (full attack investigation)  
- Review **Project 4** (LolBin process detection).
- NOTE **Certutil use-case** (contains Analytics-rule detection query and investigation process)
- Review **Project 5** (CertUtil LOLBin & Ceprolad Investigation)
  
  
**For recruiters**
- project 4 demonstrates detection evasion usually used by adversaries and how to detect them (Full Soc workflow)
- Project 5 (CertUtil LOLBin & Malware Investigation) shows step by step Real incident investigation
- Project 3 demonstrates full SOC workflow  
- Project 2 highlights analytical thinking  
- All projects show practical, hands-on experience  

---

## 📞 Contact
- **Education:** OND in Computer-Engineering
- **Certification:** SC-900 (Azure Fundamentals), Microsoft-Cyber-Security Analyst Certificate (Course-era)
- **Location:** Nigeria  
- **GitHub:** https://github.com/olatunjiabel/sc200-soc-portfolio
---

## ⚠️ Disclaimer

This portfolio is created in a controlled lab environment for learning purposes.  
No real-world systems or organizations were affected.

---

**Last Updated:** May 2026
**Status:** 🟢 Active (ongoing improvements)

