---
title: Deploy required features for UE-V 2.1 SP1
description: All Microsoft User Experience Virtualization (UE-V) 2.1 SP1 deployments require these features.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Deploy required features for UE-V 2.1 SP1

All Microsoft User Experience Virtualization (UE-V) 2.1 SP1 deployments require these features.

- [Deploy a Settings Storage Location](#ssl) that is accessible to end users.

    This is a standard network share that stores and retrieves user settings.

- [Choose the Configuration Method for UE-V](#config)

    UE-V can be deployed and configured using common management tools including group policy, Configuration Manager, or Windows Management Infrastructure and PowerShell.

- [Deploy a UE-V agent](#agent) to be installed on every computer that synchronizes settings.

    This monitors registered applications and the operating system for any settings changes and synchronizes those settings between computers.

The sections in this article describe how to deploy these features.

## <a href="" id="ssl"></a>Deploy a UE-V settings storage location

UE-V requires a location in which to store user settings in settings package files. You can configure this settings storage location in one of these ways:

- Create your own settings storage location.

- Use existing Active Directory for your settings storage location.

If you don't create a settings storage location, the UE-V agent uses Active Directory (AD) by default.

> [!NOTE]
> As a matter of [performance and capacity planning](prepare-a-ue-v-2x-deployment-new-uevv2.md#capacity) and to reduce problems with network latency, create settings storage locations on the same local networks where the users' computers reside. We recommend 20 MB of disk space per user for the settings storage location.

### Create a UE-V settings storage location

Before you define the settings storage location, you must create a root directory with read/write permissions for users who store settings on the share. The UE-V agent creates user-specific folders under this root directory.

The settings storage location is defined by setting the SettingsStoragePath configuration option, which you can configure by using one of these methods:

- When you [Deploy the UE-V agent](#agent) through a command-line parameter or in a batch script.

- Through [group policy](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md) settings.

- With the [System Center configuration pack](configuring-ue-v-2x-with-system-center-configuration-manager-2012-both-uevv2.md) for UE-V.

- After installation of the UE-V agent, by using [Windows PowerShell or Windows Management Instrumentation (WMI)](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md).

The path must be in a universal naming convention (UNC) path of the server and share. For example, `\\Server\Settingsshare\`. This configuration option supports the use of variables to enable specific synchronization scenarios. For example, you can use the `%username%\%computername%` variables to preserve the end user settings experience in these scenarios:

- Users that use multiple physical computers in your enterprise.

- Enterprise computers that are used by multiple end users.

The UE-V agent dynamically creates a user-specific settings storage path, with a hidden system folder named `SettingsPackages`, based on the configuration setting of **SettingsStoragePath**. The agent reads and writes settings to this location as defined by the registered UE-V settings location templates.

**UE-V settings are determined by a "Last write wins" rule:** If the settings storage location is the same for user with multiple managed computers, one UE-V agent reads and writes to the settings location independently of agents running on other computers. The last written settings and values are the ones applied when the next agent reads from the settings storage location.

**Deploy the settings storage location:** Follow these steps to define the settings storage location rather than using your existing Active Directory service. You should limit access to the settings storage share to those users that require it, as shown in the following tables.

## To deploy the UE-V network share

1.  Create a new security group for UE-V users.

2.  Create a new folder on the centrally located computer that stores the UE-V settings packages, and then grant the UE-V users access with group permissions to the folder. The administrator who supports UE-V must have permissions to this shared folder.

3.  Set the following share-level Server Message Block (SMB) permissions for the settings storage location folder.

    | User account                  | Recommended permissions |
    |-------------------------------|-------------------------|
    | Everyone                      | No permissions          |
    | Security group of UE-V users  | Full control            |

4.  Set the following NTFS file system permissions for the settings storage location folder.

    | User account                  | Recommended permissions                              | Folder                     |
    |-------------------------------|------------------------------------------------------|----------------------------|
    | Creator/owner                 | Full control                                         | Subfolders and files only  |
    | Security group of UE-V users  | List folder/read data, create folders/append data    | This folder only           |

With this configuration, the UE-V agent creates and secures a `Settingspackage` folder while it runs in the context of the user, and grants each user permission to create folders for settings storage. Users receive full control to their `Settingspackage` folder while other users can't access it.

> [!NOTE]
> If you create the settings storage share on a computer running a Windows Server operating system, configure UE-V to verify that either the local Administrators group or the current user is the owner of the folder where settings packages are stored. To enable this additional security, specify this setting in the Windows Server Registry Editor:
>
> 1.  Add a **REG_DWORD** registry key named `RepositoryOwnerCheckEnabled` to `HKEY_LOCAL_MACHINE\Software\Microsoft\UEV\Agent\Configuration`.
>
> 2.  Set the registry key value to `1`.

### Use Active Directory with UE-V 2.1 SP1

The UE-V agent uses Active Directory (AD) by default if a settings storage location isn't otherwise defined. In these cases, the UE-V agent dynamically creates the settings storage folder under the root of the AD home directory of each user. But, if a custom directory setting is configured in AD, then that directory is used instead.

## <a href="" id="config"></a>Choose the configuration method for UE-V 2.1 SP1

You want to figure out which configuration method you'll use to manage UE-V after deployment since this is the configuration method you use to deploy the UE-V agent. Typically, this is the configuration method that you already use in your environment, such as Windows PowerShell or Configuration Manager.

You can configure UE-V before, during, or after UE-V agent installation, depending on the configuration method that you use.

- [Group policy](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md): You can use your existing group policy infrastructure to configure UE-V before or after UE-V agent deployment. The UE-V group policy ADMX template enables the central management of common UE-V agent configuration options, and it includes settings to configure UE-V synchronization.

    **Installing the UE-V group policy ADMX templates:** group policy ADMX templates for UE-V configure the synchronization settings for the UE-V agent and enable the central management of common UE-V agent configuration settings by using an existing group policy infrastructure.

    Supported operating systems for the domain controller that deploys the group policy objects include the following:

    Windows Server 2008 R2

    Windows Server 2012 and Windows Server 2012 R2

- [Configuration Manager](configuring-ue-v-2x-with-system-center-configuration-manager-2012-both-uevv2.md): The UE-V configuration pack lets you use the compliance settings feature of System Center Configuration Manager 2012 SP1 or later to apply consistent configurations across sites where UE-V and Configuration Manager are installed.

- [Windows PowerShell and WMI](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md) You can use scripted commands for Windows PowerShell and Windows Management Instrumentation (WMI) to modify configurations after you install the UE-V agent.

    > [!NOTE]
    > Registry modification can result in data loss, or the computer becomes unresponsive. We recommend that you use other configuration methods.

- **Command-line or batch script installation:** Parameters that are used when you [Deploy the UE-V agent](#agent) configure many UE-V settings. Electronic software distribution systems, such as System Center 2012 Configuration Manager, use these parameters to configure their clients when they deploy and install the UE-V agent software.

## <a href="" id="agent"></a>Deploy the UE-V 2.1 SP1 agent

The UE-V agent is the core of a UE-V deployment and must run on each computer that uses UE-V to synchronize application and Windows settings.

**UE-V agent installation files:** A single installation file, AgentSetup.exe, installs the UE-V agent on both 32-bit and 64-bit operating systems. In addition, AgentSetupx86.msi or AgentSetupx64.msi architecture-specific Windows Installer files are provided, and since they're smaller, they might streamline the agent deployments. The [command-line parameters for the AgentSetup.exe installer](#params) are supported for the Windows Installer installation as well.

> [!IMPORTANT]
> During UE-V agent installation or uninstallation, you can either use the AgentSetup.exe file or the AgentSetup&lt;arch&gt;.msi file, but not both. The same file must be used to uninstall the UE-V agent that was used to install the UE-V agent.

### To deploy the UE-V agent

You can use the following methods to deploy the UE-V agent:

- An electronic software distribution (ESD) solution system, such as Configuration Manager, that can install a Windows Installer (.msi) file.

- An installation script that references the Windows Installer (.msi) file that is stored centrally on a share.

- An installation program that you run manually on the computer.

Use the following procedure to deploy the UE-V agent from a network share.

### To install and configure the UE-V agent from a network share

1.  Stage the UE-V agent installation file AgentSetup.exe on a network share to which users have Read permission.

2.  Deploy a script to user computers that installs the UE-V agent. The script should specify the settings storage location.

## Deployment options

Be sure to use the correct variable format when you install the UE-V agent. The following table provides examples of deployment options for using the AgentSetup.exe or the Windows Installer (.msi) files.

### Command prompt

When you install the UE-V agent at a command prompt, use the `%^username%` variable format. If quotation marks are required because of spaces in the settings storage path, use a batch script file for deployment.

`AgentSetup.exe /quiet /norestart /log "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\\server\settingsshare\%username%`

`msiexec.exe /i "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\\server\settingsshare\%username%`

### Batch script

When you install the UE-V agent from a batch script file, use the `%%username%%` variable format. If you use this installation method, you must escape the variable with the %% characters. Without this character, the script expands the *username* variable at installation time, rather than at run time, which causes UE-V to use a single settings storage location for all users.

`AgentSetup.exe /quiet /norestart /log "%temp%\UE-VAgentInstaller.log" SettingsStoragePath="\\server\settingsshare%%username%%"`

`msiexec.exe /i "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log" SettingsStoragePath="\\server\settingsshare%%username%%"`

### Windows PowerShell

When you install the UE-V agent from a Windows PowerShell prompt or a Windows PowerShell script, use the `%username%` variable format.

`AgentSetup.exe /quiet /norestart /log "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\server\settingsshare%username%`

`msiexec.exe /i "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\server\settingsshare%username%`

### Electronic software distribution

When you install the UE-V agent by using Configuration Manager, use the `^%username^%` variable format.

`AgentSetup.exe /quiet /norestart /log "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\server\settingsshare^%username^%`

`msiexec.exe /i "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\server\settingsshare^%username^%`

> [!NOTE]
> The installation of the UE-V agent requires administrator rights, and the computer requires a restart before the UE-V agent can run.

### <a href="" id="params"></a>Command-line parameters for UE-V agent deployment

The following sections detail the command-line parameters of the UE-V agent.

### `/help` or `/h` or `/?`

Displays the AgentSetup.exe usage dialog box.

### `SettingsStoragePath`

Indicates the Universal Naming Convention (UNC) path that defines where settings are stored.

> [!IMPORTANT]
> You must specify a SettingsStoragePath in UE-V 2.1 SP1. You can set the AdHomePath string to specify that the user's Active Directory home path is used. For example, `SettingsStoragePath = \share\path|AdHomePath`.

`%username%` or `%computername%` environment variables are accepted. Scripting can require escaped variables.

Default: None

### `SettingsStoragePathReg`

Gets the SettingsStoragePath value from the registry during installation.

At the command prompt, type the following example to force UE-V to use the Active Directory home path instead of a specific UNC.

`msiexec.exe /i AgentSetupx64.msi acceptlicenseterms=true SettingsStoragePathReg=TRUE /quiet /norestart`

### `SettingsTemplateCatalogPath`

Indicates the Universal Naming Convention (UNC) path that defines the location that was checked for new settings location templates.

Only required for custom settings location templates.

### `RegisterMSTemplates`

Specifies whether the default Microsoft templates should be registered during installation.

True | False

Default: True

### `SyncMethod`

Specifies which synchronization method should be used.

SyncProvider | None

Default: SyncProvider

### `SyncTimeoutInMilliseconds`

Specifies the number of milliseconds that the computer waits before time-out when it retrieves user settings from the settings storage location.

Default: 2,000 milliseconds (wait up to 2 seconds)

### `SyncEnabled`

Specifies whether UE-V synchronization is enabled or disabled.

True | False

Default: True

### `MaxPackageSizeInBytes`

Specifies a settings package file size in bytes when the UE-V agent reports that files exceed the threshold.

Default: None (no warning threshold)

### `CEIPEnabled`

Specifies the setting for participation in the Customer Experience Improvement program. If set to **True**, installer information is uploaded to the Microsoft Customer Experience Improvement Program site. If set to **False**, no information is uploaded.

True | False

Default: False

### `NoRestart`

Supports deferral of the restart of the computer after the UE-V agent is installed.

### `INSTALLFOLDER`

Enables a different installation folder to be set for the UE-V agent or UE-V Generator.

### `MUENABLED`

Enables Setup to accept the option to be included in the Microsoft Update program.

### `ACCEPTLICENSETERMS`

Lets UE-V be installed silently. This must be set to **True** to install UE-V silently and bypass the requirement that the user accepts the UE-V license terms. If set to **False** or left empty, the user receives an error message and UE-V isn't installed.

> [!IMPORTANT]
> This parameter is required to install UE-V silently.

### `NORESTART`

Prevents a mandatory restart after the UE-V agent is installed.

### Update the UE-V agent

Updates for the UE-V agent software are provided through Microsoft Update. You can deploy UE-V agent updates by using Enterprise Software Distribution (ESD) infrastructure systems.

During a UE-V agent upgrade, the default group of settings location templates for common Microsoft applications and Windows settings can be updated.

### Upgrade the UE-V 2.1 SP1 Agent

The UE-V 2.1 SP1 Agent introduces many new features and modifies how and when the agent uploads content to the settings storage share. The upgrade process automates these changes. To upgrade the UE-V agent, run the UE-V agent install package (AgentSetup.exe, AgentSetupx86.msi, or AgentSetupx64.msi) on users' computers.

> [!NOTE]
> When you upgrade the UE-V agent, you must use the same installer type (.exe file or .msi packet) that installed the previous UE-V agent. For example, use the UE-V 2 AgentSetup.exe to upgrade UE-V 1.0 agents that were installed by using AgentSetup.exe.

The following configurations are preserved when the agent setup program runs:

- Settings storage path

- Registry settings

- Scheduled tasks (Interval settings are reset to their defaults)

> [!NOTE]
> A computer with UE-V 2.1 SP1 settings location templates that are registered in the UE-V 1.0 Agent register errors in the Windows Event Log.

You can use Microsoft System Center 2012 Configuration Manager or another enterprise software distribution tool to automate and distribute the UE-V agent upgrade.

#### Recommendations

We recommend that you upgrade all of the UE-V 1.0 agents in a computing environment, but it isn't required. UE-V 2.1 SP1 settings location templates can interact with a UE-V 1.0 agent because they only share the settings from the settings storage path. We recommend, however, that you move the deployments to a single agent version to simplify management and to support UE-V.

### Repair the UE-V agent after an unsuccessful upgrade

You might experience errors after you attempt one of the following operations:

- Upgrade from UE-V 1.0 to UE-V 2.

- Upgrade to a newer version of Windows, for example, from Windows 7 to Windows 8 or from Windows 8 to Windows 8.1.

- Uninstall the agent after upgrading the UE-V agent.

To resolve any issues, attempt to repair the UE-V agent by entering this command at a command prompt on the computer where the agent is installed.

```command
msiexec.exe /f "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log
```

You can then retry the uninstall process or upgrade by installing the newer version of the UE-V agent.

## Related articles

[Prepare a UE-V 2.1 SP1 deployment](prepare-a-ue-v-2x-deployment-new-uevv2.md)

[Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md)
