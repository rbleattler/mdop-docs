---
title: Prepare a UE-V 2.1 SP1 deployment
description: There's some planning and preparation to do before you deploy Microsoft User Experience Virtualization (UE-V) 2.1 as a solution for synchronizing settings between devices that users access in your enterprise.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/19/2017
---

# Prepare a UE-V 2.1 SP1 deployment

There's some planning and preparation to do before you deploy Microsoft User Experience Virtualization (UE-V) 2.1 as a solution for synchronizing settings between devices that users access in your enterprise. This article helps you determine what type of deployment to do and what preparation you can make beforehand so that your deployment is successful.

The following list summarizes the tasks to do to deploy UE-V:

- Plan your UE-V deployment. Before you deploy anything, a good first step is to do some planning so that you can determine which UE-V features to deploy.

- [Deploy required features for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md).

    Every UE-V deployment requires these activities:

  - [Define a settings storage location](deploy-required-features-for-ue-v-2x-new-uevv2.md#ssl).
  - [Decide how to deploy the UE-V agent and manage UE-V configurations](deploy-required-features-for-ue-v-2x-new-uevv2.md#config).
  - [Install the UE-V agent](deploy-required-features-for-ue-v-2x-new-uevv2.md#agent) on every user computer that needs settings synchronized.

- Optionally, you can [Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md).

    Planning helps you figure out whether you want UE-V to support the synchronization of settings for line-of-business or non-Microsoft applications, which requires these UE-V features:

  - [Install the UEV generator](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#uevgen) so you can create, edit, and validate the custom settings location templates required to synchronize custom application settings.
  - [Create custom settings location templates](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#createcustomtemplates) by using the UE-V generator.
  - [Deploy a UE-V settings template catalog](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#deploycatalogue) that you use to store your custom settings location templates.

This workflow diagram provides a high-level understanding of a UE-V deployment and the decisions that determine how you deploy UE-V in your enterprise.

![A conceptual workflow diagram of the UE-V deployment preparation process.](images/deploymentworkflow.png)

## <a href="" id="deciding"></a>Decide whether to synchronize settings for custom applications

In a UE-V deployment, many settings are automatically synchronized. But you can also customize UE-V to synchronize settings for other applications, such as line-of-business and non-Microsoft apps.

Deciding if you want UE-V to synchronize settings for custom applications is probably the most important part of planning your UE-V deployment. The sections in this article help you make that decision.

### <a href="" id="autosyncsettings"></a>Settings that are automatically synchronized in a UE-V deployment

This section provides information about the settings that are synchronized by default in UE-V, including the following areas:

- Desktop applications whose settings are synchronized by default.

- Windows desktop settings that are synchronized by default.

- A statement of support for Windows app setting synchronization.

To download a complete list of the specific Microsoft Office settings that are synchronized by UE-V, see [User Experience Virtualization (UE-V) settings templates for Microsoft Office](https://www.microsoft.com/download/details.aspx?id=46367).

### Desktop applications synchronized by default in UE-V 2.1 SP1

When you install the UE-V 2.1 SP1 agent, it registers a default group of settings location templates that capture settings values for these common Microsoft applications.

#### Microsoft Office 2010 applications

[Download a list of all settings synced](https://www.microsoft.com/download/details.aspx?id=46367).

- Microsoft Word 2010
- Microsoft Excel 2010
- Microsoft Outlook 2010
- Microsoft Access 2010
- Microsoft Project 2010
- Microsoft PowerPoint 2010
- Microsoft Publisher 2010
- Microsoft Visio 2010
- Microsoft SharePoint Workspace 2010
- Microsoft InfoPath 2010
- Microsoft Lync 2010
- Microsoft OneNote 2010
- Microsoft SharePoint Designer 2010

#### Microsoft Office 2013 applications

[Download a list of all settings synced](https://www.microsoft.com/download/details.aspx?id=46367).

- Microsoft Word 2013
- Microsoft Excel 2013
- Microsoft Outlook 2013
- Microsoft Access 2013
- Microsoft Project 2013
- Microsoft PowerPoint 2013
- Microsoft Publisher 2013
- Microsoft Visio 2013
- Microsoft InfoPath 2013
- Microsoft Lync 2013
- Microsoft OneNote 2013
- Microsoft SharePoint Designer 2013
- Microsoft Office 2013 Upload Center
- Microsoft OneDrive for Business 2013

The UE-V 2.1 SP1 Microsoft Office 2013 settings location templates include improved Outlook signature support. We added synchronization of default signature settings for new, reply, and forwarded emails.

> [!NOTE]
> An Outlook profile must be created for any device on which a user wants to sync their Outlook signature. If the profile isn't already created, the user can create one, and then restart Outlook on that device to enable signature synchronization.

#### Internet Explorer browser options

These options include favorites, home page, tabs, and toolbars.

- Internet Explorer 8
- Internet Explorer 9
- Internet Explorer 10
- Internet Explorer 11

> [!NOTE]
> UE-V doesn't roam settings for Internet Explorer cookies.

#### Windows accessories

- Microsoft Calculator
- Notepad
- WordPad

> [!NOTE]
> UE-V 2.1 SP1 doesn't synchronize settings between the Microsoft Calculator in Windows 10 and the Microsoft Calculator in previous operating systems.

### <a href="" id="autosyncsettings2"></a>Windows settings synchronized by default

UE-V includes settings location templates that capture settings values for these Windows settings.

| Windows settings | Description | Apply on | Export on | Default state |
|--|--|--|--|--|
| Desktop background | Currently active desktop background or wallpaper. | Sign in, unlock, remote connect, Scheduled Task events. | Sign out, lock, remote disconnect, user clicking **Sync Now** in Company Settings Center, or scheduled task interval | Enabled |
| Ease of Access | Accessibility and input settings, Microsoft Magnifier, Narrator, and on-Screen Keyboard. | Sign in only. | Sign out, user selecting **Sync Now** in Company Settings Center, or scheduled task interval | Enabled |
| Desktop settings | Start menu and Taskbar settings, Folder options, Default desktop icons, Additional clocks, and Region and Language settings. | Sign in only. | Sign out, user clicking **Sync Now** in Company Settings Center, or scheduled task | Enabled |

> [!NOTE]
> Starting in Windows 8, UE-V doesn't roam settings related to the Start screen, such as items and locations. In addition, UE-V doesn't support synchronization of pinned taskbar items or Windows file shortcuts.

> [!IMPORTANT]
> UE-V 2.1 SP1 roams taskbar settings between Windows 10 devices. However, UE-V doesn't synchronize taskbar settings between Windows 10 devices and devices running previous operating systems.

| Settings group | Category | Capture | Apply |
|--|--|--|--|
| **Application Settings** | Windows apps | Close app<br>Windows app settings change event | Start the UE-V App Monitor at startup<br>Open app<br>Windows App Settings change event<br>Arrival of a settings package |
|  | Desktop applications | Application closes | Application opens and closes |
| **Desktop settings** | Desktop background | Lock or sign out | Sign in, unlock, remote connect, notification of new package arrival, user selects **Sync Now** in Company Settings Center, or scheduled task runs |
|  | Ease of Access (Common - Accessibility, Narrator, Magnifier, On-Screen-Keyboard) | Lock or sign out | Sign in |
|  | Ease of Access (Shell - Audio, Accessibility, Keyboard, Mouse) | Lock or sign out | Sign in, unlock, remote connect, notification of new package arrival, user selects **Sync Now** in Company Settings Center, or scheduled task runs |
|  | Desktop settings | Lock or sign out | Sign in |

### UE-V-support for Windows apps

For Windows apps, the app developer specifies the settings that are synchronized. You can specify which Windows apps are enabled for settings synchronization.

To display a list of Windows apps that can synchronize settings on a computer with their package family name, enabled status, and enabled source, at a Windows PowerShell command prompt, enter: `Get-UevAppxPackage`

> [!NOTE]
> As of Windows 8, UE-V doesn't synchronize Windows app settings if the domain user links their sign-in credentials to their Microsoft Account. This linking synchronizes settings to Microsoft OneDrive so UE-V, which disables synchronization of Windows app settings.

### UE-V-support for roaming printers

UE-V 2.1 SP1 lets network printers roam between devices so that a user has access to their network printers when logged on to any device on the network. This includes roaming the printer that they set as the default.

Printer roaming in UE-V requires one of these scenarios:

- The print server can download the required driver when it roams to a new device.

- The driver for the roaming network printer is preinstalled on any device that needs to access that network printer.

- The printer driver can be obtained from Windows Update.

> [!NOTE]
> The UE-V printer roaming feature doesn't roam printer settings or preferences, such as printing double-sided.

### <a href="" id="determinesettingssync"></a>Determine whether you need settings synchronized for other applications

After you review the settings that UE-V synchronizes automatically, decide whether to synchronize settings for other applications. This decision determines how you deploy UE-V throughout your enterprise.

As an administrator, when you consider which desktop applications to include in your UE-V solution, consider which settings users can customize, and how and where the application stores its settings. Not all desktop applications have settings that can be customized or that users routinely customize. In addition, not all desktop applications settings can safely be synchronized across multiple computers or environments.

In general, you can synchronize settings that meet the following criteria:

- Settings that are stored in user-accessible locations. For example, don't synchronize settings that are stored in System32 or outside the HKEY\_CURRENT\_USER (HKCU) section of the registry.

- Settings that aren't specific to the particular computer. For example, exclude network or hardware configurations.

- Settings that can be synchronized between computers without risk of corrupted data. For example, don't use settings that are stored in a database file.

### <a href="" id="checklistsettingssync"></a>Checklist for evaluating custom applications

If you decided that you need settings synchronized for other applications, you can use this checklist to help figure out which applications to include.

- Does this application contain settings that the user can customize?
- Is it important for the user that these settings are synchronized?
- Are these user settings already managed by an application management or settings policy solution? UE-V applies application settings at application startup and Windows settings at sign in, unlock, or remote connect events. If you use UE-V with other settings sharing solutions, users might experience inconsistency across synchronized settings.
- Are the application settings specific to the computer? Application preferences and customizations that are associated with hardware or specific computer configurations don't consistently synchronize across sessions and can cause a poor application experience.
- Does the application store settings in the Program Files directory or in the file directory that is located in the **Users**\[User name]\**AppData**\**LocalLow** directory? Application data that is stored in either of these locations usually shouldn't synchronize with the user, because this data is specific to the computer or because the data is too large to synchronize.
- Does the application store any settings in a file that contains other application data that shouldn't synchronize? UE-V synchronizes files as a single unit. If settings are stored in files that include application data other than settings, then synchronizing this other data can cause a poor application experience.
- How large are the files that contain the settings? The performance of the settings synchronization is affected by large files. Including large files can affect the performance of settings synchronization.

## <a href="" id="considerations"></a>Other considerations when preparing a UE-V deployment

You should also consider these things when you prepare to deploy UE-V:

- [Managing credentials synchronization](#creds)

- [Windows app settings synchronization](#appxsettings)

- [Custom UE-V settings location templates](#custom)

- [Unintentional user settings configurations](#prevent)

- [Performance and capacity](#capacity)

- [High availability](#high)

- [Computer clock synchronization](#clocksync)

### <a href="" id="creds"></a>Managing credentials synchronization in UE-V 2.1 SP1

Many enterprise applications, including Microsoft Outlook and Lync, prompt users for their domain credentials at sign in. Users have the option of saving their credentials to disk to prevent having to enter them every time they open these applications. Enabling roaming credentials synchronization lets users save their credentials on one computer and avoid reentering them on every computer they use in their environment. Users can synchronize some domain credentials with UE-V 2.1 SP1.

> [!IMPORTANT]
> Credentials synchronization is disabled by default. To implement this feature, you must explicitly enable credentials synchronization during deployment.

UE-V 2.1 SP1 can synchronize enterprise credentials, but don't roam credentials intended only for use on the local computer.

Credentials are synchronous settings, meaning they're applied to your profile the first time you sign in to your computer after UE-V synchronizes.

> [!NOTE]
> Credentials are encrypted during synchronization.

Credentials synchronization is managed by its own settings location template, which is disabled by default. You can enable or disable this template through the same methods used for other templates. The template identifier for this feature is RoamingCredentialSettings.

> [!IMPORTANT]
> If you use Active Directory credential roaming in your environment, don't also enable the UE-V credential roaming template.

Use one of the following methods to enable credentials synchronization:

- [Company Settings Center](configuring-the-company-settings-center-for-ue-v-2x-both-uevv2.md): To enable credential synchronization, in Windows Settings, enable the Roaming Credential Settings option. This setting only appears in Company Settings Center if your account isn't configured to synchronize settings using a Microsoft Account.

- [Windows PowerShell](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md):

  - This PowerShell cmdlet enables credential synchronization:

    ```powershell
    Enable-UevTemplate RoamingCredentialSettings
    ```

  - This PowerShell cmdlet disables credential synchronization:

    ```powershell
    Disable-UevTemplate RoamingCredentialSettings
    ```

- [Group policy](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md): To enable credential synchronization through group policy, first [deploy the latest MDOP ADMX template](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md). Credentials synchronization is managed with the Windows settings. To manage this feature with group policy, enable the **Synchronize Windows** settings policy.

    1.  Open Group Policy Editor and navigate to **User Configuration - Administrative Templates - Windows Components - Microsoft User Experience Virtualization**.

    2.  Double-click on **Synchronize Windows settings**.

    3.  If this policy is enabled, you can enable credentials synchronization by checking the **Roaming Credentials** check box, or disable credentials synchronization by unchecking it.

    4.  Select **OK**.

### Credential locations synchronized by UE-V

Credential files saved by applications into the following locations are synchronized:

- `%UserProfile%\AppData\Roaming\Microsoft\Credentials\`

- `%UserProfile%\AppData\Roaming\Microsoft\Crypto\`

- `%UserProfile%\AppData\Roaming\Microsoft\Protect\`

- `%UserProfile%\AppData\Roaming\Microsoft\SystemCertificates\`

Credentials saved to other locations aren't synchronized by UE-V.

### <a href="" id="appxsettings"></a>Windows app settings synchronization

UE-V manages Windows app settings synchronization in three ways:

- **Sync Windows Apps:** Allow or deny any Windows app synchronization.

- **Windows App List:** Synchronize a list of Windows apps.

- **Unlisted Default Sync Behavior:** Determine the synchronization behavior of Windows apps that aren't in the Windows app list.

For more information, see the [Windows app list](managing-ue-v-2x-settings-location-templates-using-windows-powershell-and-wmi-both-uevv2.md#win8applist).

### <a href="" id="custom"></a>Custom UE-V settings location templates

If you deploy UE-V to synchronize settings for custom applications, use the UE-V generator to create custom settings location templates for those desktop applications. After you create and test a custom settings location template in a test environment, you can deploy the settings location templates to computers in the enterprise.

Custom settings location templates must be deployed with an existing deployment infrastructure, like an enterprise software distribution (ESD) method such as System Center Configuration Manager, with preferences, or by configuring an UE-V settings template catalog. Templates that are deployed with Configuration Manager or group policy must be registered by using UE-V WMI or Windows PowerShell.

For more information about custom settings location templates, see [Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md). For more information about using UE-V with Configuration Manager, see [Configuring UE-V 2.1 SP1 with System Center Configuration Manager 2012](configuring-ue-v-2x-with-system-center-configuration-manager-2012-both-uevv2.md).

### <a href="" id="prevent"></a>Prevent unintentional user settings configuration

UE-V downloads new user settings information from a settings storage location and applies the settings to the local computer in these instances:

- Every time an application is started that has a registered UE-V template.

- When a user signs in to a computer.

- When a user unlocks a computer.

- When a connection is made to a remote desktop computer that has UE-V installed.

- When the Sync Controller Application scheduled task is run.

If UE-V is installed on computer A and computer B, and the settings that you want for the application are on computer A, then computer A should open and close the application first. If the application is opened and closed on computer B first, then the application settings on computer A are configured to the application settings on computer B. Settings are synchronized between computers on per-application basis. Over time, settings become consistent between computers as they're opened and closed with preferred settings.

This scenario also applies to Windows settings. If the Windows settings on computer B should be the same as the Windows settings on computer A, then the user should sign in and sign out computer A first.

If the user settings that the user wants are applied in the wrong order, they can be recovered by performing a restore operation for the specific application or Windows configuration on the computer on which the settings were overwritten. For more information, see [Manage administrative backup and restore in UE-V 2.1 SP1](manage-administrative-backup-and-restore-in-ue-v-2x-new-topic-for-21.md).

### <a href="" id="capacity"></a>Performance and capacity planning

Specify your requirements for UE-V with standard disk capacity and network health monitoring.

UE-V uses a Server Message Block (SMB) share for the storage of settings packages. The size of settings packages varies depending on the settings information for each application. While most settings packages are small, the synchronization of potentially large files, such as desktop images, can result in poor performance, particularly on slower networks.

To reduce problems with network latency, create settings storage locations on the same local networks where the users' computers reside. We recommend 20 MB of disk space per user for the settings storage location.

By default, UE-V synchronization times out after 2 seconds to prevent excessive lag due to a large settings package. You can configure the SyncMethod=SyncProvider setting by using [group policy objects](configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md).

### <a href="" id="high"></a>High availability for UE-V

The UE-V settings storage location and settings template catalog support storing user data on any writable share. To ensure high availability, follow these criteria:

- Format the storage volume with an NTFS file system.

- The share can use Distributed File System (DFS) but there are restrictions. Specifically, Distributed File System Replication (DFS-R) single target configuration with or without a Distributed File System Namespace (DFS-N) is supported. Likewise, only single target configuration is supported with DFS-N. For more information, see [Information about Microsoft support policy for a DFS-R and DFS-N deployment scenario](/troubleshoot/windows-server/networking/support-policy-for-dfsr-dfsn-deployment).

    In addition, because SYSVOL uses DFS-R for replication, SYSVOL can't be used for UE-V data file replication.

- Configure the share permissions and NTFS access control lists (ACLs) as specified in [Deploying the settings storage location for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md#ssl).

- Use file server clustering along with the UE-V agent to provide access to copies of user state data if communication fails.

- You can store the settings storage path data (user data) and settings template catalog templates on clustered shares, on DFS-N shares, or on both.

### <a href="" id="clocksync"></a>Synchronize computer clocks for UE-V settings synchronization

Computers that run the UE-V agent must use a time server to maintain a consistent settings experience. UE-V uses time stamps to determine if settings must be synchronized from the settings storage location. If the computer clock is inaccurate, older settings can overwrite newer settings, or the new settings might not be saved to the settings storage location.

## <a href="" id="prereqs"></a>Confirm prerequisites and supported configurations for UE-V

Before you proceed, make sure your environment includes these requirements for running UE-V.

| Operating system | Edition | Service pack | System architecture | Windows PowerShell | Microsoft .NET Framework |
|--|--|--|--|--|--|
| Windows 7 | Ultimate, Enterprise, or Professional Edition | SP1 | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 or higher for UE-V 2.1.<br>.NET Framework 4 or higher for UE-V 2.0. |
| Windows Server 2008 R2 | Standard, Enterprise, Datacenter, or Web Server | SP1 | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 or higher for UE-V 2.1.<br>.NET Framework 4 or higher for UE-V 2.0. |
| Windows 8 and Windows 8.1 | Enterprise or Pro | None | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 or higher |
| Windows 10, pre-1607 version | Enterprise or Pro | None | 32-bit or 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.6 |
| Windows Server 2012 and Windows Server 2012 R2 | Standard or Datacenter | None | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.5 or higher |
| Windows Server 2016 | Standard or Datacenter | None | 64-bit | Windows PowerShell 3.0 or higher | .NET Framework 4.6 or higher |

- **MDOP license:** This technology is a part of the Microsoft Desktop Optimization Pack (MDOP). Enterprise customers can get MDOP with Microsoft Software Assurance.

- **Administrative credentials** for any computer where you install UE-V.

> [!NOTE]
>
> - Starting with WIndows 10, version 1607, UE-V is included with [Windows 10 for Enterprise](https://www.microsoft.com/windows/business) and is no longer part of the Microsoft Desktop Optimization Pack.
>
> - The UE-V Windows PowerShell feature of the UE-V agent requires .NET Framework 4 or higher and Windows PowerShell 3.0 or higher to be enabled. [Download Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595).
>
> - Install .NET Framework 4 or .NET Framework 4.5 on computers that run the Windows 7 or the Windows Server 2008 R2 operating system. The Windows 8, Windows 8.1, and Windows Server 2012 operating systems come with .NET Framework 4.5 installed. The Windows 10 operating system comes with .NET Framework 4.6 installed.
>
> - The **Delete Roaming Cache** policy for mandatory profiles isn't supported with UE-V and shouldn't be used.

There are no special memory (RAM) requirements specific to UE-V.

### Synchronization of settings through the sync provider

Sync provider is the default setting for users, which synchronizes a local cache with the settings storage location in these instances:

- Sign in/sign out

- Lock/unlock

- Remote desktop connect/disconnect

- Application open/close

A scheduled task manages this synchronization of settings every 30 minutes or through certain trigger events for certain applications. For more information, see [Changing the frequency of UE-V 2.1 SP1 scheduled tasks](changing-the-frequency-of-ue-v-2x-scheduled-tasks-both-uevv2.md).

The UE-V agent synchronizes user settings for computers that aren't always connected to the enterprise network (remote computers and laptops) and computers that are always connected to the network (computers that run Windows Server and host virtual desktop interface (VDI) sessions).

**Synchronization for computers with always-available connections:** When you use UE-V on computers that are always connected to the network, you must configure the UE-V agent to synchronize settings by using the *SyncMethod=None* parameter, which treats the settings storage server as a standard network share. In this configuration, the UE-V agent can be configured to notify if the import of the application settings is delayed.

Enable this configuration through one of these methods:

- During UE-V installation, at the command prompt or in a batch file, set the AgentSetup.exe parameter *SyncMethod = None*. [Deploying the UE-V 2.1 SP1 agent](deploy-required-features-for-ue-v-2x-new-uevv2.md#agent) provides more information.

- After the UE-V installation, use the Settings Management feature in System Center 2012 Configuration Manager or the MDOP ADMX templates to push the *SyncMethod = None* configuration.

- Use Windows PowerShell or Windows Management Instrumentation (WMI) to set the *SyncMethod = None* configuration.

    > [!NOTE]
    > These last two methods don't work for pooled virtual desktop infrastructure (VDI) environments.

You must restart the computer before the settings start to synchronize.

> [!NOTE]
> If you set *SyncMethod = None*, any settings changes are saved directly to the server. If the network connection to the settings storage path isn't found, then the settings changes are cached on the device and are synchronized the next time that the sync provider runs. If the settings storage path isn't found and the user profile is removed from a pooled VDI environment on sign out, settings changes are lost and the user must reapply the change when the computer is reconnected to the settings storage path.

**Synchronization for external sync engines:** The *SyncMethod=External* parameter specifies that if UE-V settings are written to a local folder on the user computer, then any external sync engine (such as OneDrive for Business, Work Folders, Sharepoint, or Dropbox) can be used to apply these settings to the different computers that users access.

**Support for shared VDI sessions:** UE-V 2.1 and 2.1 SP1 provide support for VDI sessions that are shared among end users. You can register and configure a special VDI template, which ensures that UE-V keeps all of its functionality intact for non-persistent VDI sessions.

> [!NOTE]
> If you don't enable VDI mode for non-persistent VDI sessions, certain features don't work. For example, [back-up/restore and last known good (LKG)](manage-administrative-backup-and-restore-in-ue-v-2x-new-topic-for-21.md).

The VDI template is provided with UE-V 2.1 and 2.1 SP1 and is typically available here after installation: `C:\Program Files\Microsoft User Experience Virtualization\Templates\VdiState.xml`.

### Prerequisites for UE-V generator support

Install the UE-V generator on the computer that is used to create custom settings location templates. This computer should be able to run the applications whose settings are synchronized. You must be a member of the Administrators group on the computer that runs the UE-V generator software.

The UE-V generator must be installed on a computer that uses an NTFS file system. The UE-V generator software requires .NET Framework 4. For more information, see [Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md).

## Other resources for this product

- [Microsoft User Experience Virtualization (UE-V) 2.1 SP1](index.md)

- [Get started with UE-V 2.1 SP1](get-started-with-ue-v-2x-new-uevv2.md)

- [Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

- [Technical Reference for UE-V 2.1 SP1](technical-reference-for-ue-v-2x-both-uevv2.md)
