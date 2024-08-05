---
title: Creating the DaRT 10 recovery image
description: After installing Microsoft Diagnostics and Recovery Toolset (DaRT) 10, you create a DaRT 10 recovery image.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/20/2021
---

# Creating the DaRT 10 recovery image

After installing Microsoft Diagnostics and Recovery Toolset (DaRT) 10, you create a DaRT 10 recovery image. The recovery image starts Windows RE, from which you can then start the DaRT tools. You can generate International Organization for Standardization (ISO) files and Windows Imaging Format (WIM) images. In addition, you can use PowerShell to generate scripts that use the settings you select in the DaRT Recovery Image wizard. You can use the script later to rebuild recovery images by using the same settings. The recovery image provides various recovery tools. For a description of the tools, see [Overview of the Tools in DaRT 10](overview-of-the-tools-in-dart-10.md).

After you boot the computer into DaRT, you can run the different DaRT tools to try to diagnose and repair the computer. This section walks you through the process of creating the DaRT recovery image and lets you select the tools and features that you want to include as part of the image.

You can create the DaRT recovery image by using either of two methods:

- Use the DaRT Recovery Image wizard, which runs in a Windows environment.

- Modify an example PowerShell script with the values you want. For more information, see [Administering DaRT 10 Using PowerShell](administering-dart-10-using-powershell.md).

You can write the ISO to a recordable CD or DVD, save it to a USB flash drive, or save it in a format that you can use to boot into DaRT from a remote partition or from a recovery partition.

Once you create the ISO image, you can burn it onto a blank CD or DVD (if your computer has a CD or DVD drive). If your computer doesn't have a drive for this purpose, you can use most generic programs that are used to burn CDs or DVDs.

## Select the image architecture and specify the path

On the Windows 10 Media page, you select whether to create a 32-bit or 64-bit DaRT recovery image. Use the 32-bit Windows to build 32-bit DaRT recovery images, and 64-bit Windows to build 64-bit DaRT recovery images. You can use a single computer to create recovery images for both architecture types, but you can't create one image that works on both 32-bit and 64-bit architectures. You also indicate the path of the Windows 10 installation media. Choose the architecture that matches the same architecture as the recovery image.

To select the image architecture and specify the path:

1. On the **Windows 10 Media** page, select one of the following:

    - If you're creating a recovery image for 64-bit computers, select **Create x64 (64-bit) DaRT image**.

    - If you're creating a recovery image for 32-bit computers, select **Create x86 (32-bit) DaRT image**.
2. In the **Specify the root path of the Windows 10 &lt;64-bit or 32-bit&gt; install media** box, type the path of the Windows 10 installation files. Use a path that matches the architecture of the recovery image.

3. Select **Next**.

## Select the tools to include on the recovery image

On the Tools page, you can select numerous tools to include on the recovery image. These tools are available to end users when they boot into the DaRT image. However, if you enable remote connectivity when creating the DaRT image, all of the tools are available when a help desk worker connects to the end user's computer, regardless of which tools you chose to include on the image.

To restrict end-user access to these tools, but still retain full access to the tools through the Remote Connection Viewer, don't select those tools on the Tools page. Users are able to use only Remote Connection and can see, but not access, any tools that you exclude from the recovery image.

To select the tools to include on the recovery image:

1. On the **Tools** page, select the check box beside each tool that you want to include on the image.

2. Select **Next**.

## Choose whether to allow remote connectivity by a help desk

On the Remote Connection page, you can choose to enable a help desk worker to remotely connect to and run the DaRT tools on an end user's computer. The remote connectivity option is then shown as an available option in the Diagnostics and Recovery Toolset window. After help desk workers establish a remote connection, they can run the DaRT tools on the end-user computer from a remote location.

To choose whether to allow remote connectivity by help desk workers:

1. On the **Remote Connection** page, select the **Allow remote connections** check box to allow remote connections, or clear the check box to prevent remote connections.

2. If you cleared the **Allow remote connections** check box, select **Next**. Otherwise, go to the next step to continue configuring remote connectivity.

3. Select one of the following options:

    - Let Windows choose an open port number.

    - Specify the port number. If you select this option, enter a port number between 1 and 65535 in the field beneath the option. This port number is used when establishing a remote connection. We recommend that you use port number 1024 or higher to minimize the possibility of a conflict.

4. (Optional) in the **Remote connection welcome** message box, create a customized message that end users receive when they establish a remote connection. The message can be a maximum of 2,048 characters.

5. Select **Next**.

    For more information about running the DaRT tools remotely, see [How to recover remote computers by using the DaRT recovery image](how-to-recover-remote-computers-by-using-the-dart-recovery-image-dart-10.md).

## Add drivers to the recovery image

On the Drivers tab of the Advanced Options page, you can add other device drivers that you might need when repairing a computer. These drivers typically include storage or network controllers that Windows 10 doesn't provide. Drivers are installed when the image is created.

> [!IMPORTANT]
> When you select drivers to include, be aware that wireless connectivity (such as Bluetooth or 802.11a/b/g/n) is not supported in DaRT.

To add drivers to the recovery image:

1. On the **Advanced Options** page, select the **Drivers** tab.

2. Select **Add**.

3. Browse to the file to be added for the driver, and then select **Open**.

    > [!NOTE]
    > The driver file is provided by the manufacturer of the storage or network controller.

4. Repeat Steps 2 and 3 for every driver that you want to include.

5. Select **Next**.

## Add WinPE optional packages to the recovery image

On the WinPE tab of the Advanced Options page, you can add WinPE optional packages to the DaRT image. These packages are part of the Windows ADK, which is an installation prerequisite for the DaRT Recovery Image wizard. The tools that you can select are all optional. Any required packages are added automatically, based on the tools you selected on the Tools page.

You can also specify the size of the scratch space. Scratch space is the amount of RAM disk space that is set aside for DaRT to run. The scratch space is useful in case the end user's hard disk isn't available. If you're running other tools and drivers, you might want to increase the scratch space.

To add WinPE optional packages to the recovery image:

1. On the **Advanced Options** page, select the **WinPE** tab.

2. Select the check box beside each package that you want to include on the image, or select the **Name** check box to select all of the packages.

3. In the **Scratch Space** field, select the amount of RAM disk space to allocate for running DaRT in case the end user's hard disk isn't available.

4. Select **Next**.

## Add the debugging tools for Crash Analyzer

If you include the Crash Analyzer tool in the ISO image, you must also include the Debugging Tools for Windows. On the Crash Analyzer tab of the Advanced Options page, you enter the path of the Windows 10 Debugging Tools, which Crash Analyzer uses to analyze memory dump files. You can use the tools that are on the computer where you're running the DaRT Recovery Image wizard, or you can use the tools that are on the end-user computer. If you decide to use the tools on the end-user computer, remember that every computer that you diagnose must have the Debugging Tools installed.

If you installed the Microsoft Windows Software Development Kit (SDK) or the Microsoft Windows Development Kit (WDK), the Windows 10 Debugging Tools are added to the recovery image by default, and the path to the Debugging Tools is automatically filled in. You can change the path of the Windows 10 Debugging Tools if the files are located somewhere other than the location indicated by the default file path. A link in the wizard lets you download and install debugging tools for Windows if they aren't already installed.

To download the Windows Debugging Tools, see the [Windows Driver Kit (WDK)](/windows-hardware/drivers/download-the-wdk). Install the debugging tools to the default location.

> [!NOTE]
> The DaRT wizard checks for the tools in the `HKLM:\Software\Microsoft\Windows Kits\Installed Roots\WindowsDebuggersRoot` registry key. If the registry value is not there, the wizard looks in one of the following locations, depending on your system architecture:
>
>- `%ProgramFilesX86%\Windows Kits\10.0\Debuggers\x64`
>- `%ProgramFilesX86%\Windows Kits\10.0\Debuggers\x86`

To add the debugging tools for Crash Analyzer:

1. On the **Advanced Options** page, select the **Crash Analyzer** tab.

2. (Optional) select **Download the Debugging Tools** to download the Debugging Tools for Windows.

3. Select one of the following options:

    - **Include the Windows 10 &lt;64-bit or 32-bit&gt; Debugging Tools**. If you select this option, browse to and select the location of the tools if the path isn't already displaying.

    - **Use the Debugging Tools from the system that is being debugged**. If you select this option, the Crash Analyzer won't work if the Debugging Tools for Windows aren't found on the problem computer.

4. Select **Next**.

## Select the types of recovery image files to create

On the Create Image page, you choose an output folder for the recovery image, enter an image name, and select the types of DaRT recovery image files to create. During the recovery image creation process, Windows source files are unpacked, DaRT files are copied to it, and the image is then "repacked" into the file formats that you select on this page.

The available image file types are:

- **Windows Imaging File (WIM)** - used to deploy DaRT to a preboot execution environment (PXE) or local partition.

- **ISO image file** - used to deploy to CD or DVD, or for use in virtual machines (VM)s. The wizard requires that the ISO image have an .iso file name extension because most programs that burn a CD or DVD require that extension. If you don't specify a different location, the ISO image is created on your desktop with the name DaRT10.ISO.

- **PowerShell script** - creates a DaRT recovery image with commands that provide essentially the same options that you can select by using the DaRT Recovery Image wizard. The script also enables you to add or changes files in the DaRT recovery image.

If you select the Edit Image check box on this page, you can customize the recovery image during the image creation process. For example, you can change the "winpeshl.ini" file to create a custom startup order or to add third-party tools.

To select the types of recovery image files to create:

1. On the **Create Image** page, select **Browse** to choose the output folder for the image file.

    > [!NOTE]
    > The size of the image will vary, depending on the tools that you select and the files that you add in the wizard.

2. In the **Image name** box, enter a name for the DaRT recovery image, or accept the default name, which is DaRT10.

    The wizard creates a subfolder in the output path by this name.

3. Select the types of image files that you want to create.

4. Choose one of the following:

    - To change the files in the recovery image before you create the image files, select the **Edit Image** check box, and then select **Prepare**.
    - To create the recovery image without changing the files, select **Create**.

5. Select **Next**.

## Edit the recovery image files

You can edit the recovery image only if you selected the Edit Image check box on the Create Image page. After the recovery image is prepared for editing, you can add and modify the recovery image files before creating the bootable media. For example, you can create a custom order for startup, add various non-Microsoft tools, and so on.

To edit the recovery image files:

1. On the **Edit Image** page, select **Open** in Windows Explorer.

2. Create a subfolder in the folder that is listed in the dialog box.

3. Copy the files that you want to the new subfolder, or remove files that you don't want.

4. Select **Create** to start creating the recovery image.

## Generate the recovery image files

On the "Generate Files" page, the DaRT recovery image is generated for the file types that you selected on the "Create Image" page.

To generate the recovery image files:

- On the **Generate Files** page, select **Next** to generate the recovery image files.

## Copy the recovery image to a CD, DVD, or USB

On the Create Bootable Media page, you can optionally copy the image file to a CD, DVD, or USB flash drive (UFD). You can also create another bootable media from this page by restarting the wizard.

> [!NOTE]
> The Preboot execution environment (PXE) and local image deployment are not supported natively by this tool since they require additional enterprise tools, such as System Center Configuration Manager server and Microsoft Development Toolkit.

To copy the recovery image to a CD, DVD, or USB:

1. On the **Create Bootable Media** page, select the iso file that you want to copy.

2. Insert a CD, DVD, or USB, and then select the drive.

    > [!NOTE]
    > If a drive isn't recognized and you install a new drive, you can select **Refresh** to force the wizard to update the list of available drives.

3. Select the **Create Bootable Media** button.

4. To create another recovery image, select Restart, or select **Close** if you've finished creating all of the media that you want.

## Related articles

- [Overview of the Tools in DaRT 10](overview-of-the-tools-in-dart-10.md)
- [Deploying DaRT 10](deploying-dart-10.md)
