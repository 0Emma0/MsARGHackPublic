# Azure DevOps + IaC 

## Challenge 6 – Build Web App
[Back](challenge05.md) - [Home](/readme.md) - [Next](challenge07.md) 

### Introduction

The pupose of any DevOps team is provide value to the end user continuously so to achive that in this exercise we are going to build a CI pipeline for the web application.
The Web App was developed in ASP .NET 4.5 and is an eCommerce app based on [Parts Unlimited](https://github.com/microsoft/PartsUnlimited) demo app published by Microsoft in GitHub.


### Challenge

A. Create a CI pipeline in Azure DevOps to generate a Zip file containing the web site ready to be deployed in the web servers of the DEV enviroment that we are going to create with the ARM Templates.<br>
B. Compile the Database project to collect the DACPAC file to latter create and populate the Azure SQL Database. 
C. Modify the release pipeline created before to add a task to run the DACPAC against the Azure SQL Server created in the [challenge 3](challenge03.md) 

1. In Azure DevOps create a new Pipeline (build).
2. Choose using the classic editor (not YAML).
3. In the next step choose the git repo where you cloned the web app and click the 'Continue' button.
4. Select the ASP .NET template .
5. In the parameters section use the '...' button to select the solution file of the web app (PartsUnlimited.sln).
6. Name you pipeline (build) like 'Tier3-CI-App' or give it the name you wish.
7. Disable the task 'Test Assemblies' because we are not going to focus in Unit Testing today.
8. Add a new 'Archive' task after the 'Build' task to compress the result of the compilation (the web site).
	- In the 'Root folder or file to archive' you need to provide the path to the PackageTmp folder where the web site is published during the build process. E.g.: 'Code/PartsUnlimited/src/PartsUnlimitedWebsite/obj/Release/Package/PackageTmp'. 
	- Disable 'Prepend root folder name to archive paths'. 
	- In the 'Archive file to create' prop set this value '$(build.artifactstagingdirectory)\Site\App.zip'. 
	- Enable the option 'Replace existing archive'. 
9. Add a new 'Copy Files' task after the 'Archive' task.
	- In the 'Source folder' property you need to provide the path where the DACPAC file is created during the build process. E.g: 'Code/PartsUnlimited/PartsUnlimited.Database/bin/Release'. 
	- In the 'Contents' property put '*.dacpac'
	- In the 'Target folder' put this value '$(build.artifactstagingdirectory)\Db'.
10. Add the build pipeline you have just created as an artifact of the release pipeline so you can access the App.zip and PartsUnlimited.Database.dacpac.
11. In the release pipeline (not the build pipeline you ended in the previous step) add a new 'Azure SQL Database deployment' task.
	- In the property 'Authentication Type' select 'SQL Server Authentication'
	- In the property 'Azure SQL Server'  put the name of the Azure SQL Server you have chosen. Tip: use variables here.
	- In the property 'Database' put the name of the database as you may find in the connection string in the web app's web.config. Tip: use variables here.
	- In the property 'Login' set the user name for the SA acount you configured when created the Azure SQL Server. Tip: use variables here.
	- In the property 'Password' set the password of the login user. Tip: use variables here.
	- In the property 'DACPAC File' use the '...' button to navigate the relases artifacts and select the file 'PartsUnlimited.Database.dacpac'.



<p>At the end your pipeline should look like this:</p>

![At the end your pipeline should look like this](https://dev.azure.com/MSLatamHack/6ce9b579-4466-41e8-8280-8765e02beb57/_apis/git/repositories/c27a3e26-944a-4abc-bb02-147219cd0995/items?path=%2FImages%2Fbuild_pipeline.JPG&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)

### Success Criteria

1. Run your build and check it completes sucessfully.
2. Check after the build finishes that you have two artifacts, the .zip file with the web site and the .dacpac file for the database.
		- Your artifacts should look like ![this](https://dev.azure.com/MSLatamHack/6ce9b579-4466-41e8-8280-8765e02beb57/_apis/git/repositories/c27a3e26-944a-4abc-bb02-147219cd0995/items?path=%2FImages%2Fbuild_artifacts.JPG&versionDescriptor%5BversionOptions%5D=0&versionDescriptor%5BversionType%5D=0&versionDescriptor%5Bversion%5D=master&resolveLfs=true&%24format=octetStream&api-version=5.0)
3. When you run the release pipeline the database gets created with its schema and initial data as needed by the web application.


[Back](challenge05.md) - [Home](/readme.md) - [Next](challenge07.md) 
