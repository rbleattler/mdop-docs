---
title: Planning for folder redirection with App-V 5.1
description: Microsoft Application Virtualization (App-V) 5.1 supports the use of folder redirection, a feature that enables users and administrators to redirect the path of a folder to a new location.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Planning for folder redirection with App-V 5.1

Microsoft Application Virtualization (App-V) 5.1 supports the use of folder redirection, a feature that enables users and administrators to redirect the path of a folder to a new location.

## <a href="" id="bkmk-folder-redir-overview"></a>Overview of folder redirection

Folder redirection enables users to work with files, which are redirected to another folder, as if the files still existed on the local drive.

It allows users and administrators to redirect the path of a folder to a network location. The documents in the folder are available to the user from any computer on the network.

- Folder redirection allows users and administrators to redirect the path of a folder to a network location. The documents in the folder are available to the user from any computer on the network.
- The new location can be a folder on the local computer or a folder on a shared network.
- Folder redirection updates the files immediately, whereas roaming data is typically synchronized when the user signs in or signs out.

For example, the Documents folder is stored by default on the computer's local hard disk. With folder redirection, you can redirect it to a network location. The user can access the documents in the folder from any computer on the network.

For more information, see [Folder redirection overview](/previous-versions/windows/it-pro/windows-server-2003/cc778976(v=ws.10)).

## <a href="" id="bkmk-folder-redir-reqs"></a>Requirements and unsupported scenarios for using folder redirection

### Requirements

To use %AppData% folder redirection, the following configurations are required:

- Have an App-V package that has an AppData virtual file system (VFS) folder.

- Enable folder redirection and redirect users' folders to a shared folder, typically a network folder.

- Roam both or neither of the following areas:

  - Files under %appdata%\Microsoft\AppV\Client\Catalog

  - Registry settings under HKEY_CURRENT_USER\Software\Microsoft\AppV\Client\Packages

    For more information, see [Application publishing and client interaction](application-publishing-and-client-interaction.md#bkmk-clt-inter-roam-reqs).

- Ensure that the following folders are available to each user who logs into the computer that is running the App-V 5.0 SP2 or later client:

  - %AppData% is configured to the desired network location with or without [Offline files](/previous-versions/windows/it-pro/windows-server-2003/cc780552(v=ws.10)) support.

  - %LocalAppData% is configured to the desired local folder.

### Unsupported scenarios

- Configuring %LocalAppData% as a network drive.

- Redirecting the Start menu to a single folder for multiple users.

- If roaming AppData (%AppData%) is redirected to a network share that isn't available, App-V applications fail to launch. The behavior depends on the App-V version:

| App-V version | Scenario description |
|--|--|
| In App-V 5.0 through App-V 5.0 SP2 plus hotfixes | This failure occurs regardless of whether Offline Files is enabled. |
| In App-V 5.0 SP3 and later | If the unavailable network share is enabled for Offline Files, the App-V application starts successfully. |

## <a href="" id="bkmk-folder-redir-cfg"></a>How to configure folder redirection for use with App-V

Folder redirection can be applied to different folders, such as Desktop, My Documents, My Pictures, etc. However, the only folder that impacts the use of App-V applications is the user's roaming AppData folder (%AppData%). You can apply folder redirection to any other supported folders without impacting App-V.

## <a href="" id="bkmk-folder-redir-works"></a>How folder redirection works with App-V

The following table describes how folder redirection works when %AppData% is redirected to a network and the proper requirements are met.

| Virtual environment state | Action that occurs |
|--|--|
| When the virtual environment starts | The virtual file system (VFS) AppData folder is mapped to the local AppData folder (%LocalAppData%) instead of to the user's roaming AppData folder (%AppData%).<br><ul><li>LocalAppData contains a local cache of the user's roaming AppData folder for the package in use. The local cache is located under:<br>`%LocalAppData%\Microsoft\AppV\Client\VFS\PackageGUID\AppData`</li><li>The latest data from the user's roaming AppData folder is copied to and replaces the data currently in the local cache.</li><li>While the virtual environment is running, data continues to be saved to the local cache. Data is served only out of %LocalAppData% and isn't moved or synchronized with %AppData% until the end user shuts down the computer.</li><li>Entries to the AppData folder are made using the user context, not the system context.</li></ul><strong>Note:</strong> The App-V client folder redirection sometimes fails to move files from %AppData% to %LocalAppData%. See [Release Notes for App-V 5.0 SP2](release-notes-for-app-v-50-sp2.md#bkmk-folderredirection). |
| When the virtual environment shuts down | The local cached data in AppData (roaming) is zipped up and copied to the "real" roaming AppData folder in %AppData%. A time stamp, which indicates the last known upload, is simultaneously saved as a registry key under:<br>`HKCU\Software\Microsoft\AppV\Client\Packages\<PACKAGE_GUID>\AppDataTime`<br>To provide redundancy, App-V keeps the three most recent copies of the compressed data under %AppData%. |
