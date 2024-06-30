---
title: Deploy the DaRT recovery image as part of a recovery partition
description: Learn how to deploy the DaRT recovery image as part of a recovery partition.
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Deploy the DaRT recovery image as part of a recovery partition

After you have finished running the Microsoft Diagnostics and Recovery Toolset (DaRT) 10 Recovery Image wizard and created the recovery image, you can extract the `boot.wim` file from the ISO image file and deploy it as a recovery partition in a Windows 10 image. A partition is recommended, because any corruption issues that prevent the Windows operating system from starting would also prevent the recovery image from starting. A separate partition also eliminates the need to provide the BitLocker recovery key twice. Consider hiding the partition to prevent users from storing files on it.

To deploy DaRT in the recovery partition of a Windows 10 image:

1. Create a target partition in your Windows 10 image that is equal to or greater than the size of the ISO image file that you created by using the **DaRT 10 Recovery Image wizard**.

    The minimum size required for a DaRT partition is 500MB to accommodate the remote connection functionality in DaRT.

2. Extract the `boot.wim` file from the DaRT ISO image file. To do so:
    1. Mount the ISO image file that you created in the **Create Startup Image** your preferred method of mounting an image. (File Explorer, PowerShell cmdlets, the Disk Management tool, or Windows ADK)
    2. Navigate to the mounted volume and copy the `boot.wim` file from the `\sources` folder to a location on your computer.

        > [!NOTE]
        > If you burned a CD or DVD of the recovery image, you can open the files on the CD or DVD and copy the `boot.wim` file from the `\sources` folder. This lets you skip the need to mount the image.

3. Use the `boot.wim` file to create a bootable recovery partition by using your company's standard method for creating a custom Windows RE image.

    For more information about how to create or customize a recovery partition, see [Customizing the Windows RE Experience](/previous-versions/windows/it-pro/windows-7/dd744576(v=ws.10)).

4. Replace the target partition in your Windows 10 image with the recovery partition.

    For more information about how to deploy a recovery solution to reinstall the factory image in the event of a system failure, see [Deploy a System Recovery Image](/previous-versions/windows/it-pro/windows-7/dd744280(v=ws.10)).

## Related information

- [Creating the DaRT 10 Recovery Image](creating-the-dart-10-recovery-image.md)
- [Deploying the DaRT Recovery Image](deploying-the-dart-recovery-image-dart-10.md)
- [Planning for DaRT 10](planning-for-dart-10.md)
