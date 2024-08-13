---
title: Installing the MBAM 2.5 server software
description: This article describes how to install the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 Server software by using the Microsoft BitLocker Administration and Monitoring Setup wizard or by using command-line parameters.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Installing the MBAM 2.5 server software

This article describes how to install the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 server software by using the Microsoft BitLocker Administration and Monitoring Setup wizard or by using command-line parameters. Repeat the server installation process for each server on which you configure MBAM 2.5 server features. After you finish the installation, see [Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md) for steps about configuring the server features.

| Before you start | Description |
|--|--|
| Review the MBAM 2.5 planning information | - [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md)<br>- [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md)<br>- [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md) |
| Read how to get log files | By default, log files are created in the local computer's `%temp%` folder. To write the log files to a specific location rather than to the `%temp%` folder, use the `/log` argument.<br>Other events might be logged in Event Viewer in the **MBAM-Setup** or **MBAM-Web** nodes under **Applications and Services Logs &gt; Microsoft &gt; Windows**. For example, if you uninstall MBAM, the uninstaller also uninstalls the MBAM-Setup and MBAM-Web logs in EventViewer. |

## Installing the MBAM 2.5 server software by using the Microsoft BitLocker Administration and Monitoring Setup wizard

Use these steps to install the MBAM server software by using the Microsoft BitLocker Administration and Monitoring Setup wizard.

## To install the MBAM 2.5 Server software by using the wizard

1.  On the server where you want to install MBAM, run **MBAMserversetup.exe** to start the Microsoft BitLocker Administration and Monitoring Setup wizard.

2.  On the **Welcome** page, select **Next**.

3.  Read and accept the Microsoft Software License Agreement, and then select **Next** to continue the installation.

4.  Choose whether to use Microsoft Update when you check for updates, and then select **Next**.

5.  Choose whether to participate in the Customer Experience Improvement Program, and then select **Next**.

6.  To start the installation, select **Install**.

7.  To configure the server features after the MBAM Server software finishes installing, select the **Run MBAM Server Configuration after the wizard closes** check box. Alternatively, you can configure MBAM later by using the **MBAM Server Configuration** shortcut that the server installation creates on your **Start** menu.

8.  Select **Finish**.

## Installing the MBAM 2.5 server software by using a command prompt window

At a command prompt, type a command similar to the following command to install the MBAM Server software.

``` syntax
MbamServerSetup.exe MBAMServerInstall.log
CEIPENABLED=True OPTIN_FOR_MICROFOST_UPDATES=True INSTALLDIR=c:\mbaminstall
```

The following table describes the command-line parameters for installing the MBAM 2.5 Server software.

| Parameter | Parameter value | Description |
|--|--|--|
| `CEIPENABLED` | True False | True - participate in the Customer Improvement Experience Program, which helps Microsoft identify which MBAM features to improve.<br>False - don't participate in the Customer Improvement Experience Program. |
| `OPTIN_FOR_MICROSOFT_UPDATES` | True False | True - use Microsoft Update to keep your computer secure and up-to-date for Windows and other Microsoft products, including MBAM.<br>False - don't use Microsoft Update. |
| `INSTALLDIR` | `<Path>` | Location where you want to install MBAM.<br>Example:<br>`INSTALLDIR=c:\mbaminstall` |
| `FORCE_UNINSTALL` | True False | True - continue the process of uninstalling MBAM, even if any features fail to be removed.<br>False (default) - if the uninstallation custom action fails to remove an added MBAM Server feature, the uninstallation fails, and MBAM remains installed.<br>In both instances, any features that were successfully removed during the attempt to uninstall MBAM stay removed. |

## Related articles

[MBAM 2.5 deployment checklist](mbam-25-deployment-checklist.md)

[Configuring the MBAM 2.5 Server Features](configuring-the-mbam-25-server-features.md)
