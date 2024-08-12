---
title: Upgrading to MBAM 2.5 or MBAM 2.5 SP1 from previous versions
description: This article describes the process for upgrading the Microsoft BitLocker Administration and Monitoring (MBAM) server and the MBAM client from earlier versions of MBAM.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Upgrading to MBAM 2.5 or MBAM 2.5 SP1 from Previous Versions

This article describes the process for upgrading the Microsoft BitLocker Administration and Monitoring (MBAM) server and the MBAM client from earlier versions of MBAM.

> [!NOTE]
> You can upgrade directly to MBAM 2.5 or MBAM 2.5 SP1 from any previous version of MBAM.

## Before you start the upgrade

Review the following information before you start the upgrade.

| What to know before you start | Details |
|-------------------------------|---------|
| If you install the MBAM websites on one server and the web services on another server, you have to use Windows PowerShell cmdlets to configure them. | The MBAM server Configuration wizard doesn't support configuring the websites on one server and the web services on a different server. |
| If you upgrade to MBAM 2.5 or 2.5 SP1 from MBAM 2.0 or 2.0 SP1 in Windows Server 2008 R2: <ul><li>The Administration and Monitoring Website and the Self-Service Portal won't work if you install the required .NET Framework 4.5 software after Internet Information Services (IIS) is already installed.</li><li>This issue occurs because ASP.NET can't be registered correctly with IIS if the .NET Framework is installed after IIS is already installed.</li></ul> | **To resolve this issue:** <ul><li>Run `aspnet_regiis -i` from the following location:</li><li>`C:\windows\microsoft.net\Framework\v4.0.30319`</li><li>For more information, see: [ASP.NET IIS registration tool](/previous-versions/dotnet/netframework-2.0/k6h9cz8h(v=vs.80)).</li></ul> |
| Register an SPN on the application pool account if all of the following are true: <ul><li>You upgrade from a previous version of MBAM.</li><li>Currently, you aren't running the MBAM websites in a load-balanced or distributed configuration, but you would like to do so when you upgrade to MBAM 2.5 or 2.5 SP1.</li></ul> | For instructions, see [Planning how to secure the MBAM websites](planning-how-to-secure-the-mbam-websites.md#bkmk-registerspn). <br><br> **What we recommend:** <ul><li>Register a service principal name (SPN) for the application pool account, even though you might already register SPNs for the machine account.</li></ul> <br> **Why we recommend it:** <ul><li>Registering an SPN on the application pool account is required to configure the websites in a load-balanced or distributed configuration.</li></ul> <br> **What happens if SPNs are already configured on a machine account?** <ul><li>MBAM uses the SPNs that you already registered, and you don't need to configure other SPNs, but you aren't able to configure the websites in a load-balanced or distributed configuration.</li></ul> |


## Steps to upgrade the MBAM server infrastructure

Use the steps in the following sections to upgrade MBAM for the Stand-alone topology or the System Center Configuration Manager integration topology.

### To upgrade the MBAM server infrastructure for Stand-alone topology

1.  Uninstall previous versions of MBAM from **Programs and Features** and from web servers to make sure that information isn't being written from MBAM clients to the MBAM infrastructure. For instructions, see [Removing MBAM server features or software](removing-mbam-server-features-or-software.md#bkmk-removeserverfeatures).

2.  Back up your databases.

3.  Uninstall previous versions of MBAM from SQL Server by using **Programs and Features**, including SQL Servers hosting the MBAM reports via SQL Server Reporting Services. Remove any remaining MBAM server temporary files or folders from the database server and reporting services.

    > [!NOTE]
    > The databases aren't removed, and all compliance and recovery data is maintained in the database.

4.  Install and configure the MBAM 2.5 or 2.5 SP1 databases, reports, and web applications, in that order. The databases are upgraded in place.

5.  Update the group policy objects (GPOs) using the MBAM 2.5 templates to use the new features in MBAM, such as enforced encryption. If you don't update the GPOs and the MBAM client to MBAM 2.5, earlier versions of MBAM clients continue to report against your current GPOs with reduced functionality. To download the latest ADMX templates, see [How to download and deploy MDOP group policy (.admx) templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md).

    After you upgrade the MBAM server infrastructure, the existing client computers continue to successfully report to the MBAM 2.5 or 2.5 SP1 server, and recovery data continues to be stored.

6.  Install the latest MBAM 2.5 or 2.5 SP1 client. After the deployment, you don't need to restart client computers.

### To upgrade the MBAM infrastructure for System Center Configuration Manager integration topology

1.  Uninstall previous versions of MBAM from **Programs and Features** and from web servers to make sure that MBAM clients aren't writing information to the MBAM infrastructure. For instructions, see [Removing MBAM server features or software](removing-mbam-server-features-or-software.md#bkmk-removeserverfeatures).

2.  Back up your databases.

3.  Uninstall previous versions of MBAM from SQL Server by using **Programs and Features**, including SQL Servers hosting the MBAM reports via SQL Server Reporting Services. Remove any remaining MBAM server temporary files or folders from the database server and reporting services.

4.  Uninstall MBAM from the Configuration Manager server.

    > [!NOTE]
    > The databases and the Configuration Manager objects aren't removed. These objects are baselines, MBAM supported computers collection, and reports. All compliance and recovery data is maintained in the database.

5.  Update the .mof files.

6.  Install and configure the MBAM 2.5 or 2.5 SP1 databases, reports, web applications, and Configuration Manager integration, in that order. The databases and Configuration Manager objects are upgraded in place.

7.  Optionally, update the group policy objects (GPOs), and edit the settings if you want to implement new features in MBAM, such as enforced encryption. If you don't update the GPOs, MBAM continues to report against your current GPOs. To download the latest ADMX templates, see [How to download and deploy MDOP group policy (.admx) templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md).

    After you upgrade the MBAM server infrastructure, the existing client computers continue to successfully report to the MBAM 2.5 or 2.5 SP1 Server, and recovery data continues to be stored.

8.  Install the latest MBAM 2.5 or 2.5 SP1 Client. After the deployment, you don't need to restart client computers.

## Upgrade support for the MBAM client

MBAM supports upgrades to the MBAM 2.5 Client from any earlier version of the MBAM client.

### Ways to install the MBAM client

- Upgrade the computers running MBAM client all at once or gradually after you install the MBAM 2.5 Server infrastructure.

- Install the MBAM client through an electronic software distribution system or through tools such as Active Directory Domain Services or System Center Configuration Manager.

## Related articles

[MBAM 2.5 deployment checklist](mbam-25-deployment-checklist.md)

[Deploying the MBAM 2.5 Client](deploying-the-mbam-25-client.md)

[Configuring the MBAM 2.5 Server Features](configuring-the-mbam-25-server-features.md)
