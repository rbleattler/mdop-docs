---
title: Sequence a package by using Windows PowerShell
description: Use the following procedure to create a new App-V 5.1 package using Windows PowerShell.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Sequence a package by using Windows PowerShell

Use the following procedure to create a new App-V 5.1 package using Windows PowerShell.

> [!NOTE]
> Before you use this procedure you must copy the associated installer files to the computer running the sequencer and you have read and understand the sequencer section of [Planning for the App-V 5.1 Sequencer and Client Deployment](planning-for-the-app-v-51-sequencer-and-client-deployment.md).

## To create a new virtual application using PowerShell

1.  Install the App-V 5.1 sequencer. For more information about installing the sequencer see [How to Install the Sequencer](how-to-install-the-sequencer-51beta-gb18030.md).

2.  To open a PowerShell console click **Start** and type **PowerShell**. Right-click **Windows PowerShell** and select **Run as Administrator**.

3.  Using the PowerShell console, type the following: **import-module appvsequencer**.

4.  To create a package, use the **New-AppvSequencerPackage** cmdlet. The following parameters are required to create a package:

    -   **Name** - specifies the name of the package.

    -   **PrimaryVirtualApplicationDirectory** - specifies the path to the directory that will be used to install the application. This path must exist.

    -   **Installer** - specifies the path to the associated application installer.

    -   **Path** - specifies the output directory for the package.

    For example:

    **New-AppvSequencerPackage -Name &lt;name of Package&gt; -PrimaryVirtualApplicationDirectory &lt;path to the package root&gt; -Installer &lt;path to the installer executable&gt; -OutputPath &lt;directory of the output path&gt;**

    Wait for the sequencer to create the package. Creating a package using PowerShell can take time. If the package was not created successfully an error will be returned.

    The following list displays additional optional parameters that can be used with **New-AppvSequencerPackage** cmdlet:

    -   AcceleratorFilePath - specifies the path to the accelerator .cab file to generate a package.

    -   InstalledFilesPath - specifies the path to where the local installed files of the application are saved.

    -   InstallMediaPath - specifies the path to where the installation media is

    -   TemplateFilePath - specifies the path to a template file if you want to customize the sequencing process.

    -   FullLoad - specifies that the package must be fully downloaded to the computer running the App-V 5.1 before it can be opened.

## Related topics

[Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md)
