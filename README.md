# Microsoft Sentinel Lab Demonstration

- Introductory Video: https://youtu.be/9iHZE7jGI88?si=-0cy_wcYJUGPEojG
- Part 2: Entra ID Logs, KQL Example: https://youtu.be/bFdEuWiFZSo
- Part 3: Powershell Execution Detection with Microsoft Defender for Endpoint: https://youtu.be/0O5JVlxSrWM
- Part 4: More Suspicious Powershell Execution/Unauthorized Domain Controller Sign in Detection Rules: 

# Lab Topology
- Resource Group
- Log Analytics Workspace
- Sentinel Instance
- M365 Admin Tenant with Intune and Defender for Endpoint Enabled
- M365 App Suite
- Various Data Connectors such as Entra, Azure Activity, and M365
- Domain Controller and Windows 11 Endpoint Installed with AMA using Azure Arc.
- Three Additional Endpoints on a Separate Domain but Enrolled in  with Microsoft Defender for Endpoint



# The lab consists of a Sentinel Instance with a Log Analytics Workspace. There are multiple Data Connectors installed to enable log ingestion capabilities. 
- Sentinel is also linked with Office 365 E5 while also equipped with Intune and Defender for Endpoint, Identity, and Cloud
- I have The Ecorp Domain Controller from my other lab as well as a Windows 11 Host device with Azure Monitor Agent installed to enable Security Logs to be ingested into Azure Sentinel. I also have another domain controller on an entirely different domain added to my list of devices for Defender for Endpoint to showcase Microsoft Defender's Versatility across multi-domain environments. 
- In Part 3 of the video series, I go through a Powershell Execution Attack Scenario, which is really a false positive but understanding the process of triaging alerts, troubleshooting accordingly, and being able to Identify a True Attack vs an Informational alert is essential for SOC analysts and Cybersecurity Analysts. The following screenshots below will also explain my thought process and actions taken step by step. 



# I started by creating the Log Analytics Workspace for Sentinel to Pull Log data from, then I installed Data Connectors for Azure Activity, O365 Activity, as well as Syslog
- The screenshot also shows some On-premesis resources I added through Azure Arc, Data Collection rules used to filter exactly what types of logs come through, among other lab resources. 

<img width="1894" height="969" alt="Sentinel Workspace" src="https://github.com/user-attachments/assets/20ab8aff-d574-4d61-8088-ab2484e157ea" />

# Once the Log Analytics Workspace was configured, I installed some data connectors: 
- Some of the connectors you'll see are Microsoft Defender XDR, Microsoft Defender for Identity, Entra ID, Azure Activity, Syslog through AMA, TAXII threat Intelligence, etc. 

<img width="1908" height="1026" alt="Sentinel Data Connectors" src="https://github.com/user-attachments/assets/a5c8607d-b86b-4720-85e4-814cdfa5a288" />

# Next I will go into the Microsoft Defender Portal
- In the portal you will find various security settings such as Information on Endpoints, Incident and Alert Management, Defender for Identity Sensors, Analytics and Detection Rules, etc
- Below you will see the list of endpoints I've added to the Environment, as well as the current Incidents I have that were triggered by detection rules.
- What you'll notice is that there are two different domains here, Ecorp.Local and Macad2022.local. The latter was configured several months back as a separate home lab. I decided to enroll the DC and a host device from that lab into defender because why not? This gives me centralized security management for both domain controllers and workstations, even without them being in the same AD forest. 

  <img width="1888" height="1021" alt="Defender Devicesd" src="https://github.com/user-attachments/assets/9ecbf98c-1c9e-4bc8-b20b-f52355ac4298" />


# Next I will talk about the Incidents I have(Both open and resolved)
- Below you'll see a few incidents, mainly for Suspicious Powershell Execution and Unauthorized Controller Login attempts. These were generated from a custom detection rule I created.
- Any other Incidents are incidents  from a separate Sentinel Workspace Instance, in addition to a separate home lab I'm working on.
- In part 3 of the video demonstration, I took a deeper dive into one of the incidents(Execution incident on one endpoint
- In part 4 I will discuss the Suspicious Powershell Execution Alert as well as the Unauthorized Domain Controller Incidents

<img width="1908" height="1015" alt="Defender Incidents" src="https://github.com/user-attachments/assets/45d8fcad-975a-4bf0-be76-fd2ae003e9c1" />


# Next I will Display the Analytics rules configured as Scheduled Query Rules to trigger the Incidents
- Right now there are only two custom made rules for the suspicious powershell execution and Unauthorized Domain Controller logins.
- Rule Logic Posted Below:
- For the powershell execution rule, the idea was to target any account that isn't an administrator account that tried to run anything through powershell. It will log both successful and unsuccessful attempts. Best practice would be to create a group policy or intune compliance policy for this to prevent powershell execution, but for the demonstration I wanted to start from a freshly configured, unhardened, unpatched  enterprise environment.
- For the Unauthorized domain controller rule. Any accounts that aren't domain administrator accounts shouldn't be able to log into DCs as best practice. In this case, I have an account called Jdoe that is oveprivileged and has access to login to domain controllers. I would personally remove this access if it is not specifically needed for any tasks pertaining to "John Doe's" daily workflow, thus, the rule picked up on his attempts at signing in. I will go over this further in part 4 of the video demonstration.  

<img width="1912" height="1029" alt="Defender Analytics Rules" src="https://github.com/user-attachments/assets/fe4263ed-8afa-41e3-9d04-91844923cb31" />


<img width="1903" height="1025" alt="Powershell Rule Logic" src="https://github.com/user-attachments/assets/3bc11fcd-2d05-41f2-be23-7e9e4baba05f" />


<img width="1898" height="1025" alt="Rule Logic 2" src="https://github.com/user-attachments/assets/72da1e96-730b-41e4-b4f8-fb8b5fd11e41" />


