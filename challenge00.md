# Azure DevOps + IaC: 

## Challenge 0 - Setup
[Home](README.md) - [Next](challenge01.md)

### Introduction

DevOps is a very broad topic and you have lots of choices when it comes to the tools that you use. In this challenge you will setup your computer and cloud environment with the minimum required tools. 

### Challenge

In this challenge we will setup the core components needed to complete this Azure DevOps Hackathon.


1. Log into the [Azure Portal](https://portal.azure.com) using the user provide by Microsoft and confirm that you have an active subscription where you can deploy cloud services
2. Invite the rest of your Team and assign the role of Global Admin of AAD and Owner of Subscription. [Reference1](https://docs.microsoft.com/en-us/azure/active-directory/b2b/b2b-quickstart-add-guest-users-portal) [Reference2](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/active-directory-users-assign-role-azure-portal) [Reference3](https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal)
3. Log into [Azure DevOps](https://dev.azure.com/) using the **SAME** account as you use to log into your Azure Subscription and create a new project named `TeamX-Hackathon`, E.G "ArgTeam1Hackathon". The project should be `Private`, use `Git` version control and an `Basic Work item` process ([hint](https://docs.microsoft.com/en-us/azure/devops/user-guide/sign-up-invite-teammates))
   1. HINT: Look under Advanced to select your version control and work item process. You cannot change these after you create your project. 
4. Grant to the other members of your team, contributor access to your project in Azure DevOps [Add](https://docs.microsoft.com/en-us/azure/devops/organizations/security/add-users-team-project).

5. Download and install [Git SCM](https://git-scm.com/download) if you don't have it or a similar Git client installed
6. Download and install [Visual Studio](https://visualstudio.microsoft.com/es/vs/) or [Visual Studio CODE](https://code.visualstudio.com/download) if you don't have them

   

### Success Criteria

1. All the Team members Team should be able to log in to the Azure Portal and the Azure DevOps Portal.
   
[Home](README.md) - [Next](challenge01.md)