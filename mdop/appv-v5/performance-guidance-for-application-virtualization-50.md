---
title: Performance Guidance for Application Virtualization 5.0
description: Performance Guidance for Application Virtualization 5.0
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.prod: w10
ms.date: 08/30/2016
---

# Performance Guidance for Application Virtualization 5.0

Learn how to configure App-V 5.0 for optimal performance, optimize virtual app packages, and provide a better user experience with RDS and VDI.

Implementing multiple methods can help you improve the end-user experience. However, your environment may not support all methods.

You should read and understand the following information before reading this document.

- [Microsoft Application Virtualization 5.0 Administrator's Guide](microsoft-application-virtualization-50-administrators-guide.md)

- [App-V 5 SP2 Application Publishing and Client Interaction](https://www.microsoft.com/download/details.aspx?id=41635)

- [Microsoft Application Virtualization 5.0 Sequencing Guide](https://go.microsoft.com/fwlink/?LinkId=269953)

> [!NOTE]
> Some terms used in this document may have different meanings depending on external source and context. For more information about terms used in this document followed by an asterisk **\\*** review the [Application Virtualization Performance Guidance Terminology](#bkmk-terms1) section of this document.

Finally, this document provides you with the information to configure the computer running App-V 5.0 client and the environment for optimal performance. Optimize your virtual application packages for performance using the sequencer, and to understand how to use User Experience Virtualization (UE-V) or other user environment management technologies to provide the optimal user experience with App-V 5.0 in both Remote Desktop Services (RDS) and non-persistent virtual desktop infrastructure (VDI).

To help determine what information is relevant to your environment you should review each section's brief overview and applicability checklist.

## App-V 5.0 in stateful\* non-persistent deployments

This section provides information about an approach that helps ensure a user will have access to all virtual applications within seconds after logging in. This is achieved by uniquely addressing the often long-running App-V 5.0 publishing refresh. As you discover the basis of the approach, the fastest publishing refresh, is one that doesn't have to actually do anything. Many conditions must be met and steps followed to provide the optimal user experience.

Use the information in the following section for more information:

[Usage Scenarios](#bkmk-us) - As you review the two scenarios, keep in mind that these are the approach extremes. Based on your usage requirements, you may choose to apply these steps to a subset of users and/or virtual applications packages.

- Optimized for Performance - To provide the optimal experience, you can expect the base image to include some of the App-V virtual application package. This and other requirements are discussed.

- Optimized for Storage - If you're concerned with the storage impact, following this scenario helps address those concerns.

[Preparing your Environment](#bkmk-pe)

- Steps to Prepare the Base Image - Whether in a non-persistent VDI or RDSH environment, only a few steps must be completed in the base image to enable this approach.

- Use UE-V 2.0 as the User Profile Management (UPM) solution for the App-V approach - the cornerstone of this approach is the ability of a UEM solution to persist the contents of just a few registry and file locations. These locations constitute the user integrations\*. Be sure to review the specific requirements for the UPM solution.

[User Experience Walk-through](#bkmk-uewt)

- Walk-through - This is a step-by-step walk-through of the App-V and UE-V operations and the expectations users should have.

- Outcome - This describes the expected results.

[Impact to Package Lifecycle](#bkmk-plc)

[Enhancing the VDI Experience through Performance Optimization/Tuning](#bkmk-evdi)

### <a name="applicability-checklist-"></a>Applicability Checklist

#### Deployment environment

|Checklist|Deployment environment|
|-----|---------------------------|
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | Non-persistent VDI or RDSH. |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | User Experience Virtualization (UE-V), other UPM solutions or User Profile Disks (UPD). |

#### Expected configuration

| Checklist | Expected configuration |
|--|--|
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | User Experience Virtualization (UE-V) with the App-V user state template enabled or User Profile Management (UPM) software. Non-UE-V UPM software must be capable of triggering on sign-in or Process/Application Start and sign out. |
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | App-V Shared Content Store (SCS) is configured or can be configured. |

#### IT administration

| Checklist | IT administratio |
|--|--|
| :::image type="icon" source="images/checklistbox.gif" border="false"::: | You may need to update the VM base image regularly to ensure optimal performance or you may need to manage multiple images for different user groups. |

### <a name="bkmk-us"></a>Usage scenario

As you review the two scenarios, keep in mind that these approach the extremes. Based on your usage requirements, you may choose to apply these steps to a subset of users, virtual application packages, or both.

| Optimized for Performance | Optimized for Storage |
|--|--|
| To provide the most optimal user experience, this approach uses the capabilities of a UPM solution and requires extra image preparation and can incur some more image management overhead. The following describes many performance improvements in stateful non-persistent deployments. For more information, see the **Sequencing Steps to Optimize Packages for Publishing Performance** and reference to **App-V 5.0 Sequencing Guide** in the **See Also section of this document**. | The general expectations of the previous scenario still apply here. However, keep in mind that VM images are typically stored in costly arrays; a slight alteration has been made to the approach. Don't preconfigure user-targeted virtual application packages in the base image. The impact of this alteration is detailed in the User Experience Walkthrough section of this document. |

### <a name="bkmk-pe"></a>Preparing your environment

The following table displays the required steps to prepare the base image and the UE-V or another UPM solution for the approach.

#### Prepare the base image

| Optimized for Performance | Optimized for Storage |
|--|--|
| - Install the Hotfix Package 4 for Application Virtualization 5.0 SP2 client version of the client.<br>- Install UE-V and download the App-V Settings Template from the UE-V template Gallery, see the following steps.<br>- Configure for Shared Content Store (SCS) mode. For more information, see [How to Install the App-V 5.0 Client for Shared Content Store Mode](how-to-install-the-app-v-50-client-for-shared-content-store-mode.md).<br>- Configure Preserve User Integrations on Login Registry DWORD.<br>- Preconfigure all user- and global-targeted packages, for example, `Add-AppvClientPackage`.<br>- Preconfigure all user- and global-targeted connection groups, for example, `Add-AppvClientConnectionGroup`.<br>- Prepublish all global-targeted packages.<br><br>Alternatively,<br>- Perform a global publishing/refresh.<br>- Perform a user publishing/refresh.<br>- Unpublish all user-targeted packages.<br>- Delete the following user-Virtual File System (VFS) entries.<br>`AppData\Local\Microsoft\AppV\Client\VFS`<br>`AppData\Roaming\Microsoft\AppV\Client\VFS` | - Install the Hotfix Package 4 for Application Virtualization 5.0 SP2 client version of the client.<br>- Install UE-V and download the App-V Settings Template from the UE-V template Gallery, see the following steps.<br>- Configure for Shared Content Store (SCS) mode. For more information, see [How to Install the App-V 5.0 Client for Shared Content Store Mode](how-to-install-the-app-v-50-client-for-shared-content-store-mode.md).<br>- Configure Preserve User Integrations on Login Registry DWORD.<br>- Preconfigure all global-targeted packages, for example, `Add-AppvClientPackage`.<br>- Preconfigure all global-targeted connection groups, for example, `Add-AppvClientConnectionGroup`.<br>- Prepublish all global-targeted packages. |

#### Configurations

For critical App-V Client configurations and for a little more context and how-to, review the following information:

##### Shared Content Store (SCS) Mode

- Configurable in PowerShell using `Set-AppvClientConfiguration -SharedContentStoreMode`, or
- During installation of the App-V 5.0 client.

When running the shared content store only publishing data is maintained on the hard disk; other virtual application assets are maintained in memory (RAM). This helps to conserve local storage and minimize disk I/O per second (IOPS).

This is recommended when low-latency connections are available between the App-V Client endpoint and the SCS content server, SAN.

##### PreserveUserIntegrationsOnLogin

- Configure in the Registry under `HKEY_LOCAL_MACHINE\Software\Microsoft\AppV\Client\Integration`.
- Create the DWORD value `PreserveUserIntegrationsOnLogin` with a value of `1`.
- Restart the App-V client service or restart the computer running the App-V Client.

If you haven't preconfigured (`Add-AppvClientPackage`) a specific package and this setting isn't configured, the App-V Client deintegrates *the persisted user integrations, then reintegrate*. For every package that meets the above conditions, effectively twice the work is done during publishing/refresh.

If you don't plan to preconfigure every available user package in the base image, use this setting.

##### MaxConcurrentPublishingRefresh

- Configure in the Registry under `HKEY_LOCAL_MACHINE\Software\Microsoft\AppV\Client\Publishing`.
- Create the DWORD value `MaxConcurrentPublishingRefresh` with the desired maximum number of concurrent publishing refreshes.
- The App-V client service and computer don't need to be restarted.

This setting determines the number of users that can perform a publishing refresh/sync at the same time. The default setting is no limit.

Limiting the number of concurrent publishing refreshes prevents excessive CPU usage that could impact computer performance. This limit is recommended in an RDS environment, where multiple users can sign in to the same computer at the same time and perform a publishing refresh sync. If the concurrent publishing refresh threshold is reached, the time required to publish new applications and make them available to end users after they sign in could take an indeterminate amount of time.

### Configure UE-V solution for App-V Approach

We recommend using Microsoft User Experience Virtualization (UE-V) to capture and centralize application settings and Windows operating system settings for a specific user. These settings are then applied to the different computers that are accessed by the user, including desktop computers, laptop computers, and virtual desktop infrastructure (VDI) sessions. UE-V is optimized for RDS and VDI scenarios.

> [!NOTE]
> Without performing an additional configuration step, the Microsoft User Environment Virtualization (UE-V) will not be able to synchronize the Start menu shortcuts (.lnk files) on the target computer. The .lnk file type is excluded by default.

UE-V will only support removing the .lnk file type from the exclusion list in the RDS and VDI scenarios, where every user's device has the same set of applications installed to the same location and every .lnk file is valid for all the users' devices. For example, UE-V wouldn't currently support the following two scenarios, because the net result will be that the shortcut will be valid on one but not all devices.

- If a user has an application installed on one device with .lnk files enabled and the same native application installed on another device to a different installation root with .lnk files enabled.

- If a user has an application installed on one device but not another with .lnk files enabled.

> [!IMPORTANT]
> This article describes how to change the Windows registry by using Registry Editor. If you change the Windows registry incorrectly, you can cause serious problems that might require you to reinstall Windows. You should make a backup copy of the registry files (System.dat and User.dat) before you change the registry. Microsoft cannot guarantee that the problems that might occur when you change the registry can be resolved. Change the registry at your own risk.

Using the Microsoft Registry Editor (regedit.exe), navigate to `HKEY_LOCAL_MACHINE\Software\Microsoft\UEV\Agent\Configuration\ExcludedFileTypes` and remove `.lnk` from the excluded file types.

#### Configure other User Profile Management (UPM) solution for App-V Approach

The expectation in a stateful environment is that a UPM solution is implemented and can support persistence of user data across sessions and between logins.

The requirements for the UPM solution are as follows.

To enable an optimized sign-in experience, for example the App-V 5.0 approach for the user, the solution must be capable of:

- Persisting the below user integrations as part of the user profile/persona.

- Triggering a user profile sync on sign-in (or application start), which can guarantee that all user integrations are applied before publishing/refresh begin, or,

- Attaching and detaching a user profile disk (UPD) or similar technology that contains the user integrations.

- Capturing changes to the locations, which constitute the user integrations, prior to session sign out.

With App-V 5.0 when you add a publishing server (**Add-AppvPublishingServer**) you can configure synchronization, for example refresh during sign in and/or after a specified refresh interval. In both cases, a scheduled task is created.

In previous versions of App-V 5.0, both scheduled tasks were configured using a VBScript that would initiate the user and global refresh. With Hotfix Package 4 for Application Virtualization 5.0 SP2 the user refresh on sign-in is initiated by **SyncAppvPublishingServer.exe**. This change was introduced to provide UPM solutions a trigger process. This process delays the publish /refresh to allow the UPM solution to apply the user integrations. It exits once the publishing/refresh is complete.

#### User integrations

Registry - `HKEY_CURRENT_USER`

- Path - `Software\Classes`

    Exclude: Local Settings, ActivatableClasses, AppX\*

- Path - `Software\Microsoft\AppV`

- Path - `Software\Microsoft\Windows\CurrentVersion\App Paths`

#### File locations

- Root - "Environment Variable" APPDATA

    Path - `Microsoft\AppV\Client\Catalog`

- Root - "Environment Variable" APPDATA

    Path - `Microsoft\AppV\Client\Integration`

- Root - "Environment Variable" APPDATA

    Path - `Microsoft\Windows\Start Menu\Programs`

- (To persist all desktop shortcuts, virtual and nonvirtual)

    Root - "KnownFolder" {B4BFCC3A-DB2C-424C-B029-7FE99A87C641}FileMask - `*.lnk`

#### Microsoft User Experience Virtualization (UE-V)

Additionally, we recommend using Microsoft User Experience Virtualization (UE-V) to capture and centralize application settings and Windows operating system settings for a specific user. These settings are then applied to the different computers that are accessed by the user, including desktop computers, laptop computers, and virtual desktop infrastructure (VDI) sessions.

For more information, see [Getting Started With User Experience Virtualization 1.0](../uev-v1/index.md) and [Sharing Settings Location Templates with the UE-V Template Gallery](../uev-v1/sharing-settings-location-templates-with-the-ue-v-template-gallery.md).

### <a name="bkmk-uewt"></a>User experience walk-through

This following is a step-by-step walk-through of the App-V and UPM operations and the expectations users should expect.

#### Optimized for performance

After implementing this approach in the VDI/RDSH environment, on first sign-in:

- (Operation) A user-publishing/refresh is initiated. (Expectation) If this is the first time a user has published virtual applications (for example, non-persistent), this takes the usual duration of a publishing/refresh.
- (Operation) After the publishing/refresh, the UPM solution captures the user integrations. (Expectation) Depending on how the UPM solution is configured, this may occur as part of the sign out process. This incurs the same/similar overhead as persisting the user state.

On subsequent logins:

- (Operation) UPM solution applies the user integrations to the system prior to publishing/refresh.
- (Operation) Publishing/refresh will process unpublish and publish operations for changes in user package entitlements. (Expectation) If there are no entitlement changes, publishing1 will complete in seconds. Otherwise, the publishing/refresh will increase relative to the number and complexity* of virtual applications.
- (Operation) UPM solution captures user integrations again at sign out. (Expectation) Same as previous.
  
¹ The publishing operation (Publish-AppVClientPackage) adds entries to the user catalog, maps entitlement to the user, identifies the local store, and finishes by completing any integration steps.

**Outcome**: Because the user integrations are entirely preserved, there will be no work for example, integration for the publishing/refresh to complete. All virtual applications are available within seconds of sign-in. The publishing/refresh will process changes to the users entitled virtual applications, which impact the experience.

#### Optimized for storage

After implementing this approach in the VDI/RDSH environment, on first sign-in:

- (Operation) A user-publishing/refresh is initiated. (Expectation)
  - If this is the first time a user has published virtual applications (for example, non-persistent), this takes the usual duration of a publishing/refresh.
  - First and subsequent logins are impacted by preconfiguring of packages (add/refresh).

(Operation) After the publishing/refresh, the UPM solution captures the user integrations. (Expectation) Depending on how the UPM solution is configured, this may occur as part of the sign out process. This incurs the same/similar overhead as persisting the user state.

On subsequent logins:

- (Operation) UPM solution applies the user integrations to the system prior to publishing/refresh.
- (Operation) Add/refresh must preconfigure all user-targeted applications. (Expectation)
  - This may increase the time to application availability significantly (on the order of tens of seconds).
  - This increases the publishing refresh time relative to the number and complexity* of virtual applications.
- (Operation) Publishing/refresh will process unpublish and publish operations for changes to user package entitlements.

**Outcome**: Because the add/refresh must reconfigure all the virtual applications to the VM, the publishing refresh time on every sign-in will be extended.

### <a name="bkmk-plc"></a>Impact to package life cycle

Upgrading a package is a crucial aspect of the package lifecycle. To help guarantee users have access to the appropriate upgraded (published) or downgraded (unpublished) virtual application packages, it's recommended you update the base image to reflect these changes. To understand why review the following section:

App-V 5.0 SP2 introduced the concept of pending states. In the past,

- If an administrator changed entitlements or created a new version of a package (upgraded) and during a publishing/refresh that package was in-use, the unpublish or publish operation, respectively, would fail.

- If a package is in use, the operation will be pending. The unpublish and publish-pend operations will be processed on service restart or if another publish or unpublish command is issued. In the latter case, if the virtual application is in-use otherwise, the virtual application remains in a pending state. For globally published packages, a restart (or service restart) often needed.

In a non-persistent environment, it's unlikely these pended operations will be processed. The pended operations, for example tasks are captured under `HKEY_CURRENT_USER\Software\Microsoft\AppV\Client\PendingTasks`. Although this location is persisted by the UPM solution, if it isn't applied to the environment prior to sign-in, it isn't processed.

### <a name="bkmk-evdi"></a>Enhancing the VDI experience through performance optimization tuning

The following section contains lists with information about Microsoft documentation and downloads that may be useful when optimizing your environment for performance.

#### .NET NGEN script (highly recommended)

- [Script](https://aka.ms/DrainNGenQueue)

#### Windows Server

Server performance tuning guidelines for

- [Microsoft Windows Server 2012 R2](/previous-versions//dn529133(v=vs.85))

- [Microsoft Windows Server 2012](https://download.microsoft.com/download/0/0/B/00BE76AF-D340-4759-8ECD-C80BC53B6231/performance-tuning-guidelines-windows-server-2012.docx)

- [Microsoft Windows Server 2008 R2](https://download.microsoft.com/download/6/B/2/6B2EBD3A-302E-4553-AC00-9885BBF31E21/Perf-tun-srv-R2.docx)

#### Server Roles

- [Remote Desktop Virtualization Host](/previous-versions/dn567643(v=vs.85))

- [Remote Desktop Session Host](/previous-versions/dn567648(v=vs.85))

- [IIS Relevance: App-V Management, Publishing, Reporting Web Services](/previous-versions/dn567678(v=vs.85))

- [File Server (SMB) Relevance: If used for App-V Content Storage and Delivery in SCS Mode](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134210(v=ws.11))

#### Windows client (guest OS) performance tuning guidance

- [Microsoft Windows 8](https://download.microsoft.com/download/6/0/1/601D7797-A063-4FA7-A2E5-74519B57C2B4/Windows_8_VDI_Image_Client_Tuning_Guide.pdf)

## Sequencing steps to optimize packages for publishing performance

App-V 5.0 and App-V 5.0 SP2 provide significant value in their respective releases. Several features facilitate new scenarios or enabled new customer deployment scenarios. These following features can impact the performance of the publishing and launch operations.

### Removing FB1

| Step | Consideration | Benefits | Tradeoffs |
|--|--|--|--|
| No Feature Block 1 (FB1, also known as Primary FB) | No FB1 means the application launches immediately and stream fault (application requires file, DLL and must pull down over the network) during launch. If there are network limitations, FB1 will: | - Reduce the number of stream faults and network bandwidth used when you launch an application for the first time.<br> - Delay launch until the entire FB1 has been streamed. | Virtual application packages with FB1 configured will need to be resequenced. |

Removing FB1 doesn't require the original application installer. After completing the following steps, it's suggested that you revert the computer running the sequencer to a clean snapshot.

#### Sequencer UI - create a new virtual application package

1. Complete the sequencing steps up to Customize, Streaming.

2. At the Streaming step, don't select **Optimize the package for deployment over slow or unreliable network**.

3. If desired, move on to **Target OS**.

#### Modify an existing virtual application package

1. Complete the sequencing steps up to Streaming.

2. Don't select **Optimize the package for deployment over a slow or unreliable network**.

3. Move to **Create Package**.

#### PowerShell - update an existing virtual application package

1. Open an elevated PowerShell session.

2. `Import-module appvsequencer`

3. `Update-AppvSequencerPackage -AppvPackageFilePath`

    `"C:\Packages\MyPackage.appv" -Installer`

    `"C:\PackageInstall\PackageUpgrade.exe empty.exe" -OutputPath`

    `"C:\UpgradedPackages"`

    > [!NOTE]
    > This cmdlet requires an executable (.exe) or batch file (.bat). You must provide an empty (does nothing) executable or batch file.

### Creating a new virtual application package on the sequencer

| Step | Considerations | Benefits | Tradeoffs |
|--|--|--|--|
| No SXS Install at Publish (Pre-Install SxS assemblies) | Virtual Application packages don't need to be resequenced. SxS Assemblies can remain in the virtual application package. | The SxS Assembly dependencies won't install at publishing time. | SxS Assembly dependencies must be preinstalled. |

During sequencer monitoring, if an SxS Assembly (such as a VC++ Runtime) is installed as part of an application's installation, SxS Assembly is automatically detected and included in the package. The administrator os notified and has the option to exclude the SxS Assembly.

#### Client Side

When publishing a virtual application package, the App-V 5.0 SP2 Client detects if a required SxS dependency is already installed. If the dependency is unavailable on the computer and it's included in the package, a traditional Windows Installer (.**msi**) installation of the SxS assembly will be initiated. As previously documented, install the dependency on the computer running the client to ensure that the Windows Installer (.msi) installation won't occur.

### Disabling a Dynamic Configuration using PowerShell

| Step | Considerations | Benefits | Tradeoffs |
|--|--|--|--|
| Selectively Employ Dynamic Configuration files | - The App-V 5.0 client must parse and process these Dynamic Configuration files.<br>- Be conscious of size and complexity (script execution, VREG inclusions/exclusions) of the file.<br>- Numerous virtual application packages may already have User- or computer-specific dynamic configurations files. | - Publishing times improve if these files are used selectively or not at all. | - Virtual application packages would need to be reconfigured individually or via the App-V server management console to remove associated Dynamic Configuration files. |

- For already published packages, you can use `Set-AppVClientPackage -Name Myapp -Path c:\Packages\Apps\MyApp.appv` without the `-DynamicDeploymentConfiguration` parameter.

- Similarly, when adding new packages using `Add-AppVClientPackage -Path c:\Packages\Apps\MyApp.appv`, don't use the `-DynamicDeploymentConfiguration` parameter.

For documentation on how to apply a dynamic configuration, see:

- [How to Apply the User Configuration File by Using PowerShell](how-to-apply-the-user-configuration-file-by-using-powershell.md)

- [How to Apply the Deployment Configuration File by Using PowerShell](how-to-apply-the-deployment-configuration-file-by-using-powershell.md)

### Determining what virtual fonts exist in the package

| Step | Considerations | Benefits | Tradeoffs |
|--|--|--|--|
| Account for Synchronous Script Execution during Package Lifecycle | - If script collateral is embedded in the package, Add (PowerShell) may be slower.<br>- Running of scripts during virtual application launch (StartVirtualEnvironment, StartProcess) and/or Add+Publish will impact the perceived performance during one or more of these lifecycle operations. | - Use of Asynchronous (Non-Blocking) Scripts ensure that the lifecycle operations complete efficiently. | - This step requires working knowledge of all virtual application packages with embedded script collateral, which have associated dynamic configurations files and which reference and run scripts synchronously. |
| Remove Extraneous Virtual Fonts from Package | - Most applications investigated by the App-V product team contained a few fonts, typically fewer than 20. | - Virtual Fonts impact publishing refresh performance. | - Desired fonts need to be enabled/installed natively. For instructions, see Install or uninstall fonts. |

- Make a copy of the package.

- Rename `Package_copy.appv` to `Package_copy.zip`

- Open AppxManifest.xml and locate the following:

    ```xml
    <appv:Extension Category="AppV.Fonts">

    <appv:Fonts>

    <appv:Font Path="[{Fonts}]\private\CalibriL.ttf" DelayLoad="true"></appv:Font>

    </appv:Fonts>
    ```

    > [!NOTE]
    > If there are fonts marked as **DelayLoad**, those will not impact first launch.

### Excluding virtual fonts from the package

Use the dynamic configuration file that best suits the user scope - deployment configuration for all users on computer, user configuration for specific user or users.

- Disable fonts with the deployment or user configuration.

```xml
<Fonts Enabled="false" />
```

## <a name="bkmk-terms1"></a> App-V 5.0 performance guidance terminology

The following terms are used when describing concepts and actions related to App-V 5.0 performance optimization.

- **Complexity** - Refers to one or more package characteristics that may impact performance during preconfigure (**Add-AppvClientPackage**) or integration (**Publish-AppvClientPackage**). Some example characteristics are: manifest size, number of virtual fonts, number of files.

- **De-Integrate** - Removes the user integrations

- **Re-Integrate** - Applies the user integrations.

- **Non-Persistent, Pooled** - Creates a computer running a virtual environment each time they sign in.

- **Persistent, Personal** - A computer running a virtual environment that remains the same for every sign-in.

- **Stateful** - For this document, implies that user integrations are persisted between sessions and a user environment management technology is used with non-persistent RDSH or VDI.

- **Stateless** - Represents a scenario when no user state is persisted between sessions.

- **Trigger** - (or Native Action Triggers). UPM uses these types of triggers to initiate monitoring or synchronization operations.

- **User Experience** - In the context of App-V 5.0, the user experience, quantitatively, is the sum of the following parts:

    - From the point that users sign in to when they're able to manipulate the desktop.

    - From the point where the desktop can be interacted with to the point a publishing refresh begins (in PowerShell terms, sync) when using the App-V 5.0 full server infrastructure. In standalone instances, it's when the **Add-AppVClientPackage** and **Publish-AppVClientPackage Powershell** commands are initiated.

    - From start to completion of the publishing refresh. In standalone instances, this is the first to last virtual application published.

    - From the point where the virtual application is available to launch from a shortcut. Alternatively, it is from the point at which the file type association is registered and will launch a specified virtual application.

- **User Profile Management** - The controlled and structured approach to managing user components associated with the environment. For example, user profiles, preference and policy management, application control and application deployment. You can use scripting or third-party solutions configure the environment as needed.

## Related information

[Microsoft Application Virtualization 5.0 Administrator's Guide](microsoft-application-virtualization-50-administrators-guide.md)
