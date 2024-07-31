---
title: Planning for High Availability with App-V 5.1
description: Microsoft Application Virtualization (App-V) 5.1 system configurations can take advantage of options that maintain a high level of available service.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Planning for High Availability with App-V 5.1

Microsoft Application Virtualization (App-V) 5.1 system configurations can take advantage of options that maintain a high level of available service.

Use the information in the following sections to help you understand the options to deploy App-V 5.1 in a highly available configuration.

- [Support for Microsoft SQL Server clustering](#bkmk-sqlcluster)

- [Support for IIS Network Load Balancing](#bkmk-iisloadbal)

- [Support for clustered file servers when running (SCS) mode](#bkmk-clusterscsmode)

- [Support for Microsoft SQL Server Mirroring](#bkmk-sqlmirroring)

- [Support for Microsoft SQL Server Always On](#bkmk-sqlalwayson)

## <a href="" id="bkmk-sqlcluster"></a>Support for Microsoft SQL Server clustering

You can run the App-V Management database and Reporting database on computers that are running Microsoft SQL Server clusters. However, you must install the databases using scripts.

For instructions, see [How to Deploy the App-V Databases by Using SQL Scripts](how-to-deploy-the-app-v-databases-by-using-sql-scripts51.md).

## <a href="" id="bkmk-iisloadbal"></a>Support for IIS Network Load Balancing

You can use Internet Information Services (IIS) Network Load Balancing to configure a highly available environment for computers running the App-V 5.x Management, Publishing, and Reporting services which are deployed through IIS.

Review the following for more information about configuring IIS and Network Load Balancing for computers running Windows Server operating systems:

- Configuring Microsoft Windows Server

  [Network Load Balancing](/previous-versions/windows/it-pro/windows-server-2003/cc740265(v=ws.10)).

  This information also applies to IIS Network Load Balancing (NLB) clusters in Windows Server 2008, Windows Server 2008 R2, or Windows Server 2012.

  > [!NOTE]
  > The IIS Network Load Balancing functionality in Windows Server 2012 is generally the same as in Windows Server 2008 R2. However, some task details are changed in Windows Server 2012. For information on new ways to do tasks, see [Common Management Tasks and Navigation in Windows Server 2012 R2 Preview and Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831491(v=ws.11)).

## <a href="" id="bkmk-clusterscsmode"></a>Support for clustered file servers when running (SCS) mode

Running App-V 5.1 in Share Content Store (SCS) mode with clustered file servers is supported.

The following steps can be used to enable this configuration:

- Configure App-V 5.1 to run in client SCS mode. For more information about configuring App-V 5.1 SCS mode, see [How to Install the App-V 5.1 Client for Shared Content Store Mode](how-to-install-the-app-v-51-client-for-shared-content-store-mode.md).

- Configure the file server cluster configured in both the Microsoft Server 2012 scale out mode and pre **2012** mode with a virtual SAN.

The following steps can be used to validate the configuration:

1.  Add a package on the publishing server. For more information about adding a package, see [How to Add or Upgrade Packages by Using the Management Console](how-to-add-or-upgrade-packages-by-using-the-management-console-51-gb18030.md).

2.  Perform a publishing refresh on the computer running the App-V 5.1 client and open an application.

3.  Switch cluster nodes mid-publishing refresh and mid-streaming to ensure fail-over works correctly.

Review the following for more information about configuring Windows Server Failover clusters:

- [Checklist: Create a Clustered File Server](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753969(v=ws.11)).

- [Use Cluster Shared Volumes in a Windows Server 2012 Failover Cluster](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612868(v=ws.11)).

## <a href="" id="bkmk-sqlmirroring"></a>Support for Microsoft SQL Server Mirroring

Using Microsoft SQL Server mirroring, where the App-V 5.1 management server database is mirrored utilizing two SQL Server instances, for App-V 5.1 management server databases is supported.

Review the following for more information about configuring Microsoft SQL Server Mirroring:

- [How to: Prepare a Mirror Database for Mirroring (Transact-SQL)](/previous-versions/sql/sql-server-2008-r2/ms189047(v=sql.105))

- [Establish a Database Mirroring Session Using Windows Authentication (SQL Server Management Studio)](/sql/database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication)

The following steps can be used to validate the configuration:

1.  Initiate a Microsoft SQL Server Mirroring session.

2.  Select **Failover** to designate a new master Microsoft SQL Server instance.

3.  Verify that the App-V 5.1 management server continues to function as expected after the failover.

The connection string on the management server can be modified to include **failover partner = &lt;server2&gt;**. This will only help when the primary on the mirror has failed over to the secondary and the computer running the App-V 5.1 client is doing a fresh connection (say after reboot).

Use the following steps to modify the connection string to include **failover partner = &lt;server2&gt;**:

> [!IMPORTANT]
> This topic describes how to change the Windows registry by using Registry Editor. If you change the Windows registry incorrectly, you can cause serious problems that might require you to reinstall Windows. You should make a backup copy of the registry files (System.dat and User.dat) before you change the registry. Microsoft cannot guarantee that the problems that might occur when you change the registry can be resolved. Change the registry at your own risk.

1.  Login to the management server and open **regedit**.

2.  Navigate to **HKEY\_LOCAL\_MACHINE** \\ **Software** \\ **Microsoft** \\ **AppV** \\ **Server** \\ **ManagementService**.

3.  Modify the **MANAGEMENT\_SQL\_CONNECTION\_STRING** value with the **failover partner = &lt;server2&gt;**.

4.  Restart management service using the IIS console.

  > [!NOTE]
  > Database Mirroring is on the list of Deprecated Database Engine Features for Microsoft SQL Server 2012 due to the **AlwaysOn** feature available with Microsoft SQL Server 2012.

For more information, see the following articles:

- [How to: Prepare a Mirror Database for Mirroring (Transact-SQL)](/previous-versions/sql/sql-server-2008-r2/ms189047(v=sql.105)).

- [How to: Configure a Database Mirroring Session (SQL Server Management Studio)](/previous-versions/sql/sql-server-2008-r2/ms188712(v=sql.105)).

- [Establish a Database Mirroring Session Using Windows Authentication (SQL Server Management Studio)](/previous-versions/sql/sql-server-2012/ms188712(v=sql.110)).

- [Deprecated Database Engine Features in SQL Server 2012](/previous-versions/sql/sql-server-2012/ms143729(v=sql.110)).

## <a href="" id="bkmk-sqlalwayson"></a>Support for Microsoft SQL Server Always On configuration

The App-V 5.1 management server database supports deployments to computers running Microsoft SQL Server with the **Always On** configuration.

## Related topics

[App-V 5.1 supported configurations](app-v-51-supported-configurations.md)
