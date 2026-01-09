# Microsoft Sentinel Lab Demonstration

- Introductory Video: https://youtu.be/9iHZE7jGI88?si=-0cy_wcYJUGPEojG
- Part 2: Entra ID Logs, KQL Example: https://youtu.be/bFdEuWiFZSo
- Part 3: Powershell Execution Detection with Microsoft Defender for Endpoint: 

# Lab Topology
- Resource Group
- Log Analytics Workspace
- Sentinel Instance
- M365 Admin Tenant with Intune and Defender for Endpoint Enabled
- M365 App Suite
- Various Data Connectors such as Entra, Azure Activity, and M365
- Domain Controller and Windows 11 Endpoint Installed with AMA using Azure Arc.



# The lab consists of a Sentinel Instance with a Log Analytics Workspace. There are multiple Data Connectors installed to enable log ingestion capabilities. 
- Sentinel is also linked with Office 365 E5 while also equipped with Intune and Defender for Endpoint, Identity, and Cloud
- I have The Ecorp Domain Controller from my other lab as well as a Windows 11 Host device with Azure Monitor Agent installed to enable Security Logs to be ingested into Azure Sentinel. I also have another domain controller on an entirely different domain added to my list of devices for Defender for Endpoint to showcase Microsoft Defender's Versatility acorss multi-domain environments. 
- In Part 3 of the video series, I go through a Powershell Execution Attack Scenario, which is really a false positive but understanding the process of triaging alerts, troubleshooting immediately, and being able to Identify a True Attack vs an Information alert is essential for SOC analysts and Cybersecurity Analysts. The following screenshots below will also explain my thought process and actions taken step by step. 

