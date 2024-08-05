---
title: Modify client configuration by using Windows PowerShell
description: Use the following procedure to configure the App-V 5.1 client configuration.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Modify client configuration by using Windows PowerShell

Use the following procedure to configure the App-V 5.1 client configuration.

## To modify App-V 5.1 client configuration using PowerShell

1.  To configure the client settings using PowerShell, use the **Set-AppvClientConfiguration** cmdlet. For more information about installing PowerShell, and a list of cmdlets see, [How to Load the PowerShell Cmdlets and Get Cmdlet Help](how-to-load-the-powershell-cmdlets-and-get-cmdlet-help-51.md).

2.  To modify the client configuration, open a PowerShell Command prompt and run the following cmdlet **Set-AppvClientConfiguration** with any required parameters. For example:

    `$config = Get-AppvClientConfiguration`

    `Set-AppvClientConfiguration $config`

    `Set-AppvClientConfiguration -AutoLoad 2`

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)
