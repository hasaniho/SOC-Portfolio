# Lab 01 – Windows Security Events Ingestion & Analysis (Microsoft Sentinel)

## Objective
Configure Microsoft Sentinel to ingest Windows Security Event logs from an Azure-hosted Windows virtual machine and validate log visibility for SOC-style investigation.

---

## Environment
- **Cloud Platform:** Microsoft Azure
- **SIEM:** Microsoft Sentinel
- **Log Analytics Workspace:** LAW-SOC-Lab
- **Data Source:** Azure Windows Virtual Machine
- **Log Type:** Windows SecurityEvent
- **OS:** Windows Server (Azure VM)

---

## Lab Overview
This lab simulates a foundational SOC task: onboarding a Windows host into a SIEM and verifying that security telemetry is successfully collected and searchable.

The focus was on:
- Proper workspace configuration
- Correct data source onboarding
- Verifying log ingestion
- Initial KQL-based exploration

---

## Steps Performed

### 1. Azure Resource Setup
- Created a Resource Group dedicated to SOC lab resources
- Deployed a Windows virtual machine in the same region as the Log Analytics Workspace
- Verified VM status and networking configuration

### 2. Log Analytics Workspace Configuration
- Created a Log Analytics Workspace (LAW)
- Ensured region alignment between the VM and workspace
- Confirmed workspace was successfully linked to Microsoft Sentinel

### 3. Microsoft Sentinel Deployment
- Enabled Microsoft Sentinel on the Log Analytics Workspace
- Verified Sentinel workspace visibility in the Defender portal

### 4. Windows Security Events Ingestion
- Added **Windows Event Logs** as a data source
- Selected **Security** events with **Audit Success** and **Audit Failure**
- Associated the Windows VM as a monitored resource
- Deployed the data collection rule

### 5. Validation & Analysis
- Confirmed successful data ingestion into the workspace
- Queried `SecurityEvent` logs using KQL
- Verified presence of authentication and system-related events
- Observed real-time log flow from the VM into Sentinel

---

## Sample KQL Query
```kql
SecurityEvent
| take 10
