---
title: Check registry keys before installing App-V 5.x server
description: If you're upgrading the App-V Server from App-V 5.0 SP1 Hotfix Package 3 or later, complete the steps in this section before installing the App-V 5.x Server.
author: aczechowski
ms.date: 06/16/2016
ms.author: aaroncz
ms.collection: must-keep
ms.topic: reference
---

# Check registry keys before installing App-V 5.x server

If you're upgrading the App-V Server from App-V 5.0 SP1 hotfix package 3 or later, complete the steps in this section before installing the App-V 5.x Server.

| When this step is required | You're upgrading from App-V 5.0 SP1 with any subsequent hotfix packages that you installed by using an .msp file. |
|----------------------------|---------------------------------------------------------------------------------------------------------------------|
| Which components require that you do this step | Only the App-V Server components that you're upgrading. |
| When you need to do this step | Before you upgrade the App-V Server to App-V 5.x |
| What you need to do | Using the information in the following tables, update each registry key value under `HKLM\Software\Microsoft\AppV\Server` with the value that you provided in your original server installation. Completing this step restores registry values that might have been removed when App-V 5.0 SP1 hotfix packages were installed. |

## ManagementDatabase key

If you're installing the management database, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ManagementDatabase`.

| Key name | Description |
|--|--|
| IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED | Describes whether a public access account is required to access nonlocal management databases. If necessary, the value is set to `1`. |
| MANAGEMENT_DB_NAME | Name of the management database. |
| MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT | Account used for read (public) access to the management database. <br> Used when `IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_SID | Secure identifier (SID) of the account used for read (public) access to the management database. <br> Used when `IS_MANAGEMENT_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| MANAGEMENT_DB_SQL_INSTANCE | SQL Server instance for the management database. <br> If the value is blank, the default database instance is used. |
| MANAGEMENT_DB_WRITE_ACCESS_ACCOUNT | Account used for write (administrator) access to the management database. |
| MANAGEMENT_DB_WRITE_ACCESS_ACCOUNT_SID | Secure identifier (SID) of the account used for write (administrator) access to the management database. |
| MANAGEMENT_REMOTE_SERVER_MACHINE_ACCOUNT | Management server remote computer account (domain\account). |
| MANAGEMENT_SERVER_INSTALL_ADMIN_ACCOUNT | Installation administrator sign-in for the management server (domain\account). |
| MANAGEMENT_SERVER_MACHINE_USE_LOCAL | Valid values are: <ul><li>**1** - the management service is on the local computer, that is, MANAGEMENT_REMOTE_SERVER_MACHINE_ACCOUNT is blank.</li><li>**0** - the management service is on a different computer from the local computer.</li></ul> |

## ManagementService key

If you're installing the management server, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ManagementService`.

| Key name | Description |
|--|--|
| MANAGEMENT_ADMINACCOUNT | Active Directory Domain Services group or account that is authorized to manage App-V (domain\account). |
| MANAGEMENT_DB_SQL_INSTANCE | SQL server instance that contains the management database. <br> If the value is blank, the default database instance is used. |
| MANAGEMENT_DB_SQL_SERVER_NAME | Name of the remote SQL server with the management database. <br> If the value is blank, the local computer is used. |

## ReportingDatabase key

If you're installing the reporting database, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ReportingDatabase`.

| Key name | Description |
|--|--|
| IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED | Describes whether a public access account is required to access nonlocal reporting databases. If necessary, the value is set to `1`. |
| REPORTING_DB_NAME | Name of the reporting database. |
| REPORTING_DB_PUBLIC_ACCESS_ACCOUNT | Account used for read (public) access to the reporting database. <br> Used when `IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_SID | Secure identifier (SID) of the account used for read (public) access to the reporting database. <br> Used when `IS_REPORTING_DB_PUBLIC_ACCESS_ACCOUNT_REQUIRED` is set to `1`. |
| REPORTING_DB_SQL_INSTANCE | SQL Server instance for the reporting database. <br> If the value is blank, the default database instance is used. |
| REPORTING_DB_WRITE_ACCESS_ACCOUNT | Account used for write (administrator) access to the reporting database. |
| REPORTING_DB_WRITE_ACCESS_ACCOUNT_SID | Secure identifier (SID) of the account used for write (administrator) access to the reporting database. |
| REPORTING_REMOTE_SERVER_MACHINE_ACCOUNT | Reporting server remote computer account (domain\account). |
| REPORTING_SERVER_INSTALL_ADMIN_ACCOUNT | Installation administrator sign-in for the reporting server (domain\account). |
| REPORTING_SERVER_MACHINE_USE_LOCAL | Valid values are: <ul><li>**1** - the reporting service is on the local computer, that is, REPORTING_REMOTE_SERVER_MACHINE_ACCOUNT is blank.</li><li>**0** - the reporting service is on a different computer from the local computer.</li></ul> |

## ReportingService key

If you're installing the reporting server, set these registry keys under `HKLM\Software\Microsoft\AppV\Server\ReportingService`.

| Key name | Description |
|--|--|
| REPORTING_DB_SQL_INSTANCE | SQL Server instance for the reporting database. <br> If the value is blank, the default database instance is used. |
| REPORTING_DB_SQL_SERVER_NAME | Name of the remote SQL server with the reporting database. <br> If the value is blank, the local computer is used. |
