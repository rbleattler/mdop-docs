---
title: App-V 5.1 Prerequisites
description: App-V 5.1 Prerequisites
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---


# App-V 5.1 Prerequisites


Before installing Microsoft Application Virtualization (App-V) 5.1, ensure that you have installed all of the following required prerequisite software.

For a list of supported operating systems and hardware requirements for the App-V Server, Sequencer, and Client, see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

## Summary of software preinstalled on each operating system


The following table indicates the software that is already installed for different operating systems.

| Operating system | Prerequisite description |
|--|--|
| Windows 10 | All of the prerequisite software is already installed. |
| Windows 8.1 | All of the prerequisite software is already installed.<br>**Note**: If you're running Windows 8, upgrade to Windows 8.1 before using App-V 5.1. |
| Windows Server 2012 | The following prerequisite software is already installed:<br>- Microsoft .NET Framework 4.5<br>- Windows PowerShell 3.0<br/>**Note**: Installing PowerShell 3.0 requires a restart. |
| Windows 7 | The prerequisite software isn't already installed. You must install it before you can install App-V. |

## App-V Server prerequisite software

Install the required prerequisite software for the App-V 5.1 Server components.

### What to know before you start

#### Account for installing the App-V Server

The account that you use to install the App-V Server components must have:

- Administrative rights on the computer on which you're installing the components.
- The ability to query Active Directory Domain Services.

#### Port and firewall

- Specify a port where each component is hosted.
- Add the associated firewall rules to allow incoming requests to the specified ports.

#### Web Distributed Authoring and Versioning (WebDAV)

WebDAV is automatically disabled for the Management Service.

#### Supported deployment scenarios

- A stand-alone deployment, where all components are deployed on the same server.
- A distributed deployment.

#### Unsupported deployment scenarios

- Installing side-by-side instances of multiple App-V Server versions on the same server.
- Installing the App-V server components on a computer that runs server core or domain controller.

### Management server prerequisite software


| Prerequisites and required settings | Details |
|--|--|
| Supported version of SQL Server | For supported versions, see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md). |
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595) | Installing PowerShell 3.0 requires a restart. |
| Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704) | Applies to Windows 7 only. |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |
| 64-bit ASP.NET registration |  |
| Windows Server Web Server Role | This role must be added to a server operating system that is supported for the Management server. |
| Web Server (IIS) Management Tools | **IIS Management Scripts and Tools**. |
| Web Server Role Services | **Common HTTP Features:**<br>- Static Content<br>- Default Document<br>**Application Development:**<br>- ASP.NET<br>- .NET Extensibility<br>- ISAPI Extensions<br>- ISAPI Filters<br>**Security:**<br>- Windows Authentication<br>- Request Filtering<br>**Management Tools:**<br>- IIS Management Console |
| Default installation location | `%PROGRAMFILES%\Microsoft Application Virtualization Server` |
| Location of the Management database | SQL Server database name, SQL Server database instance name, and database name. |
| Management console and Management database permissions | A user or group that can access the Management console and database after the deployment is complete. Only these users or groups have access to the Management console and database unless other administrators are added by using the Management console. |
| Management service website name | Name for the Management console website. |
| Management service port binding | Unique port number for the Management service. This port can't be used by another process on the computer. |

> [!IMPORTANT]
> JavaScript must be enabled on the browser that opens the Web Management Console.

### Management server database prerequisite software

The Management database is required only if you're using the App-V 5.1 Management server.

| Prerequisites and required settings | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |
| Default installation location | `%PROGRAMFILES%\Microsoft Application Virtualization Server` |
| Custom SQL Server instance name (if applicable) | Format to use: **INSTANCENAME**<br>This format is based on the assumption that the installation is on the local computer.<br>If you specify the name with the format **SVR\INSTANCE**, the installation fails. |
| Custom database name (if applicable) | Unique database name.<br>Default: AppVManagement |
| Management server location | Machine account on which the Management server is deployed.<br>Format to use: Domain\MachineAccount |
| Management server installation administrator | Account used to install the Management server.<br>Format to use: Domain\AdministratorLoginName |
| Microsoft SQL Server Service Agent | Configure the Management database computer so that the Microsoft SQL Server Agent service is restarted automatically. For instructions, see [Configure SQL Server Agent to Restart Services Automatically](/previous-versions/technet-magazine/gg313742(v=msdn.10)). |

### Publishing server prerequisite software

| Prerequisites and required settings | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |
| 64-bit ASP.NET registration |  |
| Windows Server Web Server Role | This role must be added to a server operating system that is supported for the Management server. |
| Web Server (IIS) Management Tools | **IIS Management Scripts and Tools**. |
| Web Server Role Services | **Common HTTP Features:**<br>- Static Content<br>- Default Document<br>**Application Development:**<br>- ASP.NET<br>- .NET Extensibility<br>- ISAPI Extensions<br>- ISAPI Filters<br>**Security:**<br>- Windows Authentication<br>- Request Filtering<br>**Management Tools:**<br>- IIS Management Console |
| Default installation location | `%PROGRAMFILES%\Microsoft Application Virtualization Server` |
| Management service URL when management server and publishing server are installed on the same server | URL of the App-V Management service. This is the port with which the Publishing server communicates: `https://localhost:12345` |
| Management service URL when management server and publishing server are installed on different servers | URL of the App-V Management service. This is the port with which the Publishing server communicates: `https://MyAppvServer.MyDomain.com` |
| Publishing service website name | Name for the Publishing website. |
| Publishing service port binding | Unique port number for the Publishing service. This port can't be used by another process on the computer. |

### Reporting server prerequisite software

| Prerequisites and required settings | Details |
|--|--|
| Supported version of SQL Server | For supported versions, see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md). |
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |
| 64-bit ASP.NET registration |  |
| Windows Server Web Server Role | This role must be added to a server operating system that is supported for the Management server. |
| Web Server (IIS) Management Tools | **IIS Management Scripts and Tools**. |
| Web Server Role Services | To reduce the risk of unwanted or malicious data being sent to the Reporting server, you should restrict access to the Reporting Web Service per your corporate security policy.<br>**Common HTTP Features:**<br>- Static Content<br>- Default Document<br>**Application Development:**<br>- ASP.NET<br>- .NET Extensibility<br>- ISAPI Extensions<br>- ISAPI Filters<br>**Security:**<br>- Windows Authentication<br>- Request Filtering<br>**Management Tools:**<br>- IIS Management Console |
| Default installation location | `%PROGRAMFILES%\Microsoft Application Virtualization Server` |
| Reporting service website name | Name for the Reporting website. |
| Reporting service port binding | Unique port number for the Reporting service. This port can't be used by another process on the computer. |

### Reporting database prerequisite software

The Reporting database is required only if you're using the App-V 5.1 Reporting server.

| Prerequisites and required settings | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |
| Default installation location | `%PROGRAMFILES%\Microsoft Application Virtualization Server` |
| Custom SQL Server instance name (if applicable) | Format to use: **INSTANCENAME**<br>This format is based on the assumption that the installation is on the local computer.<br>If you specify the name with the format **SVR\INSTANCE**, the installation fails. |
| Custom database name (if applicable) | Unique database name.<br>Default: AppVReporting |
| Reporting server location | Machine account on which the Reporting server is deployed.<br>Format to use: Domain\MachineAccount |
| Reporting server installation administrator | Account used to install the Reporting server.<br>Format to use: Domain\AdministratorLoginName |
| Microsoft SQL Server Service and Microsoft SQL Server Service Agent | Configure these services to be associated with user accounts that have access to query AD DS. |

## App-V client prerequisite software

Install the following prerequisite software for the App-V client.

| Prerequisite | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595) | Installing PowerShell 3.0 requires a restart. |
| [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704) | Applies to Windows 7 only: Download and install the KB. |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |

## Remote Desktop Services client prerequisite software

Install the following prerequisite software for the App-V Remote Desktop Services client.

| Prerequisite | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595) | Installing PowerShell 3.0 requires a restart. |
| [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704) | Applies to Windows 7 only: Download and install the KB. |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |

## Sequencer prerequisite software

Before installing the prerequisites:

- The computer that runs the Sequencer should have the same hardware and software configurations as the computers that run the virtual applications.

- The sequencing process is resource intensive, so make sure that the computer that runs the Sequencer has plenty of memory, a fast processor, and a fast hard drive. The system requirements of locally installed applications can't exceed those of the Sequencer. For more information, see [App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md).

| Prerequisite | Details |
|--|--|
| [Microsoft .NET Framework 4.5.1 (Web Installer)](https://www.microsoft.com//download/details.aspx?id=40773) |  |
| [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595) | Installing PowerShell 3.0 requires a restart. |
| [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704) | Applies to Windows 7 only: Download and install the KB. |
| [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784) |  |

## Related information

[Planning for App-V 5.1](planning-for-app-v-51.md)

[App-V 5.1 Supported Configurations](app-v-51-supported-configurations.md)
