---
title: Troubleshooting AGPM Upgrades
description: Troubleshooting AGPM Upgrades
author: aczechowski
ms.assetid: 1abbf0c1-fd32-46a8-a3ba-c005f066523d
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.pagetype: mdop
ms.mktglfcycl: manage
ms.sitesec: library
ms.date: 06/16/2016
---


# Troubleshooting AGPM Upgrades

> [!div class="nextstepaction"]
> <a href="https://vsa.services.microsoft.com/v1.0/?partnerId=7d74cf73-5217-4008-833f-87a1a278f2cb&flowId=DMC&initialQuery=31806284" target='_blank'>Try our Virtual Agent</a> - It can help you quickly identify and fix common Group Policy Management issues.

This section lists common issues that you may encounter when you upgrade your Advanced Group Policy Management (AGPM) server to a newer version (e.g. AGPM 4.0 to AGPM 4.3). To diagnose issues not listed here, it may be helpful to view the [Troubleshooting AGPM](troubleshooting-agpm-agpm40.md) or for an AGPM Administrator (Full Control) to use logging and tracing. For more information, see [Configure Logging and Tracing](configure-logging-and-tracing-agpm40.md).

## What problems are you having?

-   [Failed to generate a HTML GPO difference report (Error code 80004003)](#bkmk-error-80004003)

### <a href="" id="bkmk-error-80004003"></a>Failed to generate a HTML GPO difference report (Error code 80004003)

-   **Cause**: You have installed the AGPM upgrade package with an incorrect account.

-   **Solution**: You will need to be an AGPM administrator in order to fix this issue.

    -   Ensure you know the username & password of your **AGPM service account**.

    -   Log onto your AGPM server interactively as your AGPM service account.

        -   This is critically important, as the install will fail if you use a different account.

    -   Shutdown the AGPM service.

    -   Install the required hotfix.

    -   Connect to AGPM using an AGPM client to test that your difference reports are now functioning.

## Install Hotfix Package 1 for Microsoft Advanced Group Policy Management 4.0 SP3

**Issue fixed in this hotfix**: AGPM can't generate difference reports when it controls or manages new Group Policy Objects (GPOs).

**How to get this update**: Install the latest version of Microsoft Desktop Optimization Pack ([March 2017 Servicing Release](https://www.microsoft.com/download/details.aspx?id=54967)). See [KB 4014009](https://support.microsoft.com/help/4014009/) for more information.

More specifically, you can choose to download only the first file, `AGPM4.0SP1_Server_X64_KB4014009.exe`, from the list presented after pressing the download button.

The download link to the Microsoft Desktop Optimization Pack (March 2017 Servicing Release) can be found [here](https://www.microsoft.com/download/details.aspx?id=54967).


## Reference link
https://support.microsoft.com/help/3127165/hotfix-package-1-for-microsoft-advanced-group-policy-management-4-0-sp

