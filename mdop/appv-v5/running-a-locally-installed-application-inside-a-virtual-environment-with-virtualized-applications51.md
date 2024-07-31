---
title: run a locally installed application inside a virtual environment with virtualized applications
description: You can run a locally installed application in a virtual environment, alongside applications that have been virtualized by using Microsoft Application Virtualization (App-V).
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Run a locally installed application inside a virtual environment with virtualized applications

You can run a locally installed application in a virtual environment, alongside applications that have been virtualized by using Microsoft Application Virtualization (App-V). You might want to do this if you:

- Want to install and run an application locally on client computers, but want to virtualize and run specific plug-ins that work with that local application.

- Are troubleshooting an App-V client package and want to open a local application within the App-V virtual environment.

Use any of the following methods to open a local application inside the App-V virtual environment:

- [RunVirtual registry key](#bkmk-runvirtual-regkey)

- [Get-AppvClientPackage PowerShell cmdlet](#bkmk-get-appvclientpackage-posh)

- [Command line switch /appvpid:&lt;PID&gt;](#bkmk-cl-switch-appvpid)

- [Command line hook switch /appvve:&lt;GUID&gt;](#bkmk-cl-hook-switch-appvve)

Each method accomplishes essentially the same task, but some methods may be better suited for some applications than others, depending on whether the virtualized application is already running.

## <a href="" id="bkmk-runvirtual-regkey"></a>RunVirtual registry key

To add a locally installed application to a package or to a connection group's virtual environment, you add a subkey to the `RunVirtual` registry key in the Registry Editor, as described in the following sections.

There is no Group Policy setting available to manage this registry key, so you have to use System Center Configuration Manager or another electronic software distribution (ESD) system, or manually edit the registry.

### <a href="" id="bkmk-"></a>Supported methods of publishing packages when using RunVirtual

| App-V version                | Supported publishing methods       |
|------------------------------|-------------------------------------|
| App-V 5.0 SP3 and App-V 5.1  | Published globally or to the user  |
| App-V 5.0 through App-V 5.0 SP2 | Published globally only            |

### Steps to create the subkey

1.  Using the information in the following table, create a new registry key using the name of the executable file, for example, **MyApp.exe**.

    | Package publishing method | Where to create the registry key |
    |---------------------------|----------------------------------|
    | Published globally        | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AppV\Client\RunVirtual`<br>**Example**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AppV\Client\RunVirtual\MyApp.exe` |
    | Published to the user     | `HKEY_CURRENT_USER\SOFTWARE\Microsoft\AppV\Client\RunVirtual`<br>**Example**: `HKEY_CURRENT_USER\SOFTWARE\Microsoft\AppV\Client\RunVirtual\MyApp.exe` |
    | Connection group can contain: <ul><li>Packages that are published just globally or just to the user</li><li>Packages that are published globally and to the user</li></ul> | Either HKEY_LOCAL_MACHINE or HKEY_CURRENT_USER key, but all of the following must be true: <ul><li>If you want to include multiple packages in the virtual environment, you must include them in an enabled connection group.</li><li>Create only one subkey for one of the packages in the connection group. If, for example, you have one package that is published globally, and another package that is published to the user, you create a subkey for either of these packages, but not both. Although you create a subkey for only one of the packages, all of the packages in the connection group, plus the local application, will be available in the virtual environment.</li><li>The key under which you create the subkey must match the publishing method you used for the package.<br>For example, if you published the package to the user, you must create the subkey under `HKEY_CURRENT_USER\SOFTWARE\Microsoft\AppV\Client\RunVirtual`.</li></ul> |

2.  Set the new registry subkey's value to the PackageId and VersionId of the package, separating the values with an underscore.

  **Syntax**: &lt;PackageId&gt;\_&lt;VersionId&gt;

  **Example**: 4c909996-afc9-4352-b606-0b74542a09c1\_be463724-Oct1-48f1-8604-c4bd7ca92fa

  The application in the previous example would produce a registry export file (.reg file) like the following:

  ``` syntax
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AppV\Client\RunVirtual]
  @=""
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AppV\Client\RunVirtual\MyApp.exe]
  @="aaaaaaaa-bbbb-cccc-dddd-eeeeeeee_11111111-2222-3333-4444-555555555
  ```

## <a href="" id="bkmk-get-appvclientpackage-posh"></a>Get-AppvClientPackage PowerShell cmdlet

You can use the **Start-AppVVirtualProcess** cmdlet to retrieve the package name and then start a process within the specified package's virtual environment. This method lets you launch any command within the context of an App-V package, regardless of whether the package is currently running.

Use the following example syntax, and substitute the name of your package for **&lt;Package&gt;**:

`$AppVName = Get-AppvClientPackage <Package>`

`Start-AppvVirtualProcess -AppvClientObject $AppVName cmd.exe`

If you don't know the exact name of your package, you can use the command line **Get-AppvClientPackage \*executable\\**<em>, where **executable</em>* is the name of the application, for example: Get-AppvClientPackage \*Word\*.

## <a href="" id="bkmk-cl-switch-appvpid"></a>Command line switch /appvpid:&lt;PID&gt;

You can apply the **/appvpid:&lt;PID&gt;** switch to any command, which enables that command to run within a virtual process that you select by specifying its process ID (PID). Using this method launches the new executable in the same App-V environment as an executable that is already running.

Example: `cmd.exe /appvpid:8108`

To find the process ID (PID) of your App-V process, run the command **tasklist.exe** from an elevated command prompt.

## <a href="" id="bkmk-cl-hook-switch-appvve"></a>Command line hook switch /appvve:&lt;GUID&gt;

This switch lets you run a local command within the virtual environment of an App-V package. Unlike the **/appvid** switch, where the virtual environment must already be running, this switch enables you to start the virtual environment.

Syntax: `cmd.exe /appvve:<PACKAGEGUID_VERSIONGUID>`

Example: `cmd.exe /appvve:aaaaaaaa-bbbb-cccc-dddd-eeeeeeee_11111111-2222-3333-4444-55555555`

To get the package GUID and version GUID of your application, run the **Get-AppvClientPackage** cmdlet. Concatenate the **/appvve** switch with the following:

- A colon

- Package GUID of the desired package

- An underscore

- Version ID of the desired package

If you don't know the exact name of your package, use the command line **Get-AppvClientPackage \*executable\\**<em>, where **executable</em>* is the name of the application, for example: Get-AppvClientPackage \*Word\*.

This method lets you launch any command within the context of an App-V package, regardless of whether the package is currently running.
