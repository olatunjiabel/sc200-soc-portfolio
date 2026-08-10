# Windows Server Onboarding to Microsoft Sentinel

This section documents the onboarding of an on-premises **Windows Server 2022 virtual machine** to Microsoft Sentinel as part of the **Project 0 – SOC Environment Setup**.

This step extends the SOC lab by integrating a locally hosted server with Azure monitoring services using **Azure Arc** and the **Azure Monitor Agent (AMA)**.

---

## Relationship to Project 0

This onboarding process builds on the SOC infrastructure created in **Project 0**.

 Return to the main project documentation:  
[Project 0 – SOC Environment Setup](../README.md)

Project 0 established the following components:

- Microsoft Entra ID tenant
- Log Analytics Workspace
- Microsoft Sentinel SIEM
- Initial SOC monitoring environment

This section focuses on **connecting an on-premises server to that environment**.

---

## Objective

Demonstrate how an on-premises system can be integrated into a cloud-based SOC monitoring pipeline.

The goal is to collect **Windows Security Event logs** from a locally hosted server and analyze them using **Microsoft Sentinel**.

---

## Architecture Overview

```
Windows Server 2022 (VMware)
        │
        │ Azure Arc Agent
        ▼
Azure Arc
        │
        ▼
Azure Monitor Agent (AMA)
        │
        ▼
Data Collection Rule
        │
        ▼
Log Analytics Workspace
        │
        ▼
Microsoft Sentinel
        │
        ▼
Security Event Analysis (KQL)
```

---

## Technologies Used

- VMware Workstation
- Windows Server 2022
- Microsoft Azure
- Azure Arc
- Azure Monitor Agent (AMA)
- Log Analytics Workspace
- Microsoft Sentinel
- Kusto Query Language (KQL)

---

## Implementation Steps

1. Deploy **Windows Server 2022** virtual machine in VMware.
2. Install the **Azure Arc agent** on the server.
3. Connect the server to **Azure Arc**.
4. Install the **Azure Monitor Agent (AMA)** extension.
5. Configure a **Data Collection Rule** to collect Windows Security Events.
6. Send logs to the **Log Analytics Workspace**.
7. Verify logs ingestion in **Microsoft Sentinel**.

---

## Screenshots

#### Windows Server VM Configuration
![Windows Server VM](../screenshots/Windows-Server-Vm-Configuration.png)

#### Azure Arc Machine Connected
![Azure Arc Machine](../screenshots/Azure-Arc-Machine-Connected.png)

#### Azure Monitor Agent Installed
![Azure Monitor Agent](../screenshots/Azure-Monitor-Windows-Agent.png)

#### Windows Security Events Collected
![Windows Security Events](../screenshots/Windows-Security-Events.png)

#### Security Logs Visible in Microsoft Sentinel
![Sentinel Security Events](../screenshots/Sentinel-Security-Events.png)

---

## Outcome

The Windows Server VM was successfully onboarded into the SOC monitoring environment.

Security logs from the on-premises system are now ingested into **Microsoft Sentinel**, enabling detection engineering and threat investigation using **KQL queries**.
