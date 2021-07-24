# Azure DevOps + IaC 

## Challenge 7 – Copy App Files to Storage Account
[Back](challenge06.md) - [Home](/readme.md) - [Next](challenge08.md) 

### Introduction

The objective of this Challenge is Copy the APP.Zip to the Storage Account Conteiner. Why? The idea is that Azure DSC invokes the Storage Account for downloading the App and set on the IIS.

1. [What is a Storage Account?](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview)
2. [What is SAS](https://docs.microsoft.com/es-es/azure/storage/common/storage-sas-overview)
3. [How it works](https://docs.microsoft.com/es-es/azure/storage/common/storage-sas-overview#how-a-shared-access-signature-works)

### Challenge


1. On the Release Pipeline created previously, Add a new task to the agent Job.
2. Add "Azure file copy".
3. On the "Source" field, browse and select the App.zip build in the last challenge. [Hint](Images/AzureBlobFileCopy1.PNG)
4. Set the  Name of the Conteiner Name where "App.zip" will be saved.
5. On Output section, type "URI" on "Storage Container URI" and SAS Token on "Storage Container SAS Token"

![Output](/Images/Output.PNG)

6. The Output of this task are two variables "URI" and "SAS Token". They will use them by Azure DSC later.

### Success Criteria

1. Run the Pipeline and the App.zip should be on the Storage Account.


[Back](challenge06.md) - [Home](/readme.md) - [Next](challenge08.md) 
