---
title: Configuring UE-V 2.1 SP1 with group policy objects
description: Some Microsoft User Experience Virtualization (UE-V) 2.1 SP1 group policy settings can be defined for computers, and other group policy settings can be defined for users.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Configuring UE-V 2.1 SP1 with group policy objects

Some Microsoft User Experience Virtualization (UE-V) 2.1 SP1 group policy settings can be defined for computers, and other group policy settings can be defined for users. For more information about how to install UE-V group policy ADMX files, see [Deploy required features for UE-V 2.1 SP1](deploy-required-features-for-ue-v-2x-new-uevv2.md).

## Group policy settings

The following policy settings can be configured for UE-V.

| Name | Target | Description | Configuration options |
|--|--|--|--|
| Configure Sync Method | Computers and Users | By using this group policy setting, you can configure whether User Experience Virtualization (UE-V) uses the sync provider feature. This policy setting also lets you enable a notification to appear when the import of user settings is delayed. | Enable this setting to configure the UE-V agent not to use the sync provider, or to use the external synchronization engine. |
| Contact IT Link Text | Computers Only | This group policy setting specifies the text of the Contact IT URL hyperlink in the Company Settings Center. | If you enable this group policy setting, the Company Settings Center displays the specified text in the link to the Contact IT URL. |
| Contact IT URL | Computers Only | This group policy setting specifies the URL for the Contact IT link in the Company Settings Center. | If you enable this setting, the Company Settings Center Contact IT text links to the specified URL. The link can be of any standard protocol, such as HTTP or mailto. |
| First Use Notification | Computers Only | This group policy setting enables a notification in the notification area that appears when the UE-V agent runs for the first time. | The default is enabled. |
| Ping the settings storage location before sync | Computers and Users | This policy setting allows configuration of the UE-V sync provider to ping the settings storage path before attempting to sync settings in order to verify the connection. | Enable or disable this group policy setting. |
| Settings package size warning threshold | Computers and Users | This group policy setting lets you configure the UE-V Agent to report when a settings package file size reaches a defined threshold. | Specify the preferred threshold for settings package sizes in kilobytes (KB). By default, the UE-V Agent doesn't have a package file size threshold. |
| Settings storage path | Computers and Users | This group policy setting configures where the user settings are to be stored. | Enter a Universal Naming Convention (UNC) path and variables such as \Server\SettingsShare%username%. |
| Settings template catalog path | Computers Only | This group policy setting configures where custom settings location templates are stored. This policy setting also configures whether the catalog is to be used to replace the default Microsoft templates that are installed with the UE-V Agent. | Enter a Universal Naming Convention (UNC) path such as \Server\TemplateShare or a folder location on the computer. Select the check box to replace the default Microsoft templates. |
| Sync settings over metered connections | Computers and Users | This group policy setting defines whether UE-V synchronizes settings over metered connections. | By default, the UE-V Agent doesn't synchronize settings over a metered connection. |
| Sync settings over metered connections even when roaming | Computers and Users | This group policy setting defines whether UE-V synchronizes settings over metered connections outside of the home provider network, for example, when the data connection is in roaming mode. | By default, UE-V doesn't synchronize settings over a metered connection when it is in roaming mode. |
| Synchronization timeout | Computers and Users | This group policy setting configures the number of milliseconds that the computer waits before a time-out when it retrieves user settings from the remote settings location. If the remote storage location is unavailable, and the user doesn't use the sync provider, the application start is delayed by this many milliseconds. | Specify the preferred synchronization time-out in milliseconds. The default value is 2000 milliseconds. |
| Synchronize Windows settings | Computers and Users | This group policy setting configures the synchronization of Windows settings. | Select which Windows settings synchronize between computers. By default, Windows themes, desktop settings, and Ease of Access settings synchronize settings between computers of the same operating system version. |
| Tray Icon | Computers Only | This group policy setting enables the UE-V tray icon. | The default is enabled. |
| Use User Experience Virtualization (UE-V) | Computers and Users | This group policy setting lets you enable or disable UE-V. | Enable or disable this group policy setting. |
| VDI Configuration | Computers and Users | This policy setting configures the synchronization of UE-V rollback information for computers running in a pooled VDI environment. If this policy is enabled, the UE-V rollback state is copied to the settings storage location on sign out and restored on sign in. | Enable or disable this group policy setting. |

> [!NOTE]
> In addition, group policy settings are available for many desktop applications and Windows apps. You can use these settings to enable or disable settings synchronization for specific applications.

## Windows app group policy settings

| Name | Target | Description | Configuration options |
|--|--|--|--|
| Don't synchronize Windows Apps | Computers and Users | This group policy setting defines whether the UE-V Agent synchronizes settings for Windows apps. | The default is to synchronize Windows apps. |
| Windows App List | Computer and User | This setting lists the family package names of the Windows apps and states expressly whether UE-V synchronizes that app's settings. | You can use this setting to specify that settings of an app are never synchronized by UE-V, even if the settings of all other Windows apps are synchronized. |
| Sync Unlisted Windows Apps | Computer and User | This group policy setting defines the default settings sync behavior of the UE-V Agent for Windows apps that aren't explicitly listed in the Windows app list. | By default, the UE-V Agent only synchronizes settings of those Windows apps that are included in the Windows app list. |

For more information about synchronizing Windows apps, see [Windows app list](managing-ue-v-2x-settings-location-templates-using-windows-powershell-and-wmi-both-uevv2.md#win8applist).

## To configure computer-targeted group policy settings

1.  Use the Group Policy Management Console (GPMC) or the Advanced Group Policy Management (AGPM) on the computer that acts as a domain controller to manage group policy settings for UE-V computers. Navigate to **Computer configuration**, select **Policies**, select **Administrative Templates**, select **Windows Components**, and then select **Microsoft User Experience Virtualization**.

2.  Select the group policy setting to be edited.

## To configure user-targeted group policy settings

1.  Use the Group Policy Management Console (GPMC) or the Advanced Group Policy Management (AGPM) tool in Microsoft Desktop Optimization Pack (MDOP) on the domain controller computer to manage group policy settings for UE-V. Navigate to **User configuration**, select **Policies**, select **Administrative Templates**, select **Windows Components**, and then select **Microsoft User Experience Virtualization**.

2.  Select the edited group policy setting.

## Order of precedence for UE-V settings

The UE-V Agent uses the following order of precedence to determine synchronization.

1.  User-targeted settings that are managed by group policy settings - These configuration settings are stored in the registry key by group policy under `HKEY_CURRENT_USER\Software\Policies\Microsoft\Uev\Agent\Configuration`.

2.  Computer-targeted settings that are managed by group policy settings - These configuration settings are stored in the registry key by group policy under `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Uev\Agent\Configuration`.

3.  Configuration settings that are defined by the current user by using Windows PowerShell or Windows management Instrumentation (WMI) - These configuration settings are stored by the UE-V Agent under this registry location: `HKEY_CURRENT_USER\Software\Microsoft\Uev\Agent\Configuration`.

4.  Configuration settings that are defined for the computer by using Windows PowerShell or WMI. These configuration settings are stored by the UE-V Agent under this registry location: `HKEY_LOCAL_MACHINE\Software\Microsoft\Uev\Agent\Configuration`.

## Related articles

[Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

[Manage configurations for UE-V 2.1 SP1](manage-configurations-for-ue-v-2x-new-uevv2.md)
