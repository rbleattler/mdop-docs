---
title: About App-V 5.1
description: Use this article to review information about significant changes that apply to Application Virtualization (App-V) 5.1.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---


# About App-V 5.1

Use this article to review information about significant changes that apply to Application Virtualization (App-V) 5.1.

## <a href="" id="bkmk-51-prereq-configs"></a>App-V 5.1 software prerequisites and supported configurations

See the following links for the App-V 5.1 software prerequisites and supported configurations.

- [App-V 5.1 Prerequisites](app-v-51-prerequisites.md): Prerequisite software that you must install before starting the App-V 5.1 installation.
- [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md): Supported operating systems and hardware requirements for the App-V Server, Sequencer, and Client components.

App-V 5.1 supports System Center 2012 R2 Configuration Manager SP1. for information about integrating your App-V environment with Configuration Manager, see [Planning for App-V Integration with Configuration Manager](/previous-versions/system-center/system-center-2012-R2/jj822982(v=technet.10)).

## <a href="" id="bkmk-migrate-to-51"></a>Migrating to App-V 5.1

Use the following information to upgrade to App-V 5.1 from earlier versions. For more information, see [Migrating to App-V 5.1 from a Previous Version](migrating-to-app-v-51-from-a-previous-version.md).

### Before you start the upgrade

Review the following information before you start the upgrade:

| Items to review before upgrading | Description |
|--|--|
| Components to upgrade, in any order | - App-V Server <br> - Sequencer <br> - App-V Client or App-V Remote Desktop Services (RDS) Client <br> **Note:** Prior to App-V 5.0 SP2, the Client Management User Interface (UI) was provided with the App-V Client installation.|
| Upgrading from App-V 4.x | You must first upgrade to App-V 5.0. You cannot upgrade directly from App-V 4.x to App-V 5.1. For more information, see: <br> - "Differences between App-V 4.6 and App-V 5.0" in [About App-V 5.0](about-app-v-50.md) <br> - [Planning for Migrating from a Previous Version of App-V](planning-for-migrating-from-a-previous-version-of-app-v.md) |
| Upgrading from App-V 5.0 or later | You can upgrade to App-V 5.1 directly from any of the following versions: <br> - App-V 5.0 <br> - App-V 5.0 SP1 <br> - App-V 5.0 SP2 <br> - App-V 5.0 SP3 <br> To upgrade to App-V 5.1, follow the steps in the remaining sections of this topic. <br> Packages and connection groups will continue to work with App-V 5.1 as they currently do. |

### <a href="" id="bkmk-steps-upgrd-infrastruc"></a>Steps to upgrade the App-V infrastructure

Complete the following steps to upgrade each component of the App-V infrastructure to App-V 5.1. The following order is only a suggestion; you may upgrade components in any order.

#### Step 1: Upgrade the App-V Server

> [!NOTE]
> If you aren't using the App-V Server, skip this step and go to the next step.

1. Do one of the following actions, depending on the method you are using to upgrade the Management database and/or Reporting database:

    - Windows Installer: Skip this step and go to step 2, "If you are upgrading the App-V Server..."

    - SQL scripts: Follow the steps in [How to Deploy the App-V Databases by Using SQL Scripts](how-to-deploy-the-app-v-databases-by-using-sql-scripts51.md)

1. If you're upgrading the App-V Server from App-V 5.0 SP1 Hotfix Package 3 or later, complete the steps in section [Check registry keys before installing App-V 5.x Server](check-reg-key-svr.md).

1. Follow the steps in [How to deploy the App-V 5.1 server](how-to-deploy-the-app-v-51-server.md)

#### Step 2: Upgrade the App-V Sequencer

For more information, see [Learn to Install the Sequencer](how-to-install-the-sequencer-51beta-gb18030.md).

#### Step 3: Upgrade the App-V Client or App-V RDS Client

For more information, see [How to deploy the App-V client](how-to-deploy-the-app-v-client-51gb18030.md).

### Converting packages created using a prior version of App-V

Use the package converter utility to upgrade virtual application packages created using versions of App-V prior to App-V 5.0. The package converter uses PowerShell to convert packages and can help automate the process if you have many packages that require conversion.

> [!NOTE]
> App-V 5.1 packages are exactly the same as App-V 5.0 packages. There has been no change in the package format between the versions and so there is no need to convert App-V 5.0 packages to App-V 5.1 packages.

## <a href="" id="bkmk-whatsnew"></a>What's New in App-V 5.1

These sections are for users who are already familiar with App-V and want to know what has changed in App-V 5.1. If you are not already familiar with App-V, you should start with the [App-V 5.1 planning checklist](app-v-51-planning-checklist.md).

### <a href="" id="bkmk-win10support"></a>App-V support for Windows 10

The following table lists the Windows 10 support for App-V. Windows 10 is not supported in versions of App-V prior to App-V 5.1.

| Component         | App-V 5.1 | App-V 5.0 |
|-------------------|-----------|-----------|
| App-V Client      | Yes       | No        |
| App-V RDS Client  | Yes       | No        |
| App-V Sequencer   | Yes       | No        |

### <a href="" id="bkmk-mgmtconsole"></a>App-V Management Console Changes

This section compares the App-V Management Console's current and previous functionality.

### Silverlight is no longer required

The Management Console UI no longer requires Silverlight. The 5.1 Management Console is built on HTML5 and Javascript.

### Notifications and messages are displayed individually in a dialog box

### App-V Management Console Changes

This section compares the App-V Management Console's current and previous functionality.

### Silverlight is no longer required

The Management Console UI no longer requires Silverlight. The 5.1 Management Console is built on HTML5 and Javascript.

### Notifications and messages are displayed individually in a dialog box

| New in App-V 5.1 | Prior to App-V 5.1 |
|--|--|
| **Number of messages indicator:** On the title bar of the App-V Management Console, a number is now displayed next to a flag icon to indicate the number of messages that are waiting to be read. | You could see only one message or error at a time, and you were unable to determine how many messages there were. |
| **Message appearance:** <ul><li>Messages that require user input appear in a separate dialog box that displays on top of the current page that you were viewing, and require a response before you can dismiss them.</li><li>Messages and errors appear in a list, with one beneath the other.</li></ul> | You could see only one message or error at a time. |
| **Dismissing messages:** Use the **Dismiss All** link to dismiss all messages and errors at one time, or dismiss them one at a time. | You could dismiss messages and errors only one at a time. |

### Console pages are now separate URLs

| New in App-V 5.1 | Prior to App-V 5.1 |
|--|--|
| Each page in the console has a different URL, which enables you to bookmark specific pages for quick access in the future. The number that appears in some URLs indicates the specific package. These numbers are unique. | All console pages are accessed through the same URL. |

### New, separate CONNECTION GROUPS page and menu option

| New in App-V 5.1 | Prior to App-V 5.1 |
|--|--|
| The CONNECTION GROUPS page is now part of the main menu, at the same level as the PACKAGES page. | To open the CONNECTION GROUPS page, you navigate through the PACKAGES page. |

### Menu options for packages have changed

| New in App-V 5.1 | Prior to App-V 5.1 |
|--|--|
| The following options are now buttons that appear at the bottom of the PACKAGES page: <ul><li>Add or Upgrade</li><li>Publish</li><li>Unpublish</li><li>Delete</li></ul> The following options will still appear when you right-click a package to open the drop-down context menu: <ul><li>Publish</li><li>Unpublish</li><li>Edit AD Access</li><li>Edit Deployment Config</li><li>Transfer deployment configuration from…</li><li>Transfer access and configuration from…</li><li>Delete</li></ul> When you click **Delete** to remove a package, a dialog box opens and asks you to confirm that you want to delete the package. | The **Add or Upgrade** option was a button at the top right of the PACKAGES page. The **Publish**, **Unpublish**, and **Delete** options were available only if you right-clicked a package name in the packages list. |
| The following package operations are now buttons on the package details page for each package: <ul><li>Transfer (drop-down menu with the following options): <ul><li>Transfer deployment configuration from…</li><li>Transfer access and configuration from…</li></ul></li><li>Edit (connection groups and AD Access)</li><li>Unpublish</li><li>Delete</li><li>Edit Default Configuration</li></ul> | These package options were available only if you right-clicked a package name in the packages list. |

### Icons in left pane have new colors and text

The colors of the icons in the left pane have been changed, and text added, to make the icons consistent with other Microsoft products.

### Overview page has been removed

In the left pane of the Management Console, the OVERVIEW menu option and its associated OVERVIEW page have been removed.

### <a href="" id="bkmk-seqimprove"></a>Sequencer Improvements

The following improvements have been made to the package editor in the App-V 5.1 Sequencer.

### Import and export the manifest file

You can import and export the AppxManifest.xml file. To export the manifest file, select the **Advanced** tab and in the Manifest File box, click **Export...**. You can make changes to the manifest file, such as removing shell extensions or editing file type associations.

After you make your changes, click **Import...** and select the file you edited. After you successfully import it back in, the manifest file is immediately updated within the package editor.

> [!CAUTION]
> When you import the file, your changes are validated against the XML schema. If the file is not valid, you will receive an error. Be aware that it is possible to import a file that is validated against the XML schema, but that might still fail to run for other reasons.

### Addition of Windows 10 to operating systems list

In the Deployment tab, Windows 10 32-bit and Windows 10-64 bit have been added to the list of operating systems for which you can sequence a package. If you select **Any Operating System**, Windows 10 is automatically included among the operating systems that the sequenced package will support.

### Current path displays at bottom of virtual registry editor

In the Virtual Registry tab, the path now displays at the bottom of the virtual registry editor, which enables you to determine the currently selected key. Previously, you had to scroll through the registry tree to find the currently selected key.

### <a href="" id="combined--find-and-replace--dialog-box-and-shortcut-keys-added-in-virtual-registry-editor"></a>Combined "find and replace" dialog box and shortcut keys added in virtual registry editor

In the virtual registry editor, shortcut keys have been added for the Find option (Ctrl+F), and a dialog box that combines the "find" and "replace" tasks has been added to enable you to find and replace values and data. To access this combined dialog box, select a key and do one of the following:

-   Press **Ctrl+H**

-   Right-click a key and select **Replace**.

-   Select **View** &gt; **Virtual Registry** &gt; **Replace**.

Previously, the "Replace" dialog box did not exist, and you had to make changes manually.

### Rename registry keys and package files successfully

You can rename virtual registry keys and files without experiencing Sequencer issues. Previously, the Sequencer stopped working if you tried to rename a key.

### Import and export virtual registry keys

You can import and export virtual registry keys. To import a key, right-click the node under which to import the key, navigate to the key you want to import, and then click **Import**. To export a key, right-click the key and select **Export**.

### Import a directory into the virtual file system

You can import a directory into the VFS. To import a directory, click the **Package Files** tab, and then click **View** &gt; **Virtual File System** &gt; **Import Directory**. If you try to import a directory that contains files that are already in the VFS, the import fails, and an explanatory message is displayed. Prior to App-V 5.1, you could not import directories.

### Import or export a VFS file without having to delete and then add it back to the package

You can import files to or export files from the VFS without having to delete the file and then add it back to the package. For example, you might use this feature to export a change log to a local drive, edit the file using an external editor, and then re-import the file into the VFS.

To export a file, select the **Package Files** tab, right-click the file in the VFS, click **Export**, and choose an export location from which you can make your edits.

To import a file, select the **Package Files** tab and right-click the file that you had exported. Browse to the file that you edited, and then click **Import**. The imported file will overwrite the existing file.

After you import a file, you must save the package by clicking **File** &gt; **Save**.

### Menu for adding a package file has moved

The menu option for adding a package file has been moved. To find the Add option, select the **Package Files** tab, then click **View** &gt; **Virtual File System** &gt; **Add File**. Previously, you right-clicked a folder under the VFS node, and chose **Add File**.

### Virtual registry node expands MACHINE and USER hives by default

When you open the virtual registry, the MACHINE and USER hives are shown below the top-level REGISTRY node. Previously, you had to expand the REGISTRY node to show the hives beneath.

### Enable or disable Browser Helper Objects

You can enable or disable Browser Helper Objects by selecting a new check box, Enable Browser Helper Objects, on the Advanced tab of the Sequencer user interface. If Browser Helper Objects:

-   Exist in the package and are enabled, the check box is selected by default.

-   Exist in the package and are disabled, the check box is clear by default.

-   Exist in the package, with one or more enabled and one or more disabled, the check box is set to indeterminate by default.

-   Do not exist in the package, the check box is disabled.

### <a href="" id="bkmk-pkgconvimprove"></a>Improvements to Package Converter

You can now use the package converter to convert App-V 4.6 packages that contain scripts, and registry information and scripts from source .osd files are now included in package converter output.

For more information including examples, see [Migrating to App-V 5.1 from a Previous Version](migrating-to-app-v-51-from-a-previous-version.md).

### <a href="" id="bkmk-supmultscripts"></a>Support for multiple scripts on a single event trigger

App-V 5.1 supports the use of multiple scripts on a single event trigger for App-V packages, including packages that you are converting from App-V 4.6 to App-V 5.0 or later. To enable the use of multiple scripts, App-V 5.1 uses a script launcher application, named ScriptRunner.exe, which is installed as part of the App-V client installation.

For more information, including a list of event triggers and the context under which scripts can be run, see the Scripts section in [About App-V 5.1 Dynamic Configuration](about-app-v-51-dynamic-configuration.md).

### <a href="" id="bkmk-hardcodepath"></a>Hardcoded path to installation folder is redirected to virtual file system root

When you convert packages from App-V 4.6 to 5.1, the App-V 5.1 package can access the hardcoded drive that you were required to use when you created 4.6 packages. The drive letter will be the drive you selected as the installation drive on the 4.6 sequencing machine. (The default drive letter is Q:\\.)

Previously, the 4.6 root folder was not recognized and could not be accessed by App-V 5.0 packages. App-V 5.1 packages can access hardcoded files by their full path or can programmatically enumerate files under the App-V 4.6 installation root.

**Technical Details:** The App-V 5.1 package converter will save the App-V 4.6 installation root folder and short folder names in the FilesystemMetadata.xml file in the Filesystem element. When the App-V 5.1 client creates the virtual process, it will map requests from the App-V 4.6 installation root to the virtual file system root.

## Related topics

[Release Notes for App-V 5.1](release-notes-for-app-v-51.md)
