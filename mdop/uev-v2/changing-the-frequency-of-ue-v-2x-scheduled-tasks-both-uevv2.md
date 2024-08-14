---
title: Changing the frequency of UE-V 2.1 SP1 scheduled tasks
description: The Microsoft User Experience Virtualization (UE-V) 2.1 SP1 agent installer, AgentSetup.exe, creates scheduled tasks during the UE-V Agent installation.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.topic: reference
ms.date: 09/29/2016
---

# Changing the frequency of UE-V 2.1 SP1 scheduled tasks

The Microsoft User Experience Virtualization (UE-V) 2.1 SP1 agent installer, AgentSetup.exe, creates the following scheduled tasks during the UE-V Agent installation:

- **Monitor Application Settings**

- **Sync Controller Application**

- **Synchronize Settings at Logoff**

- **Template Auto Update**

- **Collect CEIP data**

- **Upload CEIP Data**

> [!NOTE]
> With the exception of Collect CEIP data, these tasks must remain enabled as UE-V can't function without them.

These scheduled tasks aren't configurable with the UE-V tools. Administrators who want to change the scheduled task for these items can create a script that uses the Schtasks.exe command-line options.

For more information, see [Task Scheduler for developers](/windows/win32/taskschd/task-scheduler-start-page).

## UE-V scheduled tasks

The following scheduled tasks are included in UE-V 2 with sample scheduled task configuration commands.

### Collect CEIP data

If upon installation the user or administrator chooses to participate in the Customer Experience Improvement Program (CEIP), UE-V collects data to help improve the product in future releases. This scheduled task only runs at sign in. The **Collect CEIP Data** task runs the UevSqmSession.exe, which is located in the UE-V Agent installation directory.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Collect CEIP data | Sign in |

### Monitor application settings

The **Monitor Application Settings** task is used to synchronize settings for Windows apps. It's run at sign in but is delayed by 30 seconds to not detrimentally affect the sign in. The Monitor Application Status task runs the UevAppMonitor.exe file, which is located in the UE-V Agent installation directory.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Monitor Application Status | Sign in |

### Sync controller application

The **Sync Controller Application** task is used to start the Sync Controller to synchronize settings from the computer to the settings storage location. By default, the task runs every 30 minutes. At that time, local settings are synchronized to the settings storage location, and updated settings on the settings storage location are synchronized to the computer. The Sync Controller application runs the Microsoft.Uev.SyncController.exe, which is located in the UE-V Agent installation directory.

> [!NOTE]
> As per the **Monitor Application Settings** task, this task is run at sign in but is delayed by 30 seconds to not detrimentally affect the sign in.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Sync Controller Application | Sign in, and every 30 minutes thereafter |

For example, the following command configures the agent to synchronize settings every 15 minutes instead of the default 30 minutes.

```command
Schtasks /change /tn "Microsoft\UE-V\Sync Controller Application" /ri 15
```

### Synchronize settings at logoff

The **Synchronize Settings at Logoff** task is used to start an application at sign in that controls the synchronization of applications at sign out for UE-V. The Synchronize Settings at Logoff task runs the Microsoft.Uev.SyncController.exe file, which is located in the UE-V Agent installation directory.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Synchronize Settings at Logoff | Sign in |

### Template auto update

The **Template Auto Update** task checks the settings template catalog for new, updated, or removed templates. This task only runs if the SettingsTemplateCatalog is configured. The **Template Auto Update** task runs the ApplySettingsCatalog.exe file, which is located in the UE-V Agent installation directory.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Template Auto Update | System start up and at 3:30 AM every day, at a random time within a one-hour window. |

#### Example: Template auto update

The following command configures the UE-V Agent to check the settings template catalog store every hour.

```command
schtasks /change /tn "Microsoft\UE-V\Template Auto Update" /ri 60
```

### Upload CEIP Data

The **Upload CEIP Data** task runs during the installation if the user or the administrator chose to participate in the Customer Experience Improvement Program (CEIP). This task uploads the data to the CEIP servers where the data is used to help improve the product for future releases of UE-V. This scheduled task runs at sign in and every 4 hours afterwards. The **Upload CEIP data** task runs the UevSqmUploader.exe file, which is located in the UE-V Agent installation directory.

| Task name | Default event |
|--|--|
| \Microsoft\UE-V\Upload CEIP data | At sign in and every 4 hours |

## UE-V 2 scheduled task details

The following chart provides additional information about scheduled tasks for UE-V 2:

| Task Name (file name) | Default Frequency | Power Toggle | Idle Only | Network Connection | Description |
|--|--|--|--|--|--|
| **Monitor Application Settings** (UevAppMonitor.exe) | Starts 30 seconds after sign in and continues until sign out. | No | Yes | N/A | Synchronizes settings for Windows (AppX) apps. |
| **Sync Controller Application** (Microsoft.Uev.SyncController.exe) | At sign in and every 30 min thereafter. | Yes | Yes | Only if Network is connected | Starts the Sync Controller, which synchronizes local settings with the settings storage location. |
| **Synchronize Settings at Logoff** (Microsoft.Uev.SyncController.exe) | Runs at sign in and then waits for sign out to Synchronize settings. | No | Yes | N/A | Start an application at sign in that controls the synchronization of applications at sign out. |
| **Template Auto Update** (ApplySettingsCatalog.exe) | Runs at initial sign in and at 3:30 AM every day thereafter. | Yes | No | N/A | Checks the settings template catalog for new, updated, or removed templates. This task only runs if SettingsTemplateCatalog is configured. |
| **Collect CEIP data** (UevSqmSession.exe) | At sign in launches service | No | Yes | N/A | If the user or administrator opts in to the Customer Experience Improvement Program (CEIP), this task collects data that helps improve UE-V future releases. |
| **Upload CEIP Data** (UevSqmUploader.exe) | Runs at sign in and at 4:00 AM every day thereafter. | No | Yes | Only if Network is connected | If the user or administrator opts in to the Customer Experience Improvement Program (CEIP), this task uploads the data to the CEIP servers. |

### Legend

- **Power Toggle** - Task Scheduler optimizes power consumption when not connected to AC power. The task might stop running if the computer switches to battery power.

- **Idle Only** - The task stops running if the computer ceases to be idle. By default the task doesn't restart when the computer is idle again. Instead the task begins again on the next task trigger.

- **Network Connection** - Tasks marked "Yes" only run if the computer has a network connection available. Tasks marked "N/A" run regardless of network connectivity.

### How to manage scheduled tasks

To find Scheduled Tasks, do the following steps:

1. Open "Schedule Tasks" on the user computer.

2. Navigate to: Task Scheduler -&gt; Task Scheduler Library -&gt; Microsoft -&gt; UE-V

3. Select the scheduled task you wish to manage and configure in the details pane.

### Additional information

The following additional information applies to UE-V scheduled tasks:

- All task sequence programs are located in the UE-V Agent installation folder, `%programFiles%\Microsoft User Experience Virtualization\Agent\[architecture]\`, by default.

- The Sync Controller Application Scheduled task is the crucial component when the UE-V SyncMethod is set to "SyncProvider" (UE-V 2 default configuration). This scheduled task keeps the SettingsSToragePath synchronized with the locally cached versions of the settings package files. If users complain that settings don't synchronize often enough, then you can reduce the scheduled task setting to as little as 1 minute. You can also increase the 30-minute default to a higher amount if necessary. If users complain that settings don't synchronize fast enough on sign in, then you can remove the delay setting for the scheduled task. (You can find the delay setting in the **Edit Trigger** dialogue box)

- You don't need to disable the Template Auto Update scheduled task if you use another method to keep the clients' templates in sync. For example, if you use group policy or Configuration Manager baselines. Leaving the SettingsTemplateCatalog property value blank prevents UE-V from checking the settings catalog for custom templates. This scheduled task runs ApplySettingsCatalog.exe and will essentially return immediately.

- The Monitor Application Settings scheduled task updates Windows app (AppX) settings in real time, based on Windows app program setting triggers built into each app.

## Related articles

[Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

[Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md#deploycatalogue)
