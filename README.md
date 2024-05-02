# Azure Honeynet: Simulating Real-World Cybersecurity Threats
![Sa18KAF - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/d0e0b178-c99c-4ae4-aea1-cef47d22cf26)

## Introduction

Welcome to my comprehensive project, where I've developed a honeynet within the Azure ecosystem to replicate authentic cyber threats. This initiative highlights my expertise in crafting secure environments, orchestrating precise incident responses, and strengthening cybersecurity defenses.

## Objective
This project aimed to [establish deliberately vulnerable virtual machines](https://github.com/PranilPrasad/azure-vm-prep)  within Azure to attract and investigate cyber threats for a better understanding of attacker strategies and honing my incident response capabilities.

## Utilized Technologies, Standards, and Azure Services:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace using Kusto Query Language (KQL)
- Azure Key Vault for Secure Management of Secrets
- Azure Storage Account for robust Data Storage
- Microsoft Sentinel as a SIEM platform
- Microsoft Defender for Cloud for comprehensive cloud security
- Windows Remote Desktop and Command Line Interface (CLI) for remote and system management
- PowerShell for automation and configuration
- Security Standards: [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) & [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for incident repsonse

## Methodology

- <b>*Establishing the Honeypot*</b>: Initial steps involved [deploying multiple vulnerable virtual machines](https://github.com/PranilPrasad/azure-vm-prep) within Azure, simulating an environment ready for cyber threats.

- <b>*Monitoring and Analysis*</b>: Configured Azure to funnel log data from various sources into a log analytics workspace, utilizing Microsoft Sentinel to construct attack visualizations, trigger alerts, and generate incident reports.

- <b>*Measuring Security Metrics*</b>: Monitored the initial insecure setup for 24 hours, documenting key security indicators to establish a benchmark for subsequent security enhancements.

- <b>*Incident Response and Remediation*</b>: Addressed identified threats and vulnerabilities, applying industry best practices and Azure-specific strategies to strengthen security measures.

- <b>*Post-Remediation Evaluation*</b>: Re-evaluated the setup post-remediation to measure improvements in security metrics, comparing them against the initial data.


## Architectural Overview Before and After Security Enhancements

<b>Prior to Security Enhancement:</b>

- Originally, all resources were publicly accessible, exposing them to potential cyber threats. Virtual Machines had open Network Security Groups (NSGs) and firewalls, allowing unrestricted internet access.

![TFv2e8F - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/cebd8473-3ee8-4e88-90c0-996ff8626b7c)

<b>Following Security Enhancement:</b>

- Implemented stringent controls on NSGs, refined firewall configurations, and transitioned to Private Endpoints to shield Azure resources from unauthorized access.

![2OpO4dC - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/91fe191f-e9f2-4047-a002-57cb07111a77)

 ## Attack Maps Overview

<b>Network Security Groups (NSGs) - Malicious Traffic Allowed In</b>:

- The first map illustrates the global distribution of malicious traffic that was allowed to enter due to initially unsecured Network Security Groups (NSGs). This visualization captures high-risk interactions, with significant concentrations appearing in North America and Europe, indicating potential hotspots for cyber attacks.

![nsg-malicious-allowed-in](https://github.com/cesarias/Secure_Cloud/assets/126536570/d6695c8e-b06b-4a92-a56c-a3d7a13a7adf)

<b>Linux Virtual Machine - SSH Authentication Failures</b>: 

- This map highlights SSH authentication attempts that failed, signifying brute force attacks or unauthorized access attempts on the Linux VM. The largest red bubble represents a substantial number of failed login attempts, centered in North America, a critical data point underscoring the need for stringent access controls.

![linux-ssh-auth-fail](https://github.com/cesarias/Secure_Cloud/assets/126536570/1d49f3f8-c354-4518-8bfc-b06badf7c294)

<b>Windows Virtual Machine - RDP Authentication Failures</b>:

- Reflecting Remote Desktop Protocol (RDP) authentication challenges, this map shows where the most significant threats were detected. The visualization indicates that while these attempts were widespread, certain regions like North America and the Middle East experienced higher frequencies, pointing to areas where additional security measures may be necessary.

![windows-rdp-auth-fail](https://github.com/cesarias/Secure_Cloud/assets/126536570/b7e957e4-5a57-4de0-a3db-d055e36b187a)

> <b>NOTE: The attack maps were generated by extracting data from a workbook utilizing pre-built [KQL .JSON](https://github.com/AmiliaSalva/Cloud-SOC-Project-Resources/blob/main/MS%20Sentinel%20Maps%20(JSON)/linux-ssh-auth-fail.json) map files. These files provided a structured representation of the attack patterns and their associated data, 
enabling the creation of visualizations that effectively illustrated the cyber threats and their impact on the system.</b>


## Analysis and Interpretation
<b>Pre-Hardening Insights</b>:

- Before implementing security controls, the maps provide a stark visual of the network's vulnerabilities, with widespread unauthorized access attempts across all services. These insights validate the initial hypothesis of the honeynet's attractiveness to threat actors and emphasize the critical need for improved security measures.

- The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-15 14:51
Stop Time 2024-04-16 14:52

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 36264
| Syslog (Linux VM)                   | 2822
| SecurityAlert (Microsoft Defender for Cloud            | 11
| SecurityIncident (Sentinel Incidents)        | 107
| NSG Inbound Malicious Flows Allowed | 671


 <b>Post-Hardening Impact</b>:

 - After enhancing security protocols, subsequent monitoring showed a stark reduction in such incidents, proving the effectiveness of the hardening strategies implemented.

- The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-04-17 14:51
Stop Time	 2024-04-18 14:52


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 783
| Syslog (Linux VM)                   | 1
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

## Conclusion

The project successfully demonstrated how a targeted honeynet setup within Microsoft Azure could be used to simulate, detect, and respond to real-world cyber threats. The results emphatically showed how tailored security enhancements substantially mitigate potential cyber risks.

This project not only validates the effectiveness of strategic security implementations but also underscores the dynamic capabilities of Azure in managing and responding to cybersecurity challenges
