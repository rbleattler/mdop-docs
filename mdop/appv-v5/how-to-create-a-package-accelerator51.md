---
title: Create a package accelerator
description: App-V 5.1 package accelerators automatically generate new virtual application packages.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Create a package accelerator

App-V 5.1 package accelerators automatically generate new virtual application packages.

> [!NOTE]
> You can use PowerShell to create a package accelerator. For more information see [How to Create a Package Accelerator by Using PowerShell](how-to-create-a-package-accelerator-by-using-powershell51.md).

Use the following procedure to create a package accelerator.

> [!IMPORTANT]
> Package Accelerators can contain password and user-specific information. Therefore you must save Package Accelerators and the associated installation media in a secure location, and you should digitally sign the Package Accelerator after you create it so that the publisher can be verified when the App-V 5.1 Package Accelerator is applied.

> [!IMPORTANT]
> Before you begin the following procedure, you should perform the following:
>
> - Copy the virtual application package that you will use to create the package accelerator locally to the computer running the sequencer.
>
> - Copy all required installation files associated with the virtual application package to the computer running the sequencer.

## To create a package accelerator

> [!IMPORTANT]
> The App-V 5.1 Sequencer does not grant any license rights to the software application you are using to create the Package Accelerator. You must abide by all end user license terms for the application you are using. It is your responsibility to make sure the software application's license terms allow you to create a Package Accelerator using App-V 5.1 Sequencer.

1. To start the App-V 5.1 sequencer, on the computer that is running the sequencer, click **Start** / **All Programs** / **Microsoft Application Virtualization** / **Microsoft Application Virtualization Sequencer**.

2. To start the App-V 5.1 **Create Package Accelerator** wizard, in the App-V 5.1 sequencer console, click **Tools** / **Create Accelerator**.

3. On the **Select Package** page, to specify an existing virtual application package to use to create the Package Accelerator, click **Browse**, and locate the existing virtual application package (.appv file).

    > [!TIP]
    > Copy the files associated with the virtual application package you plan to use locally to the computer running the Sequencer.

4. On the **Installation Files** page, to specify the folder that contains the installation files that you used to create the original virtual application package, click **Browse**, and then select the directory that contains the installation files.

    > [!TIP]
    > Copy the folder that contains the required installation files to the computer running the Sequencer.

5. If the application is already installed on the computer running the sequencer, to specify the installation file, select **Files installed on local system**. To use this option, the application must already be installed in the default installation location.

6. On the **Gathering Information** page, review the files that were not found in the location specified on the **Installation Files** page of this wizard. If the files displayed are not required, select **Remove these files**, and then click **Next**. If the files are required, click **Previous** and copy the required files to the directory specified on the **Installation Files** page.

    > [!NOTE]
    > You must either remove the unrequired files, or click **Previous** and locate the required files to advance to the next page of this wizard.

7. On the **Select Files** page, carefully review the files that were detected, and clear any file that should be removed from the package accelerator. Select only files that are required for the application to run successfully, and then click **Next**.

8. On the **Verify Applications** page, confirm that all installation files that are required to build the package are displayed. When the Package Accelerator is used to create a new package, all installation files displayed in the **Applications** pane are required to create the package.

   If necessary, to add additional Installer files, click **Add**. To remove unnecessary installation files, select the Installer file, and then click **Delete**. To edit the properties associated with an installer, click **Edit**. The installation files specified in this step will be required when the Package Accelerator is used to create a new virtual application package. After you have confirmed the information displayed, click **Next**.

9. On the **Select Guidance** page, to specify a file that contains information about how the Package Accelerator, click **Browse**. For example, this file can contain information about how the computer running the Sequencer should be configured, application prerequisite information for target computers, and general notes. You should provide all required information for the Package Accelerator to be successfully applied. The file you select must be in rich text (.rtf) or text file (.txt) format. Click **Next**.

10. On the **Create Package Accelerator** page, to specify where to save the Package Accelerator, click **Browse** and select the directory.

11. On the **Completion** page, to close the **Create Package Accelerator** wizard, click **Close**.

    > [!IMPORTANT]
    > To help ensure that the package accelerator is as secure as possible, and so that the publisher can be verified when the package accelerator is applied, you should always digitally sign the package accelerator.

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)

[How to Create a Virtual Application Package Using an App-V Package Accelerator](how-to-create-a-virtual-application-package-using-an-app-v-package-accelerator51.md)
