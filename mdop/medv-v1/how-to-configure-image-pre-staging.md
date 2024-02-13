---
title: How to Configure Image Prestaging
description: How to Configure Image Prestaging
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.date: 06/16/2016
---


# How to Configure Image Prestaging

> [!NOTE]
> Image pre-staging is useful only for the initial image download. It is not supported for image update.

## To configure image prestaging

1. On the client computer, under the image store directory, create a folder for the prestaging image, and name it *MED-V Images*.

    > [!NOTE]
    > This folder must be called *MED-V Images*.

2. Inside the MED-V Images folder, create a subfolder and name it *PrestagedImages*.

    > [!NOTE]
    > This folder must be called *PrestagedImages*.

3. To apply Access Control Lists (ACL) security to the *MED-V Images* folder, set the following ACL:

    - `NT AUTHORITY\\Authenticated Users:(OI)(CI)(special access:)`
    - `READ_CONTROL`
    - `SYNCHRONIZE`
    - `FILE_GENERIC_READ`
    - `FILE_READ_DATA`
    - `FILE_APPEND_DATA`
    - `FILE_READ_EA`
    - `FILE_READ_ATTRIBUTES`
    - `NT AUTHORITY\SYSTEM:(OI)(CI)F`
    - `BUILTIN\Administrators:(OI)(CI)F`

    > [!NOTE]
    > It's recommended to apply ACL security to the *MED-V Images* folder.

4. To apply ACL security to the *PrestagedImages* folder, set the following ACL:

    - `NT AUTHORITY\\Authenticated Users:(OI)(CI)(special access:)`
    - `READ_CONTROL`
    - `SYNCHRONIZE`
    - `FILE_GENERIC_READ`
    - `FILE_READ_DATA`
    - `FILE_APPEND_DATA`
    - `FILE_READ_EA`
    - `FILE_READ_ATTRIBUTES`
    - `NT AUTHORITY\SYSTEM:(OI)(CI)F`
    - `BUILTIN\Administrators:(OI)(CI)F`

    > [!NOTE]
    > It's recommended to apply ACL security to the *PrestagedImages* folder.

5. Push the image files (CKM and INDEX files) to the *PrestagedImages* folder.

    > [!NOTE]
    > After the image files have been pushed to the pre-stage folder, it is recommended to run a data integrity check and to mark the files as read-only.

6. Include the following parameter in the MED-V client installation: `Client.MSI VMSFOLDER="C:\MED-V Images"`.

## How to update the prestage location

1. The registry key, *PrestagedImagesPath*, points to the default image location. It's located in the following directory:

    - On an x86 - `HKEY_LOCAL_MACHINE\SOFTWARE\Kidaro`

    - On an x64 - `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432node`

2. If the image is in a different location, change the path.
