# Azure DevOps + IaC 

## Challenge 5 – Azure Pipelines: Continuous Delivery
[Back](challenge04.md) - [Home](readme.md) - [Next](challenge06.md)

### Introduction

----
> "Continuous Delivery is a software development discipline where you build software in such a way that the software can be released to production at any time". 
>>“ by Martin Fowler”
----

In DevOps after we automate our build process, we want to automate our release process, we do this with a technique called Continuous Delivery. Please take a moment to review this brief article talking about why this is important. 

1. [What is Continuous Delivery?](https://docs.microsoft.com/en-us/azure/devops/learn/what-is-continuous-delivery)

Look at the eight principles of Continuous Delivery:
- The process for releasing/deploying software must be repeatable and reliable.
- Automate everything!
-  If something is difficult or painful, do it more often.
-  Keep everything in source control.
-  Done means “released.”
-  Build quality in!
-  Everybody has responsibility for the release process.
-  Improve continuously.

We need to move towards a situation where the value is not piled up and released all at once, but where
value flows through a pipeline. Just like in the picture, a piece of work is a marble. And only one piece of
work can flow through the pipeline at once. So work has to be prioritized in the right way. As you can see
the pipeline has green and red outlets. These are the feedback loops or quality gates that we want to
have in place.

![Image alt text](../Images/CD.PNG)


2. [How do release pipelines work?](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/?view=azure-devops#how-do-release-pipelines-work)


Release pipelines store the data about your pipelines, stages, tasks, releases, and deployments in Azure Pipelines.


![Azure Pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/_img/what-is-release-management/understand-rm-05.png?view=azure-devops)


3.[How do I use a release pipeline?](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/?view=azure-devops#how-do-i-use-a-release-pipeline)

You start using Azure Pipelines releases by authoring a release pipeline for your application. To author a release pipeline, you must specify the artifacts that make up the application and the release pipeline.
An artifact is a deployable component of your application. It is typically produced through a Continuous Integration or a build pipeline.

You define the release pipeline using stages, and restrict deployments into or out of a stage using approvals. You define the automation in each stage using jobs and tasks. You use variables to generalize your automation and triggers to control when the deployments should be kicked off automatically.

![Release Pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/_img/definition-01.png?view=azure-devops)

### Discussion

What's the difference between a release pipeline and a release? [Hint](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/releases?view=azure-devops)

### Challenge

In Azure DevOps we use an Azure Pipeline to release our infrastructure and application. In this challenge we will deploy our infrastructure and apps out to our dev environments. 

1. Create a new Release Pipeline, go to Pipelines, then "Releases". Click on "New Pipeline" and after that Select  "Empty Job".
2. Change the name of Stage, the new name should be "DEV".
3. Rename the name of the Release Pipeline from "New release pipeline" to "MsARGHack".
4. Add the artifacts created in previous Challenges. (They should be Vnet, Automation Account, Storage Account and Azure SQL Server or just the repo you are using.)
5. To start off our deployment will only have one stage, lets call it `Dev`, Change the name of Stage, the new name should be "DEV".
6. ***The output of our CI Build pipeline will be the input artifact to our CD Release pipeline, add it. ***
7. Enable Continuous deployment so that each time the CI pipeline finishes successfully, this pipeline will start. 
8. On the tasks for our `Dev` stage, Add Task to the Agent Job. For ARM Templates, should you use "Azure resource group deployment"
9. Set your Team Azure subscription, the Resource Group and Location.
10. On "Template" Seccion, get the ARM Templates for an Azure resource, like "Vnet".
11. Populate the parameters of ARM Templates with the respective values.
12. Manually kick off a release and check that your VNET got deployed to your dev instance. 
13. If everything worked, go ahead and the remaining Azure Resouces. (Storage Account, Automation Account, Azure SQL Server)
 

### Success Criteria

1. You should have all Tier1 resources deployed.
1. Make a small change to your code (for example: add a new subnet), it should automatically trigger a build and release to your `Dev` environment.
   

### Optional

1. Enable Pre-deployment Approvals. [Hint](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/approvals/approvals?view=azure-devops)
2. Use Variable Groups for each environment, for example for "Dev" [Hint](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups?view=azure-devops&tabs=yaml)

[Back](challenge04.md) - [Home](readme.md) - [Next](challenge06.md)
