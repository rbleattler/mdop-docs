---
title: Managing the UE-V 2.x agent and packages with Windows PowerShell and WMI
description: You can use Windows Management Instrumentation (WMI) and Windows PowerShell to manage Microsoft User Experience Virtualization (UE-V) 2.1 SP1 Agent configuration and synchronization behavior.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Managing the UE-V 2.x agent and packages with Windows PowerShell and WMI

You can use Windows Management Instrumentation (WMI) and Windows PowerShell to manage Microsoft User Experience Virtualization (UE-V) 2.1 SP1 Agent configuration and synchronization behavior. For a complete list of UE-V PowerShell cmdlets, see [MDOP cmdlet reference](/powershell/mdop/get-started).

## To deploy the UE-V Agent by using Windows PowerShell

1.  Stage the UE-V installer file in an accessible network share.

    > [!NOTE]
    > Use AgentSetup.exe to deploy both 32-bit and 64-bit versions of the UE-V Agent. Windows Installer packages, AgentSetupx86.msi and AgentSetupx64.msi, are available for each architecture. To uninstall the UE-V Agent at a later time by using the installation file, you must use the same file type.

2. To install the UE-V Agent, use one of the following Windows PowerShell commands:

```powershell
& AgentSetup.exe /quiet /norestart /log "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\\server\settingsshare\%username%
```

```powershell
& msiexec.exe /i "<path to msi file>" /quiet /norestart /l*v "%temp%\UE-VAgentInstaller.log" SettingsStoragePath=\\server\settingsshare\%username%
```

## To configure the UE-V Agent by using Windows PowerShell

1. Open a Windows PowerShell window. To manage computer settings that affect all users of the computer by using the *Computer* parameter, open the window with an account that has administrator rights.

2. Use the following Windows PowerShell commands to configure the agent.

| Windows PowerShell command | Description |
|--|--|
| `Get-UevConfiguration` | Gets the effective UE-V Agent settings. User-specific settings have precedence over the computer settings. |
| `Get-UevConfiguration -CurrentComputerUser` | Gets the UE-V Agent settings values for the current user only. |
| `Get-UevConfiguration -Computer` | Gets the UE-V Agent configuration settings values for all users on the computer. |
| `Get-UevConfiguration -Details` | Gets the details for each configuration setting. Displays where the setting is configured or if it uses the default value. Is displayed if the current setting is valid. |
| `Set-UevConfiguration -Computer -ContactITDescription <IT description>` | Sets the text that is displayed in the Company Settings Center for the help link. |
| `Set-UevConfiguration -Computer -ContactITUrl <string>` | Sets the URL of the link in the Company Settings Center for the help link. Any URL protocol can be used. |
| `Set-UevConfiguration -Computer -EnableDontSyncWindows8AppSettings` | Configures the UE-V Agent to not synchronize any Windows apps for all users on the computer. |
| `Set-UevConfiguration -CurrentComputerUser -EnableDontSyncWindows8AppSettings` | Configures the UE-V Agent to not synchronize any Windows apps for the current computer user. |
| `Set-UevConfiguration -Computer -EnableFirstUseNotification` | Configures the UE-V Agent to display notification the first time the agent runs for all users on the computer. |
| `Set-UevConfiguration -Computer -DisableFirstUseNotification` | Configures the UE-V Agent to not display notification the first time that the agent runs for all users on the computer. |
| `Set-UevConfiguration -Computer -EnableSettingsImportNotify` | Configures the UE-V Agent to notify all users on the computer when settings synchronization is delayed. Use the *DisableSettingsImportNotify* parameter to disable notification. |
| `Set-UevConfiguration -CurrentComputerUser -EnableSettingsImportNotify` | Configures the UE-V Agent to notify the current user when settings synchronization is delayed. Use the *DisableSettingsImportNotify* parameter to disable notification. |
| `Set-UevConfiguration -Computer -EnableSyncUnlistedWindows8Apps` | Configures the UE-V Agent to synchronize all Windows apps that aren't explicitly disabled by the Windows app list for all users of the computer. Use the `DisableSyncUnlistedWindows8Apps` parameter to configure the UE-V Agent to synchronize only Windows apps that are explicitly enabled by the Windows App List. |
| `Set-UevConfiguration -CurrentComputerUser -EnableSyncUnlistedWindows8Apps` | Configures the UE-V Agent to synchronize all Windows apps that aren't explicitly disabled by the Windows app list for the current user on the computer. Use the `DisableSyncUnlistedWindows8Apps` parameter to configure the UE-V Agent to synchronize only Windows apps that are explicitly enabled by the Windows App List. |
| `Set-UevConfiguration -Computer -DisableSync` | Disables UE-V for all the users on the computer. Use the *EnableSync* parameter to enable or re-enable. |
| `Set-UevConfiguration -CurrentComputerUser -DisableSync` | Disables UE-V for the current user on the computer. Use the *EnableSync* parameter to enable or re-enable. |
| `Set-UevConfiguration -Computer -EnableTrayIcon` | Enables the UE-V icon in the notification area for all users of the computer. Use the *DisableTrayIcon* parameter to disable the icon. |
| `Set-UevConfiguration -Computer -MaxPackageSizeInBytes <size in bytes>` | Configures the UE-V agent to report when a settings package file size reaches the defined threshold for all users on the computer. Sets the threshold package size in bytes. |
| `Set-UevConfiguration -CurrentComputerUser -MaxPackageSizeInBytes <size in bytes>` | Configures the UE-V agent to report when a settings package file size reaches the defined threshold. Sets the package size warning threshold for the current user. |
| `Set-UevConfiguration -Computer -SettingsImportNotifyDelayInSeconds` | Specifies the time in seconds before the user is notified for all users of the computer. |
| `Set-UevConfiguration -CurrentComputerUser -SettingsImportNotifyDelayInSeconds` | Specifies the time in seconds before notification for the current user is sent. |
| `Set-UevConfiguration -Computer -SettingsStoragePath <path to settings storage location>` | Defines a per-computer settings storage location for all users of the computer. |
| `Set-UevConfiguration -CurrentComputerUser -SettingsStoragePath <path to settings storage location>` | Defines a per-user settings storage location. |
| `Set-UevConfiguration -Computer -SettingsTemplateCatalogPath <path to catalog>` | Sets the settings template catalog path for all users of the computer. |
| `Set-UevConfiguration -Computer -SyncMethod <sync method>` | Sets the synchronization method for all users of the computer: SyncProvider or None. |
| `Set-UevConfiguration -CurrentComputerUser -SyncMethod <sync method>` | Sets the synchronization method for the current user: SyncProvider or None. |
| `Set-UevConfiguration -Computer -SyncTimeoutInMilliseconds <timeout in milliseconds>` | Sets the synchronization time-out in milliseconds for all users of the computer. |
| `Set-UevConfiguration -CurrentComputerUser -SyncTimeoutInMilliseconds <timeout in milliseconds>` | Sets the synchronization time-out for the current user. |
| `Clear-UevConfiguration -Computer -<setting name>` | Clears the specified setting for all users on the computer. |
| `Clear-UevConfiguration -CurrentComputerUser -<setting name>` | Clears the specified setting for the current user only. |
| `Export-UevConfiguration <settings migration file>` | Exports the UE-V computer configuration to a settings migration file. The file name extension must be `.uev`. The *Export* cmdlet exports all UE-V Agent settings that are configurable with the *Computer* parameter. |
| `Import-UevConfiguration <settings migration file>` | Imports the UE-V computer configuration from a settings migration file. The file name extension must be `.uev`. |

## To export UE-V package settings and repair UE-V templates by using Windows PowerShell

1.  Open a Windows PowerShell window as an administrator.

2.  Use the following Windows PowerShell commands to configure the agent.

    | Windows PowerShell command | Description |
    |--|--|
    | Export-UevPackage MicrosoftCalculator6.pkgx | Extracts the settings from a Microsoft Calculator package file and converts them into a human-readable format in XML. |
    | Repair-UevTemplateIndex | Repairs the index of the UE-V settings location templates. |

## To configure the UE-V Agent by using WMI

1.  User Experience Virtualization provides the following set of WMI commands. Administrators can use this interface to configure the UE-V agent at the command line and automate typical configuration tasks.

    Use an account with administrator rights to open a Windows PowerShell window.

2.  Use the following WMI commands to configure the agent.

    | Windows PowerShell command | Description |
    |--|--|
    | `Get-WmiObject -Namespace root\Microsoft\UEV Configuration` | Displays the active UE-V Agent settings. User-specific settings have precedence over the computer settings. |
    | `Get-WmiObject -Namespace root\Microsoft\UEV UserConfiguration` | Displays the UE-V Agent configuration that is defined for a user. |
    | `Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration` | Displays the UE-V Agent configuration that is defined for a computer. |
    | `Get-WmiObject -Namespace root\Microsoft\Uev ConfigurationItem` | Displays the details for each configuration item. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.SettingsStoragePath = <path_to_settings_storage_location>`<br>`$config.Put()` | Defines a per-computer settings storage location. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV UserConfiguration`<br>`$config.SettingsStoragePath = <path_to_settings_storage_location>`<br>`$config.Put()` | Defines a per-user settings storage location. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.SyncTimeoutInMilliseconds = <timeout_in_milliseconds>`<br>`$config.Put()` | Sets the synchronization time-out in milliseconds for all users of the computer. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.MaxPackageSizeInBytes = <size_in_bytes>`<br>`$config.Put()` | Configures the UE-V Agent to report when a settings package file size reaches a defined threshold. Set the threshold package file size in bytes for all users of the computer. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.SyncMethod = <sync_method>`<br>`$config.Put()` | Sets the synchronization method for all users of the computer: SyncProvider or None. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.<setting name> = $true`<br>`$config.Put()` | To enable a specific per-computer setting, clear the setting, and use *$null* as the setting value. Use UserConfiguration for per-user settings. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.<setting name> = $false`<br>`$config.Put()` | To disable a specific per-computer setting, clear the setting, and use *$null* as the setting value. Use User Configuration for per-user settings. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.<setting name> = <setting value>`<br>`$config.Put()` | Updates a specific per-computer setting. To clear the setting, use *$null* as the setting value. |
    | `$config = Get-WmiObject -Namespace root\Microsoft\UEV ComputerConfiguration`<br>`$config.<setting name> = <setting value>`<br>`$config.Put()` | Updates a specific per-user setting for all users of the computer. To clear the setting, use *$null* as the setting value. |

Upon configuration of the UE-V Agent with WMI and Windows PowerShell, the defined configuration is stored in the registry in the following locations.

`\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UEV\Agent\Configuration`

`\HKEY_CURRENT_USER\SOFTWARE\Microsoft\UEV\Agent\Configuration`

## To export UE-V package settings and repair UE-V templates by using WMI

1.  UE-V provides the following set of WMI commands. Administrators can use this interface to export a package or repair UE-V templates.

2.  Use the following WMI commands.

    | WMI command | Description |
    |--|--|
    | `Invoke-WmiMethod -Namespace root\Microsoft\UEV -Class UserSettings -Name ExportPackage -ArgumentList <package name>` | Extracts the settings from a package file and converts them into a human-readable format in XML. |
    | `Invoke-WmiMethod -Namespace root\Microsoft\UEV -Class SettingsLocationTemplate -Name RebuildIndex` | Repairs the index of the UE-V settings location templates. Must be run as administrator. |

## Related articles

[Administering UE-V 2.x with Windows PowerShell and WMI](administering-ue-v-2x-with-windows-powershell-and-wmi-both-uevv2.md)

[Administering UE-V 2.x](administering-ue-v-2x-new-uevv2.md)
