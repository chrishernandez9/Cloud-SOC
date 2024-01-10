# Building a SOC + Honeynet in Azure
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I built a honeynet in Azure and analyzed the live traffic by using Microsoft Sentinet to learn a bit more about enhancing cloud security swiftly and effectively handling incident responses. I utilized Sentinel bto help me build attack maps, trigger alerts, and record some metrics. 

Metrics:
- Windows Event Logs (SecurityEvent)
- Linux Event Logs (Syslog)
- Triggered Log Analytics Alerts (SecurityAlert)
- Incidents created by Sentinel (SecurityIncident)
- Malicious Flows allowed into our honeynet (AzureNetworkAnalytics_CL)

## Architecture Before Implementing Security Controls
<img width="604" alt="Screenshot 2024-01-09 at 21 40 16" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/7095acf5-7501-4021-9009-16b4781cfaa5">

## Architecture After Hardening and Implementing Security Controls
<img width="828" alt="Screenshot 2024-01-09 at 23 45 54" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/d895fe4d-3e88-427b-978a-1521f5a7c872">

The architecture of the honeynet in Azure consists of the following components:
- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" metrics, all resources were deployed with unrestricted exposure to the internet. Both the Virtual Machines and their Network Security Groups, alongside built-in firewalls, were configured with wide-open settings that completely exposed the environment. 

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic (except administrative entities), and all other resources were protected with firewalls as well as private endpoints.

## Attack Maps Before Hardening / Security Controls
Network Security Groups Allowed Inbound Malicious Flows 
<img width="1343" alt="(BEFORE)nsg-malicious-allowed-in" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/ebb08079-ce43-456b-8aa8-d235c9ec428e">
<br>
Linux Syslog Authentication Failures 
<img width="1313" alt="(BEFORE)linux-ssh-auth-fail" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/fd6f9924-0bd9-4d33-be17-cba1b70be03a">
<br>
Windows RDP/SMB Authentication Failures
<img width="1294" alt="(BEFORE)windows-rdp-auth-fail" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/462da0bd-59b5-4d76-8e4d-44145faed469">
<br>
MS SQL Server Authentication Failures
<img width="1132" alt="(BEFORE)mssql-auth-fail" src="https://github.com/chrishernandez9/Cloud-SOC/assets/156137903/885a2052-1ea1-4f9a-8fac-9d3ef6975d74">
<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2024-01-08 18:35:29


Stop Time 2023-01-09 18:35:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 53615
| Syslog                   | 17373
| SecurityAlert            | 11
| SecurityIncident         | 361
| AzureNetworkAnalytics_CL | 1648







## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

I created a honeypot in Azure and analyzed live network traffic by incorporating log sources and utilizing Microsoft Sentinel to facilitate the generation of alerts and incidents based on the ingested logs. 
Metrics were initially measured in the insecure environment before applying NIST security controls. 

Subsequently, the same metrics were assessed after the implementation of these security controls. 
The results showcased a significant reduction in the number of security events and incidents post-implementation. 
