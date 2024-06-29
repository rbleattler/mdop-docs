---
title: About App-V 5.0 SP3
description: About App-V 5.0 SP3
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/02/2016
---

# About App-V 5.0 SP3

Use the following sections to review information about significant changes that apply to Microsoft Application Virtualization (App-V) 5.0 SP3:

- [App-V 5.0 SP3 software prerequisites and supported configurations](#bkmk-sp3-prereq-configs)

- [Migrating to App-V 5.0 SP3](#bkmk-migrate-to-50sp3)

- [Manually created connection group xml file requires update to schema](#bkmk-update-schema-cg)

- [Improvements to connection groups](#bkmk-cg-improvements)

- [Administrators can publish and unpublish packages for a specific user](#bkmk-usersid-pub-pkgs-specf-user)

- [Enable only administrators to publish and unpublish packages](#bkmk-admins-only-pub-unpub-pkgs)

- [RunVirtual registry key supports packages that are published to the user](#bkmk-runvirtual-reg-key)

- [New PowerShell cmdlets and updateable cmdlet help](#bkmk-posh-cmdlets-help)

- [Primary virtual application directory (PVAD) is hidden but can be turned on](#bkmk-pvad-hidden)

- [ClientVersion is required to view App-V publishing metadata](#bkmk-pub-metadata-clientversion)

- [App-V event logs have been consolidated](#bkmk-event-logs-moved)

## <a name="bkmk-sp3-prereq-configs"></a>App-V 5.0 SP3 software prerequisites and supported configurations

For the App-V 5.0 SP3 software prerequisites and supported configurations, see the following articles:

- [App-V 5.0 SP3 Prerequisites](app-v-50-sp3-prerequisites.md): Prerequisite software that you must install before starting the App-V 5.0 SP3 installation.

- [App-V 5.0 SP3 Supported Configurations](app-v-50-sp3-supported-configurations.md): Supported operating systems and hardware requirements for the App-V Server, Sequencer, and Client components.

## <a name="bkmk-migrate-to-50sp3"></a>Migrating to App-V 5.0 SP3

Use the following information to upgrade to App-V 5.0 SP3 from earlier versions.

### Before you start the upgrade

Review the following information before you start the upgrade:

| Items to review before upgrading | Description |
|--|--|
| Components to upgrade | - App-V Server<br/>- Sequencer<br/>- App-V client or App-V Remote Desktop Services (RDS) client<br/>- Connection groups |
| Upgrading from App-V 4.x | You must first upgrade to App-V 5.0. You can't upgrade directly from App-V 4.x to App-V 5.0 SP3.<br/>For more information, see:<br/>- [About App-V 5.0](about-app-v-50.md)<br/>- [Planning for Migrating from a Previous Version of App-V](planning-for-migrating-from-a-previous-version-of-app-v.md) |
| Upgrading from App-V 5.0 or later | You can upgrade to App-V 5.0 SP3 directly from any of the following versions:<br/>- App-V 5.0<br/>- App-V 5.0 SP1<br/>- App-V 5.0 SP2<br/><br/>To upgrade to App-V 5.0 SP3, follow the steps in the remaining sections of this article. |
| Required changes to packages and connection groups after upgrade | None. Packages and connection groups continue to work as they currently do. |

### <a name="bkmk-steps-upgrd-infrastruc"></a>Steps to upgrade the App-V infrastructure

Complete the following steps to upgrade each component of the App-V infrastructure to App-V 5.0 SP3.

#### Step 1: Upgrade the App-V Server

If you aren't using the App-V Server, skip this step and go to the next step.

> [!NOTE]
> The App-V 5.0 SP3 client is compatible with the App-V 5.0 SP1 Server.

Follow these steps:

1. Review the [Release Notes for App-V 5.0 SP3](release-notes-for-app-v-50-sp3.md) for issues that may affect the App-V Server installation.
2. Do one of the following, depending on the method you're using to upgrade the Management database and/or Reporting database:

    - If you're using **Windows Installer** to upgrade the database, skip this step and go to step 3, "If you're upgrading the App-V Server...."

    - If you're using **SQL scripts** to upgrade the database, see [How to Deploy the App-V Databases by Using SQL Scripts](how-to-deploy-the-app-v-databases-by-using-sql-scripts.md).

3. If you're upgrading the App-V Server from App-V 5.0 SP1 Hotfix Package 3 or later, complete the steps in section [Check registry keys after installing the App-V 5.0 SP3 Server](#bkmk-check-reg-key-svr).

4. Follow the steps in [How to Deploy the App-V 5.0 Server](how-to-deploy-the-app-v-50-server-50sp3.md).

#### Step 2: Upgrade the App-V Sequencer

For more information, see [How to Install the Sequencer](how-to-install-the-sequencer-beta-gb18030.md).

#### Step 3: Upgrade the App-V client or App-V RDS client

For more information, see [How to Deploy the App-V Client](how-to-deploy-the-app-v-client-gb18030.md).

### <a name="bkmk-check-reg-key-svr"></a>Check registry keys before installing the App-V 5.0 SP3 Server

| **When this step is required** | You're upgrading from App-V SP1 with any subsequent Hotfix Packages that you installed by using an .msp file. |
|--|--|
| **Which components require that you do this step** | Only the App-V Server components that you're upgrading. |
| **When you need to do this step** | Before you upgrade the App-V Server to App-V 5.0 SP3 |
| **What you need to do** | Using the information in the following tables, update each registry key value under `HKLM\Software\Microsoft\AppV\Server` with the value that you provided in your original server installation. Completing this step restores registry values that may have been removed when App-V SP1 Hotfix Packages were installed. |

#### `ManagementDatabase` key

If you're installing the Management database, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ManagementDatabase`.

| Key name | Description |
|--|--|
| `IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` | Describes whether a public access account is required to access nonlocal management databases. Value is set to `1` if it's required. |
| `MANAGEMENT_DB_NAME` | Name of the Management database. |
| `MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT` | Account used for read (public) access to the Management database. Used when `IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| `MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_SID` | Secure identifier (SID) of the account used for read (public) access to the Management database. Used when `IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| `MANAGEMENT_DB_SQL_INSTANCE` | SQL Server instance for the Management database. If the value is blank, the default database instance is used. |
| `MANAGEMENT_DB_WRITE_ACCESS_ACCOUNT` | Account used for write (administrator) access to the Management database. |
| `MANAGEMENT_DB_WRITE_ACCESS_ACCOUNT_SID` | Secure identifier (SID) of the account used for write (administrator) access to the Management database. |
| `MANAGEMENT_REMOTE_SERVER_MACHINE_ACCOUNT` | Management server remote computer account (domain\account). |
| `MANAGEMENT_SERVER_INSTALL_ADMIN_ACCOUNT` | Installation administrator sign-in for the Management server (domain\account). |
| `MANAGEMENT_SERVER_MACHINE_USE_LOCAL` | Valid values are:<br>- `1`: the Management service is on the local computer, that is, `MANAGEMENT_REMOTE_SERVER_MACHINE_ACCOUNT` is blank.<br>- `0`: the Management service is on a different computer from the local computer. |

#### `ManagementService` key

If you're installing the Management server, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ManagementService`.

| Key name | Description |
|--|--|
| `MANAGEMENT_ADMINACCOUNT` | Active Directory Domain Services (AD DS) group or account that is authorized to manage App-V (domain\account). |
| `MANAGEMENT_DB_SQL_INSTANCE` | SQL server instance that contains the Management database. If the value is blank, the default database instance is used. |
| `MANAGEMENT_DB_SQL_SERVER_NAME` | Name of the remote SQL server with the Management database. If the value is blank, the local computer is used. |

#### `ReportingDatabase` key

If you're installing the Reporting database, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ReportingDatabase`.

| Key name | Description |
|--|--|
| `IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` | Describes whether a public access account is required to access nonlocal reporting databases. Value is set to `1` if it's required. |
| `REPORTING_DB_NAME` | Name of the Reporting database. |
| `REPORTING_DB_PUBLIC_ACCESS_ACCOUNT` | Account used for read (public) access to the Reporting database. Used when `IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| `REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_SID` | Secure identifier (SID) of the account used for read (public) access to the Reporting database. Used when `IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| `REPORTING_DB_SQL_INSTANCE` | SQL Server instance for the Reporting database. If the value is blank, the default database instance is used. |
| `REPORTING_DB_WRITE_ACCESS_ACCOUNT` | Account used for write (administrator) access to the Reporting database. |
| `REPORTING_DB_WRITE_ACCESS_ACCOUNT_SID` | Secure identifier (SID) of the account used for write (administrator) access to the Reporting database. |
| `REPORTING_REMOTE_SERVER_MACHINE_ACCOUNT` | Reporting server remote computer account (domain\account). |
| `REPORTING_SERVER_INSTALL_ADMIN_ACCOUNT` | Installation administrator sign-in for the Reporting server (domain\account). |
| `REPORTING_SERVER_MACHINE_USE_LOCAL` | Valid values are: <br> - `1`: the Reporting service is on the local computer, that is, `REPORTING_REMOTE_SERVER_MACHINE_ACCOUNT` is blank. <br> - `0`: the Reporting service is on a different computer from the local computer. |

#### `ReportingService` key

If you're installing the Reporting server, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ReportingService`.

| Key name | Description |
|--|--|
| `REPORTING_DB_SQL_INSTANCE` | SQL Server instance for the Reporting database. If the value is blank, the default database instance is used. |
| `REPORTING_DB_SQL_SERVER_NAME` | Name of the remote SQL server with the Reporting database. If the value is blank, the local computer is used. |

## <a name="bkmk-update-schema-cg"></a>Manually created connection group xml file requires update to schema

If you're manually creating the connection group XML file, and want to use the new "optional packages" and "use any version" features that are described in [Improvements to connection groups](#bkmk-cg-improvements), you must specify the following schema in the XML file:

`xmlns="http://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"`

For examples and more information, see [About the Connection Group File](about-the-connection-group-file.md).

## <a name="bkmk-cg-improvements"></a>Improvements to connection groups

You can manage connection groups more easily by using optional packages and other improvements that have been added in App-V 5.0 SP3. The following table summarizes the tasks that you can perform by using the new connection group features, and links to more detailed information about each task.

### Enable a connection group to include optional packages

Including optional packages in a connection group enables you to dynamically determine which applications will be included in the connection group's virtual environment, based on the applications that users are entitled to. You don't need to manage as many connection groups because you can mix optional and nonoptional packages in the same connection group. Mixing packages allows different groups of users to use the same connection group, even though users might have only one package in common. For example, you can enable a package with Microsoft Office for all users, but enable different optional packages, which contain different Office plug-ins, to different subsets of users.

For more information, see [How to use optional packages in connection groups](how-to-use-optional-packages-in-connection-groups.md#bkmk-apps-plugs-optional).

### Unpublish or delete an optional package without changing the connection group

Unpublish or delete, or unpublish and republish an optional package, which is in a connection group, without having to disable or re-enable the connection group on the App-V client.

For more information, see [How to use optional packages in connection groups](how-to-use-optional-packages-in-connection-groups.md#bkmk-apps-plugs-optional).

### Publish connection groups that contain user-published and globally published packages

Create a user-published connection group that contains user-published and globally published packages.

For more information, see [How to Create a Connection Group with User-Published and Globally Published Packages](how-to-create-a-connection-group-with-user-published-and-globally-published-packages.md).

### Make a connection group ignore the package version

Configure a connection group to accept any version of a package, which enables you to upgrade a package without having to disable the connection group. In addition, if there's an optional package with an incorrect version in the connection group, the package is ignored and won't block the connection group's virtual environment from being created.

For more information, see [How to make a connection group ignore the package version](how-to-make-a-connection-group-ignore-the-package-version.md).

### Limit end users' publishing capabilities

Enable only administrators (not end users) to publish packages and to enable connection groups.

For more information, see [How to allow only administrators to enable connection groups](how-to-allow-only-administrators-to-enable-connection-groups.md).

For information about packages, see the following articles:

- [How to Publish a Package by Using the Management Console](how-to-publish-a-package-by-using-the-management-console-50.md)

- [How to Manage Connection Groups on a Stand-alone Computer by Using PowerShell](how-to-manage-connection-groups-on-a-stand-alone-computer-by-using-powershell.md#bkmk-admin-only-posh-topic-cg)

- [How to Enable Only Administrators to Publish Packages by Using an ESD](how-to-enable-only-administrators-to-publish-packages-by-using-an-esd.md)

### Enable or disable a connection group for a specific user

Administrators can enable or disable a connection group for a specific user by using the optional `-UserSID` parameter. For more information, see [How to manage connection groups on a stand-alone computer by using PowerShell](how-to-manage-connection-groups-on-a-stand-alone-computer-by-using-powershell.md#bkmk-enable-cg-for-user-poshtopic).

### Merging identical package paths into one virtual directory in connection groups

If two or more packages in a connection group contain identical directory paths, the paths are merged into a single virtual directory inside the connection group virtual environment. This merging of paths allows an application in one package to access files that are in a different package.

For more information, see [About the connection group virtual environment](about-the-connection-group-virtual-environment.md#bkmk-merged-root-ve-exp).

## <a name="bkmk-usersid-pub-pkgs-specf-user"></a>Administrators can publish and unpublish packages for a specific user

Administrators can use the following cmdlets to publish or unpublish packages for a specific user. To use the cmdlets, enter the `-UserSID` parameter, followed by the user's security identifier (SID). For more information, see:

- [How to Manage App-V 5.0 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-50-packages-running-on-a-stand-alone-computer-by-using-powershell.md#bkmk-pub-pkg-a-user-standalone-posh)

- [How to Manage App-V 5.0 Packages Running on a Stand-Alone Computer by Using PowerShell](how-to-manage-app-v-50-packages-running-on-a-stand-alone-computer-by-using-powershell.md#bkmk-unpub-pkg-specfc-use)

For example:

```powershell
Publish-AppvClientPackage "ContosoApplication" -UserSID S-1-2-34-56789012-3456789012-345678901-2345
```

```powershell
Unpublish-AppvClientPackage "ContosoApplication" -UserSID S-1-2-34-56789012-3456789012-345678901-2345
```

## <a name="bkmk-admins-only-pub-unpub-pkgs"></a>Enable only administrators to publish and unpublish packages

You can enable only administrators (not end users) to publish and unpublish packages by using one of the following methods:

- Group policy setting: Navigate to the following group policy object node: **Computer Configuration > Policies > Administrative Templates > System > App-V > Publishing**. Enable the **Require publish as administrator** Group Policy setting.

- PowerShell: For more information, see [How to manage App-V 5.0 packages running on a stand-alone computer by using PowerShell](how-to-manage-app-v-50-packages-running-on-a-stand-alone-computer-by-using-powershell.md#bkmk-admins-pub-pkgs).

## <a name="bkmk-runvirtual-reg-key"></a>`RunVirtual` registry key supports packages that are published to the user

App-V 5.0 SP3 adds support for using the `RunVirtual` registry key with virtualized applications that are in user-published packages. The `RunVirtual` registry key lets you run a locally installed application in a virtual environment, along with applications that have been virtualized by using App-V.

Previously, the virtualized applications in App-V packages had to be published globally. For more information about `RunVirtual` and about other methods of running locally installed applications in a virtual environment with virtualized applications, see [Running a locally installed application inside a virtual environment with virtualized applications](running-a-locally-installed-application-inside-a-virtual-environment-with-virtualized-applications.md).

## <a name="bkmk-posh-cmdlets-help"></a>New PowerShell cmdlets and updateable cmdlet help

New PowerShell cmdlets and updateable cmdlet help are included in App-V 5.0 SP3. To download the cmdlet modules, see [How to load the PowerShell cmdlets and get cmdlet help](how-to-load-the-powershell-cmdlets-and-get-cmdlet-help-50-sp3.md#bkmk-load-cmdlets).

### New App-V 5.0 SP3 Server PowerShell cmdlets

New Windows PowerShell cmdlets for the App-V Server have been added to help you manage connection groups.

- **Add-AppvServerConnectionGroupPackage**: Appends a package to the end of a connection group's package list and enables you to configure the package as optional and/or with no version within the connection group.
- **Set-AppvServerConnectionGroupPackage**: Enables you to edit details about the connection group package, such as whether it's optional.
- **Remove-AppvServerConnectionGroupPackage**: Removes a package from a connection group.

### <a name="bkmk-get-cmdlet-help"></a>Getting help for the PowerShell cmdlets

Cmdlet help is available as a downloadable module. To get the latest help after downloading the cmdlet module, open Windows PowerShell or Windows PowerShell Integrated Scripting Environment (ISE) and run one the following commands:

- App-V Server: `Update-Help-Module AppvServer`
- App-V Sequencer: `Update-Help-Module AppvSequencer`
- App-V client: `Update-Help-Module AppvClient`

For more information, see [How to load the PowerShell cmdlets and get cmdlet help](how-to-load-the-powershell-cmdlets-and-get-cmdlet-help-50-sp3.md).

## <a name="bkmk-pvad-hidden"></a>Primary virtual application directory (PVAD) is hidden but can be turned on

The primary virtual application directory (PVAD) is hidden in App-V 5.0 SP3, but you can turn it back on and make it visible by using one of the following methods.

> [!NOTE]
> **More about PVAD:** When you use the Sequencer to create a package, you can enter any installation path for the package. In past versions of App-V, you were required to specify the primary virtual application directory (PVAD) of the application as the path. PVAD is the directory to which you would typically install an application on your local computer if you weren't using App-V. For example, if you were installing Office on a computer, the PVAD typically would be `C:\Program Files\Microsoft Office\`.

### Use a command line parameter

Pass the `-EnablePVADControl` parameter to the `Sequencer.exe`.

### Create a registry subkey

1. In the Registry Editor, navigate to: `HKLM\SOFTWARE\Microsoft\AppV\Sequencer\Compatibility`. If the `Compatibility` subkey doesn't exist, you must create it.

2. Create a DWORD Value named `EnablePVADControl`, and set the value to `1`. A value of `0` means that PVAD is hidden.

## <a name="bkmk-pub-metadata-clientversion"></a>ClientVersion is required to view App-V publishing metadata

In App-V 5.0 SP3, you must provide the following values in the address when you query the App-V Publishing server for metadata:

| Value | Additional details |
|--|--|
| `ClientVersion` | If you omit the `ClientVersion` parameter from the query, the metadata excludes the new App-V 5.0 SP3 features. |
| `ClientOS` | You have to provide this value only if you select specific client operating systems when you sequence the package. If you select the default (all operating systems), don't specify this value in the query. If you omit the `ClientOS` parameter from the query, only the packages that were sequenced to support any operating system appear in the metadata. |

For syntax and examples of this query, see [Viewing App-V Server Publishing Metadata](viewing-app-v-server-publishing-metadata.md).

## <a name="bkmk-event-logs-moved"></a>App-V event logs have been consolidated

The following event logs, previously located at `Applications and Services Logs/Microsoft/AppV/<App-V component>`, have been moved to `Applications and Services Logs/Microsoft/AppV/ServiceLog`.

To view the logs, select **View** &gt; **Show Analytic and Debug Logs** in the Event Viewer application.

`Client-Catalog Client-Integration Client-Orchestration Client-PackageConfig Client-Scripting Client-Service Client-Vemgr Client-VFSC FilesystemMetadataLibrary ManifestLibrary PolicyLibrary Subsystems-ActiveX Subsystems-AppPath Subsystems-Com Subsystems-fta`

## How to get MDOP

App-V is a part of the Microsoft Desktop Optimization Pack (MDOP). MDOP is part of Microsoft Software Assurance. For more information about Microsoft Software Assurance and acquiring MDOP, see [How to get MDOP](../index.md#how-to-get-mdop).

## Related information

[Release Notes for App-V 5.0 SP3](release-notes-for-app-v-50-sp3.md)
