---
title: Get started with UE-V 2.1 SP1
description: Follow the steps in this guide to quickly deploy Microsoft User Experience Virtualization (UE-V) 2.1 SP1 in a small test environment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 02/13/2017
---

# Get started with UE-V 2.1 SP1

Follow the steps in this guide to quickly deploy Microsoft User Experience Virtualization (UE-V) 2.1 SP1 in a small test environment. This article helps you determine whether UE-V is the right solution to manage user settings across multiple devices within your enterprise.

> [!NOTE]
> The information in this article is repeated in greater detail throughout the rest of the documentation. If you already know that UE-V 2 is the right solution and you don't need to evaluate it, see [Prepare a UE-V 2.1 SP1 deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md).

The standard installation of UE-V synchronizes the default Microsoft Windows and Office settings and many Windows app settings. Make sure your test environment includes two or more user computers that share network access.

- [Step 1: Confirm prerequisites](#step1): Make sure your environment is able to run UE-V, including details about supported configurations.

- [Step 2: Deploy the settings storage location for UE-V 2](#step2): All UE-V deployments require a location for settings packages that contain the synchronized setting values.

- [Step 3: Deploy the UE-V 2 agent](#step3): To synchronize settings using UE-V, devices must have the UE-V agent installed and running.

- [Step 4: Test your UE-V 2 evaluation deployment](#step4): Run a few tests on two computers that have the UE-V agent installed and see how UE-V works.

> [!TIP]
> You can also do more steps to configure line-of-business and non-Microsoft applications to synchronize their settings using UE-V. For more information, see [Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md).

## <a href="" id="step1"></a>Step 1: Confirm prerequisites

Before you proceed, make sure your environment includes these requirements for running UE-V.

| Operating system | Edition | Service pack | System architecture | Windows PowerShell | Microsoft .NET Framework |
|--|--|--|--|--|--|
| Windows 7 | Ultimate, Enterprise, or Professional Edition | SP1 | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4 or higher |
| Windows Server 2008 R2 | Standard, Enterprise, Datacenter, or Web Server | SP1 | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4 or higher |
| Windows 8.1 | Enterprise or Pro | None | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 |
| Windows Server 2012 or Windows Server 2012 R2 | Standard or Datacenter | None | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 |
| Windows 10, pre-1607 version | Enterprise or Pro | None | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 |
| Windows Server 2016 | Standard or Datacenter | None | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 |

> [!NOTE]
> Starting with Windows 10, version 1607, UE-V is included with [Windows 10 for Enterprise](https://www.microsoft.com/windows/business) and is no longer part of the Microsoft Desktop Optimization Pack. For more information, see [UE-V for Windows overview](../ue-v/uev-for-windows.md).

- **MDOP license:** This technology is a part of the Microsoft Desktop Optimization Pack (MDOP). Enterprise customers can get MDOP with Microsoft Software Assurance.

- **Administrative credentials** for any computer where you install UE-V.

## <a href="" id="step2"></a>Step 2: Deploy the settings storage location for UE-V 2

You need to deploy a settings storage location, which is a standard network share where user settings are stored in a settings package file. When you create the settings storage share, you should limit access to users that require it. For more information, see [Deploy a settings storage location](deploy-required-features-for-ue-v-2x-new-uevv2.md#ssl).

### Create a network share

1.  Create a new security group and add UE-V users to it.

2.  Create a new folder on the centrally located computer that stores the UE-V settings packages, and then grant the UE-V users access with group permissions to the folder. The administrator who supports UE-V must have permissions to this shared folder.

3.  Assign UE-V users permission to create a directory when they connect. Grant full permission to all subdirectories of that directory, but block access to anything above.

    1.  Set the following share-level Server Message Block (SMB) permissions for the settings storage location folder.

        | User account                  | Recommended permissions |
        |-------------------------------|-------------------------|
        | Everyone                      | No permissions          |
        | Security group of UE-V users  | Full control            |

    2.  Set the following NTFS file system permissions for the settings storage location folder.

        | User account                 | Recommended permissions                         | Folder                     |
        |------------------------------|-------------------------------------------------|----------------------------|
        | Creator/owner                | Full control                                    | Subfolders and files only  |
        | Security group of UE-V users | List folder/read data, create folders/append data | This folder only           |

> [!IMPORTANT]
> If you create the settings storage share on a computer running a Windows Server operating system, configure UE-V to verify that either the local Administrators group or the current user is the owner of the folder where settings packages are stored. To enable this additional security, specify this setting in the Windows Server Registry Editor:
>
> 1. Add a **REG_DWORD** registry key named `RepositoryOwnerCheckEnabled` to `HKEY_LOCAL_MACHINE\Software\Microsoft\UEV\Agent\Configuration`.
>
> 2. Set the registry key value to `1`.

## <a href="" id="step3"></a>Step 3: Deploy the UE-V 2 agent

The UE-V agent synchronizes application and Windows settings between users' computers and devices. For evaluation purposes, install the agent on at least two computers in your test environment that belong to the same user.

Run the AgentSetup.exe file from the command line to install the UE-V agent. It installs on both 32-bit and 64-bit operating systems.

``` syntax
AgentSetup.exe SettingsStoragePath=\\server\settingsshare\%username%
```

You must specify the SettingsStoragePath command line parameter as the network share from Step 2. For more information, see [Deploy a settings storage location](deploy-required-features-for-ue-v-2x-new-uevv2.md#agent).

## <a href="" id="step4"></a>Step 4: Test your UE-V 2 evaluation deployment

You can now run a few tests on your UE-V evaluation deployment to see how UE-V works.

1.  On the first computer (Computer A), make one or more of these changes:

    1.  Open to Windows Desktop and move the taskbar to a different location in the window.

    2.  Change the default fonts.

    3.  Open Calculator and set to **scientific**.

    4.  Change the behavior of any Windows app, as detailed in [Managing UE-V 2.1 SP1 settings location templates using Windows PowerShell and WMI](managing-ue-v-2x-settings-location-templates-using-windows-powershell-and-wmi-both-uevv2.md).

    5.  Disable Microsoft Account settings synchronization and Roaming Profiles.

2.  Sign out Computer A. Settings are saved in a UE-V settings package when users lock, sign out, exit an application, or when the sync provider runs (every 30 minutes by default).

3.  Sign in to the second computer (Computer B) as the same user as Computer A.

4.  Open to Windows Desktop and verify that the taskbar location matches that of Computer A. Verify that the default fonts match and that Calculator is set to **scientific**. Also verify the change you made to any Windows app.

You can change the settings in Computer B back to the original Computer A settings. Then sign out Computer B and sign in to Computer A to verify the changes.

## Other resources for this product

- [Microsoft User Experience Virtualization (UE-V) 2.1 SP1](index.md)

- [Prepare a UE-V 2.1 SP1 deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md)

- [Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

- [Troubleshooting UE-V 2.1 SP1](troubleshooting-ue-v-2x-both-uevv2.md)

- [Technical reference for UE-V 2.1 SP1](technical-reference-for-ue-v-2x-both-uevv2.md)
