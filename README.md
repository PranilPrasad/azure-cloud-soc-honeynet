# Azure Honeynet: Simulating Real-World Cyber Attacks
![Sa18KAF - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/d0e0b178-c99c-4ae4-aea1-cef47d22cf26)

## Introduction

 I am thrilled to present my latest project, which focuses on building a honeynet in Azure to simulate real-world cyber attacks. 
This project showcases my skills in Azure security, incident response, and environment hardening

## Objective
The main objective of this project was to [set up virtual machines that were intentionally vulnerable](https://github.com/AmiliaSalva/Azure-VM-Prep/blob/main/README.md) in the Azure infrastructure to attract and analyze cyber attacks. This helped me to better understand the tactics and techniques used by attackers, while also showcasing my ability to respond quickly and effectively to any identified issues.

## Technologies, Regulations, and Azure Components Employed:

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- [NIST SP 800-53 Revision 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final) for Security Controls
- [NIST SP 800-61 Revision 2](https://www.nist.gov/privacy-framework/nist-sp-800-61) for Incident Handling Guidance

## Methodology

- <b>*Creating the honeynet*</b>: I began by [deploying multiple vulnerable virtual machines](https://github.com/AmiliaSalva/Azure-VM-Prep/blob/main/README.md) in Azure, simulating an insecure environment.

- <b>*Monitoring and analysis*</b>: Azure was configured to ingest log sources from various resources into a log analytics workspace. Microsoft Sentinel was then used to build attack maps, trigger alerts, and create incidents based on the collected data.

- <b>*Security metrics measurement*</b>: I observed the environment for 24 hours, recording key security metrics while it was insecure. This provided a baseline to compare against after implementing remediation measures.

- <b>*Incident response and remediation*</b>: After addressing the incidents and identifying vulnerabilities, I began the process of hardening the environment by applying security best practices and Azure-specific recommendations.

- <b>*Post-remediation analysis*</b>: I re-observed the environment for another 24 hours to measure security metrics again, comparing the results with the initial baseline.


## Architecture Prior to Implementing Hardening Measures and Security Controls
![TFv2e8F - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/cebd8473-3ee8-4e88-90c0-996ff8626b7c)

<b>Before Hardening Measures and Security Controls:</b>

- In the "BEFORE" stage of the project, all resources were initially deployed with public exposure to the internet. This setup was intentionally insecure to attract potential cyber attackers and observe their tactics. The Virtual Machines had both their Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without utilizing any Private Endpoints for added security.

## Architecture After Implementing Hardening Measures and Security Controls
![2OpO4dC - Imgur](https://github.com/PranilPrasad/azure-cloud-soc-honeynet/assets/126536570/91fe191f-e9f2-4047-a002-57cb07111a77)
 <b>For the "AFTER" stage, I implemented a series of hardening measures and security controls to improve the environment's overall security posture. These improvements included:</b>

- <b>Network Security Groups (NSGs)</b>: I hardened the NSGs by blocking all inbound and outbound traffic, with the sole exception of my own public IP address. This ensured that only authorized traffic from a trusted source was allowed to access the virtual machines.

- <b>Built-in Firewalls</b>: I configured the built-in firewalls on the virtual machines to restrict access and protect the resources from unauthorized connections. This step involved fine-tuning the firewall rules based on the specific requirements of each VM, thereby minimizing the potential attack surface.

- <b>Private Endpoints</b>: To enhance the security of other Azure resources, I replaced the public endpoints with Private Endpoints. This ensured that access to sensitive resources, such as storage accounts and databases, was limited to the virtual network and not exposed to the public internet. As a result, these resources were protected from unauthorized access and potential attacks.

By comparing the security metrics before and after implementing these hardening measures and security controls, I was able to demonstrate the effectiveness of each step in improving the overall security posture of the Azure environment.

## Attack Maps Before Hardening / Security Controls
<br />


> <b>NOTE: The attack maps were generated by extracting data from a workbook utilizing pre-built [KQL .JSON](https://github.com/AmiliaSalva/Cloud-SOC-Project-Resources/blob/main/MS%20Sentinel%20Maps%20(JSON)/linux-ssh-auth-fail.json) map files. These files provided a structured representation of the attack patterns and their associated data, 
enabling the creation of visualizations that effectively illustrated the cyber threats and their impact on the system.</b>


 <br />
 <br />
 
- <b>This attack map demonstrates the consequences of leaving the Network Security Group (NSG) open, as it allowed for malicious traffic to flow unimpeded. This visualization underscores the importance of implementing proper security measures, such as restricting NSG rules, to prevent unauthorized access and minimize potential threats.</b>

![nsg-malicious-allowed-in](https://github.com/cesarias/Secure_Cloud/assets/126536570/d6695c8e-b06b-4a92-a56c-a3d7a13a7adf)

 <br />
 <br />
 
 - <b>This attack map highlights the numerous syslog authentication failures experienced by the Linux server I deployed, indicating that unauthorized access attempts were made from outisde. This serves as a reminder of the importance of securing Linux servers with strong authentication mechanisms and monitoring system logs for signs of intrusion attempts.</b>
 
![linux-ssh-auth-fail](https://github.com/cesarias/Secure_Cloud/assets/126536570/1d49f3f8-c354-4518-8bfc-b06badf7c294)

 <br />
 <br />
 
 - <b>This attack map showcases numerous RDP and SMB failures, illustrating the persistent attempts by potential attackers to exploit these protocols. The visualization emphasizes the need for securing remote access and file sharing services to protect against unauthorized access and potential cyber threats.</b>
 
![windows-rdp-auth-fail](https://github.com/cesarias/Secure_Cloud/assets/126536570/b7e957e4-5a57-4de0-a3db-d055e36b187a)

 <br />
 <br />

## Attack Maps After Hardening / Security Controls

> All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

 <br />
 <br />
 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-15 14:51
Stop Time 2024-04-16 14:52

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 36264
| Syslog (Linux VM)                   | 2822
| SecurityAlert (Microsoft Defender for Cloud            | 11
| SecurityIncident (Sentinel Incidents)        | 107
| NSG Inbound Malicious Flows Allowed | 671



## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
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

In conclusion, I set up a compact, but effective honeynet using Microsoft Azure's robust cloud infrastructure. Microsoft Sentinel was then utilized to trigger alerts and generate incidents based on the logs ingested from the implemented watch lists. Baseline metrics were recorded in the unprotected environment before the implementation of any security controls. Following this, a range of security measures were enforced to fortify the network against potential threats. Upon implementation of these controls, another set of measurements was taken.

The comparison of pre- and post-implementation metrics demonstrated a significant reduction in security events and incidents, which highlights the effectiveness of the enforced security controls.
It's important to mention that if the network's resources were extensively engaged by regular users, it's plausible that a higher number of security events and alerts could have been produced within the 24-hour timeframe post-security control implementation.
