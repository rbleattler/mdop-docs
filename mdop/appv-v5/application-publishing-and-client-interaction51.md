---
title: Application publishing and client interaction reference
description: This article provides technical information about common App-V 5.1 client operations and their integration with the local operating system.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.topic: reference
ms.date: 08/30/2016
---

# Application publishing and client interaction reference

This article provides technical information about common App-V client operations and their integration with the local operating system.

For more reference information, see [Microsoft Application Virtualization (App-V) documentation resources download page](https://www.microsoft.com/download/details.aspx?id=27760).

## <a href="" id="bkmk-appv-pkg-files-list"></a>App-V package files created by the Sequencer

The Sequencer creates App-V packages and produces a virtualized application. The sequencing process creates the following files:

| File | Description |
|--|--|
| `.appv` | - The primary package file, which contains the captured assets and state information from the sequencing process. <br> - Architecture of the package file, publishing information, and registry in a tokenized form that can be reapplied to a machine and to a specific user upon delivery. |
| `.MSI` | Executable deployment wrapper that you can use to deploy `.appv` files manually or by using a non-Microsoft deployment platform. |
| `_DeploymentConfig.XML` | File used to customize the default publishing parameters for all applications in a package that is deployed globally to all users on a computer that is running the App-V client. |
| `_UserConfig.XML` | File used to customize the publishing parameters for all applications in a package that is deployed to a specific user on a computer that is running the App-V client. |
| `Report.xml` | Summary of messages resulting from the sequencing process, including omitted drivers, files, and registry locations. |
| `.CAB` | *Optional:* Package accelerator file used to automatically rebuild a previously sequenced virtual application package. |
| `.appvt` | *Optional:* Sequencer template file used to retain commonly reused Sequencer settings. |

## <a href="" id="bkmk-appv-file-contents"></a>What's in the `appv` file?

The `appv` file is a container that stores XML and non-XML files together in a single entity. This file is built from the AppX format, which is based on the Open Packaging Conventions (OPC) standard.

To view the `appv` file contents, make a copy of the package, and then rename the copied file to a ZIP extension.

The `appv` file contains the following folder and files, which are used when creating and publishing a virtual application:

| Name | Type | Description |
|--|--|--|
| `Root` | File folder | Directory that contains the file system for the virtualized application that is captured during sequencing. |
| `[Content_Types].xml` | XML File | List of the core content types in the `appv` file (for example DLL, EXE, BIN). |
| `AppxBlockMap.xml` | XML File | Layout of the `appv` file, which uses File, Block, and BlockMap elements that enable location and validation of files in the App-V package. |
| `AppxManifest.xml` | XML File | Metadata for the package that contains the required information for adding, publishing, and launching the package. Includes extension points (file type associations and shortcuts) and the names and GUIDs associated with the package. |
| `FilesystemMetadata.xml` | XML File | List of the files captured during sequencing, including attributes (for example, directories, files, opaque directories, empty directories, and long and short names). |
| `PackageHistory.xml` | XML File | Information about the sequencing computer (operating system version, Internet Explorer version, .NET Framework version) and process (upgrade, package version). |
| `Registry.dat` | DAT File | Registry keys and values captured during the sequencing process for the package. |
| `StreamMap.xml` | XML File | List of files for the primary and publishing feature block. The publishing feature block contains the ICO files and required portions of files (EXE and DLL) for publishing the package. When present, the primary feature block includes files that are optimized for streaming during the sequencing process. |

## <a href="" id="bkmk-files-data-storage"></a>App-V client data storage locations

The App-V client performs tasks to ensure that virtual applications run properly and work like locally installed applications. The process of opening and running virtual applications requires mapping from the virtual file system and registry to ensure the application has the required components of a traditional application expected by users. This section describes the assets that are required to run virtual applications and lists the location where App-V stores the assets.

| Name | Location | Description |
|--|--|--|
| Package Store | %ProgramData%\App-V | Default location for read-only package files |
| Machine Catalog | %ProgramData%\Microsoft\AppV\Client\Catalog | Contains per-machine configuration documents |
| User Catalog | %AppData%\Microsoft\AppV\Client\Catalog | Contains per-user configuration documents |
| Shortcut Backups | %AppData%\Microsoft\AppV\Client\Integration\ShortCutBackups | Stores previous integration points that enable restore on package unpublish |
| Copy on Write (COW) Roaming | %AppData%\Microsoft\AppV\Client\VFS | Writeable roaming location for package modification |
| Copy on Write (COW) Local | %LocalAppData%\Microsoft\AppV\Client\VFS | Writeable non-roaming location for package modification |
| Machine Registry | HKLM\Software\Microsoft\AppV | Contains package state information, including VReg for machine or globally published packages (Machine hive) |
| User Registry | HKCU\Software\Microsoft\AppV | Contains user package state information including VReg |
| User Registry Classes | HKCU\Software\Classes\AppV | Contains additional user package state information |

More details for the table are provided in the following sections.

### Package store

The App-V client manages the applications assets mounted in the package store. This default storage location is `%ProgramData%\App-V`, but you can configure it during or after setup by using the `Set-AppVClientConfiguration` PowerShell command, which modifies the local registry (`PackageInstallationRoot` value under the `HKLM\Software\Microsoft\AppV\Client\Streaming` key). The package store must be located at a local path on the client operating system. The individual packages are stored in the package store in subdirectories named for the Package GUID and Version GUID.

Example of a path to a specific application:

``` syntax
C:\ProgramData\App-V\PackGUID\VersionGUID
```

To change the default location of the package store during setup, see [How to Deploy the App-V client](how-to-deploy-the-app-v-client-51gb18030.md).

### Shared Content Store

If the App-V client is configured in Shared Content Store mode, no data is written to disk when a stream fault occurs, which means that the packages require minimal local disk space (publishing data). The use of less disk space is highly desirable in VDI environments, where local storage can be limited, and streaming the applications from a high performance network location (such as a SAN) is preferable.

> [!NOTE]
> The machine and package store must be located on a local drive, even when you're using Shared Content Store configurations for the App-V client.

### Package catalogs

The App-V client manages the following two file-based locations:

- **Catalogs (user and machine).**

- **Registry locations** - depends on how the package is targeted for publishing. There's a catalog (data store) for the computer, and a catalog for each individual user. The machine catalog stores global information applicable to all users or any user, and the user catalog stores information applicable to a specific user. The catalog is a collection of dynamic configurations and manifest files; there's discrete data for both file and registry per package version.

### Machine catalog

#### Machine catalog description

Stores package documents that are available to users on the machine, when packages are added and published. However, if a package is "global" at publishing time, the integrations are available to all users.

If a package is nonglobal, the integrations are published only for specific users, but there are still global resources that are modified and visible to anyone on the client computer. For example, the package directory is in a shared disk location.

If a global or nonglobal package is available to a user on the computer, the manifest is stored in the machine catalog. When a package is published globally, there's a dynamic configuration file stored in the Machine Catalog. The determination of whether a package is global is defined according to whether there's a UserDeploymentConfiguration policy file in the machine catalog.

#### Machine catalog default storage location

`%programdata%\Microsoft\AppV\Client\Catalog`

This location isn't the same as the Package Store location. The Package Store is the golden or pristine copy of the package files.

#### Files in the machine catalog

- Manifest.xml
- DeploymentConfiguration.xml
- UserManifest.xml (Globally Published Package)
- UserDeploymentConfiguration.xml (Globally Published Package)

#### Another machine catalog location, used when the package is part of a connection group

The following location is in addition to the specific primary package location:

`%programdata%\Microsoft\AppV\Client\Catalog\PackageGroups\ConGroupGUID\ConGroupVerGUID`

#### Other files in the machine catalog when the package is part of a connection group

- PackageGroupDescriptor.xml
- UserPackageGroupDescriptor.xml (globally published Connection Group)

### User catalog

#### User catalog description

Created during the publishing process. Contains information used for publishing the package, and also used at launch to ensure that a package is provisioned to a specific user. Created in a roaming location and includes user-specific publishing information.

When a package is published for a user, the policy file is stored in the User Catalog. At the same time, a copy of the manifest is also stored in the User Catalog. When a package entitlement is removed for a user, the relevant package files are removed from the User Catalog. Looking at the user catalog, an administrator can view the presence of a Dynamic Configuration file, which indicates that the package is entitled for that user.

For roaming users, the User Catalog needs to be in a roaming or shared location to preserve the legacy App-V behavior of targeting users by default. Entitlement and policy are tied to a user, not a computer, so they should roam with the user once they're provisioned.

#### User catalog default storage location

`appdata\roaming\Microsoft\AppV\Client\Catalog\Packages\PkgGUID\VerGUID`

#### Files in the user catalog

- UserManifest.xml
- DynamicConfiguration.xml or UserDeploymentConfiguration.xml

#### Another user catalog location, used when the package is part of a connection group

The following location is in addition to the specific primary package location:

`appdata\roaming\Microsoft\AppV\Client\Catalog\PackageGroups\PkgGroupGUID\PkgGroupVerGUID`

#### Another file in the machine catalog when the package is part of a connection group

`UserPackageGroupDescriptor.xml`

### Shortcut backups

During the publishing process, the App-V client backs up any shortcuts and integration points to `%AppData%\Microsoft\AppV\Client\Integration\ShortCutBackups.` This backup enables the restoration of these integration points to the previous versions when the package is unpublished.

### Copy on Write files

The package store contains a pristine copy of the package files that streamed from the publishing server. During normal operation of an App-V application, the user or service might require changes to the files. These changes aren't made in the package store in order to preserve your ability to repair the application, which removes these changes. These locations are called "copy on write" (COW), which supports both roaming and nonroaming locations. The location where the modifications are stored depends on where the application natively writes changes to.

### COW roaming

The COW Roaming location described above stores changes to files and directories that are targeted to the typical %AppData% location or \\Users\\{username}\\AppData\\Roaming location. These directories and files are then roamed based on the operating system settings.

### COW local

The COW Local location is similar to the roaming location, but the directories and files aren't roamed to other computers, even if roaming support is configured. The COW Local location described above stores changes applicable to typical windows and not the %AppData% location. The directories listed vary but there are two locations for any typical Windows locations. For example, common AppData and common AppDataS. The **S** signifies the restricted location when the virtual service requests the change as a different elevated user from the logged on users. The non-**S** location stores user based changes.

## <a href="" id="bkmk-pkg-registry"></a>Package registry

Before an application can access the package registry data, the App-V client must make the package registry data available to the applications. The App-V client uses the real registry as a backing store for all registry data.

When a new package is added to the App-V client, a copy of the REGISTRY.DAT file from the package is created at `%ProgramData%\Microsoft\AppV\Client\VREG\{Version GUID}.dat`. The name of the file is the version GUID with the .DAT extension. The reason this copy is made is to ensure that the actual hive file in the package is never in use, which would prevent the removal of the package at a later time.

**Registry.dat from Package Store**  **>**  **%ProgramData%\Microsoft\AppV\Client\Vreg{VersionGuid}.dat**

When the first application from the package is launched on the client, the client stages or copies the contents out of the hive file, re-creating the package registry data in an alternate location `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AppV\Client\Packages\PackageGuid\Versions\VersionGuid\REGISTRY`. The staged registry data has two distinct types of machine data and user data. Machine data is shared across all users on the machine. User data is staged for each user to a user-specific location `HKCU\Software\Microsoft\AppV\Client\Packages\PackageGuid\Registry\User`. The machine data is ultimately removed at package removal time, and the user data is removed on a user unpublish operation.

### Package registry staging vs. connection group registry staging

When connection groups are present, the previous process of staging the registry holds true, but instead of having one hive file to process, there are more than one. The files are processed in the order in which they appear in the connection group XML, with the first writer winning any conflicts.

The staged registry persists the same way as in the single package case. Staged user registry data remains for the connection group until it's disabled. Staged machine registry data is removed on connection group removal.

### Virtual registry

The purpose of the virtual registry (VREG) is to provide a single merged view of the package registry and the native registry to applications. It also provides copy-on-write (COW) functionality - that is any changes made to the registry from the context of a virtual process are made to a separate COW location. This means that the VREG must combine up to three separate registry locations into a single view based on the populated locations in the registry COW -&gt; package -&gt; native. When a request is made for a registry data, it locates in order until it finds the data it was requesting. If there's a value stored in a COW location it doesn't proceed to other locations. If there's no data in the COW location, it proceeds to the package and then native location until it finds the appropriate data.

### Registry locations

There are two package registry locations and two connection group locations where the App-V client stores registry information, depending on whether the Package is published individually or as part of a connection group. There are three COW locations for packages and three for connection groups, which are created and managed by the VREG. Settings for packages and connection groups aren't shared:

#### Single package VReg

| Location | Description |
|--|--|
| **COW** | - Machine Registry\Client\Packages\PkgGUID\REGISTRY (Only elevate process can write) <br> - User Registry\Client\Packages\PkgGUID\REGISTRY (User Roaming anything written under HKCU except Software\Classes) <br> - User Registry Classes\Client\Packages\PkgGUID\REGISTRY (HKCU\Software\Classes writes and HKLM for non elevated process) |
| **Package** | - Machine Registry\Client\Packages\PkgGUID\Versions\VerGuid\Registry\Machine <br> - User Registry Classes\Client\Packages\PkgGUID\Versions\VerGUID\Registry |
| **Native** | - Native application registry location |

#### Connection group VReg

| Location | Description |
|--------------|-----------------|
| **COW** | - Machine Registry\Client\PackageGroups\GrpGUID\REGISTRY (only elevate process can write) <br> - User Registry\Client\PackageGroups\GrpGUID\REGISTRY (Anything written to HKCU except Software\Classes) <br> - User Registry Classes\Client\PackageGroups\GrpGUID\REGISTRY |
| **Package** | - Machine Registry\Client\PackageGroups\GrpGUID\Versions\VerGUID\REGISTRY <br> - User Registry Classes\Client\PackageGroups\GrpGUID\Versions\VerGUID\REGISTRY |
| **Native** | - Native application registry location |

There are two COW locations for HKLM; elevated and nonelevated processes. Elevated processes always write HKLM changes to the secure COW under HKLM. Nonelevated processes always write HKLM changes to the nonsecure COW under HKCU\\Software\\Classes. When an application reads changes from HKLM, elevated processes read changes from the secure COW under HKLM. Nonelevated reads from both, favoring the changes made in the unsecure COW first.

### Pass-through keys

Pass-through keys enable an administrator to configure certain keys so they can only be read from the native registry, bypassing the Package and COW locations. Pass-through locations are global to the machine (not package specific) and can be configured by adding the path to the key, which should be treated as pass-through to the **REG\_MULTI\_SZ** value called **PassThroughPaths** of the key `HKLM\Software\Microsoft\AppV\Subsystem\VirtualRegistry`. Any key and its children that appear under this multi-string value are treated as pass-through.

The following locations are configured as pass-through locations by default:

- HKEY\_CURRENT\_USER\\SOFTWARE\\Classes\\Local Settings\\Software\\Microsoft\\Windows\\CurrentVersion\\AppModel

- HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Classes\\Local Settings\\Software\\Microsoft\\Windows\\CurrentVersion\\AppModel

- HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\WINEVT

- HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\eventlog\\Application

- HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\WMI\\Autologger

- HKEY\_CURRENT\_USER\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Internet Settings

- HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Perflib

- HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies

- HKEY\_CURRENT\_USER\\SOFTWARE\\Policies

The purpose of pass-through keys is to ensure that a virtual application doesn't write registry data in the VReg that is required for nonvirtual applications for successful operation or integration. The policies key ensures that group policy based settings set by the administrator are utilized and not per package settings. The AppModel key is required for integration with Windows modern UI based applications. It's recommended that administers don't modify any of the default pass-through keys, but in some instances, based on application behavior might require adding more pass-through keys.

## <a href="" id="bkmk-pkg-store-behavior"></a>App-V package store behavior

App-V 5 manages the Package Store, which is the location where the expanded asset files from the `appv` file are stored. By default, this location is stored at %ProgramData%\\App-V, and is limited in terms of storage capabilities only by free disk space. The package store is organized by the GUIDs for the package and version as mentioned in the previous section.

### Add packages

App-V Packages are staged upon addition to the computer with the App-V client. The App-V client provides on-demand staging. During publishing or a manual Add-AppVClientPackage, the data structure is built in the package store (c:\\programdata\\App-V\\{PkgGUID}\\{VerGUID}). The package files identified in the publishing block defined in the StreamMap.xml are added to the system and the top level folders and child files staged to ensure proper application assets exist at launch.

### Mounting packages

Packages can be explicitly loaded using the PowerShell `Mount-AppVClientPackage` or by using the **App-V client UI** to download a package. This operation completely loads the entire package into the package store.

### Streaming packages

The App-V client can be configured to change the default behavior of streaming. All streaming policies are stored under the following registry key: `HKEY_LOCAL_MAcHINE\Software\Microsoft\AppV\Client\Streaming`. Policies are set using the PowerShell cmdlet `Set-AppvClientConfiguration`. The following policies apply to Streaming:

| Policy | Description |
|------------|------------------|
| AllowHighCostLaunch | On Windows 8 and later, it allows streaming over 3G and cellular networks. |
| AutoLoad | Specifies the Background Load setting: <br> **0** - Disabled <br> **1** - Previously Used Packages only <br> **2** - All Packages |
| PackageInstallationRoot | The root folder for the package store in the local machine. |
| PackageSourceRoot | The root-override where packages should be streamed from. |
| SharedContentStoreMode | Enables the use of Shared Content Store for VDI scenarios. |

These settings affect the behavior of streaming App-V package assets to the client. By default, App-V only downloads the assets required after downloading the initial publishing and primary feature blocks. There are three specific behaviors around streaming packages that must be explained:

- Background Streaming

- Optimized Streaming

- Stream Faults

### Background streaming

The PowerShell cmdlet `Get-AppvClientConfiguration` can be used to determine the current mode for background streaming with the AutoLoad setting and modified with the cmdlet Set-AppvClientConfiguration or from the registry (HKLM\\SOFTWARE\\Microsoft\\AppV\\ClientStreaming key). Background streaming is a default setting where the Autoload setting is set to download previously used packages. The behavior based on default setting (value=1) downloads App-V data blocks in the background after the application launches. This setting can be disabled all together (value=0) or enabled for all packages (value=2), whether they're launched.

### Optimized streaming

App-V packages can be configured with a primary feature block during sequencing. This setting allows the sequencing engineer to monitor launch files for a specific application, or applications, and mark the blocks of data in the App-V package for streaming at first launch of any application in the package.

### Stream faults

After the initial stream of any publishing data and the primary feature block, requests for more files perform stream faults. These blocks of data are downloaded to the package store on an as-needed basis. This allows a user to download only a small part of the package, typically enough to launch the package and run normal tasks. All other blocks are downloaded when a user initiates an operation that requires data not currently in the package store.

### Package upgrades

App-V Packages require updating throughout the lifecycle of the application. App-V Package upgrades are similar to the package publish operation, as each version is created in its own PackageRoot location: `%ProgramData%\App-V\{PkgGUID}\{newVerGUID}`. The upgrade operation is optimized by creating hard links to identical- and streamed-files from other versions of the same package.

### Package removal

The behavior of the App-V client when packages are removed depends on the method used for removal. Using an App-V full infrastructure to unpublish the application, the user catalog files (machine catalog for globally published applications) are removed, but retains the package store location and COW locations. When the PowerShell cmdlet `Remove-AppVClientPackge` is used to remove an App-V package, the package store location is cleaned. Remember that unpublishing an App-V package from the management server doesn't perform a remove operation. Neither operation removes the package store package files.

## <a href="" id="bkmk-roaming-reg-data"></a>Roaming registry and data

App-V 5 is able to provide a near-native experience when roaming, depending on how the application is written. By default, App-V roams AppData that is stored in the roaming location, based on the roaming configuration of the operating system. Other locations for storage of file-based data don't roam from computer to computer, since they are in locations that aren't roamed.

### <a href="" id="bkmk-clt-inter-roam-reqs"></a>Roaming requirements and user catalog data storage

App-V stores data, which represents the state of the user's catalog, in the form of:

- Files under %appdata%\\Microsoft\\AppV\\Client\\Catalog

- Registry settings under `HKEY_CURRENT_USER\Software\Microsoft\AppV\Client\Packages`

Together, these files and registry settings represent the user's catalog, so either both must be roamed, or neither must be roamed for a given user. App-V doesn't support roaming %AppData%, but not roaming the user's profile (registry), or vice versa.

> [!NOTE]
> The **Repair-AppvClientPackage** cmdlet does not repair the publishing state of packages, where the user's App-V state under `HKEY_CURRENT_USER` is missing or mismatched with the data in %appdata%.

### Registry-based data

App-V registry roaming falls into two scenarios, as shown in the following table.

| Scenario | Description |
|----------|-------------|
| Applications that are run as standard users | When a standard user launches an App-V application, both HKLM and HKCU for App-V applications are stored in the HKCU hive on the machine. This presents as two distinct paths: <br> - HKLM: `HKCU\SOFTWARE\Classes\AppV\Client\Packages{PkgGUID}\REGISTRY\MACHINE\SOFTWARE` <br> - HKCU: `HKCU\SOFTWARE\Microsoft\AppV\Client\Packages{PkgGUID}\REGISTRY\USER{UserSID}\SOFTWARE` <br> The locations are enabled for roaming based on the operating system settings. |
| Applications that are run with elevation | When an application is launched with elevation: <br> - HKLM data is stored in the HKLM hive on the local computer <br> - HKCU data is stored in the User Registry location <br> In this scenario, these settings aren't roamed with normal operating system roaming configurations, and the resulting registry keys and values are stored in the following location: <br> - `HKLM\SOFTWARE\Microsoft\AppV\Client\Packages{PkgGUID}{UserSID}\REGISTRY\MACHINE\SOFTWARE` <br> - `HKCU\SOFTWARE\Microsoft\AppV\Client\Packages{PkgGUID}\Registry\User{UserSID}\SOFTWARE` |

### App-V and folder redirection

App-V 5.1 supports folder redirection of the roaming AppData folder (%AppData%). When the virtual environment is started, the roaming AppData state from the user's roaming AppData directory is copied to the local cache. Conversely, when the virtual environment is shut down, the local cache that is associated with a specific user's roaming AppData is transferred to the actual location of that user's roaming AppData directory.

A typical package has several locations mapped in the user's backing store for settings in both AppData\\Local and AppData\\Roaming. These locations are the Copy on Write locations that are stored per user in the user's profile, and that are used to store changes made to the package VFS directories and to protect the default package VFS.

The following table shows local and roaming locations, when folder redirection hasn't been implemented.

| VFS directory in package | Mapped location of backing store |
|--------------------------|----------------------------------|
| ProgramFilesX86          | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\ProgramFilesX86 |
| SystemX86                | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\SystemX86 |
| Windows                  | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\Windows |
| appv_ROOT                | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\appv_ROOT |
| AppData                  | C:\users\jsmith\AppData\Roaming\Microsoft\AppV\Client\VFS\<GUID>\AppData |

The following table shows local and roaming locations, when folder redirection is implemented for %AppData%, and the location is redirected (typically to a network location).

| VFS directory in package | Mapped location of backing store |
|--------------------------|----------------------------------|
| ProgramFilesX86          | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\ProgramFilesX86 |
| SystemX86                | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\SystemX86 |
| Windows                  | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\Windows |
| appv_ROOT                | C:\users\jsmith\AppData\Local\Microsoft\AppV\Client\VFS\<GUID>\appv_ROOT |
| AppData                  | \Fileserver\users\jsmith\roaming\Microsoft\AppV\Client\VFS\<GUID>\AppData |

The current App-V client VFS driver can't write to network locations, so the App-V client detects the presence of folder redirection and copies the data on the local drive during publishing and when the virtual environment starts. After the user closes the App-V application and the App-V client closes the virtual environment, the local storage of the VFS AppData is copied back to the network, enabling roaming to other machines, where the process will be repeated. The detailed steps of the processes are:

1. During publishing or virtual environment startup, the App-V client detects the location of the AppData directory.

2. If the roaming AppData path is local or an AppData\\Roaming location is mapped, nothing happens.

3.  If the roaming AppData path isn't local, the VFS AppData directory is mapped to the local AppData directory.

This process solves the problem of a nonlocal %AppData% that isn't supported by the App-V client VFS driver. However, the data stored in this new location isn't roamed with folder redirection. All changes during the running of the application happen to the local AppData location and must be copied to the redirected location. The detailed steps of this process are:

1.  App-V application is shut down, which shuts down the virtual environment.

2.  The local cache of the roaming AppData location is compressed and stored in a ZIP file.

3.  A timestamp at the end of the ZIP packaging process is used to name the file.

4.  The timestamp is recorded in the registry: HKEY\_CURRENT\_USER\\Software\\Microsoft\\AppV\\Client\\Packages\\&lt;GUID&gt;\\AppDataTime as the last known AppData timestamp.

5.  The folder redirection process is called to evaluate and initiate the ZIP file uploaded to the roaming AppData directory.

The timestamp is used to determine a "last writer wins" scenario if there's a conflict and is used to optimize the download of the data when the App-V application is published or the virtual environment is started. Folder redirection makes the data available from any other clients covered by the supporting policy and starts the process of storing the AppData\\Roaming data to the local AppData location on the client. The detailed processes are:

1.  The user starts the virtual environment by starting an application.

2.  The application's virtual environment checks for the most recent time stamped ZIP file, if present.

3.  The registry is checked for the last known uploaded timestamp, if present.

4.  The most recent ZIP file is downloaded unless the local last known upload timestamp is greater than or equal to the timestamp from the ZIP file.

5.  If the local last known upload timestamp is earlier than that of the most recent ZIP file in the roaming AppData location, the ZIP file is extracted to the local temp directory in the user's profile.

6.  After the ZIP file is successfully extracted, the local cache of the roaming AppData directory is renamed and the new data is moved into place.

7.  The renamed directory is deleted and the application opens with the most recently saved roaming AppData data.

This completes the successful roaming of application settings that are present in AppData\\Roaming locations. The only other condition that must be addressed is a package repair operation. The details of the process are:

1.  During repair, detect if the path to the user's roaming AppData directory isn't local.

2.  Map the nonlocal roaming AppData path targets are recreated the expected roaming and local AppData locations.

3.  Delete the timestamp stored in the registry, if present.

This process re-creates both the local and network locations for AppData and remove the registry record of the timestamp.

## <a href="" id="bkmk-clt-app-lifecycle"></a>App-V client application lifecycle management

In an App-V full infrastructure, after applications are sequenced they're managed and published to users or computers via the App-V Management and Publishing servers. This section details the operations that occur during the common App-V application lifecycle operations (Add, publishing, launch, upgrade, and removal) and the file and registry locations that are changed and modified from the App-V client perspective. The App-V client operations are performed as a series of PowerShell commands initiated on the computer running the App-V client.

This document focuses on App-V full infrastructure solutions. For specific information on App-V integration with Configuration Manager 2012, see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

The App-V application lifecycle tasks are triggered at user sign-in (default), machine startup, or as background timed operations. The settings for the App-V client operations, including Publishing Servers, refresh intervals, package script enablement, and others, are configured during setup of the client or post-setup with PowerShell commands. See the How to Deploy the Client section on TechNet at: [How to deploy the App-V client](how-to-deploy-the-app-v-client-51gb18030.md) or utilize the PowerShell:

```powershell
get-command *appv*
```

### Publishing refresh

The publishing refresh process includes several smaller operations that happen on the App-V client. Since App-V is an application virtualization technology and not a task scheduling technology, the Windows Task Scheduler is utilized to enable the process at user sign-in, machine startup, and at scheduled intervals. The configuration of the client during setup listed is the preferred method when distributing the client to a large group of computers with the correct settings. These client settings can be configured with the following PowerShell cmdlets:

- **Add-AppVPublishingServer:** Configures the client with an App-V Publishing Server that provides App-V packages.

- **Set-AppVPublishingServer:** Modifies the current settings for the App-V Publishing Server.

- **Set-AppVClientConfiguration:** Modifies the currents settings for the App-V client.

- **Sync-AppVPublishingServer:** Initiates an App-V Publishing Refresh process manually. This is also utilized in the scheduled tasks created during configuration of the publishing server.

The focus of the following sections is to detail the operations that occur during different phases of an App-V Publishing Refresh.

### Adding an App-V package

Adding an App-V package to the client is the first step of the publishing refresh process. The end result is the same as the `Add-AppVClientPackage` cmdlet in PowerShell, except during the publishing refresh add process, the configured publishing server is contacted and passes a high-level list of applications back to the client to pull more detailed information and not a single package add operation. The process continues by configuring the client for package or connection group additions or updates, then accesses the `appv` file. Next, the contents of the `appv` file are expanded and placed on the local operating system in the appropriate locations. The following is a detailed workflow of the process, assuming the package is configured for Fault Streaming.

#### How to add an App-V package

1.  Manual initiation via PowerShell or task sequence initiation of the publishing refresh process.

    1.  The App-V client makes an HTTP connection and requests a list of applications based on the target. The publishing refresh process supports targeting machines or users.

    2.  The App-V publishing server uses the identity of the initiating target, user or machine, and queries the database for a list of entitled applications. The list of applications is provided as an XML response, which the client uses to send other requests to the server for more information on a per package basis.

2.  The publishing agent on the App-V client does all of the following actions in a serialized way.

    Evaluate any connection groups that are unpublished or disabled, since package version updates that are part of the connection group can't be processed.

3.  Configure the packages by identifying an add or update operations.

    1.  The App-V client utilizes the AppX API from Windows and accesses the `appv` file from the publishing server.

    2.  The package file is opened and the AppXManifest.xml and StreamMap.xml are downloaded to the Package Store.

    3.  Completely stream publishing block data defined in the StreamMap.xml. Stores the publishing block data in the Package Store\\PkgGUID\\VerGUID\\Root.

        - Icons: Targets of extension points.

        - Portable Executable Headers (PE Headers): Targets of extension points that contain the base information about the image need on disk, directly accessed or via file types.

        - Scripts: Download scripts directory for use throughout the publishing process.

    4.  Populate the Package store:

        1.  Create sparse files on disk that represent the extracted package for any directories listed.

        2.  Stage top level files and directories under root.

        3.  All other files are created when the directory is listed as sparse on disk and streamed on demand.

    5.  Create the machine catalog entries. Create the Manifest.xml and DeploymentConfiguration.xml from the package files (if no DeploymentConfiguration.xml file in the package a placeholder is created).

    6.  Create location of the package store in the registry HKLM\\Software\\Microsoft\\AppV\\Client\\Packages\\PkgGUID\\Versions\\VerGUID\\Catalog

    7.  Create the Registry.dat file from the package store to %ProgramData%\\Microsoft\\AppV\\Client\\VReg\\{VersionGUID}.dat

    8.  Register the package with the App-V Kernel Mode Driver HKLM\\Microsoft\\Software\\AppV\\MAV

    9.  Invoke scripting from the AppxManifest.xml or DeploymentConfig.xml file for Package Add timing.

4.  Configure Connection Groups by adding and enabling or disabling.

5.  Remove objects that aren't published to the target (user or machine).

    > [!NOTE]
    > This action doesn't delete a package. It removes integration points for the specific target (user or machine) and removes user catalog files (machine catalog files for globally published).

6.  Invoke background load mounting based on client configuration.

7.  Packages that already have publishing information for the machine or user are immediately restored.

    > [!NOTE]
    > This condition occurs as a product of removal without unpublishing with background addition of the package.

This completes an App-V package add of the publishing refresh process. The next step is publishing the package to the specific target (machine or user).

![package add file and registry data.](images/packageaddfileandregistrydata.png)

### Publishing an App-V package

During the publishing refresh operation, the specific publishing operation (Publish-AppVClientPackage) adds entries to the user catalog, maps entitlement to the user, identifies the local store, and finishes by completing any integration steps. The following are the detailed steps.

#### How to publish and App-V package

1.  Package entries are added to the user catalog

    1.  User targeted packages: the UserDeploymentConfiguration.xml and UserManifest.xml are placed on the machine in the User Catalog

    2.  Machine targeted (global) packages: the UserDeploymentConfiguration.xml is placed in the Machine Catalog

2.  Register the package with the kernel mode driver for the user at HKLM\\Software\\Microsoft\\AppV\\MAV

3.  Perform integration tasks.

    1.  Create extension points.

    2.  Store backup information in the user's registry and roaming profile (Shortcut Backups).

        > [!NOTE]
        > This action enables restore extension points if the package is unpublished.

    3.  Run scripts targeted for publishing timing.

Publishing an App-V package that is part of a connection group is similar to the previous process. For connection groups, the path that stores the specific catalog information includes PackageGroups as a child of the catalog directory.

![package add file and registry data - global.](images/packageaddfileandregistrydata-global.png)

### Application launch

After the publishing refresh process, the user launches and then relaunches an App-V application. The process is optimized to launch quickly with a minimum of network traffic. The App-V client checks the path to the user catalog for files created during publishing. After rights to launch the package are established, the App-V client creates a virtual environment, begins streaming any necessary data, and applies the appropriate manifest and deployment configuration files during virtual environment creation. With the virtual environment created and configured for the specific package and application, the application starts.

#### How to launch App-V applications

1.  User launches the application by clicking on a shortcut or file type invocation.

2.  The App-V client verifies existence in the User Catalog for the following files

    - UserDeploymentConfiguration.xml

    - UserManifest.xml

3.  If the files are present, the application is entitled for that specific user and the application starts the process for launch. There's no network traffic at this point.

4.  Next, the App-V client checks that the path for the package registered for the App-V client service is found in the registry.

5.  Upon finding the path to the package store, the virtual environment is created. If this is the first launch, the primary feature block downloads if present.

6.  After downloading, the App-V client service consumes the manifest and deployment configuration files to configure the virtual environment and all App-V subsystems are loaded.

7.  The application launches. For any missing files in the package store (sparse files), App-V stream-faults the files on an as needed basis.

    ![package add file and registry data - stream.](images/packageaddfileandregistrydata-stream.png)

### Upgrading an App-V package

The App-V 5 package upgrade process differs from the older versions of App-V. App-V supports multiple versions of the same package on a machine entitled to different users. Package versions can be added at any time as the package store and catalogs are updated with the new resources. The only process specific to the addition of new version resources is storage optimization. During an upgrade, only the new files are added to the new version store location and hard links are created for unchanged files. This reduces the overall storage by only presenting the file on one disk location and then projecting it into all folders with a file location entry on the disk. The specific details of upgrading an App-V Package are as follows:

#### How to upgrade an App-V package

1.  The App-V client performs a Publishing Refresh and discovers a newer version of an App-V Package.

2.  Package entries are added to the appropriate catalog for the new version

    1.  User targeted packages: the UserDeploymentConfiguration.xml and UserManifest.xml are placed on the machine in the user catalog at appdata\\roaming\\Microsoft\\AppV\\Client\\Catalog\\Packages\\PkgGUID\\VerGUID

    2.  Machine targeted (global) packages: the UserDeploymentConfiguration.xml is placed in the machine catalog at %programdata%\\Microsoft\\AppV\\Client\\Catalog\\Packages\\PkgGUID\\VerGUID

3.  Register the package with the kernel mode driver for the user at HKLM\\Software\\Microsoft\\AppV\\MAV

4.  Perform integration tasks.

    - Integrate extensions points (EP) from the Manifest and Dynamic Configuration files.

    1.  File based EP data is stored in the AppData folder utilizing Junction Points from the package store.

    2.  Version 1 EPs already exist when a new version becomes available.

    3.  The extension points are switched to the Version 2 location in machine or user catalogs for any newer or updated extension points.

5.  Run scripts targeted for publishing timing.

6.  Install Side by Side assemblies as required.

### Upgrading an in-use App-V package

**Starting in App-V 5 SP2**: If you try to upgrade a package that is in use by an end user, the upgrade task is placed in a pending state. The upgrade runs later, according to the following rules:

| Task type | Applicable rule |
|-----------|------------------|
| User-based task, for example, publishing a package to a user | The pending task runs after the user signs out and then signs in again. |
| Globally based task, for example, enabling a connection group globally | The pending task runs when the computer is shut down and then restarted. |

When a task is placed in a pending state, the App-V client also generates a registry key for the pending task, as follows:

| User-based or globally based task | Where the registry key is generated |
|-----------------------------------|-------------------------------------|
| User-based tasks                  | KEY_CURRENT_USER\Software\Microsoft\AppV\Client\PendingTasks |
| Globally based tasks              | HKEY_LOCAL_MACHINE\Software\Microsoft\AppV\Client\PendingTasks |

The following operations must be completed before users can use the newer version of the package:

| Task | Details |
|--|--|
| Add the package to the computer | This task is computer specific and you can perform it at any time by completing the steps in the Package Add section. |
| Publish the package | See the Package Publishing section for steps. This process requires that you update extension points on the system. End users can't be using the application when you complete this task. |

Use the following example scenarios as a guide for updating packages.

| Scenario | Requirements |
|--|--|
| App-V package isn't in use when you try to upgrade | None of the following components of the package can be in use: virtual application, COM server, or shell extensions. <br> The administrator publishes a newer version of the package and the upgrade works the next time a component or application inside the package is launched. The new version of the package is streamed and run. Nothing changed in this scenario in App-V 5 SP2 from previous releases of App-V 5. |
| App-V package is in use when the administrator publishes a newer version of the package | The upgrade operation is set to pending by the App-V client, which means that it's queued and carried out later when the package isn't in use. <br> If the package application is in use, the user shuts down the virtual application, after which the upgrade can occur. <br> If the package has shell extensions (Office 2013), which are permanently loaded by Windows Explorer, the user can't be signed in. Users must sign out and then sign in again to start the App-V package upgrade. |

### Global vs user publishing

App-V packages can be published in one of two ways. User publishing entitles an App-V package to a specific user or group of users. Global publishing entitles the App-V package to the entire machine for all users of the machine. Once a package upgrade is pending and the App-V package isn't in use, consider the two types of publishing:

- **Globally published**: the application is published to a machine; all users on that machine can use it. The upgrade happens when the App-V client Service starts, which effectively means a machine restart.

- **User published**: the application is published to a user. If there are multiple users on the machine, the application can be published to a subset of the users. The upgrade happens when the user signs in or when it's published again. This happens periodically, with Configuration Manager policy refresh and evaluation, an App-V periodic publishing/refresh, or explicitly via PowerShell commands.

### Removing an App-V package

Removing App-V applications in a full infrastructure is an unpublish operation, and doesn't start a package removal. The process is the same as the publish process, but instead of adding the removal process reverses the changes that are made for App-V packages.

### Repairing an App-V package

The repair operation might affect many locations on the machine. The previously mentioned Copy on Write (COW) locations are removed, and extension points are deintegrated and then reintegrated. Review the COW data placement locations by reviewing where they're registered in the registry. This operation is done automatically and there's no administrative control other than initiating a Repair operation from the App-V client console or via PowerShell (Repair-AppVClientPackage).

## <a href="" id="bkmk-integr-appv-pkgs"></a>Integration of App-V packages

The App-V client and package architecture provides specific integration with the local operating system during the addition and publishing of packages. Three files define the integration or extension points for an App-V Package:

- AppXManifest.xml: Stored inside of the package with fallback copies stored in the package store and the user profile. Contains the options created during the sequencing process.

- DeploymentConfig.xml: Provides configuration information of computer and user based integration extension points.

- UserConfig.xml: A subset of the Deploymentconfig.xml that only provides user-based configurations and only targets user-based extension points.

### Rules of integration

When App-V applications are published to a computer with the App-V client, some specific actions take place as described in the following list:

- Global Publishing: Shortcuts are stored in the All Users profile location and other extension points are stored in the registry in the HKLM hive.

- User Publishing: Shortcuts are stored in the current user account profile and other extension points are stored in the registry in the HKCU hive.

- Back up and restore: Existing native application data and registry (such as FTA registrations) are backed up during publishing.

    1.  App-V packages are given ownership based on the last integrated package where the ownership is passed to the newest published App-V application.

    2.  Ownership transfers from one App-V package to another when the owning App-V package is unpublished. This process doesn't start a restore of the data or registry.

    3.  Restore the backed-up data when the last package is unpublished or removed on a per extension point basis.

### Extension points

The App-V publishing files (manifest and dynamic configuration) provide several extension points that enable the application to integrate with the local operating system. These extension points perform typical application installation tasks, such as placing shortcuts, creating file type associations, and registering components. As these are virtualized applications that aren't installed in the same manner a traditional application, there are some differences. The following list is the extension points covered in this section:

- Shortcuts

- File Type Associations

- Shell Extensions

- COM

- Software Clients

- Application capabilities

- URL Protocol Handler

- AppPath

- Virtual Application

### Shortcuts

The shortcut is one of the basic elements of integration with the OS and is the interface for direct user launch of an App-V application.

From the package manifest and dynamic configuration XML files, the path to a specific application executable can be found in a section similar to the following example:

```xml
<Extension Category="AppV.Shortcut">
          <Shortcut>
            <File>[{Common Desktop}]\Adobe Reader 9.lnk</File>
            <Target>[{AppVPackageRoot}]\Reader\AcroRd32.exe</Target>
            <Icon>[{Windows}]\Installer\{AC76BA86-7AD7-1033-7B44-A94000000001}\SC_Reader.ico</Icon>
            <Arguments />
            <WorkingDirectory />
            <ShowCommand>1</ShowCommand>
            <ApplicationId>[{AppVPackageRoot}]\Reader\AcroRd32.exe</ApplicationId>
          </Shortcut>
        </Extension>
```

As mentioned previously, the App-V shortcuts are placed by default in the user's profile based on the refresh operation. Global refresh places shortcuts in the All Users profile and user refresh stores them in the specific user's profile. The actual executable is stored in the package store. The location of the ICO file is a tokenized location in the App-V package.

### File type associations

The App-V client manages the local operating system File Type Associations during publishing, which enables users to use file type invocations or to open a file with a registered extension, like `.docx`, to start an App-V application. File type associations are present in the manifest and dynamic configuration files as represented in the following example:

```xml
<Extension Category="AppV.FileTypeAssociation">
          <FileTypeAssociation>
            <FileExtension MimeAssociation="true">
              <Name>.xdp</Name>
              <ProgId>AcroExch.XDPDoc</ProgId>
              <ContentType>application/vnd.adobe.xdp+xml</ContentType>
            </FileExtension>
            <ProgId>
              <Name>AcroExch.XDPDoc</Name>
              <Description>Adobe Acrobat XML Data Package File</Description>
              <EditFlags>65536</EditFlags>
              <DefaultIcon>[{Windows}]\Installer\{AC76BA86-7AD7-1033-7B44-A94000000001}\XDPFile_8.ico</DefaultIcon>
              <ShellCommands>
                <DefaultCommand>Read</DefaultCommand>
                <ShellCommand>
                  <ApplicationId>[{AppVPackageRoot}]\Reader\AcroRd32.exe</ApplicationId>
                  <Name>Open</Name>
                  <CommandLine>"[{AppVPackageRoot}]\Reader\AcroRd32.exe" "%1"</CommandLine>
                </ShellCommand>
                <ShellCommand>
                  <ApplicationId>[{AppVPackageRoot}]\Reader\AcroRd32.exe</ApplicationId>
                  <Name>Printto</Name>
                  <CommandLine>"[{AppVPackageRoot}]\Reader\AcroRd32.exe"  /t "%1" "%2" "%3" "%4"</CommandLine>
                </ShellCommand>
                <ShellCommand>
                  <ApplicationId>[{AppVPackageRoot}]\Reader\AcroRd32.exe</ApplicationId>
                  <Name>Read</Name>
                  <FriendlyName>Open with Adobe Reader 9</FriendlyName>
                  <CommandLine>"[{AppVPackageRoot}]\Reader\AcroRd32.exe" "%1"</CommandLine>
                </ShellCommand>
              </ShellCommands>
            </ProgId>
          </FileTypeAssociation>
        </Extension>
```

> [!NOTE]
> In this example:
>
> - `<Name>.xdp</Name>` is the extension
>
> - `<Name>AcroExch.XDPDoc</Name>` is the ProgId value (which points to the adjoining ProgId)
>
> - `<CommandLine>"[{AppVPackageRoot}]\Reader\AcroRd32.exe" "%1"</CommandLine>` is the command line, which points to the application executable

### Shell extensions

Shell extensions are embedded in the package automatically during the sequencing process. When the package is published globally, the shell extension gives users the same functionality as if the application were locally installed. The application requires no other setup or configuration on the client to enable the shell extension functionality.

#### Requirements for using shell extensions

- Packages that contain embedded shell extensions must be published globally.

- The "bitness" of the application, sequencer, and App-V client must match, or the shell extensions won't work. For example:

  - The version of the application is 64-bit.

  - The Sequencer is running on a 64-bit computer.

  - The package is being delivered to a 64-bit App-V client computer.

The following table displays the supported shell extensions.

| Handler | Description |
|--|--|
| Context menu handler | Adds menu items to the context menu. It's called before the context menu is displayed. |
| Drag-and-drop handler | Controls the action upon right-click drag-and-drop and modifies the context menu that appears. |
| Drop target handler | Controls the action after a data object is dragged-and-dropped over a drop target such as a file. |
| Data object handler | Controls the action after a file is copied to the clipboard or dragged-and-dropped over a drop target. It can provide other clipboard formats to the drop target. |
| Property sheet handler | Replaces or adds pages to the property sheet dialog box of an object. |
| Infotip handler | Allows retrieving flags and infotip information for an item and displaying it inside a popup tooltip upon mouse-hover. |
| Column handler | Allows creating and displaying custom columns in Windows Explorer *Details view*. It can be used to extend sorting and grouping. |
| Preview handler | Enables a preview of a file to be displayed in the Windows Explorer Preview Pane. |

### COM

The App-V client supports publishing applications with support for COM integration and virtualization. COM integration allows the App-V client to register COM objects on the local operating system and virtualization of the objects. For the purposes of this document, the integration of COM objects requires more detail.

App-V supports registering COM objects from the package to the local operating system with two process types: Out-of-process and in-process. Registering COM objects is accomplished with one or a combination of multiple modes of operation for a specific App-V package that includes off, Isolated, and Integrated. The integrated mode is configured for either the out-of-process or in-process type. Configuration of COM modes and types is accomplished with dynamic configuration files (deploymentconfig.xml or userconfig.xml).

### Software clients and application capabilities

App-V supports specific software clients and application capabilities extension points that enable virtualized applications to be registered with the software client of the operating system. This enables users to select default programs for operations like email, instant messaging, and media player. This operation is performed in the control panel with the Set Program Access and Computer Defaults, and configured during sequencing in the manifest or dynamic configuration files. Application capabilities are only supported when the App-V applications are published globally.

Example of software client registration of an App-V based mail client.

```xml
    <SoftwareClients Enabled="true">
      <ClientConfiguration EmailEnabled="true" />
      <Extensions>
        <Extension Category="AppV.SoftwareClient">
          <SoftwareClients>
            <EMail MakeDefault="true">
              <Name>Mozilla Thunderbird</Name>
              <Description>Mozilla Thunderbird</Description>
              <DefaultIcon>[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe,0</DefaultIcon>
              <InstallationInformation>
                <RegistrationCommands>
                  <Reinstall>"[{ProgramFilesX86}]\Mozilla Thunderbird\uninstall\helper.exe" /SetAsDefaultAppGlobal</Reinstall>
                  <HideIcons>"[{ProgramFilesX86}]\Mozilla Thunderbird\uninstall\helper.exe" /HideShortcuts</HideIcons>
                  <ShowIcons>"[{ProgramFilesX86}]\Mozilla Thunderbird\uninstall\helper.exe" /ShowShortcuts</ShowIcons>
                </RegistrationCommands>
                <IconsVisible>1</IconsVisible>
                <OEMSettings />
              </InstallationInformation>
              <ShellCommands>
                <ApplicationId>[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe</ApplicationId>
                <Open>"[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe" -mail</Open>
              </ShellCommands>
              <MAPILibrary>[{ProgramFilesX86}]\Mozilla Thunderbird\mozMapi32_InUse.dll</MAPILibrary>
              <MailToProtocol>
                <Description>Thunderbird URL</Description>
                <EditFlags>2</EditFlags>
                <DefaultIcon>[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe,0</DefaultIcon>
                <ShellCommands>
                  <ApplicationId>[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe</ApplicationId>
                  <Open>"[{ProgramFilesX86}]\Mozilla Thunderbird\thunderbird.exe" -osint -compose "%1"</Open>
                </ShellCommands>
              </MailToProtocol>
            </EMail>
          </SoftwareClients>
        </Extension>
      </Extensions>
    </SoftwareClients>
```

> [!NOTE]
> In this example:
>
> - `<ClientConfiguration EmailEnabled="true" />` is the overall Software Clients setting to integrate Email clients
>
> - `<EMail MakeDefault="true">` is the flag to set a particular Email client as the default Email client
>
> - `<MAPILibrary>[{ProgramFilesX86}]\Mozilla Thunderbird\mozMapi32_InUse.dll</MAPILibrary>` is the MAPI dll registration

### URL protocol handler

Applications don't always call virtualized applications utilizing file type invocation. For example, an application supports embedding a `mailto:` link inside a document or web page. The user selects the `mailto:` link and expects to get their registered mail client. App-V supports URL protocol handlers that you can register with Windows for each package. During sequencing, the URL protocol handlers are automatically added to the package.

For situations where there's more than one application that could register the specific URL protocol handler, the dynamic configuration files can be utilized to modify the behavior and suppress or disable this feature for an application that shouldn't be the primary application launched.

### AppPath

The AppPath extension point supports calling App-V applications directly from Windows. This behavior typically happens from the run or start screen. You can provide access to App-V applications from OS commands or scripts without calling the specific path to the executable. It avoids modifying the system path environment variable on all systems, as it happens during publishing.

The AppPath extension point is configured either in the manifest or in the dynamic configuration files and is stored in the registry on the local machine during publishing for the user.

### Virtual application

This subsystem provides a list of applications captured during sequencing, which is usually consumed by other App-V components. Integration of extension points belonging to a particular application can be disabled using dynamic configuration files. For example, if a package contains two applications, it's possible to disable all extension points belonging to one application, in order to allow only integration of extension points of other application.

### Extension point rules

The extension points are integrated into the OS based on how the packages are published. Global publishing places extension points in public machine locations, where user publishing places extension points in user locations. For example a shortcut that's created on the desktop and published globally results in the file data for the shortcut (%Public%\\Desktop) and the registry data (HKLM\\Software\\Classes). The same shortcut has file data (%UserProfile%\\Desktop) and registry data (HKCU\\Software\\Classes).

Extension points aren't all published the same way. Some extension points require global publishing. Others require sequencing on the specific OS and architecture where they're delivered. The following table describes these two key rules.

| Virtual Extension         | Requires target OS Sequencing | Requires Global Publishing |
|---------------------------|------------------------------|----------------------------|
| Shortcut                  |                              |                            |
| File Type Association     |                              |                            |
| URL Protocols             | X                            |                            |
| AppPaths                  | X                            |                            |
| COM Mode                  |                              |                            |
| Software Client           | X                            |                            |
| Application Capabilities  | X                            | X                          |
| Context Menu Handler      | X                            | X                          |
| Drag-and-drop Handler     | X                            |                            |
| Data Object Handler       | X                            |                            |
| Property Sheet Handler    | X                            |                            |
| Infotip Handler           | X                            |                            |
| Column Handler            | X                            |                            |
| Shell Extensions          | X                            |                            |
| Browser Helper Object     | X                            | X                          |
| Active X Object           | X                            | X                          |

## <a href="" id="bkmk-dynamic-config"></a>Dynamic configuration processing

As organizations deploy App-V applications across business lines and geographic and political boundaries, the ability to sequence an application one time with one set of settings becomes impossible. App-V was designed for this scenario, as it captures specific settings and configurations during sequencing in the manifest file, but also supports modification with dynamic configuration files.

App-V dynamic configuration allows for specifying a policy for a package either at the machine level or at the user level. The dynamic configuration files enable sequencing engineers to modify the configuration of a package, post-sequencing, to address the needs of individual groups of users or machines. In some instances, you might need to make modifications to the application to provide proper functionality within the App-V environment. For example, you might need to make modifications to the `_*config.xml` files to allow certain actions to be performed at a specified time during the execution of the application, like disabling a mailto extension to prevent a virtualized application from overwriting that extension from another application.

App-V Packages contain the manifest file inside of the `appv` package file, which is representative of sequencing operations and is the policy of choice unless dynamic configuration files are assigned to a specific package. Post-sequencing, the dynamic configuration files can be modified to allow the publishing of an application to different desktops or users with different extension points. The two dynamic configuration files are the dynamic deployment configuration (DDC) and dynamic user configuration (DUC) files. This section focuses on the combination of the manifest and dynamic configuration files.

### Example for dynamic configuration files

The following manifest example shows the combination of the manifest, deployment configuration, and user configuration files after publishing and during normal operation. These examples are abbreviated examples of each of the files. The purpose is to show the combination of the files only and not to be a complete description of the specific categories available in each of the files.

#### Manifest

```xml
<appv:Extension Category="AppV.Shortcut">
     <appv:Shortcut>
          <appv:File>[{Common Programs}]\7-Zip\7-Zip File Manager.lnk</appv:File>
          <appv:Target>[{AppVPackageRoot}]\7zFM.exe</appv:Target>
          <appv:Icon>[{AppVPackageRoot}]\7zFM exe.O.ico</appv:Icon>
     </appv:Shortcut>
</appv:Extension>
```

#### Deployment configuration

```xml
<MachineConfiguration>
     <Subsystems>
          <Registry>
               <Include>
                    <Key Path= "\REGISTRY\Machine\Software\7zip">
                    <Value Type="REG_SZ" Name="Config" Data="1234"/>
                    </Key>
               </Include>
          </Registry>
     </Subsystems>
```

#### User configuration

```xml
<UserConfiguration>
     <Subsystems>
<appv:ExtensionCategory="AppV.Shortcut">
     <appv:Shortcut>
          <appv:File>[{Desktop}]\7-Zip\7-Zip File Manager.lnk</appv:File>
          <appv:Target>[{AppVPackageRoot}]\7zFM.exe</appv:Target>
          <appv:Icon>[{AppVPackageRoot}]\7zFM exe.O.ico</appv:Icon>
     </appv:Shortcut>
</appv:Extension>
     </Subsystems>
<UserConfiguration>
     <Subsystems>
<appv:Extension Category="AppV.Shortcut">
     <appv:Shortcut>
          <appv:Fìle>[{Desktop}]\7-Zip\7-Zip File Manager.lnk</appv:File>
          <appv:Target>[{AppVPackageRoot}]\7zFM.exe</appv:Target>
          <appv:Icon>[{AppVPackageRoot}]\7zFM.exe.O.ico</appv:Icon>
     </appv:Shortcut>
     <appv:Shortcut>
          <appv:File>[{Common Programs}]\7-Zip\7-Zip File Manager.Ink</appv:File>
          <appv:Target>[{AppVPackageRoot}]\7zFM.exe</appv:Target>
          <appv:Icon>[{AppVPackageRoot)]\7zFM.exe.O.ico</appv: Icon>
     </appv:Shortcut>
</appv:Extension>
     </Subsystems>
<MachineConfiguration>
     <Subsystems>
          <Registry>
               <Include>
                    <Key Path="\REGISTRY\Machine\Software\7zip">
                    <Value Type="REG_SZ" Name="Config" Data="1234"/>
               </Include>
          </Registry>
     </Subsystems>
```

## <a href="" id="bkmk-sidebyside-assemblies"></a>Side-by-side assemblies

App-V supports the automatic packaging of side-by-side (SxS) assemblies during sequencing and deployment on the client during virtual application publishing. App-V 5 SP2 supports capturing SxS assemblies during sequencing for assemblies not present on the sequencing machine. For assemblies that use Visual C++ version 8 and later and/or MSXML run-time, the sequencer automatically detects and captures these dependencies. This behavior happens even if they weren't installed during monitoring. The SxS assemblies feature removes the limitations of previous versions of App-V. Previously, the App-V sequencer didn't capture assemblies already present on the sequencing workstation and privatizing the assemblies, which limited to one-bit version per package. This behavior resulted in deployed App-V applications to clients missing the required SxS assemblies, causing application launch failures. This forced the packaging process to document and then ensure that all assemblies required for packages were locally installed on the user's client operating system to ensure support for the virtual applications. Based on the number of assemblies and the lack of application documentation for the required dependencies, this task was both a management and implementation challenge.

SxS assembly support in App-V has the following features.

- Automatic captures of SxS assembly during sequencing, regardless of whether the assembly was already installed on the sequencing workstation.

- The App-V client automatically installs required SxS assemblies to the client computer at publishing time when they aren't present.

- The sequencer reports the VC run-time dependency in sequencer reporting mechanism.

- The sequencer allows opting to not package the assemblies that are already installed on the sequencer. It supports scenarios where the assemblies were previously installed on the target computers.

### Automatic publishing of SxS assemblies

During publishing of an App-V package with SxS assemblies, the App-V client checks for the presence of the assembly on the machine. If the assembly doesn't exist, the client deploys the assembly to the machine. Packages that are part of connection groups rely on the SxS assembly installations that are part of the base packages, as the connection group doesn't contain any information about assembly installation.

> [!NOTE]
> Unpublishing or removing a package with an assembly doesn't remove the assemblies for that package.

## <a href="" id="bkmk-client-logging"></a>Client logging

The App-V client logs information to the Windows event log and uses standard ETW format. The specific App-V events can be found in the event viewer, under Applications and Services Logs\\Microsoft\\AppV\\Client.

> [!NOTE]
> In App-V 5.0 SP3, some logs were consolidated and moved to the following location:
>
> `Event logs/Applications and Services Logs/Microsoft/AppV/ServiceLog`
>
> For a list of the moved logs, see [About App-V 5.0 SP3](about-app-v-50-sp3.md#bkmk-event-logs-moved).

There are three specific categories of events recorded:

**Admin**: Logs events for configurations being applied to the App-V client, and contains the primary warnings and errors.

**Operational**: Logs the general App-V execution and usage of individual components creating an audit log of the App-V completed operations on the App-V client.

**Virtual Application**: Logs virtual application launches and use of virtualization subsystems.
