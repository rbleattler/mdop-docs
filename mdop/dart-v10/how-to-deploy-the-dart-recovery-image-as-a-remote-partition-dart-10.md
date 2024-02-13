---
title: Deploy the DaRT recovery image as a remote partition
description: Learn how to deploy the DaRT recovery image as a remote partition.
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Learn to deploy the DaRT recovery image as a remote partition

After you have finished running the Microsoft Diagnostics and Recovery Toolset (DaRT) 10 Recovery Image wizard and created the recovery image, you can extract the `boot.wim` file from the ISO image file and deploy it as a remote partition on the network.

To deploy DaRT 10 as a remote partition:

1. Extract the `boot.wim` file from the DaRT ISO image file. To do so:

    1. Mount the ISO image file that you created in the **Create Startup Image** your preferred method of mounting an image. (File Explorer, PowerShell cmdlets, the Disk Management tool, or Windows ADK)

    2. Navigate to the mounted volume and copy the `boot.wim` file from the `\sources` folder to a location on your computer.

        > [!NOTE]
        > If you burned a CD or DVD of the recovery image, you can open the files on the CD or DVD and copy the `boot.wim` file from the `\sources` folder. This lets you skip the need to mount the image.

2. Deploy the `boot.wim` file to a WDS server that can be accessed from end-user computers in your enterprise.

3. Configure the WDS server to use the `boot.wim` file for DaRT by following your standard WDS deployment procedures.

For more information about how to deploy DaRT as a remote partition, see [Walkthrough: Deploy an Image by Using PXE](/previous-versions/windows/it-pro/windows-7/dd744541(v=ws.10)) and [Windows Deployment Services Getting Started Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771670(v=ws.10)).

## Related topics

- [Creating the DaRT 10 Recovery Image](creating-the-dart-10-recovery-image.md)
- [Deploying the DaRT Recovery Image](deploying-the-dart-recovery-image-dart-10.md)
- [Planning for DaRT 10](planning-for-dart-10.md)
