---
title: MBAM 2.5 supported configurations
description: You can run Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 in a stand-alone topology or in a Configuration Manager integration topology that integrates MBAM with System Center Configuration Manager. If you use the recommended configuration for either topology in a production environment, MBAM supports up to 500,000 MBAM clients.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 10/24/2018
---

# MBAM 2.5 supported configurations

[!INCLUDE [mdop-lifecycle-statement](../includes/mdop-lifecycle-statement.md)]

You can run Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 in a stand-alone topology or in a Configuration Manager integration topology that integrates MBAM with System Center Configuration Manager. If you use the recommended configuration for either topology in a production environment, MBAM supports up to 500,000 MBAM clients. For information about the recommended architecture and features that are configured on each server for each topology, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).

For other configurations that are specific to the Configuration Manager integration topology, see [Versions of Configuration Manager that MBAM supports](#bkmk-cm-ramreqs).

## MBAM supported languages

The following table shows the languages that are supported for the MBAM client, and the MBAM server in MBAM 2.5 SP1. The client languages also apply to the Self-Service Portal.

| Client languages                          | Server languages                          |
|-------------------------------------------|-------------------------------------------|
| Czech (Czech Republic) cs-CZ              | English (United States) en-US             |
| Danish (Denmark) da-DK                    | French (France) fr-FR                     |
| Dutch (Netherlands) nl-NL                 | German (Germany) de-DE                    |
| English (United States) en-US             | Italian (Italy) it-IT                     |
| Finnish (Finland) fi-FI                   | Japanese (Japan) ja-JP                    |
| French (France) fr-FR                     | Korean (Korea) ko-KR                      |
| German (Germany) de-DE                    | Portuguese (Brazil) pt-BR                 |
| Greek (Greece) el-GR                      | Russian (Russia) ru-RU                    |
| Hungarian (Hungary) hu-HU                 | Spanish (Spain) es-ES                     |
| Italian (Italy) it-IT                     | Simplified Chinese (PRC) zh-CN            |
| Japanese (Japan) ja-JP                    | Traditional Chinese (Taiwan) zh-TW        |
| Korean (Korea) ko-KR                      |                                           |
| Norwegian, Bokmål (Norway) nb-NO          |                                           |
| Polish (Poland) pl-PL                     |                                           |
| Portuguese (Brazil) pt-BR                 |                                           |
| Portuguese (Portugal) pt-PT               |                                           |
| Russian (Russia) ru-RU                    |                                           |
| Slovak (Slovakia) sk-SK                   |                                           |
| Spanish (Spain) es-ES                     |                                           |
| Swedish (Sweden) sv-SE                    |                                           |
| Turkish (Türkiye) tr-TR                   |                                           |
| Slovenian (Slovenia) sl-SI                |                                           |
| Simplified Chinese (PRC) zh-CN            |                                           |
| Traditional Chinese (Taiwan) zh-TW        |                                           |

## <a href="" id="---------mbam-server-system-requirements"></a> MBAM server system requirements

### MBAM server OS requirements

We strongly recommend that you run the MBAM client and MBAM server on the same line of operating systems. For example, Windows 10 with Windows Server 2016, Windows 8.1 with Windows Server 2012 R2, and so on.

The following table lists the operating systems that are supported for the MBAM server installation.

| OS        | Edition                             | Service pack | System architecture |
|-------------------------|-------------------------------------|--------------|---------------------|
| Windows Server 2019     | Standard or Datacenter              |              | 64-bit              |
| Windows Server 2016     | Standard or Datacenter              |              | 64-bit              |
| Windows Server 2012 R2  | Standard or Datacenter              |              | 64-bit              |
| Windows Server 2012     | Standard or Datacenter              |              | 64-bit              |
| Windows Server 2008 R2  | Standard, Enterprise, or Datacenter | SP1          | 64-bit              |

The enterprise domain must contain at least one Windows Server 2008 or later domain controller.

### <a href="" id="bkmk-stand-alone-ramreqs"></a>MBAM server processor, RAM, and disk space requirements - stand-alone topology

These requirements are for the MBAM stand-alone topology. For the requirements for the Configuration Manager integration topology, see [MBAM server processor, RAM, and disk space requirements - Configuration Manager integration topology](#bkmk-cm-ramreqs).

| Hardware item    | Minimum requirement | Recommended requirement |
|------------------|---------------------|-------------------------|
| Processor        | 2.33 GHz            | 2.33 GHz or greater     |
| RAM              | 8 GB                | 12 GB                   |
| Free disk space  | 1 GB                | 2 GB                    |

### <a href="" id="bkmk-cm-ramreqs"></a>MBAM server processor, RAM, and disk space requirements - Configuration Manager integration topology

The following table lists the server processor, RAM, and disk space requirements for MBAM servers when you're using the Configuration Manager integration topology. For the requirements for the stand-alone topology, see [MBAM server processor, RAM, and disk space requirements - stand-alone topology](#bkmk-stand-alone-ramreqs).

| Hardware item    | Minimum requirement | Recommended requirement |
|------------------|---------------------|-------------------------|
| Processor        | 2.33 GHz            | 2.33 GHz or greater     |
| RAM              | 4 GB                | 8 GB                    |
| Free disk space  | 1 GB                | 2 GB                    |

### <a href="" id="bkmk-cmversions"></a>Versions of Configuration Manager that MBAM supports

> [!IMPORTANT]
> Since all versions of Configuration Manager that MBAM supported are out of support, use of MBAM with Configuration Manager is no longer supported. Customers using MBAM with Configuration Manager should [migrate to Configuration Manager BitLocker Management](/mem/configmgr/protect/deploy-use/bitlocker/migration-considerations).

MBAM supports the following versions of Configuration Manager.

| Supported version                                                       | Service pack | System architecture |
|-------------------------------------------------------------------------|--------------|---------------------|
| Microsoft System Center Configuration Manager (Current Branch), versions up to 1902 |              | 64-bit              |
| Microsoft System Center Configuration Manager 1806                      |              | 64-bit              |
| Microsoft System Center Configuration Manager (LTSB - version 1606)     |              | 64-bit              |
| Microsoft System Center 2012 Configuration Manager                      | SP1          | 64-bit              |
| Microsoft System Center Configuration Manager 2007 R2 or later          |              | 64-bit              |

> [!NOTE]
> Although Configuration Manager 2007 R2 is 32-bit, you must install it and SQL Server on a 64-bit operating system in order to match the 64-bit MBAM software.

For a list of supported configurations for the Configuration Manager server, see the appropriate documentation for the version of Configuration Manager that you're using. MBAM has no other system requirements for the Configuration Manager server.

### <a href="" id="sql-server-database-requirements-"></a>SQL Server database requirements

The following table lists the Microsoft SQL Server versions that are supported for the MBAM server features, which include the Recovery Database, Compliance and Audit Database, and the Reports feature. The required versions apply to the Stand-alone or the Configuration Manager integration topologies.

Install SQL Server with the `SQL_Latin1_General_CP1_CI_AS` collation.

| SQL Server version          | Edition                             | Service pack      | System architecture |
|-----------------------------|-------------------------------------|-------------------|---------------------|
| Microsoft SQL Server 2019   | Standard, Enterprise, or Datacenter |                   | 64-bit              |
| Microsoft SQL Server 2017   | Standard, Enterprise, or Datacenter |                   | 64-bit              |
| Microsoft SQL Server 2016   | Standard, Enterprise, or Datacenter | SP1               | 64-bit              |
| Microsoft SQL Server 2014   | Standard, Enterprise, or Datacenter | SP1, SP2          | 64-bit              |
| Microsoft SQL Server 2012   | Standard, Enterprise, or Datacenter | SP3               | 64-bit              |
| Microsoft SQL Server 2008 R2| Standard or Enterprise              | SP3               | 64-bit              |

> [!NOTE]
> MBAM has a maximum supported compatibility level of 140. The default compatibility level for new databases created on SQL Server 2019 is 150. After the database is created, use the ALTER DATABASE command to set the compatibility level to 140 or lower. Existing databases migrated from SQL server 2017 or earlier remain at their previous compatibility level and don't need to be changed.

To support SQL 2016, install the [March 2017 servicing release for MDOP](https://www.microsoft.com/download/details.aspx?id=54967). To support SQL 2017, install the [July 2018 Servicing Release for MDOP](https://www.microsoft.com/download/details.aspx?id=57157). In general, stay current by always using the most recent servicing update as it also includes all bug fixes and new features.

### <a href="" id="bkmk-sql-stand-alone-ramreqs"></a>SQL Server processor, RAM, and disk space requirements - stand-alone topology

The following table lists the recommended server processor, RAM, and disk space requirements for the SQL Server computer when you're using the stand-alone topology. Use these requirements as a guide. Your specific requirements might vary based on the number of client computers you're supporting in your organization. To view the requirements for the Configuration Manager integration topology, see [SQL Server processor, RAM, and disk space requirements - Configuration Manager integration topology](#bkmk-cm-sql-ramreqs).

| Hardware item    | Minimum requirement | Recommended requirement |
|------------------|---------------------|-------------------------|
| Processor        | 2.33 GHz            | 2.33 GHz or greater     |
| RAM              | 8 GB                | 12 GB                   |
| Free disk space  | 5 GB                | 5 GB or greater         |

### <a href="" id="bkmk-cm-sql-ramreqs"></a>SQL Server processor, RAM, and disk space requirements - Configuration Manager integration topology

The following table lists the server processor, RAM, and disk space requirements for the Microsoft SQL Server computer when you're using the Configuration Manager integration topology, see [SQL Server processor, RAM, and disk space requirements - stand-alone topology](#bkmk-sql-stand-alone-ramreqs).

| Hardware item    | Minimum requirement | Recommended requirement |
|------------------|---------------------|-------------------------|
| Processor        | 2.33 GHz            | 2.33 GHz or greater     |
| RAM              | 4 GB                | 8 GB                    |
| Free disk space  | 5 GB                | 5 GB                    |

## <a href="" id="---------mbam-client-system-requirements"></a> MBAM client system requirements

### Client OS requirements

Run the MBAM client and MBAM server on the same line of operating systems. For example, Windows 10 with Windows Server 2016 or Windows 8.1 with Windows Server 2012 R2.

The following table lists the operating systems that are supported for MBAM client installation. The same requirements apply to the stand-alone and the Configuration Manager integration topologies.

| OS | Edition                          | Service pack | System architecture |
|------------------|----------------------------------|--------------|---------------------|
| Windows 11       | Enterprise                       |              | 32-bit or 64-bit    |
| Windows 10 IoT   | Enterprise                       |              | 32-bit or 64-bit    |
| Windows 10       | Enterprise                       |              | 32-bit or 64-bit    |
| Windows 8.1      | Enterprise                       |              | 32-bit or 64-bit    |
| Windows 7        | Enterprise or Ultimate           | SP1          | 32-bit or 64-bit    |
| Windows To Go    | Windows 8.1 and Windows 10 Enterprise |              | 32-bit or 64-bit    |

### <a href="" id="client-ram-requirements-"></a>Client RAM requirements

There are no RAM requirements that are specific to the MBAM client installation.

## <a href="" id="---------mbam-group-policy-system-requirements"></a> MBAM group policy system requirements

The following table lists the operating systems that are supported for MBAM group policy templates installation.

| OS        | Edition                            | Service pack | System architecture |
|-------------------------|------------------------------------|--------------|---------------------|
| Windows 11              | Enterprise                         |              | 32-bit or 64-bit    |
| Windows 10 IoT          | Enterprise                         |              | 32-bit or 64-bit    |
| Windows 10              | Enterprise                         |              | 32-bit or 64-bit    |
| Windows 8.1             | Enterprise                         |              | 32-bit or 64-bit    |
| Windows 7               | Enterprise, or Ultimate            | SP1          | 32-bit or 64-bit    |
| Windows Server 2012 R2  | Standard or Datacenter             |              | 64-bit              |
| Windows Server 2012     | Standard or Datacenter             |              | 64-bit              |
| Windows Server 2008 R2  | Standard, Enterprise, or Datacenter | SP1          | 64-bit              |

## MBAM in Microsoft Azure

You can deploy the MBAM server in Azure on any of the supported OS versions. It can connect to an Active Directory hosted on premises or an Active Directory also hosted in Azure. For more information, see [Safely virtualizing Active Directory Domain Services](/windows-server/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).

The MBAM client isn't supported on virtual machines and is also not supported on Azure IaaS.

## Service releases

- [September 2016](https://support.microsoft.com/topic/september-2016-servicing-release-for-microsoft-desktop-optimization-pack-ef0f16a3-c087-4865-f49b-8b5010327792)
- [December 2016](https://support.microsoft.com/topic/december-2016-servicing-release-for-microsoft-desktop-optimization-pack-024c3b70-f351-e3fd-f73a-4815b864a8e9)
- [March 2017](https://support.microsoft.com/topic/march-2017-servicing-release-for-microsoft-desktop-optimization-pack-f1c4a8d5-4af5-37f6-cb23-24fb934f416b)
- [June 2017](https://support.microsoft.com/topic/june-2017-servicing-release-for-microsoft-desktop-optimization-pack-8e87c251-5f37-dbf0-3bc3-5553942e18d1)
- [September 2017](https://support.microsoft.com/topic/september-2017-servicing-release-for-microsoft-desktop-optimization-pack-a7fd0b37-32f7-d544-2bbd-19e330b34cfe)
- [March 2018](https://support.microsoft.com/topic/march-2018-servicing-release-for-microsoft-desktop-optimization-pack-75ebd55c-91f1-07fe-15ab-e4e7f5f899f0)
- [July 2018](https://support.microsoft.com/topic/july-2018-servicing-release-for-microsoft-desktop-optimization-pack-0981e587-99bb-1505-ad53-cda51c0a172d)
- [May 2019](https://support.microsoft.com/topic/may-2019-servicing-release-for-microsoft-desktop-optimization-pack-53df7972-c633-bada-950d-4afe6574ed84)

## Related articles

[Planning to deploy MBAM 2.5](planning-to-deploy-mbam-25.md)

[Preparing your environment for MBAM 2.5](preparing-your-environment-for-mbam-25.md)
