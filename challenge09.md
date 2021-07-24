# Azure DevOps + IaC

## Challenge 9 – Creating Load Balancers using ARM Templates - Tier2 components
[Back](challenge08.md) - [Home](/readme.md) - [Next](challenge10.md)

### Introduction

An Azure load balancer is a Layer-4 (TCP, UDP) load balancer. The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set. Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.


You can configure a load balancer to:

- Load balance incoming Internet traffic to virtual machines (VMs). We refer to a load balancer in this scenario as an Internet-facing load balancer.
- Load balance traffic between VMs in a virtual network (VNet), between VMs in cloud services, or between on-premises computers and VMs in a cross-premises virtual network. We refer to a load balancer in this scenario as an internal load balancer (ILB).
- Forward external traffic to a specific VM instance.

![LoadBalancer](https://docs.microsoft.com/en-us/azure/includes/media/load-balancer-get-started-internet-scenario-include/scenario-classic.png)



1. [What is Azure Load Balancer?](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)
2. [Load Balancer components](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview#load-balancer-components)

### Challenge

The following tasks will be done in this scenario:

1. Using ARM templates create a load balancer that receives network traffic on port 80 and send load-balanced traffic to virtual machines.
2. Create NAT rules for remote desktop access for virtual machines behind the load balancer. [Hint1](https://docs.microsoft.com/en-us/azure/templates/microsoft.network/2019-04-01/loadbalancers), [Hint2](../Images/NatLB.PNG)
3. Create health probes. [Hint](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-custom-probe-overview)
4. Once the ARM Template are created, push it to Azure Repo. (we recommend create a folder called LoadBalancer on Azure Repo and push the code there).
5. Create the Artifact doing a build as you done it on the previous steps.
6. Once the Artifact are ready, on Release Pipeline add a Task to the Agent Job, search "Azure resource group deployment" and add it.
7. Set the "Template" box with the Load Balancer ARM Template and override the Parameters.

### Success Criteria

1. You should have a Load Balancer Deployed.


### Parcial Solution 
----
> [Here](CH09-parcialsolution.md) (Only use if it needed)
----



[Back](challenge08.md) - [Home](../../readme.md) - [Next](challenge10.md)
