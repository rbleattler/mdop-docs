---
title: Learn to install the sequencer
description: Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.1 sequencer.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Learn to install the sequencer

Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.1 sequencer. The computer that will run the sequencer must not be running any version of the App-V 5.1 client.

Upgrading a previous installation of the App-V sequencer is not supported.

> [!IMPORTANT]
> For a full list of the sequencer requirements see sequencer sections of [App-V 5.1 Prerequisites](app-v-51-prerequisites.md) and [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

You can also use the command line to install the App-V 5.1 sequencer. The following list displays information about options for installing the sequencer using the command line and **appv\_sequencer\_setup.exe**:

| Command | Description |
|--|--|
| /INSTALLDIR | Specifies the installation directory. |
| /CEIPOPTIN | Enables participation in the Microsoft Customer Experience Improvement Program. |
| /Log | Specifies where the installation log will be saved, the default location is **%Temp%**. For example, **C:\ Logs \ log.log**. |
| /q | Specifies a quiet or silent installation. |
| /Uninstall | Specifies the removal of the sequencer. |
| /ACCEPTEULA | Accepts the license agreement. This is required for an unattended installation. Example usage: **/ACCEPTEULA** or **/ACCEPTEULA=1**. |
| /LAYOUT | Specifies the associated layout action. It also extracts the Windows Installer (.msi) and script files to a folder without installing App-V 5.1. No value is expected. |
| /LAYOUTDIR | Specifies the layout directory. Requires a string value. Example usage: **/LAYOUTDIR="C:\Application Virtualization Client"**. |
| /? Or /h or /help | Displays associated help. |

## To install the App-V 5.1 sequencer

1.  Copy the App-V 5.1 sequencer installation files to the computer on which it will be installed. Double-click **appv\_sequencer\_setup.exe** and then click **Install**.

2.  On the **Software License Terms** page, you should review the license terms. To accept the license terms select **I accept the license terms.** Click **Next**.

3.  On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, to enable Microsoft updates select **Use Microsoft Update when I check for updates (recommended).** To disable Microsoft updates from running select **I don't want to use Microsoft Update**. Click **Next**.

4.  On the **Customer Experience Improvement Program** page, to participate in the program select **Join the Customer Experience Improvement Program**. This will allow information to be collected about how you are using App-V 5.1. If you don't want to participate in the program select **I don't want to join the program at this time**. Click **Install**.

5.  To open the sequencer, click **Start** and then click **Microsoft Application Virtualization Sequencer**.

## To troubleshoot the App-V 5.1 sequencer installation

-   For more information regarding the sequencer installation, you can view the error log in the **%temp%** folder. To review the log files, click **Start**, type **%temp%**, and then look for the **appv\_ log**.

## Related topics

[App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md)
