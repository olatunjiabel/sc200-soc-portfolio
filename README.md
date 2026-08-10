#  Microsoft Sentinel SOC Lab – Security Operations Portfolio

##  About Me

Hi, my name is **Olatunji Olubi Abel**.

This portfolio showcases hands-on cybersecurity projects aligned with the **Microsoft SC-200 (Security Operations Analyst)** certification.

It documents my journey toward becoming a **SOC Analyst**, with a strong focus on practical, real-world security operations.

---

##  Skills Demonstrated

-  Security Monitoring  
-  Detection Engineering  
-  Security Incident Investigation  
-  Threat Analysis  
-  Log Analysis  
-  Microsoft Security Tools  

---

##  Tools & Technologies

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

##  Portfolio Projects

### 🔹 Project 0: SOC Environment Setup

Foundational project where I built a complete SOC lab environment from scratch.

**What I Did:**
- Configured Microsoft Entra ID (Azure AD) tenant  
- Created Log Analytics Workspace  
- Deployed Microsoft Sentinel (SIEM)  
- Connected Windows Server via Azure Arc  
- Set up data ingestion pipelines  

**Status:**  Completed  

 [View Project Details](PROJECT-0-soc-enviroment-setup/README.md)

---

###  Project 1: Azure AD Brute Force Detection

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

**Status:**  Completed  

 [View Project Details](PROJECT-1-detection-engineering/README.md)

---

###  Project 2: False Positive - Brute Force Detection

Focused on distinguishing real threats from false positives.

**What I Did:**
- Generated failed login events on a Windows workstation  
- Alert triggered for 3+ failed attempts  
- Investigated to validate the alert  

**Investigation Findings:**
- Source: `127.0.0.1` (localhost, not external attacker)  
- Activity: Workstation unlock attempts (**LogonType 7**)  
- Conclusion: User error (incorrect password), not malicious activity  

**Lesson Learned:**
- Not all alerts are real threats  
- Context and investigation are critical in SOC workflows  
- Understanding log data reduces alert fatigue  

**Status:**  Completed  

 [View Project Details](PROJECT-2-brute-force-detection/README.md)

---

###  Project 3: RDP Brute Force Detection & Investigation

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

**Status:**  Completed  

 [View Project Details](PROJECT-3-RDP-brute-force-detection/README.md)

---

###  Project 4: LOLBIN Process Abuse Detection & Investigation

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
  
**Status:**  Completed  

 [View Project Details](PROJECT-4-lolbins-process-detection)


---

##  Project 5: CertUtil LOLBin & Ceprolad Investigation

This project focuses on detecting and investigating malicious activity involving **CertUtil (a Windows LOLBin)** and suspicious file execution behavior, including the use of a file named **“ceprolad”**, commonly associated with obfuscated or staged malware activity.

---

###  What I Did:
- Simulated abuse of **CertUtil.exe** for malicious purposes (download, encode, decode operations)  
- Investigated execution of suspicious file named **“ceprolad”** in command-line activity  
- Generated Windows Security and Sysmon logs (Process Creation events)  
- Built KQL queries to detect CertUtil-based LOLBin misuse  
- Analyzed parent-child process relationships in Microsoft Sentinel  
- Correlated command-line arguments with suspicious execution behavior  

---

###  Detection Logic Focus:
- CertUtil usage with suspicious flags:
  - `-urlcache`
  - `-encode`
  - `-decode`
- Execution of unknown or non-standard file names (e.g. **ceprolad**)  
- PowerShell or cmd spawning CertUtil processes  
- Encoded or obfuscated command-line activity  
- Abnormal process execution chains  

---

###  Key Findings:
- CertUtil was used as a LOLBin to simulate file retrieval and encoding abuse  
- Suspicious execution of **ceprolad** identified as potentially malicious or staged payload  
- Encoded command-line activity made direct interpretation difficult  
- Parent processes included PowerShell and cmd.exe, indicating script-based execution  
- Clear LOLBin abuse pattern consistent with defense evasion techniques  

---

###  Outcome:
- Successfully detected CertUtil LOLBin abuse using KQL  
- Identified suspicious execution behavior tied to unknown file activity (ceprolad)  
- Improved ability to detect encoded and obfuscated command execution  
- Strengthened understanding of LOLBin-based attack chains and evasion techniques  

---

**Status:**  Completed  

 [View Project Details](PROJECT-5-certutil-lolbin-ceprolad-investigation/README.md)


###  Project 6: Sentinel SOAR — Brute Force Automated Response

This project sole aim is to showcase the step-by-step process of generating an automated response to alerts or incidents in Microsoft Sentinel.

SOAR (Security Orchestration and Automated Remediation) refers to the activities that are put in place to automatically respond to alerts or incidents in a SOC.

**What I Did:**
- Created an Analytics rule (Brute-force-detection) to trigger when multiple failed attempts occur on my Microsoft account
- Wrote a KQL query to detect 5+ failed login attempts with 1+ successful attempt within 1 hour
- Created a Logic App and added a Playbook to alert my Outlook mail every time a brute force incident happens
- Assigned the Playbook to the Analytic rule via the Automation Tab in Sentinel
- Assigned the role of Sentinel Automation Contributor to Azure Security Insights in IAM to enable SOAR
- Simulated a Brute Force Attack by entering multiple wrong passwords on my Microsoft user account to generate an alert/incident

**Key Findings:**
- Analytics rule successfully generated an incident from the brute force simulation
- Attacker user account identified with 20 failed attempts from IP `102.88.110.157`
- MITRE ATT&CK Technique: **T1110 – Brute Force** (Credential Access)
- Logic App playbook triggered automatically and sent email notification to SOC analyst Outlook mailbox

**SOAR Workflow:**
Brute Force Attempt → KQL Query Detection → Analytics Rule
→ Incident Creation → Automation Rule → Logic App Workflow → Outlook Alert 
**What I Learned:**
- To enable SOAR and to be able to add automation rules to my Analytic rule, I was prompted to assign the role of Sentinel Automation Contributor to Azure Security Insights in IAM (Identity Access Management)
- The license for Defender for Office 365 Plan 2 E5 is needed or Business Premium License to be able to use the Outlook connector in the Logic App
- SOAR allows for the immediate remediation of threats — the SOC Analyst was alerted directly on Outlook to check out a potential Brute Force Attack

**Status:**  Completed  
 [View Project Details](PROJECT-6-Sentinel-SOAR-BruteForce-Automation)

###  Project 7: Email Phishing Detection & Investigation

This project focuses on simulating and investigating a credential harvesting phishing attack using Microsoft Defender for Office 365 Plan 2.

The objective was to understand how phishing emails are delivered, how users interact with them, and how SOC analysts investigate email-based threats.

**What I Did:**

* Created a credential harvesting phishing simulation using Microsoft Attack Simulation Training
* Delivered a phishing email to a user within my Microsoft 365 tenant
* Simulated user interaction by clicking the phishing link and submitting credentials
* Investigated the phishing email using Microsoft Defender Threat Explorer
* Reviewed sender information, sender IP address, and recipient details
* Analyzed SPF, DKIM, and DMARC authentication results
* Investigated URLs contained within the phishing email
* Validated sender IP reputation using VirusTotal
* Documented SOC analyst response procedures for credential harvesting incidents

**Key Findings:**

* The phishing simulation successfully harvested user credentials
* The phishing email was delivered and interacted with by the user
* SPF, DKIM, and DMARC all passed successfully
* Three URLs were identified within the email
* No malicious verdict was assigned because the email originated from Microsoft Attack Simulation Training
* User click activity was recorded and available for investigation in Microsoft Defender
* Authentication checks validate sender infrastructure but do not guarantee email legitimacy

**What I Learned:**

* Phishing emails can still be successful even when SPF, DKIM, and DMARC pass
* Threat Explorer provides valuable visibility into email activity, sender information, and user interactions
* User awareness remains a critical security control against phishing attacks
* Microsoft Attack Simulation Training provides a safe environment for testing phishing scenarios
* Advanced investigations may require additional correlation using Advanced Hunting or Microsoft Sentinel

**Status:** Completed

 [View Project Details](PROJECT-7-Email%20phishing%20detection%20and%20investigation%20using%20microsoft%20defender%20for%20office%20365/README.md)

###  Project 8: Adversary TTP Mapping with MITRE ATT&CK

This project focuses on mapping adversary tactics and techniques observed across earlier investigations to the MITRE ATT&CK framework, showing the analyst reasoning behind each mapping and how that mapping drives detection strategy.

**What I Did:**

* Mapped three real findings from my Azure lab environment to MITRE ATT&CK tactics and techniques (Azure AD brute force, RDP brute force, and LOLBin/Certutil abuse)
* Documented my analyst reasoning for navigating attack.mitre.org and arriving at each tactic and technique
* Built a detection strategy and KQL detection rule for each mapped technique
* Correlated DeviceProcessEvents and DeviceNetworkEvents to check for C2 beacon activity
* Built an ATT&CK Navigator heatmap and coverage summary across all findings

**Key Findings:**

* Azure AD brute force mapped to T1110.001 – Password Guessing (Credential Access)
* RDP brute force mapped to the same technique, T1110.001, but required a different data source (Windows Security Event Logs instead of Azure AD Sign-in Logs) — demonstrating that the same technique can require different detection coverage depending on protocol
* LOLBin abuse (PowerShell spawning Certutil) mapped to three separate techniques across three tactics: T1059.001 (Execution), T1140 (Defense Evasion), and T1105 (Command and Control)
* 5 techniques mapped in total, with full detection coverage (0 gaps) across all findings

**What I Learned:**

* MITRE ATT&CK mapping is not just documentation — it directly determines what to monitor and why
* The same adversary technique can manifest differently across data sources and protocols, requiring broader detection coverage than a single query
* Correlating process and network events together is necessary to answer questions like "is this a C2 beacon attack?"

**Status:**  Completed

 [View Project Details](PROJECT-8-Adversary%20TTP%20Mapping%20with%20MITRE%20ATT%26CK/README.md)

###  Project 9: XDR Multi-Alert Correlation Investigation

This project investigates a full hands-on-keyboard incident in which Microsoft Defender XDR correlated 16 separate alerts, generated across a two-day window on the same endpoint and identity, into a single incident.

**What I Did:**

* Investigated an incident where a compromised Administrator account was used to run a LOLBin (Certutil) download attempt, followed two days later by a reconnaissance-to-persistence attack chain
* Used the Attack Story, Incident Graph, and Evidence and Response tabs in Microsoft Defender XDR to reconstruct the full timeline
* Wrote and ran Advanced Hunting KQL queries across DeviceProcessEvents, DeviceFileEvents, and DeviceLogonEvents to confirm every claim against raw telemetry
* Separated findings into Indicators of Attack (behavior-based) and Indicators of Compromise (artifact-based)
* Mapped the full attack chain to MITRE ATT&CK, built an Incident Response Procedure (7 phases), a Business Impact assessment, and a Detection Strategy
* Wrote my own Blast Radius KQL queries to check whether the compromised account or the attacker-created account touched any other device in the environment

**Key Findings:**

* Attack began with Certutil (`-urlcache -split -f`) invoked via PowerShell to download a file from an external URL — blocked as Trojan:Win32/Ceprolad.A
* Two days later, the same compromised account ran a tight reconnaissance sequence (whoami, net user enumeration, tasklist, ipconfig) followed by creation of a local "backdoor" account and its escalation into the local Administrators group — all within roughly 45 seconds
* XDR correlated all 16 alerts into a single incident based on shared device and shared identity, despite the 2-day gap between the two stages of the attack
* Multiple individually-flagged alerts (account creation, password change, group modification) were confirmed to trace back to the same single net.exe command, not separate events

**What I Learned:**

* How XDR actually correlates alerts into incidents — by device and identity, not just time proximity
* The value of verifying every claim against raw Advanced Hunting telemetry rather than trusting an alert summary — this process caught and corrected several of my own early assumptions during the investigation
* How to stay methodical rather than overwhelmed when a single incident contains 16 alerts

**Status:**  Completed

 [View Project Details](PROJECT-9-XDR-Multi-Alert-Correlation/README.md)

##  Key Achievements

- Built a functional SOC lab environment from scratch  
- Simulated and detected real-world attack scenarios  
- Developed detection rules using KQL  
- Performed incident investigation and validation  
- Reduced false positives through proper analysis  
- Worked with multiple log sources (Azure AD & Windows Events)
- Built and automated a full SOAR pipeline using Logic Apps and Microsoft Sentinel
- - Investigated phishing emails using Microsoft Defender for Office 365
- Performed email authentication analysis (SPF, DKIM, DMARC)
- Validated sender IP reputation using VirusTotal
- Mapped adversary tactics and techniques to MITRE ATT&CK with full documented analyst reasoning
- Investigated a 16-alert multi-stage XDR-correlated incident from initial access through privilege escalation

##  Attack Patterns Detected

| Attack Type               | Project   | Status       |
|--------------------------|----------|-------------|
| Cloud Login Brute Force  | Project 1 |  Complete |
| Local Login Failures     | Project 2 |  Complete |
| RDP Brute Force + Success| Project 3 |  Complete |
| Suspicious Lolbin-Process| Project 4 |  Complete |
| Lolbin Investigation     | Project 5 |  Complete |
| SOAR Automated Response  | Project 6 |  Complete |
| Email Phishing Investigation | Project 7 |  Complete |
| MITRE ATT&CK TTP Mapping | Project 8 |  Complete |
| XDR Multi-Alert Correlated Incident | Project 9 |  Complete |
---


---

##  SC-200 Alignment

This portfolio demonstrates hands-on experience with:

- Microsoft Sentinel configuration and deployment  
- Log ingestion and data connectors  
- Analytics rule creation  
- Incident investigation workflows  
- KQL query development  
- Windows Security Event analysis  
- Azure AD authentication monitoring
- SOAR automation using Logic Apps and Playbooks  
- Simulated a credential harvesting phishing attack
- Investigated phishing email delivery and user interaction
- Analyzed SPF, DKIM, and DMARC authentication results
- Reviewed sender IP addresses and URL activity
- Used Threat Explorer to investigate phishing events
- Performed external threat intelligence validation with VirusTotal
- Mapped adversary behavior to MITRE ATT&CK tactics and techniques
- Built and used an ATT&CK Navigator heatmap for coverage tracking
- Investigated and correlated a multi-alert incident using Microsoft Defender XDR
- Verified findings against raw telemetry using Advanced Hunting across multiple device tables
- Built a full Incident Response Procedure and Business Impact assessment
  
---

##  Career Goal

To become a **SOC Analyst / Security Operations Engineer**, specializing in:

- Threat detection and analysis  
- Incident response and investigation  
- SIEM operations (Microsoft Sentinel)  
- Log analysis and correlation  
- Attack pattern identification  

---

##  How To Use This Portfolio

**For learners:**
- Start with **Project 0** (environment setup)  
- Move to **Project 1** (detection logic)  
- Study **Project 2** (false positives)  
- Review **Project 3** (full attack investigation)  
- Review **Project 4** (LolBin process detection).
- NOTE **Certutil use-case** (contains Analytics-rule detection query and investigation process)
- Review **Project 5** (CertUtil LOLBin & Ceprolad Investigation)
- Review **Project 6** (SOAR automated response pipeline)
- Review **Project 7** (PROJECT 7: Email phishing detection and investigation using microsoft defender  for office 365)
- Review **Project 8** (Adversary TTP Mapping with MITRE ATT&CK)
- Review **Project 9** (XDR Multi-Alert Correlation Investigation)
  
**For Recruiters:**

* Project 9 demonstrates full incident investigation using Microsoft Defender XDR — correlating 16 alerts into one incident, verifying every claim against raw Advanced Hunting telemetry, and producing a complete IOA/IOC breakdown, MITRE mapping, Incident Response Procedure, and Business Impact assessment.
* Project 8 demonstrates MITRE ATT&CK mapping with documented analyst reasoning across three real findings, tied directly to detection rules and an ATT&CK Navigator heatmap.
* Project 7 demonstrates hands-on phishing detection and investigation using Microsoft Defender for Office 365, including Attack Simulation Training, Threat Explorer, email authentication analysis (SPF, DKIM, DMARC), URL investigation, and IP reputation validation.
* Project 6 demonstrates end-to-end SOAR automation from detection to analyst notification using Microsoft Sentinel and Logic Apps.
* Project 5 demonstrates step-by-step LOLBin and malware investigation using CertUtil abuse, process analysis, and KQL-based detection.
* Project 4 demonstrates detection of LOLBin abuse, encoded commands, and defense evasion techniques commonly used by adversaries.
* Project 3 demonstrates a complete SOC workflow from attack simulation to detection, incident creation, and investigation.
* Project 2 highlights analytical thinking and the ability to distinguish true positives from false positives.
* All projects demonstrate practical, hands-on experience with Microsoft security technologies, detection engineering, threat investigation, and incident response workflows.


---

##  Contact
- **Education:** OND in Computer-Engineering
- **Certification:** SC-900 (Azure Fundamentals), Microsoft-Cyber-Security Analyst Certificate (Coursera)
- **Location:** Nigeria  
- **GitHub:** https://github.com/olatunjiabel231-coder/sc200-soc-portfolio
---
##  Quick Navigation

1. [Project 0: SOC Environment Setup](#project-0)
2. [Project 1: Azure AD Brute Force Detection](#project-1)
3. [Project 2: False Positive Analysis](#project-2)
4. [Project 3: RDP Brute Force Detection](#project-3)
5. [Project 4: LOLBIN Process Detection](#project-4)
6. [Project 5: CertUtil & Malware Investigation](#project-5)
7. [Project 6: SOAR Automated Response](#project-6)
8. [PROJECT 7: Email phishing detection and investigation using microsoft defender  for office 365](#project-7)
9. [Project 8: Adversary TTP Mapping with MITRE ATT&CK](#project-8)
10. [Project 9: XDR Multi-Alert Correlation Investigation](#project-9)

##  Disclaimer

This portfolio is created in a controlled lab environment for learning purposes.  
No real-world systems or organizations were affected.

---

**Last Updated:** JULY 2026
**Status:**  Active (ongoing improvements)

