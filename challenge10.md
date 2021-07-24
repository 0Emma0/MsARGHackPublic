# Azure DevOps + IaC

## Challenge 10 – Creating VMs with Availability Set - Tier2 components
[Back](challenge09.md) - [Home](/readme.md) - [Next](Solutions.md)


### Introduction

Azure Virtual Machines (VM) is one of several types of on-demand, scalable computing resources that Azure offers. Typically, you choose a VM when you need more control over the computing environment than the other choices offer.
An Azure VM gives you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it. However, you still need to maintain the VM by performing tasks, such as configuring, patching, and installing the software that runs on it.
What do I need to think about before creating a VM?

There are always a multitude of design considerations when you build out an application infrastructure in Azure. These aspects of a VM are important to think about before you start:

- The names of your application resources
- The location where the resources are stored
- The size of the VM
- The maximum number of VMs that can be created
- The operating system that the VM runs
- The configuration of the VM after it starts
- The related resources that the VM needs

The resources in this table are used by the VM and need to exist or be created when the VM is created.

- Resource	Required	Description
- Resource group	Yes	The VM must be contained in a resource group.
- Storage account	Yes	The VM needs the storage account to store its virtual hard disks.
- Virtual network	Yes	The VM must be a member of a virtual network.
- Public IP address	No	The VM can have a public IP address assigned to it to remotely access it.
- Network interface	Yes	The VM needs the network interface to communicate in the network.
- Data disks	No	The VM can include data disks to expand storage capabilities.

1. [What is Azure Load Balancer?](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)
2. [Very simple deployment of a Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
3. [Create Availability Set](https://github.com/Azure/azure-quickstart-templates/tree/master/101-availability-set-create-3FDs-20UDs)

Availability sets

An availability set is a logical grouping of VMs within a datacenter that allows Azure to understand how your application is built to provide for redundancy and availability. We recommended that two or more VMs are created within an availability set to provide for a highly available application and to meet the 99.95% Azure SLA. There is no cost for the Availability Set itself, you only pay for each VM instance that you create. When a single VM is using Azure premium SSDs, the Azure SLA applies for unplanned maintenance events.

In an availability set, VMs are automatically distributed across these fault domains. This approach limits the impact of potential physical hardware failures, network outages, or power interruptions.

![AvailabilitySet](https://docs.microsoft.com/en-us/azure/includes/media/virtual-machines-common-manage-availability/md-fd-updated.png)


### Challenge

The following tasks will be done in this scenario:

1. Using ARM Templates you should create two Virtual Machines [Hint](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-multiple) with Availability set, they should be add to the Loadbalancer created on previous steps. [Hint](https://stackoverflow.com/questions/54551804/adding-an-existing-vms-to-the-azure-load-balancer-through-arm-templates)
2. Also, The VMs should be register to the DSC Node Configuration created previously. [Hint](../Help/VM.json) ( Once the Vms are joined to the Azure DSC, its will set all the configurations and set up the web application on the virtual machines).
3. Once the ARM Template are created, push it to Azure Repo. (we recommend create a folder called VMs on Azure Repo and push the code there).
4. Create the Artifact doing a build as you done it on the previous steps.
5. Once the Artifact are ready, on Release Pipeline add a Task to Agent Job, search "Azure resource group deployment" and add it.
6. Set the Template box with the VMs ARM Template and overwrite the Parameters.

### Success Criteria

1. You should have created Two VMs with an Availability Set and the Application working on it.
2. :smile: You should have all the enviroment working :smile:


### Parcial Solution 
----
> [Here](CH10-parcialsolution.md) (Only use if it needed)
----

[Back](challenge09.md) - [Home](../../readme.md) - [Next](Solutions.md)
