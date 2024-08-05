---
title: Planning to deploy App-V 5.1 with an electronic software distribution system
description: If you are using an electronic software distribution system to deploy App-V packages, review the following planning considerations.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Planning to deploy App-V 5.1 with an electronic software distribution system

If you are using an electronic software distribution system to deploy App-V packages, review the following planning considerations. For information about using System Center Configuration Manager to deploy App-V, see [Introduction to Application Management in Configuration Manager](/previous-versions/system-center/system-center-2012-R2/gg682125(v=technet.10)).

Review the following component and architecture requirements options that apply when you use an ESD to deploy App-V packages:

| Deployment requirement or option | Description |
|----------------------------------|-------------|
| The App-V Management server, Management database, and Publishing server are not required. | These functions are handled by the implemented ESD solution. |
| You can deploy the App-V Reporting server and Reporting database side by side with the ESD. | The side-by-side deployment lets you collect data and generate reports. If you enable the App-V client to send report information, and you are not using the App-V Reporting server, the reporting data is stored in associated .xml files. |

## Related topics

[App-V 5.1 supported configurations](app-v-51-supported-configurations.md)
