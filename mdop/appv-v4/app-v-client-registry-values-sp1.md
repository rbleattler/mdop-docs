---
title: App-V Client Registry Values
description: App-V Client Registry Values
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.topic: reference
ms.prod: w10
ms.date: 08/30/2016
---


# App-V Client Registry Values


The Microsoft Application Virtualization (App-V) client stores its configuration in the registry. You can gather some useful information about the client if you understand the format of data in the registry. You can also configure many client actions by changing registry entries. This article lists all the Application Virtualization (App-V) client registry keys and explains their uses.

> [!IMPORTANT]
> On a computer running a 64-bit operating system, the keys and values described in the following sections will be under `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\SoftGrid\4.5\Client`.



## Configuration Key

The following sections provide information about the registry values associated with the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Configuration` key.

### ProductName

Type: String

Example data: Microsoft Application Virtualization Desktop Client

Don't modify.

### Version

Type: String

Example data: 4.5.0.xxx

Don't modify.

### Drivers

Type: String

Example data: Sftfs.sys

If this key value is present, it contains the name of the driver that caused a stop error the last time the core was starting. After you have fixed the stop error, you must delete this key value so that sftlist can start.

### InstallPath

Type: String

Example data: Default=C:\Program Files\Microsoft Application Virtualization Client

The location where the client is installed. Don't modify.

### LogFileName

Type: String

Example data: Default=CSIDL_COMMON_APPDATA\Microsoft\Application Virtualization Client\sftlog.txt

The path and name for the client log file.

> [!NOTE]
> If you're running an earlier version than App-V 4.6, SP1 and you modify the log file name or location, you must restart the sftlist service for the change to take effect.

### LogMinSeverity

Type: DWORD

Example data: Default=4, Informational

| Value   | Description       |
| ------- | ----------------- |
| 0x0     | None              |
| 0x1     | Critical          |
| 0x2     | Error             |
| 0x3     | Warning           |
| 0x4     | Information (Default) |
| 0x5     | Verbose           |

The log level is configurable from the Application Virtualization (App-V) client console and from the command prompt. At a command prompt, the command `sftlist.exe /verboselog` increases the log level to verbose.

### LogRolloverCount

Type: DWORD

Example data: Default=4

Defines the number of backup copies of the log file that are kept when it's reset. The valid range is 0-9999. The default is 4. A value of 0 means no copies will be kept.

### LogMaxSize

Type: DWORD

Example data: Default=256

Defines the maximum size in megabytes (MB) that the log file can grow before being reset. The default size is 256 MB. When this size is reached, a log reset will be forced on the next write attempt.

### SystemEventLogLevel

Type: DWORD

Example data: Default=0x4 (App-V 4.5)

Indicates the logging level at which log messages are written to the NT event log. The value indicates a threshold of what's logged. That is, everything equal to or less than that value is logged. For example, a value of 0x3 (Warning) indicates that Warnings (0x3), Errors (0x2), and Critical Errors (0x1) are logged.

| Value   | Description       |
| ------- | ----------------- |
| 0x0     | None              |
| 0x1     | Critical          |
| 0x2     | Error             |
| 0x3     | Warning           |
| 0x4     | Information (Default) |
| 0x5     | Verbose           |

### AllowIndependentFileStreaming

Type: DWORD

Example data: Default=0

Indicates whether streaming from file will be enabled regardless of how the client has been configured with the `APPLICATIONSOURCEROOT` parameter. If set to FALSE, the transport won't enable streaming from files even if the OSD HREF or the `APPLICATIONSOURCEROOT` parameter contains a file path. 

| Value   | Description       |
| ------- | ----------------- |
| 0x0     | False (default) |
| 0x1     | True          |

### ApplicationSourceRoot

Type: String

Example data:

- `rtsps://mainserver:322/prodapps`
- `file://\uncserver\share\prodapps`
- `file://\uncserver\share`

Enables an administrator or electronic software distribution (ESD) system to ensure application loading is performed according to the topology management scheme. Use this key value to override the OSD CODEBASE for the HREF element (for example, the source location) for an application. Application Source Root supports URLs and Universal Naming Convention (UNC) path formats.

The correct format for the URL path is protocol://servername:[port][/path][/], where port and path are optional. If a port isn't specified, the default port for the protocol is used. Only the protocol://server:port portion of the OSD URL is replaced.

The correct format for the UNC path is \computername\sharefolder[folder][], where folder is optional. The computer name can be a fully qualified domain name (FQDN) or an IP address, and sharefolder can be a drive letter. Only the \computername\sharefolder or drive letter portion of the OSD path is replaced.

### OSDSourceRoot

Type: String

Example data:

- `\computername\sharefolder\resource`
- `\computername\content`
- `C:\foldername`
- `https://computername/productivity/`

Specify a source location for OSD file retrieval for a sequenced application package during publication. Acceptable formats for the OSDSourceRoot include UNC paths and URLs.

### IconSourceRoot

Type: String

- `\computername\sharefolder\resource`
- `\computername\content`
- `C:\foldername`
- `https://computername/productivity/`

Specify a source location for icon file retrieval for a sequenced application package during publication. Acceptable formats for the IconSourceRoot include UNC paths and URLs.

### AutoLoadTriggers

Type: DWORD

Example data: 5

AutoLoad is a client runtime policy configuration parameter that enables the secondary feature block of a virtualized application to be streamed to the client automatically in the background. The AutoLoad triggers are flags to indicate events that initiate auto-loading of applications. AutoLoad implicitly uses background streaming to enable the application to be fully loaded into cache. The primary feature block is loaded first, and the remaining feature blocks are loaded in the background to enable foreground operations, such as user interaction with applications, to take place and provide optimal perceived performance.

| Bit mask value | Name | Description |
|--|--|--|
| 0 | Never | No bits are set (value is 0), no auto loading is performed, because there are no triggers set. |
| 1 | OnLaunch | Loading starts when a user starts an application. |
| 2 | OnRefresh | Loading starts when the application is published. This occurs whenever the package record is added or updated—for example, when a publishing refresh occurs. |
| 4 | OnLogin | Loading starts when a user logs in. |
| 5 | OnLaunch and OnLogin | Default. |

### AutoLoadTarget

Type: DWORD

Example data: 1

Indicates what will be auto-loaded when any given AutoLoad triggers occur.

| Bit mask value | Name | Description |
|--|--|--|
| 0 | None | No auto-loading, regardless of what triggers may be set. |
| 1 | PreviouslyUsed (default) | If any AutoLoad trigger is enabled, load only the packages where at least one application in the package has been previously used—that is, started or precached. |
| 2 | All | If any AutoLoad trigger is enabled, all applications in the package (per package) or all packages (set for client) will be automatically loaded, whether or not they have ever been started. |

### RequireAuthorizationIfCached

Type: DWORD

Example data: 1

Indicates that authorization is always required, whether or not an application is already in cache.

Possible values:

- 0=False: Always try to connect to the server. If a connection to the server can't be established, the client still allows the user to launch an application that has previously been loaded into cache.
- 1=True (default): Application always must be authorized at startup. For RTSP streamed applications, the user authorization token is sent to the server for authorization. For file-based applications, file ACLs control whether a user may access the application.

Restart the sftlist service for the change to take effect.

### UserDataDirectory

Type: String

Example data: `%APPDATA%`

Location where the icon cache and user settings are stored.

### GlobalDataDirectory

Type: String

Example data: `C:\Users\Public\Documents`

Directory to use for global App-V data, including caches for OSD files, icon files, shortcut information, and SystemGuard resources such as .ini files.

### AllowCrashes

Type: DWORD

Example data: 0

Default=0: A value of 0 means that the client tries to catch internal program exceptions so that other user applications can recover and continue when a crash happens. A value of 1 means that the client allows the internal program exceptions to occur so that they can be captured in a debugger.

### CoreInternalTimeout

Type: DWORD

Example data: 60

Time-out in seconds for internal IPC requests between core and front-end. Don't modify.

### DefaultSuiteCombineTime

Type: DWORD

Example data: 10

This value is used to indicate how soon after being started that a program can shut down and not generate any error messages when another application in the same suite is running.

### SerializedSuiteLaunchTimeout

Type: DWORD

Example value: 60000 (Default)

Defines how long in milliseconds the client waits as it tries to serialize program starts in the same suite. If the client times out, the program start continues but it will not be serialized.

### ScriptTimeout

Type: DWORD

Example data: `300`

Default time-out in seconds for scripts in OSD file if WAIT=TRUE. You can specify per-script time-outs with TIMEOUT instead of WAIT. A value of 0 means no wait, and `0xFFFFFFFF` means wait forever.

### LaunchRecordLogPath

Type: String

If, under either HKLM or HKCU, this value contains a valid path to a log file, SFTTray will write to this log when programs start, shut down, fail to launch, and enter or exit disconnected mode.

### LaunchRecordMask

Type: DWORD

| Value | Decimal | Description                                     |
| ----- | ------- | ----------------------------------------------- |
| `0x1A`  | `26`      | Log launch errors and disconnected mode entry and exit activity |
| `0x1F`  | `31`      | Logs everything                                |
| `0x0`   | `0`       | Logs nothing                                   |

Specifies which of the five events are logged (bitmask values):

| Value | Description                                        |
| ----- | -------------------------------------------------- |
| `1`     | Program starts                                     |
| `2`     | Launch failure errors                              |
| `4`     | Shutdowns                                          |
| `8`     | Entering disconnected mode                        |
| `16`    | Exiting disconnected mode to reconnect to a server |

Add any combination of those numbers to turn on the respective messages. If not in registry, defaults to 0x1F.

### LaunchRecordWriteTimeout

Type: DWORD

Example data: Default=3000

Specifies in milliseconds how long the tray waits when trying to write to the launch record log if another process is using it.

### ImportSearchPath

Type: String

Example data: `d:\files;C:\documents and settings\user1\SFTs`

A semicolon delimited list of up to five directories to search for portable SFT files before prompting the user to select a directory. Trailing backslash in paths is optional. This value isn't present by default and must be set manually.

### UserImportPath

Type: String

Example data: `D:\SFTs\`

Valid only under HKCU. The last location the user browsed to while finding a SFT file for package import. Set automatically if the SFT is found successfully. This is used on successive imports when trying to automatically locate SFT files.

## Shared key


The `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Shared` key controls values that are shared across App-V components. The following table provides information about the registry values associated with the Shared key.

| Name | Type | Data (Examples) | Description |
|--|--|--|--|
| DumpPath | String | Default=C:\ | Default path to create dump files when generating a minidump on an exception. This defaults to C:\ if not specified. The Client installer sets this key to the `<App Virtualization global data directory>\Dumps`. The Sequencer installer sets this key to the installation directory. |
| DumpPathSizeLimit | DWORD | 1000 | Specifies the maximum total amount of disk space in megabytes that can be used to store minidumps. Default = 1000 MB. |

## Network key

The `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Network` key controls various network-related parameters. This key is primarily used by the network transport agent. The following table provides information about the registry values associated with the Network key.

| Name | Type | Data (Examples) | Description |
|--|--|--|--|
| Online | DWORD | Default=1 | Enables or disables offline mode. If set to 0, the client won't communicate with App-V Management Servers or publishing servers. In disconnected operations, the client can start a loaded application even when it isn't connected to an App-V Management Server. In offline mode, the client doesn't attempt to connect to an App-V Management Server or publishing server. You must allow disconnected operations to be able to work offline. Default value is 1 enabled (online), and 0 is disabled (offline). |
| AllowDisconnectedOperation | DWORD | Default=1 | Enables or disables disconnected operation. Default value is 1 enabled, and 0 is disabled. When disconnected operations are enabled, the App-V client can start a loaded application even when it isn't connected to an App-V Management Server. |
| FastConnectTimeout | DWORD | Default=1000 | This value specifies the TCP connect time-out in milliseconds to determine when to go into disconnected operations mode. This value can be used to override the default ConnectTimeout of 20 seconds (App-V connect time-out for network transactions) or the system's TCP time-out of approximately 25 seconds. This brings the client into disconnected operations mode quickly. Applied on the next connect. |
| LimitDisconnectedOperation | DWORD | Default=1 | Applicable only if AllowDisconnectedOperation is 1, enabled. This value determines whether there will be a time limit for how long the client will be allowed to operate in disconnected operations. 1=limited. 0=unlimited. |
| DOTimeoutMinutes | DWORD | Default=129,600 | Indicates how many minutes an application may be used in disconnected operation mode. The valid values are 1-999,999 in days expressed in minutes (1-1,439,998,560 minutes). The default value is 90 days or 129,600 minutes. |
| Protocol | DWORD | Default=8 | Default protocol to use (TCP vs SSL). Configure in Options Dialog. |
| ReadTimeout | DWORD | 20 | Read time-out for network transactions, in seconds. Don't modify. |
| WriteTimeout | DWORD | 20 | Write time-out for network transactions, in seconds. Don't modify. |
| ConnectTimeout | DWORD | 20 | Connect time-out for network transactions, in seconds. Don't modify. |
| ReestablishmentRetries | DWORD | 3 | The number of times to try to reestablish a dropped session. |
| ReestablishmentInterval | DWORD | 15 | The number of seconds to wait between tries to reestablish a dropped session. |

## HTTP key

The `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Network\Http` key controls the parameters that are related to HTTP streaming. This key is used primarily by the network transport agent.

### LaunchIfNotFound

Type: DWORD

Example data: Default=0

Controls the behavior of HTTP streaming when a connection to the HTTP server can be established and the package file no longer exists on the HTTP server. If the value doesn't exist or if it's not set to 1, the App-V client doesn't let you launch an application that has previously been loaded into cache.

If this value is set to 1, the App-V client lets you launch an application that has previously been loaded into cache.

## File system key

The values under the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\AppFS` key control the file system parameters for App-V. The following table provides information about the registry values associated with the AppFS key.

| Name | Type | Data (Examples) | Description |
|--|--|--|--|
| FileSize | DWORD | 4096 | Maximum size in megabytes of file system cache file. If you change this value in the registry, you must set State to 0 and reboot. |
| FileName | String | C:\Users\Public\Documents\SoftGrid Client\sftfs.fsd | Location of file system cache file. If you change this value in the registry, you must either leave FileSize the same and reboot or set State to 0 and reboot. |
| DriveLetter | String | Q: | Drive where App-V file system is mounted, if it's available. This value is set either by the listener or the installer, and it's read by the file system. |
| State | DWORD | 0x100 | State of file system. Set to 0 and reboot to completely clear the file system cache. |
| FileSystemStorage | String | C:\Profiles\Joe\SG | Path for symlinks, set under HKCU. Don't modify (use data directory under Configuration to change). |
| GlobalFileSystemStorage | String | C:\Users\Public\Documents\SoftGrid Client\AppFS Storage | Path for global file system data. Don't modify. |
| MaxPercentToLockInCache | DWORD | Default=90 | Specifies the maximum percentage of the file system cache file that can be locked. Don't modify. |
| UnloadLeastRecentlyUsed | DWORD | Default=1 | The file system cache space management feature uses a Least Recently Used (LRU) algorithm and is enabled by default. If the space that is required for a new package would exceed the available free space in the cache, the App-V Client uses this feature to determine which, if any, existing packages it can delete from the cache to make room for the new package. The client deletes the package with the oldest last-accessed date if it's older than the value specified in the MinPkgAge registry value. Values are 0 (disabled) and 1 (default, enabled). |
| MinPackageAge | DWORD | 1 | To determine when the package can be selected for discard, set this registry value to equal the minimum number of days you want to elapse since the package was last accessed. Packages that have been used more recently aren't discarded. |

## Permissions key

To help to prevent users from making mistakes, you can use the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Permissions` key to control access to some actions for non-administrative users—for example, to prevent users from accidentally unloading programs. Users with administrative rights can give themselves any of these permissions. On shared systems, such as a Remote Desktop Session Host (RD Session Host) server (formerly Terminal Server) system, be careful when granting more permissions to users because some of these permissions would enable users to control the applications used by all users on the system. Possible values for these settings are 1 (allow) and 0 (disallow).

The Permissions key settings control all interfaces that enable the named actions. This includes the Options Dialog, SFTTray, and SFTMime. These settings don't affect administrators. The following sections provide information about the registry values associated with the Permissions key.

### ChangeFSDrive

Type: DWORD

Example data: Default=0

A value of 1 allows users to pick a different drive letter to be used as the file system drive.

### ChangeCacheSize

Type: DWORD

Example data: Default=0

A value of 1 allows users to change the cache size.

### ChangeLogSettings

Type: DWORD

Example data: Default=0

A value of 1 allows users to modify the log level, change its location, and reset it through the user interface.

### AddApp

Type: DWORD

Example data: Default=0

A value of 1 allows users to add applications explicitly. This doesn't affect applications that are added through publishing refresh nor does it prevent users from starting (and thereby implicitly adding) applications that haven't already been added. Values are 0 or 1.

### LoadApp

Type: DWORD

- 0: Doesn't allow a user to load an application. This is the default for RD Session Hosts. If you're a mobile user, you might want to fully load your applications in the cache to use them during disconnected operation or offline mode. To stream applications from the App-V Management Server or the App-V Streaming Server, you must be connected to a server to load applications.

- 1: Allows a user to load an application. This is the default for Windows desktops.

### UnloadApp

Type: DWORD

- 0: Doesn't allow a user to unload an application. When you load or unload a package, all the applications in the package are loaded into or removed from cache.

- 1: Allows a user to unload an application.

### LockApp

Type: DWORD

- 0: Doesn't allow a user to lock and unlock an application. This is the default for RD Session Hosts. A locked application can't be removed from the cache to make room for new applications. To remove a locked application from the App-V Desktop or Client for Remote Desktop Services (formerly Terminal Services) cache, you must unlock it.

- 1: Allows a user to lock and unlock an application. This is the default for Windows Desktops.

### ManageTypes

Type: DWORD

- 0: Doesn't allow a user to add, edit, or remove file type associations for that User alone. This is the default for RD Session Hosts.

- 1: Allows a user to add, edit, and remove file type associations for that user only and not globally. This is the default for Windows Desktops.

### RefreshServer

Type: DWORD

- 0: Doesn't allow a user to trigger a refresh of MIME settings. This is the default for RD Session Hosts.

- 1: Enables a user to trigger a refresh of MIME settings. This is the default for Windows Desktops.

### UpdateOSDFile

Type: DWORD

Example data: Default= 0

A value of 1 enables a user to use a modified OSD file.

### ImportApp

Type: DWORD

- 0: Doesn't allow a user to import applications into cache. The difference between Load and Import is that when a Load is triggered, the client gets the package from the currently configured location contained in the OSD, ASR, or Override URL. When using Import, a location to get the package from must be specified. 

- 1: Allows a user to import applications into cache.

### ChangeRefreshSettings

Type: DWORD

Example data: Default=0

A value of 1 allows users to modify the refresh settings for servers (refresh on sign-in and periodic refresh). This doesn't imply that the user can modify other server settings (path, host, and so on).

### ManageServers

Type: DWORD

Example data: Default=0

A value of 1 allows the user to add, edit, and remove servers, except for editing the refresh settings, which is controlled by the ChangeRefreshSettings permission.

### PublishShortcut

Type: DWORD

Example data: Default=0

A value of 1 allows users to publish shortcuts through the user interface. This doesn't affect shortcuts that are published during a publishing refresh.

### ViewAllApplications

Type: DWORD

Example data: Default=0

A value of 1 displays all applications through the user interface; otherwise, only the user's applications are displayed.

### RepairApp

Type: DWORD

Example data: Default=1

A value of 1 allows the user to use the Repair action on applications in SFTMime or the Client Management Console. When you repair an application, you remove any custom user settings and restore the default settings. This action doesn't change or delete shortcuts or file type associations, and it doesn't remove the application from cache.

### ClearApp

Type: DWORD

Example data: Default=1

A value of 1 allows the user to use the Clear action on applications in SFTMime or the Client Management Console. When you clear an application from the console, you can no longer use that application. However, the application remains in cache and is still available to other users on the same system. After a publishing refresh, the cleared applications will again become available to you.

### DeleteApp

Type: DWORD

Example data: Default=0

A value of 1 allows the user to use the Delete action on applications in SFTMime or the Client Management Console. When you delete an application, the selected application will no longer be available to any users on that client. Shortcuts and file type associations are deleted and the application is deleted from cache. However, if another application refers to data in the file system cache or settings data for the selected application, these items won't be deleted.

After a publishing refresh, the deleted applications will again become available to you.

### ToggleOfflineMode

Type: DWORD

A value of 1 allows the users to select to run the client in Offline Mode. In Offline Mode, the Application Virtualization client can start a loaded application even when it isn't connected to an Application Virtualization Server.

## Custom settings key

The `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\CustomSettings` key contains values specific to front-end components. All custom settings are stored as strings. The following table provides information about the registry values associated with the CustomSettings key.

| Name | Type | Data (Examples) | Description |
|--|--|--|--|
| TrayErrorDelay | DWORD | Default=30 | Time in seconds that the Application Virtualization notification area displays error messages like "Launch failed". Minimum value of 1. |
| TraySuccessDelay | DWORD | Default=10 | Time in seconds that the appvmed notification area displays success messages like "Word launched" or "Excel shut down". If 0, those messages are suppressed. |
| TrayVisibility | DWORD | Default=0 | 0=Show Tray when virtualized applications are in use.<br>1=Show Tray always.<br>2=Never show Tray. |
| TrayShowRefresh | DWORD |  | When present and set to a value of 1, allows menu item Refresh Applications to be displayed on the Tray menu and is accessible by the user. |
| TrayShowLoad | DWORD |  | When present and set to a value of 1, allows menu item Load Applications to be displayed on the Tray menu and is accessible by the user. |

## Reporting settings key

The `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SoftGrid\4.5\Client\Reporting` key contains values specific to reporting to an App-V Management Server. The following table provides information about the registry values associated with the Reporting key.

| Name | Type | Data (Examples) | Description |
|--|--|--|--|
| DataCacheLimit | DWORD | Default=20 | This value specifies the maximum size in megabytes (MB) of the XML cache for storing reporting information. The size applies to the cache in memory. When the limit is reached, the log file rolls over. When a new record is added (bottom of the list), one or more of the oldest records (top of the list) will be deleted to make room. A warning will be logged to the Client log and the event log the first time this occurs, and it will not be logged again until after the cache has been successfully cleared on transmission and the log has filled up again. |
| DataBlockSize | DWORD | Default=65536 | This value specifies the maximum size in bytes to transmit to the server at once on publishing refresh, to avoid permanent transmission failures when the log has reached a significant size. The default value is 65536. When transmitting report data to the server, one block of application records—less than or equal to the block size in bytes of XML data—will be removed from the cache and sent to the server. Each block has the general Client data and global package list data prepended, and these won't factor into the block size calculations; the potential exists for an large package list to result in transmission failures over low bandwidth or unreliable connections. |

## Related information

[Application Virtualization Client Reference](application-virtualization-client-reference.md)
