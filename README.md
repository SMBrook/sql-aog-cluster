# # Create an Always On Availability Group with SQL Server 2019 replica virtual machines

![Azure Public Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/PublicLastTestDate.svg)
![Azure Public Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/PublicDeployment.svg)

![Azure US Gov Last Test Date](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/FairfaxLastTestDate.svg)
![Azure US Gov Last Test Result](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/FairfaxDeployment.svg)

![Best Practice Check](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/BestPracticeResult.svg)
![Cred Scan Check](https://azurequickstartsservice.blob.core.windows.net/badges/application-workloads/sql/sqlvm-alwayson-cluster/CredScanResult.svg)

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fapplication-workloads%2Fsql%2Fsqlvm-alwayson-cluster%2Fazuredeploy.json)  
[![Deploy To Azure US Gov](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.svg?sanitize=true)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fapplication-workloads%2Fsql%2Fsqlvm-alwayson-cluster%2Fazuredeploy.json)
[![Visualize](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/visualizebutton.svg?sanitize=true)](http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fapplication-workloads%2Fsql%2Fsqlvm-alwayson-cluster%2Fazuredeploy.json)



## Solution overview

This template uses the PowerShell DSC extension to deploy a fully configured Always On Availability Group with Windows Server 2019 and SQL Server 2019 replicas.

This template creates the following resources:

+   1 Virtual Network
+   4 Azure storage accounts
    +    1 for domain controller virtual machines
    +    1 for SQL Server virtual machines
    +    1 for Failover Cluster File Share Witness
    +    1 for deployment diagnostics
+   1 internal load balancer
+   1 external load balancer
+   3 virtual machines in a Windows Server Cluster
    +    3 SQL Server 2014 Enterprise edition replicas with an availability group
    +    2 domain controller virtual machines replicas for a new Forest and Domain
+   2 Availability Sets
    +     1 for domain controller virtual machines
    +     1 for SQL Server and Witness virtual machines
+   1 public IP addresses for RDP access

`Tags: SQL Server, AlwaysOn, High Availability, Cluster `

## Notes

+ 	File Share Witness and SQL Server VMs are from the same Availability Set and currently there is a constraint for mixing DS-Series machine, DS_v2-Series machine and GS-Series machine into the same Availability Set. If you decide to have DS-Series SQL Server VMs you must also have a DS-Series File Share Witness; If you decide to have GS-Series SQL Server VMs you must also have a GS-Series File Share Witness; If you decide to have DS_v2-Series SQL Server VMs you must also have a DS_v2-Series File Share Witness.

+	The default settings for SQL Server storage are to deploy using **premium storage**, the AD witness uses a P10 Disk and the SQL VMs use P30 disks, these sizes can be changed by changing the relevant variables. In addition there is a P10 Disk used for each VMs OS Disk.

+ 	In default settings for compute require that you have at least 15 cores of free quota to deploy.

+ 	The images used to create this deployment are
	+ 	DC - Latest Windows Server 2019 Image
	+ 	SQL Server - Latest SQL Server 2019 on Windows Server 2019 Image
	
+ 	Once deployed access can be gained by the public IP address of Primary Domain Controller


