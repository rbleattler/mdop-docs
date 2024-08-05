---
title: How to modify client configuration by using Windows PowerShell
description: Learn how to modify the Application Virtualization (App-V) client configuration by using Windows PowerShell.
author: aczechowski
ms.date: 04/19/2017
---

# How to modify client configuration by using Windows PowerShell

[!INCLUDE [Applies to Windows client versions](../includes/applies-to-windows-client-versions.md)]

Use the following procedure to configure the App-V client configuration.

1.  To configure the client settings using Windows PowerShell, use the **Set-AppVClientConfiguration** cmdlet. For more information about installing Windows PowerShell, and a list of cmdlets see, [How to Load the Windows PowerShell Cmdlets for App-V and Get Cmdlet Help](appv-load-the-powershell-cmdlets-and-get-cmdlet-help.md).

2.  To modify the client configuration, open a Windows PowerShell Command prompt and run **Set-AppVClientConfiguration** with any required parameters. For example:

    `$config = Get-AppVClientConfiguration`

    `Set-AppVClientConfiguration $config`

    `Set-AppVClientConfiguration -Name1 MyConfig -Name2 "xyz"`

## Related articles

[Operations for App-V](appv-operations.md)
