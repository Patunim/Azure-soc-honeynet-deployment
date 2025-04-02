Azure SOC Honeynet Deployment

Goal of the Project: Build a small honeynet in Azure to simulate cyber-attacks and measure security metrics, both before and after applying security controls.

Components Used:
Virtual Network (VNet)
Network Security Group (NSG)
Virtual Machines: 2 Windows VMs and 1 Linux VM.
Log Analytics Workspace
Azure Key Vault
Azure Storage Account
Microsoft Sentinel

Deployment Details: The environment was initially set up with VMs running insecure configurations—Windows and Linux—deployed within a Virtual Network (VNet) and a Network Security Group (NSG) to control access. Logs were ingested into a Log Analytics Workspace for tracking, and Microsoft Sentinel was integrated to manage alerts and incidents.

Metrics Collection:
Before implementing security measures, the environment was vulnerable. Metrics were collected over 24 hours:


| Start Time           | Stop Time            | Metric                   | Count |
|----------------------|----------------------|--------------------------|-------|
| 2024-04-12 10:00:00  | 2024-04-13 10:00:00  | SecurityEvent            | 13495 |
| 2024-04-12 10:00:00  | 2024-04-13 10:00:00  | Syslog                   | 1120  |
| 2024-04-12 10:00:00  | 2024-04-13 10:00:00  | SecurityAlert            | 15    |
| 2024-04-12 10:00:00  | 2024-04-13 10:00:00  | SecurityIncident         | 112   |
| 2024-04-12 10:00:00  | 2024-04-13 10:00:00  | AzureNetworkAnalytics_CL | 945   |



Key points: The initial data shows 13,495 SecurityEvents on Windows, 1,120 Syslog events on Linux, 15 SecurityAlerts, and 112 incidents created. There was also a substantial amount of malicious traffic recorded—945 instances of malicious flow detected within the network.

Applying Security Controls:
After security controls were applied, metrics were collected again after another 24-hour period:

| Start Time           | Stop Time            | Metric                   | Count |
|----------------------|----------------------|--------------------------|-------|
| 2024-04-14 09:30:00  | 2024-04-15 09:30:00  | SecurityEvent            | 5123  |
| 2024-04-14 09:30:00  | 2024-04-15 09:30:00  | Syslog                   | 45    |
| 2024-04-14 09:30:00  | 2024-04-15 09:30:00  | SecurityAlert            | 2     |
| 2024-04-14 09:30:00  | 2024-04-15 09:30:00  | SecurityIncident         | 4     |
| 2024-04-14 09:30:00  | 2024-04-15 09:30:00  | AzureNetworkAnalytics_CL | 16    |


Post-hardening, the metrics show a dramatic reduction. SecurityEvents dropped to 5,123 from 13,495. Syslog events went from 1,120 to just 45. SecurityAlerts were reduced to 2, and only 4 incidents were created—down from 112. Malicious flows into the network almost vanished, dropping from 945 to just 16.

Architecture:
Before security controls, the architecture was unprotected. After applying security measures, the environment was hardened with more stringent controls. A tighter network security configuration, along with better monitoring from Sentinel, ensured that malicious activity was blocked or flagged early.

Attack Maps: The attack maps before hardening showed significant activity. Post-hardening, no malicious activity was recorded, and the attack maps were empty, which indicates that the security measures worked as expected.

Conclusion:

This project focused on setting up a honeynet in Azure, simulating potential cyber-attacks, and then improving security by applying effective measures. The data from before and after hardening demonstrated that the security controls were successful in reducing security events, incidents, and malicious traffic.
