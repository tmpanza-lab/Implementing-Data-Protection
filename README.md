# Implementing Data Protection

## Objective

This Lab is aimed to provide hands-on experience implementing Azure cloud data protection strategies, including backup, monitoring, and replication for High Availability (HA) and Resiliency. I learned about backup and recovery of Azure VMs, creating Recovery Services Vault and a backup policies for Azure VMs. Finally I also learned about disaster recovery using Azure Site Recovery.


## Architecture diagram
![image](https://github.com/user-attachments/assets/fcc3232f-2e31-4fee-af0f-88d94f0e60b2)
 


### Job Skills

- Using a template to provision an infrastructure.
- Creating and configuring a Recovery Services vault.
- Configuring Azure virtual machine-level backup.
- Monitoring Azure Backup.
- Enabling virtual machine replication.


### Tools Used

- Azure portal - https://portal.azure.com


## Steps



## Task 1: Use a template to provision an infrastructure
In this task, I will use a template to deploy a virtual machine. The virtual machine will be used to test different backup scenarios.
1.	Download the \Allfiles\Lab10\ lab files.
![image](https://github.com/user-attachments/assets/4ab9d657-4777-4bdd-8d85-495a387d9fd9)
 
2.	Sign in to the Azure portal - https://portal.azure.com.
3.	Search for and select Deploy a custom template.
![image](https://github.com/user-attachments/assets/3bca048e-2d1c-4e18-8386-1291d7a7d6ab)
 
4.	On the custom deployment page, select Build you own template in the editor.
![image](https://github.com/user-attachments/assets/4954db51-6af8-4ac0-9262-f1f14abc6d9b)
 
5.	On the edit template page, select Load file.
6.	Locate and select the \Allfiles\Lab10\az104-10-vms-edge-template.json file and select Open.
![image](https://github.com/user-attachments/assets/d46a8626-587d-48a3-b0f9-88b607f70cb3)
 
7.	Save your changes.
8.	Select Edit parameters and then Load file.
9.	Load and select the \Allfiles\Lab10\az104-10-vms-edge-parameters.json file.
![image](https://github.com/user-attachments/assets/d2a2623c-8212-4352-b8dc-ee395f761139)
 
10.	Save your changes.
11.	Use the following information to complete the custom deployment fields, leaving all other fields with their default values:
![image](https://github.com/user-attachments/assets/7c3f9e1c-03a6-487c-873c-d55d70139493)
![image](https://github.com/user-attachments/assets/82788377-1d4e-4172-b828-755070d9a831)
![image](https://github.com/user-attachments/assets/7bf671ad-cfd2-45f2-a503-81c1b0336e49)
 
 
 
12.	Select Review + Create, then select Create.


## Task 2: Create and configure a Recovery Services vault

In this task, I will create a Recovery Services vault. A Recovery Services vault provides storage for the virtual machine data.
1.	In the Azure portal, search for and select Recovery Services vaults and, on the Recovery Services vaults blade, click + Create.
 ![image](https://github.com/user-attachments/assets/536a6fc8-04dd-4b3c-9471-aec6b79aa826)

2.	On the Create Recovery Services vault blade, specify the following settings:
![image](https://github.com/user-attachments/assets/616e667b-9532-4a45-9c80-4e272c96aa5f)
 
3.	Click Review + Create, ensure that the validation passes and then click Create.
![image](https://github.com/user-attachments/assets/d2680b6f-9af1-4a78-8bf1-5cf2c95d8bcc)
 
4.	When the deployment is completed, click Go to Resource.
5.	In the Settings section, click Properties.
![image](https://github.com/user-attachments/assets/0c074478-d13b-49ce-82d8-f862f3f7bb34)
 
6.	Select the Update link under Backup Configuration label.
7.	On the Backup Configuration blade, review the choices for Storage replication type. Leave the default setting of Geo-redundant in place and close the blade.
![image](https://github.com/user-attachments/assets/2f7ff83c-401e-4b61-a488-2f6702cbc4b2)
 
8.	Select the Update link under Security Settings > Soft Delete and security settings label.
![image](https://github.com/user-attachments/assets/700a0206-4331-4a25-bd36-23610d9ed740)
 
9.	On the Security Settings blade, note that Soft Delete (For workload running in Azure) is Enabled. Notice the soft delete retention period is 14 days.
![image](https://github.com/user-attachments/assets/2df6a721-9a20-4557-9994-a11bd7850072)
 


## Task 3: Configure Azure virtual machine-level backup

In this task, I will implement Azure virtual-machine level backup. As part of a VM backup, I will need to define the backup and retention policy that applies to the backup. Different VMs can have different backup and retention policies assigned to them.

1.	On the Recovery Services vault blade, click Overview, then click + Backup.
2.	On the Backup Goal blade, specify the following settings:
![image](https://github.com/user-attachments/assets/73cf73f8-cc51-4ee7-a1b5-5f0f17972af6)
 
3.	Select Backup.
4.	Notice there a two Policy sub types: Enhanced and Standard. Review the choices and select Standard.
![image](https://github.com/user-attachments/assets/6ee402c7-0d61-468f-b81b-dd57fa141c00)
 
5.	In Backup policy, select Create a new policy.
6.	Define a new backup policy with the following settings (leave others with their default values):
![image](https://github.com/user-attachments/assets/45d133d5-e905-4bf4-b74d-8416863f24df)
 
7.	Click OK to create the policy and then, in the Virtual Machines section, select Add.
![image](https://github.com/user-attachments/assets/e4161800-3238-4be3-8d4f-097e529778f2)
 
8.	On the Select virtual machines blade, select az-104-10-vm0, click OK, and then back on the Backup blade, click Enable backup.
![image](https://github.com/user-attachments/assets/ecafd513-2fdc-4d76-80ac-f444bbe38c78)
![image](https://github.com/user-attachments/assets/5fe47f4e-82e1-4a2b-8bb6-ef93cd04631a)
 
 
9.	In the Protected items section, click Backup items, and then click the Azure virtual machine entry.
![image](https://github.com/user-attachments/assets/e20b8d49-dae1-440c-afc4-73362f2861bd)
 
10.	Select the View details link for az104-10-vm0, and review the values of the Backup Pre-Check and Last Backup Status entries.
![image](https://github.com/user-attachments/assets/17ffc6c4-f2da-44e9-86d1-77cf9dc5a051)
 
11.	Select Backup now, accept the default value in the Retain Backup Till drop-down list, and click OK.
![image](https://github.com/user-attachments/assets/a2c41f6b-ab1e-4ca2-ba13-bb060c9b759f)
![image](https://github.com/user-attachments/assets/0e80eca8-2a5b-45e6-a3aa-c3c340fd2646)
 
 


## Task 4: Monitor Azure Backup

In this task, I will deploy an Azure storage account. Then you will configure the vault to send the logs and metrics to the storage account. This repository can then be used with Log Analytics or other third-party monitoring solutions.

1.	From the Azure portal, search for and select Storage accounts.
2.	On the Storage accounts page, select Create.
3.	Use the following information to define the storage account, then and select Review + create.
 ![image](https://github.com/user-attachments/assets/48e2af77-6e27-438c-972b-42d93d03871e)

4.	Select Create.
5.	Search and select your Recovery Services vault.
6.	In the Monitoring blade, select Diagnostic Settings and then select Add diagnostic setting.
 ![image](https://github.com/user-attachments/assets/fe34e491-196c-4fef-8e20-c5cfe04b1245)

7.	Name the setting Logs and Metrics to storage.
8.	Place a checkmark next to the following log and metric categories:
1.	Azure Backup Reporting Data
2.	Addon Azure Backup Job Data
3.	Addon Azure Backup Alert Data
4.	Azure Site Recovery Jobs
5.	Azure Site Recovery Events
6.	Health
![image](https://github.com/user-attachments/assets/2323ffe5-f003-4941-8e67-ab11d88a5c1a)
 
9.	In the Destination details, place a checkmark next to Archive to a storage account.
10.	In the Storage account drop-down field, select the storage account that you deployed earlier in this task.
![image](https://github.com/user-attachments/assets/d8fa23fd-461a-46fd-ab74-a4aa1ac010af)
 
11.	Select Save.
12.	Return to your Recovery Services vault, in the Monitoring blade select Backup jobs.
13.	Locate the backup operation for the az104-10-vm0 virtual machine.
![image](https://github.com/user-attachments/assets/5f699ee9-65e5-40fa-9694-e2c485bf7441)
 
14.	Review the details of the backup job.


## Task 5: Enable virtual machine replication

1.	In the Azure portal, search for and select Recovery Services vaults and, on the Recovery Services vaults blade, click + Create.
2.	On the Create Recovery Services vault blade, specify the following settings:
![image](https://github.com/user-attachments/assets/eb6b8ee0-6396-4cf5-83ed-6eb596549d0d)
 
3.	Click Review + Create, ensure that the validation passes and then click Create.
4.	Search for and select the az104-10-vm0 virtual machine.
5.	In the Backup + Disaster recovery blade, select Disaster recovery.
6.	Select Enable replication.
7.	On the Basics tab, notice the Target region.
![image](https://github.com/user-attachments/assets/6e655082-5420-4c82-809c-e9c574d84a58)
 
8.	Move to the Advanced settings tab. Resource selections have been made for you. It is important to review them.
9.	Verify your subscription, vm resource group, virtual network, and availability (take the default) settings.
![image](https://github.com/user-attachments/assets/3ab7cb75-1df9-4049-9789-51ba8f9d4c23)
 
10.	In Storage settings select Show details.
![image](https://github.com/user-attachments/assets/51a1a2d9-5733-4d81-bc27-d0997615204a)
 
11.	In Replication settings select Show details. Notice your recovery resources vault in region 2 was automatically selected.
![image](https://github.com/user-attachments/assets/71c1d594-2fbb-4f07-8a60-af2eb98fbc98)
 
12.	Select Review + Start replication and then Enable replication.
![image](https://github.com/user-attachments/assets/5dba9217-2a98-46e6-b15e-bbbbdc4d1bd6)
 
13.	Once the replication is complete, search for and locate your Recovery Services Vault, az104-rsv-region2. You may need to Refresh the page.
14.	In the Protected items section, select Replicated items.
15.	Check that the virtual machine is showing as healthy for the replication health. Note that the status will show the synchronization (starting at 0%) status and ultimately show Protected after the initial synchronization completes.
![image](https://github.com/user-attachments/assets/62fac3ed-32d2-41a5-a562-d14a8885b8b7)
 
16.	Select the virtual machine to view more details.
![image](https://github.com/user-attachments/assets/a6ce71e8-9272-49ee-bd34-e8f8130a4ad5)





