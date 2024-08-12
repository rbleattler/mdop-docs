---
title: Applying hotfixes on MBAM 2.5 SP1
description: This article describes the process for applying the hotfixes for Microsoft BitLocker Administration and Monitoring (MBAM) Server 2.5 SP1.
ms.author: aaroncz
ms.collection: must-keep
author: aczechowski
ms.date: 8/30/2018
---

# Applying hotfixes on MBAM 2.5 SP1

This article describes the process for applying the hotfixes for Microsoft BitLocker Administration and Monitoring (MBAM) Server 2.5 SP1.

## Prerequisites

Before you begin, download the latest hotfix of Microsoft BitLocker Administration and Monitoring (MBAM) Server 2.5 SP1: [Servicing Release](https://www.microsoft.com/download/details.aspx?id=102262)

> [!NOTE]
> For more information about the hotfix releases, see the [MBAM version chart](/archive/blogs/dubaisec/mbam-version-chart).

## Steps to update the MBAM Server for existing MBAM environment

1. Remove the MBAM server feature. Open the MBAM Server Configuration Tool, then select **Remove Features**.
2. Remove MDOP MBAM from Control Panel | Programs and Features.
3. Install MBAM 2.5 SP1 RTM server components.
4. Install the latest MBAM 2.5 SP1 hotfix rollup.
5. Configure MBAM features using MBAM Server Configurator.

## Steps to install the new MBAM 2.5 SP1 server hotfix

For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
