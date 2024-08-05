---
title: Only allow administrators to enable connection groups
description: You can configure the App-V client so that only administrators (not end users) can enable or disable connection groups. In earlier versions of App-V, you could not prevent end users from performing these tasks.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Only allow administrators to enable connection groups

You can configure the App-V client so that only administrators (not end users) can enable or disable connection groups. In earlier versions of App-V, you could not prevent end users from performing these tasks.

> [!NOTE]
> This feature is supported starting in App-V 5.0 SP3.

Use one of the following methods to allow only administrators to enable or disable connection groups.

| Method | Steps |
|--|--|
| Group Policy setting | Enable the "Require publish as administrator" Group Policy setting, which is located in the following Group Policy Object node: **Computer Configuration > Policies > Administrative Templates > System > App-V > Publishing** |
| PowerShell cmdlet | Run the **Set-AppvClientConfiguration** cmdlet with the **-RequirePublishAsAdmin** parameter. <br> Parameter values: <ul><li>0 - False</li><li>1 - True</li></ul> <br> **Example:** Set-AppvClientConfiguration -RequirePublishAsAdmin 1 |

## Related topics

[Managing Connection Groups](managing-connection-groups51.md)
