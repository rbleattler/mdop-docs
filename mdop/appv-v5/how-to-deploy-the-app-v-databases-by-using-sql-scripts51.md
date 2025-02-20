---
title: How to Deploy the App-V Databases by Using SQL Scripts
description: How to Deploy the App-V Databases by Using SQL Scripts
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to Deploy the App-V Databases by Using SQL Scripts

Use the following instructions to use SQL scripts, rather than the Windows Installer, to:

- Install the App-V 5.1 databases
- Upgrade the App-V databases to a later version

> [!NOTE]
> If you have already deployed the App-V 5.0 SP3 database, the SQL scripts are not required to upgrade to App-V 5.1.

## How to install the App-V databases by using SQL scripts

1. Before you install the database scripts, review and keep a copy of the App-V license terms. By running the database scripts, you're agreeing to the license terms. If you don't accept them, you shouldn't use this software.
1. Copy the `appv_server_setup.exe` from the App-V release media to a temporary location.
1. From a command prompt, run `appv_server_setup.exe` and specify a temporary location for extracting the database scripts.

    Example: `appv_server_setup.exe /layout c:\<temporary location path>`

1. Browse to the temporary location that you created, open the extracted `DatabaseScripts` folder, and review the appropriate Readme.txt file for instructions:

    - Management database: `ManagementDatabase` subfolder

    - Reporting database: `ReportingDatabase` subfolder

> [!CAUTION]
> The readme.txt file in the `ManagementDatabase` subfolder is out of date. The information in the updated readme files below is the most current and should supersede the readme information provided in the `DatabaseScripts` folders.

> [!IMPORTANT]
> The InsertVersionInfo.sql script is not required for versions of the App-V management database later than App-V 5.0 SP3.

## Updated management database README file content

```plaintext
******************************************************************
Before you install and use the Application Virtualization Database Scripts you must:
1.Review the Microsoft Application Virtualization Server 5.0 license terms.
2.Print and retain a copy of the license terms for your records.
By running the Microsoft Application Virtualization Database Scripts you agree to such license terms.  If you do not accept them, do not use the software.
******************************************************************


Steps to install "AppVManagement" schema in SQL SERVER.


## PREREQUISITES:

 1. Review the installation package.  The following files MUST exist:

    SQL files
    ---------
    Database.sql
    CreateTables.sql
    CreateStoredProcs.sql
    UpdateTables.sql
    Permissions.sql

 2. Ensure the target SQL Server instance and SQL Server Agent service are running.

 3. If you are not running the scripts directly on the server, ensure the
    necessary SQL Server client software is installed and available from
    the specified location.  Specifically, the "osql" command must
##     be supported for these scripts to run.



## PREPARATION:

 1. Review the database.sql file and modify as necessary.  Although the
    defaults are likely sufficient, it is suggested that the following
    settings be reviewed:

    DATABASE - ensure name is satisfactory - default is "AppVManagement".

 2. Review the Permissions.sql file and provide all the necessary account information
    for setting up read and write access on the database. Note: Default settings
##     in the file will not work.



## INSTALLATION:

 1. Run the database.sql against the "master" database.  Your user
    credential must have the ability to create databases.
    This script will create the database.

 2. Run the following scripts against the "AppVManagement" database using the
    same account as above in order.

    CreateTables.sql
    CreateStoredProcs.sql
    UpdateTables.sql
##     Permissions.sql

```

## Updated reporting database README file content

```plaintext
******************************************************************
Before you install and use the Application Virtualization Database Scripts you must:
1.Review the Microsoft Application Virtualization Server 5.0 license terms.
2.Print and retain a copy of the license terms for your records.
By running the Microsoft Application Virtualization Database Scripts you agree to such license terms.  If you do not accept them, do not use the software.
******************************************************************

Steps to install "AppVReporting" schema in SQL SERVER.


## PREREQUISITES:

 1. Review the installation package.  The following files MUST exist:

    SQL files
    ---------
    Database.sql
    UpgradeDatabase.sql
    CreateTables.sql
    CreateReportingStoredProcs.sql
    CreateStoredProcs.sql
    CreateViews.sql
    InsertVersionInfo.sql
    Permissions.sql
    ScheduleReportingJob.sql

 2. Ensure the target SQL Server instance and SQL Server Agent service are running.

 3. If you are not running the scripts directly on the server, ensure the
    necessary SQL Server client software is installed and executable from
    the location you have chosen.  Specifically, the "osql" command must
##     be supported for these scripts to run.



## PREPARATION:

 1. Review the database.sql file and modify as necessary.  Although the
    defaults are likely sufficient, it is suggested that the following
    settings be reviewed:

    DATABASE - ensure name is satisfactory - default is "AppVReporting".

 2. Review the Permissions.sql file and provide all the necessary account information
    for setting up read and write access on the database. Note: Default settings
    in the file will not work.

 3. Review the ScheduleReportingJob.sql file and make sure that the stored proc schedule
    time is acceptable. The default stored proc schedule time is at 12.01 AM (line 84).
    If this time is not suitable, you can change this to a more suitable time. The time is
##     in the format HHMMSS.



## INSTALLATION:

 1. Run the database.sql against the "master" database.  Your user
    credential must have the ability to create databases.
    This script will create the database.

 2. If upgrading the database, run UpgradeDatabase.sql This will upgrade database schema.

 2. Run the following scripts against the "AppVReporting" database using the
    same account as above in order.

    CreateTables.sql
    CreateReportingStoredProcs.sql
    CreateStoredProcs.sql
    CreateViews.sql
    InsertVersionInfo.sql
    Permissions.sql
##     ScheduleReportingJob.sql

```

## Related information

[Deploying the App-V 5.1 Server](deploying-the-app-v-51-server.md)

[How to Deploy the App-V 5.1 Server](how-to-deploy-the-app-v-51-server.md)
