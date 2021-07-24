# Azure DevOps + IaC 

## Challenge 3 – ARM Templates: Infrastructure as Code
[Back](challenge02.md) - [Home](README.md) - [Next](challenge04.md)

### Introduction

Infrastructure as Code is the process of managing and provisioning computing infrastructure and its configuration through machine-processable definition files. It treats the infrastructure as a software system, applying software engineering practices to manage changes to the system in a repeatable, structured and safe way.

Infrastructure as Code characteristics:

- Declarative.
- Single source of truth.
- Increase repeatability and testability.
- Decrease provisioning time.
- Rely less on availability of persons to perform tasks.
- Use proven software development practices for deploying infrastructure.
- Repeatable and testable.
- Faster to provision.
- Idempotent provisioning and configuration (calls can be executed repeatedly while producing the same result).
----
> Modularization of IaC: Divide automation assets into logical parts Databases, networks, storage, security, OS, and other components.

> Benefits of modularization.
>>Reuse of components.

>>Manage and maintain your code.

>>Sub-divide work and responsibilities across teams.

>>Troubleshooting.

> NOTE: We suggested work using Modularization. Identify What Azure resources have dependencies and are connected. For example, Storage Account Resource could have a ARM Template dedicated.
----

In DevOps we can automate the process of deploying the Azure Services we need with an Azure Resource Manager (ARM) template. Review the following articles.

1. [Azure Resource Manager overview](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)
2. [Create Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/how-to-create-template)
3. [Azure Resource Manager template functions](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-template-functions)


###



### Challenge
## Begin programming 

1. Create ARM Templates using Visual Studio or Visual Studio Code. You could start developing a Tier1 resources, like Vnet, Automation Account,Azure SQL Server and Storage Account. (We recommend create one ARM template file for each Azure resource).
2. Commit the code and push to Azure Repo. [Hint](https://docs.microsoft.com/en-us/azure/devops/repos/git/pushing?view=azure-devops&tabs=visual-studio)

> NOTE: Explore Github to get ARM Templates references. [Hint](https://github.com/Azure/azure-quickstart-templates/tree/master/101-storage-account-create), you could create the ARM Template in your IDE and [deploy](https://docs.microsoft.com/en-us/azure/azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy#deploy-project-to-azure) and test it from your workstation before to push Azure Repo.  

### Success Criteria

1. Having Tier1 Azure resources code in your Azure Repo. (VNet, Automation Account, Storage Account, Azure SQL Server)

[Back](challenge02.md) - [Home](README.md) - [Next](challenge04.md)

### Parcial Solution 
----
> [Here](CH03-parcialsolution.md) (Only use if it needed)
----
