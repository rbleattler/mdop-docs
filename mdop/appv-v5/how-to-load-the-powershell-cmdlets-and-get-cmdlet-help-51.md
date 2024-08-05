---
title: How to load the Windows PowerShell cmdlets and get cmdlet help
description: This article provides more information about how to use the Windows PowerShell cmdlets for App-V.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/02/2016
---

# How to load the Windows PowerShell cmdlets and get cmdlet help

This article provides more information about how to use the Windows PowerShell cmdlets for App-V.

## <a href="" id="bkmk-reqs-using-posh"></a>Requirements for using PowerShell cmdlets

Review the following requirements for using the App-V PowerShell cmdlets:

### Users can run App-V Server cmdlets only if you grant them access by using one of the following methods

- When you are deploying and configuring the App-V Server: Specify an Active Directory group or individual user that has permissions to manage the App-V environment. For more information, see [How to Deploy the App-V 5.1 Server](how-to-deploy-the-app-v-51-server.md).
- After you've deployed the App-V Server: Use the App-V Management console to add an additional Active Directory group or user. For more information, see [How to Add or Remove an Administrator by Using the Management Console](how-to-add-or-remove-an-administrator-by-using-the-management-console51.md).

### Cmdlets that require an elevated command prompt

- Add-AppvClientPackage
- Remove-AppvClientPackage
- Set-AppvClientConfiguration
- Add-AppvClientConnectionGroup
- Remove-AppvClientConnectionGroup
- Add-AppvPublishingServer
- Remove-AppvPublishingServer
- Send-AppvClientReport
- Set-AppvClientMode
- Set-AppvClientPackage
- Set-AppvPublishingServer

### Cmdlets that end users can run, unless you configure them to require an elevated command prompt

- Publish-AppvClientPackage
- Unpublish-AppvClientPackage

To configure these cmdlets to require an elevated command prompt, use one of the following methods:

- Run the **Set-AppvClientConfiguration** cmdlet with the **-RequirePublishAsAdmin** parameter. For more information, see the following articles:
  - [Manage Connection Groups on a Stand-alone Computer by Using PowerShell](how-to-manage-connection-groups-on-a-stand-alone-computer-by-using-powershell51.md)
  - [How to Manage App-V 5.1 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-51-packages-running-on-a-stand-alone-computer-by-using-powershell.md)
- Enable the "Require publish as administrator" group policy setting for App-V clients. For more information, see [Publish a Package by Using the Management Console](how-to-publish-a-package-by-using-the-management-console-51.md).

## <a href="" id="bkmk-load-cmdlets"></a>Loading the PowerShell cmdlets

To load the PowerShell cmdlet modules:

1.  Open Windows PowerShell or Windows PowerShell Integrated Scripting Environment (ISE).

2.  Type one of the following commands to load the cmdlets for the module you want:

| App-V component  | Command to type           |
|------------------|----------------------------|
| App-V Server     | `Import-Module AppvServer`   |
| App-V Sequencer  | `Import-Module AppvSequencer`|
| App-V Client     | `Import-Module AppvClient`   |

## <a href="" id="bkmk-get-cmdlet-help"></a>Getting help for the PowerShell cmdlets

Starting in App-V 5.0 SP3, cmdlet help is available in two formats:

### As a downloadable module

To download the latest help after downloading the cmdlet module:

1. Open Windows PowerShell or Windows PowerShell Integrated Scripting Environment (ISE).
2. Type one of the following commands to load the cmdlets for the module you want:

    | App-V component | Command to type |
    |--|--|
    | App-V Server | `Update-Help -Module AppvServer` |
    | App-V Sequencer | `Update-Help -Module AppvSequencer` |
    | App-V Client | `Update-Help -Module AppvClient` |

### On the web

| App-V component | Module documentation |
| ---------------- | -------------------------------------- |
| App-V Server | [AppvServer](/powershell/module/appvserver/) |
| App-V Sequencer | [AppvSequencer](/powershell/module/appvsequencer/) |
| App-V Client | [AppvClient](/powershell/module/appvclient/) |

## <a href="" id="bkmk-display-help-cmdlet"></a>Displaying the help for a PowerShell cmdlet

To display help for a specific PowerShell cmdlet:

1.  Open Windows PowerShell or Windows PowerShell Integrated Scripting Environment (ISE).

2.  Type **Get-Help** &lt;*cmdlet*&gt;, for example, **Get-Help Publish-AppvClientPackage**.
