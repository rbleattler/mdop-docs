---
title: Planning for MBAM 2.5 high availability
description: Microsoft BitLocker Administration and Monitoring (MBAM) can maintain high availability through use of one or more technologies.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Planning for MBAM 2.5 high availability

Microsoft BitLocker Administration and Monitoring (MBAM) can maintain high availability through use of one or more technologies.

Use the information in the following sections to help you understand the options to deploy MBAM in a highly available configuration.

## <a href="" id="bkmk-alwayson"></a>Support for SQL Server AlwaysOn availability groups

MBAM enables you to configure and manage availability groups for the databases in Microsoft SQL Server. An availability group for MBAM supports a failover environment where the Compliance and Audit Database and the Recovery Database fail over together rather than separately.

An availability group supports a set of read/write primary databases and one to four sets of corresponding secondary databases. Optionally, secondary databases can be made available for read-only permission, some backup operations, or for both.

For information about how to set up availability groups, see [AlwaysOn availability groups](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

## <a href="" id="bkmk-sql-clustering"></a>Microsoft SQL Server clustering

You can run the MBAM 2.5 Compliance and Audit Database and the Recovery Database on computers that are running SQL Server clusters.

## <a href="" id="bkmk-load-balance"></a>IIS network load balancing

You can use network load balancing to configure a highly available environment for computers that are running the Administration and Monitoring website (also known as Help Desk), the Self-Service Portal, and the web services, which are deployed through Internet Information Services (IIS).

### Prerequisites

Before configuring load balancing, ensure that your environment meets the following prerequisites:

- A load balancer must be available. You can use load balancers from Microsoft or another company. For more information about Microsoft load balancer technology, see [Build a web farm with IIS servers](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj129543(v=ws.11)).

- At least two servers are running IIS and the servers meet all of the MBAM prerequisites to support its web features, including ASP.NET MVC 4.

- MBAM databases and reports are running on a server.

### <a href="" id="-------------mbam-specific-changes-that-are-required-to-enable-load-balancing"></a> MBAM-specific changes that are required to enable Load Balancing

Complete the following tasks:

1.  Register a Service Principal Name (SPN) for the virtual host name under the domain account that you use for the web application pools. For example, if the virtual host name is mbamvirtual.contoso.com, and the domain account used for the web application pools is contoso\\mbamapppooluser, the following command registers the SPN appropriately.

    `Setspn -s http//mbamvirtual contoso\mbamapppooluser`

    `Setspn -s http//mbamvirtual.contoso.com contoso\mbamapppooluser`

2.  Configure the following MBAM web features:

    - On each server that hosts the MBAM web features, use the same domain account for the application pool administrative credentials.

    - Specify a host name that matches the virtual host name (DNS name) of the Load Balancing cluster. For example, when you install MBAM on a server called "NLB1" with a virtual host name of **mbamvirtual.contoso.com**, ensure that the host name that you specify in the Windows PowerShell cmdlet is **mbamvirtual.contoso.com**.

3.  If you configure the websites in a web farm with a load balancer, you must configure the websites to use the same machine key.

    For more information, see the following sections in [machineKey Element (ASP.NET Settings Schema)](/previous-versions/dotnet/netframework-4.0/w8h3skw9(v=vs.100)):

    - Machine Key Explained

    - Web Farm Deployment Considerations

    For instructions about how to automatically generate a key, see [Generate a machine key (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772287(v=ws.10)).

The information about load balancing also applies to IIS Network Load Balancing (NLB) clusters in Windows Server 2012 or Windows Server 2008 R2. The IIS network load balancing functionality in Windows Server 2012 is the same as in Windows Server 2008 R2. However, some task details are different in Windows Server 2012. For information about new ways to do tasks, see [Common management tasks and navigation in Windows Server 2012 R2 Preview and Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831491(v=ws.11)).

## <a href="" id="bkmk-db-mirroring"></a>Database mirroring in SQL Server

MBAM supports the use of SQL Server mirroring, where the Compliance and Audit Database and the Recovery Database are mirrored by using two instances of SQL Server for each database.

> [!NOTE]
> Mirroring is slowly being phased out, in favor of availability groups.

To implement mirroring for MBAM, you must specify the appropriate connection strings for the mirrored database configuration by using the **Enable-MbamWebApplication** Windows PowerShell cmdlet. For more information about the MBAM 2.5 Windows PowerShell cmdlets, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

### Examples of implementing SQL Server mirroring by using Windows PowerShell

The following examples show how you might implement SQL Server mirroring by using Windows PowerShell cmdlets.

#### Example 1

```powershell
Enable-MbamWebApplication -AdministrationPortal -ComplianceAndAuditDBConnectionString 'Integrated Security=SSPI;Data Source=MyDatabaseServer;Failover Partner=myMirrorServerAddress;Initial Catalog="MBAM Compliance Status";' -RecoveryDBConnectionString 'Integrated Security=SSPI;Data Source=MyDatabaseServer;Failover Partner=myMirrorServerAddress;Initial Catalog="MBAM Recovery and Hardware";' -AdvancedHelpdeskAccessGroup "MyDomain\AdvancedUserGroup" -HelpdeskAccessGroup "MyDomain\StandardUserGroup" -ReportsReadOnlyAccessGroup "MyDomain\ReportUserGroup" -ReportUrl "https://MyReportServer/ReportServer" -Port 443 -WebServiceApplicationPoolCredential (Get-Credential) -Certificate (dir cert:\LocalMachine\My\E2A7EA5533890D6567E40DFC46F53B3D31D6B689)
```

#### Example 2

```powershell
Enable-MbamWebApplication -SelfServicePortal -ComplianceAndAuditDBConnectionString 'Integrated Security=SSPI;Data Source=MyDatabaseServer; Failover Partner=myMirrorServerAddress;Initial Catalog="MBAM Compliance Status";' -RecoveryDBConnectionString 'Integrated Security=SSPI;Data Source=MyDatabaseServer;I Failover Partner=myMirrorServerAddress;Initial Catalog="MBAM Recovery and Hardware";' -Port 443 -WebServiceApplicationPoolCredential (Get-Credential) -Certificate (dir cert:\LocalMachine\My\E2A7EA5533890D6567E40DFC46F53B3D31D6B689)
```

### More information about SQL Server mirroring

For more information about configuring SQL Server mirroring, see the following articles:

- [How to: prepare a mirror database for mirroring (Transact-SQL)](/previous-versions/sql/sql-server-2008-r2/ms189047(v=sql.105))

- [Establish a database mirroring session - Windows Authentication](/sql/database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication)

## <a href="" id="bkmk-vss"></a>Backing up MBAM databases by using the Volume Shadow Copy Service (VSS)

MBAM provides a Volume Shadow Copy Service (VSS) writer, called the Microsoft BitLocker Administration and Management Writer. This VSS writer facilitates the backup of the Compliance and Audit Database and the Recovery Database.

The VSS writer is registered on every server where you enable an MBAM web application. The MBAM VSS writer depends on the SQL Server VSS Writer, which is registered as part of the Microsoft SQL Server installation. Any backup technology that uses VSS writers to perform backup can discover the MBAM VSS writer.

## Related articles

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)
