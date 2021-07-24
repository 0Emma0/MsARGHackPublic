# Azure DevOps + IaC 

## Challenge 4 – Azure Pipelines: Continuous Integration
[Back](challenge03.md) - [Home](README.md) - [Next](challenge05.md)

### Introduction

Great, we now have some infrastructure code, lets build it. In DevOps we automate this process using something called Continuous Integration. Take a moment to review the article below to gain a better understanding of what CI is. 

1. [What is Continuous Integration?](https://docs.microsoft.com/en-us/azure/devops/learn/what-is-continuous-integration)
2. [Introduction To Continuous Integration](https://www.youtube.com/watch?v=4gAe6JQi8L4)

The Four Pillars of Continuous Integration:

![Image alt text](../Images/CIPilars.PNG)


- A Version Control System manages changes to your source code over time.
- A Package Management System is used to install, uninstall and manage software packages.
- A Continuous Integration System merges all developer working copies to a shared mainline several times a day.
- An Automated Build Process creates a software build including compiling, packaging, and running automated tests.

Benefits of Continuous Integration:
- Improving code quality based on rapid feedback
- Triggering automated testing for every code change
- Reducing build times for rapid feedback and early detection of problems (risk reduction)
- Better management of technical debt and code analysis
- Reducing long, difficult, and bug-inducing merges
- Increasing confidence in codebase health long before production deployment
- Rapid feedback to the developer

2. How to use Azure Pipelines: 
   >  [Azure Pipelines - classic editor](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/pipelines-get-started?view=azure-devops&tabs=classic)

   >  [YAML schema reference](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=example)
3. [Key Concepts](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts?view=azure-devops)

### Discussion

>Have you tried to implement continuous integration in your organization? 

>>If you where successful, what lessons did you learn? 

>>If you were not successful, what were the challenges?


### Challenge

In Azure DevOps we use Azure Pipelines to automate our build process. 

1. Go to Pipelines, then click on "New Pipeline", on the Connect Tab use the **classic editor** to create a build pipeline using the ARM Templates( Look "Use the classic editor to create a pipeline without YAML,displayed in the lower part of the screen").
2. Select your repository and Master Branch.
3. On the Template page, select "Empty Job".
4. Edit the Pipeline Name.
5. On "Agent Job 1", Add task to Agent Job 1, on the "search box" type Publis Build Artifact and add it.
6. On the Task "Publish Artifact: drop", Change the display Name, for example: "Tier1-CI-AutomationAccount" and on "Path to publish" select the Folder of the Azure Resource.
7. Let's kick off a build manually to ensure that we have a working build. Save and Queue, Save and Run. 
8. Enable continuous integration on your build pipeline [Hint](https://azuredevopslabs.com/labs/azuredevops/continuousintegration/)
9. Set Brach Filters [Hint](https://docs.microsoft.com/en-us/azure/devops/pipelines/build/triggers?view=azure-devops&tabs=classic)

Create a Pipeline for the rest of the Azure Resources.

### Success Criteria

1. Your builds should complete without any errors.
1. You should have one build for each Tier1 Azure Resource.

[Back](challenge03.md) - [Home](README.md) - [Next](challenge05.md)
