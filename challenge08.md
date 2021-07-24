# Azure DevOps + IaC

## Challenge 8 – Azure DSC
[Back](challenge07.md) - [Home](readme.md) - [Next](challenge09.md)

### Introduction

Cloud has driven the popularity of these tools by making it easy to create large numbers of new server instances which then need to be configured and updated. Using scripts and automation to create, provision, and update servers is not especially new, but a new generation of tools has emerged over the past decade

Goals for Automated Management

- A new server can be completely provisioned on demand, without waiting more than a few minutes.
- A new server can be completely provisioned without human involvement—for example, in response to events.
- When a server configuration change is defined, it is applied to servers without human involvement.
- Each change is applied to all the servers it is relevant to, and is reflected in all new servers provisioned after the change has been made.
- The processes for provisioning and for applying changes to servers are repeatable, consistent, self-documented, and transparent.
- It is easy and safe to make changes to the processes used to provision servers and change their configuration.
- Automated tests are run every time a change is made to a server configuration definition, and to any process involved in provisioning and modifying servers.
- Changes to configuration, and changes to the processes that carry out tasks on an infrastructure, are versioned and applied to different environments, in order to support controlled testing and staged release strategies.

1. [The what, why and how of Azure Automation Desired State Configuration (DSC)](https://azure.microsoft.com/es-mx/blog/what-why-how-azure-automation-desired-state-configuration/) 
2. [Introduction to the Azure Desired State Configuration extension handler](https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/dsc-overview)
3. [Azure Automation State Configuration Overview](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
4. [Import Modules into your Azure Automation](https://docs.microsoft.com/en-us/azure/automation/shared-resources/modules#import-modules)


### Challenge

In this challenge we will first create a Powershell File for Configuration DSC, then create other powershell file to import the Automation Module needed and compile the Configuration DSC File.

1. Create a Powershell file in your workstation called "WebServer.ps1".
2. Insert the code below:

```
configuration WebServer
{
    
    param(

     [string] $SAS

    )
   
   $LocalPath = "C:\Files"
   $LocalPathZipApp = "C:\Files\app.zip"
   $DestinationApp = "C:\inetpub\wwwroot"
   
   
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'
    Import-DscResource -ModuleName xPSDesiredStateConfiguration
    Import-DscResource -ModuleName  xNetworking
    


    Node localhost
    {   
    #crea carpeta
    File Sources{
    Type = “Directory”
    Ensure = “Present”
    DestinationPath = $LocalPath
    }

    #Descarga zip desde el SA  y guarda en la carpeta    
    xRemoteFile Downloader{
    Uri = $SAS
    DestinationPath = $LocalPathZipApp 
    DependsOn = "[File]Sources"
    }
    #descomprime
    Archive ArchiveExample {
    Ensure = "Present"
    Path = $LocalPathZipApp 
    Destination = $DestinationApp
    DependsOn = "[xRemoteFile]Downloader"
    }

    #Install IIS
    WindowsFeature ASP { 
    Ensure = "Present"
    Name = "Web-Asp-Net45"
	} 
        
    WindowsFeature InstallIIS {
    Name = "Web-Server"
    Ensure = "Present"
    DependsOn = "[WindowsFeature]ASP"
	}

    WindowsFeature IISConsole{
    Ensure = "Present"
    Name = "Web-Mgmt-Console"
    DependsOn = "[WindowsFeature]InstallIIS"
	}

    WindowsFeature IISScriptingTools{
    Ensure = "Present"
    Name = "Web-Scripting-Tools"
    DependsOn = "[WindowsFeature]InstallIIS"
	}
   
    WindowsFeature EnableWinAuth {
    Name = "Web-Windows-Auth"
    Ensure = "Present"
    DependsOn = "[WindowsFeature]InstallIIS"
	}

    WindowsFeature StaticContent {
    Name = "Web-Static-Content"
    Ensure = "Present"
    DependsOn = "[WindowsFeature]InstallIIS"
	}

    #Disable firewall
    xFirewallProfile DisablePublic {
    Enabled = "False"
    Name   = "Public"
    }

    xFirewallProfile DisablePrivate {
    Enabled = "False"
    Name   = "Private"
    }



    }
       
} 
```
3. Save it.
3. Now create other powershell file called "ReleaseDSCNode.ps1" and insert the code below:

```
param(
[string] $ResourceGroup,
[string] $Automation,
[string] $URI,
[string] $Zip,
[string] $Token
)

$SAS = $URI + $Zip + $Token


###Install Module.
$Uri1 = "https://www.powershellgallery.com/api/v2/package/xNetworking/5.7.0.0"
New-AzureRmAutomationModule -Name xNetworking  -ResourceGroupName $ResourceGroup -AutomationAccountName $Automation  -ContentLinkUr $Uri1
$Uri2 = "https://www.powershellgallery.com/api/v2/package/xPSDesiredStateConfiguration/8.4.0.0"
New-AzureRmAutomationModule -Name xPSDesiredStateConfiguration  -ResourceGroupName $ResourceGroup -AutomationAccountName $Automation  -ContentLinkUr $Uri2



Start-Sleep -s 250

##########
$Params = @{"SAS"=$SAS}
###Update DSC Node.
$AA = Get-AzureRMAutomationAccount -ResourceGroupName $ResourceGroup -Name $Automation 
$AA | Import-AzureRmAutomationDscConfiguration -SourcePath "$env:SYSTEM_ARTIFACTSDIRECTORY\_Tier1-CI-AutomationAccount\drop\DSC\WebServer.ps1" -Published -Force
$AA | Start-AzureRmAutomationDscCompilationJob -ConfigurationName WebServer -Parameters $Params
```
3. In your Azure Repo, inside of Azure Automation Account Folder, create a new subdirectory called "DSC" and upload the "WebServer.ps1" and "ReleaseDSCNode.ps1" files.
4. Take care with this line "$env:SYSTEM_ARTIFACTSDIRECTORY\_Tier1-CI-AutomationAccount\drop\DSC\WebServer.ps1", you should reemplace it base on your Artifact Name.
5. You should rebuild the Artifact to add the new files.
6. On the Release Pipeline, on the Agent Job will need to create a new Task and search "Azure Powershell Script:FilePath.
7. On the "Azure Powershell Script:FilePath, Select "Script File Path".
8. On Script Path, Browse and select the file called "ReleaseDSCNode.ps1"
9. On the Script Argument, type:
```
-ResourceGroup "Hackathon" -Automation $(AAName) -URI "$(URI)" -Zip "App.zip" -Token "$(SAS Token)" 

```
Replace "Hackathon" by the name of your Resource Group.


> Note: the variables $URI and $SAS Token, have been generated by the Task called "Azure file copy"

Reference:

![Image alt text](../Images/AzurePowershell.PNG)



### Success Criteria

1. You should have the DSC configuration uploaded on your Automation Account and DSC Configuration file should be "compiled". [Hint](../Images/Compiled.PNG)


[Back](challenge07.md) - [Home](/readme.md) - [Next](challenge09.md)
