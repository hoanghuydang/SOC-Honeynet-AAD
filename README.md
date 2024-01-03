# SOC-Honeynet-AAD
# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

Within this project, I constructed a miniature honeynet within Azure, integrating log sources from diverse origins into a Log Analytics workspace. Microsoft Sentinel leverages this workspace to construct attack maps, initiate alerts, and generate incidents. I conducted a comprehensive analysis of security metrics within the insecure environment over a 24-hour period. Following this, I implemented various security controls to fortify the environment, subsequently measuring metrics for an additional 24 hours. The outcomes of these efforts are detailed below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel


In evaluating the "BEFORE" metrics, it's crucial to note that all resources were initially deployed with direct exposure to the internet. The Virtual Machines, in particular, had both their Network Security Groups and built-in firewalls configured in a wide-open manner, while all other deployed resources featured public endpoints visible to the Internet, rendering private endpoints redundant.

In contrast, the "AFTER" metrics reflect a significant enhancement in security measures. Specifically, the Network Security Groups underwent rigorous hardening, restricting all traffic except that originating from my admin workstation. Furthermore, additional protection was implemented for all other resources through the utilization of their built-in firewalls alongside the integration of Private Endpoints, marking a substantial improvement in the overall security posture.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/hoanghuydang/SOC-Honeynet-AAD/assets/127445164/81be8d38-73cd-4ca6-9414-9a54835676f3)
![image](https://github.com/hoanghuydang/SOC-Honeynet-AAD/assets/127445164/6791444d-69f9-4f8b-a146-e4eaef684fa2)
![image](https://github.com/hoanghuydang/SOC-Honeynet-AAD/assets/127445164/c1a4670b-74d5-45e3-a180-70f6e7893abe)
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>
![image](https://github.com/hoanghuydang/SOC-Honeynet-AAD/assets/127445164/71579f5b-cd64-41d8-bde1-e6d0742ff951)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-12-26 14:14:17
Stop Time 2023-12-26 14:14:17

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 41599
| Syslog                   | 16753
| SecurityAlert            | 34
| SecurityIncident         | 363
| AzureNetworkAnalytics_CL | 68043

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-12-28 14:31:28
Stop Time	2023-12-29 14:31:28

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9321
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

Within the scope of this project, a compact honeynet was established in Microsoft Azure, seamlessly integrating log sources into a Log Analytics workspace. The deployment of Microsoft Sentinel played a pivotal role in orchestrating alerts and incidents based on the assimilated logs. Notably, the project involved assessing metrics within the insecure environment both before and after the application of security controls. The results indicated a substantial reduction in the number of security events and incidents after the implementation of these security measures, underscoring their efficacy in fortifying the system.

An additional point of consideration is that if the network resources were extensively utilized by regular users, it is conceivable that a higher volume of security events and alerts might have been generated during the 24-hour period following the implementation of the security controls. This emphasizes the dynamic nature of security assessments and the need for tailored solutions that account for the specific usage patterns within a network.
