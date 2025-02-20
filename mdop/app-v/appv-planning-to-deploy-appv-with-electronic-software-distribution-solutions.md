---
title: Planning to deploy App-V in Windows with an electronic software distribution system
description: If you're using an electronic software distribution (ESD) system to deploy App-V packages, review the following planning considerations for App-V in Windows.
author: aczechowski
ms.date: 04/18/2018
---

# Planning to deploy App-V in Windows with an electronic software distribution system

[!INCLUDE [Applies to Windows client versions](../includes/applies-to-windows-client-versions.md)]

If you're using an electronic software distribution (ESD) system to deploy App-V packages, review the following planning considerations. For information about deploying App-V with Microsoft Configuration Manager, see [Introduction to application management in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682125(v=technet.10)#BKMK_Appv).

Review the following component and architecture requirements options that apply when you use an ESD to deploy App-V packages:

| Deployment requirement or option | Description |
|---|---|
| The App-V Management server, Management database, and Publishing server aren't required. | These functions are handled by the implemented ESD solution. |
| You can deploy the App-V Reporting server and Reporting database side-by-side with the ESD. | The side-by-side deployment lets you collect data and generate reports.<br/>If you enable the App-V client to send report information without using the App-V Reporting server, the reporting data will be stored in associated .xml files. |

## Related articles

* [App-V supported configurations](appv-supported-configurations.md)
* [How to deploy App-V packages Using Electronic Software Distribution](appv-deploy-appv-packages-with-electronic-software-distribution-solutions.md)
* [How to enable only administrators to publish packages by using an ESD](appv-enable-administrators-to-publish-packages-with-electronic-software-distribution-solutions.md)
