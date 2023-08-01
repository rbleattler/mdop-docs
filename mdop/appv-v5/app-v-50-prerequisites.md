---
title: App-V 5.0 Prerequisites
description: App-V 5.0 Prerequisites
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 08/30/2016
---

# App-V 5.0 Prerequisites

Before you begin the Microsoft Application Virtualization (App-V) 5.0 Setup, you should make sure that you have met the prerequisites to install the product. This article contains information to help you successfully plan for preparing your computing environment before you deploy the App-V 5.0 features.

> [!IMPORTANT]
> **The prerequisites in this article apply only to App-V 5.0**. For additional prerequisites that apply to App-V 5.0 Service Packs, see the following web pages:

-   [What's new in App-V 5.0 SP1](whats-new-in-app-v-50-sp1.md)

-   [About App-V 5.0 SP2](about-app-v-50-sp2.md)

-   [App-V 5.0 SP3 Prerequisites](app-v-50-sp3-prerequisites.md)

The following table lists prerequisite information that pertains to specific operating systems.

| Operating systems | Prerequisite description |
|--|--|
| Computers that are running:<br>- Windows 8<br>- Windows Server 2012 | The following prerequisites are already installed:<br>- Microsoft .NET Framework 4.5 - you don't need Microsoft .NET Framework 4<br>- Windows PowerShell 3.0 |
| Computers that are running:<br>- Windows 7<br>- Windows Server 2008 | You may want to download the following KB: [Microsoft Security Advisory: Insecure library loading could allow remote code execution](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704). Be sure to check for subsequent KBs that have superseded this one, and note that some KBs may require that you uninstall previous updates. |

## Installation prerequisites for App-V 5.0

> [!NOTE]
> The following prerequisites are already installed for computers that run Windows 8.

Each of the App-V 5.0 features have specific prerequisites that must be met before the App-V 5.0 features can be successfully installed.

### Prerequisites for the App-V 5.0 client

The following list is the installation prerequisites for the App-V 5.0 client:

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)
- [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595)

  > [!NOTE]
  > Installing PowerShell 3.0 requires a restart.

- Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)

  > [!IMPORTANT]
  > You can download and install the previous KB article. However, it may have been replaced with a more recent version.

- The client installer (.exe) will detect if it's necessary to install the following prerequisites, and it does so accordingly:

  - [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784). This prerequisite is only required if you have installed Hotfix Package 4 for Application Virtualization 5.0 SP2 or later.

  - [The Microsoft Visual C++ 2010 Redistributable](https://www.microsoft.com/download/details.aspx?id=26999)

  - Microsoft Visual C++ 2005 SP1 Redistributable Package (x86)

### Prerequisites for the App-V 5.0 Remote Desktop Services client

> [!NOTE]
> The following prerequisites are already installed for computers that run Windows Server 2012.

The following list is the installation prerequisites for the App-V 5.0 Remote Desktop Services client:

- [Microsoft.NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)
- [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595)

  > [!NOTE]
  > Installing PowerShell 3.0 requires a restart.

- Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)

  > [!IMPORTANT]
  > You can download and install the previous KB article. However, it may have been replaced with a more recent version.

- The client (.exe) installer detects if it's necessary to install the following prerequisites, and it does so accordingly:

  - [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784). This prerequisite is required only if you have installed Hotfix Package 4 for Application Virtualization 5.0 SP2 or later.

  - [The Microsoft Visual C++ 2010 Redistributable](https://www.microsoft.com/download/details.aspx?id=26999)

  - Microsoft Visual C++ 2005 SP1 Redistributable Package (x86)

### Prerequisites for the App-V 5.0 Sequencer

> [!NOTE]
> The following prerequisites are already installed for computers that run Windows 8 and Windows Server 2012.

The following list is the installation prerequisites for the App-V 5.0 Sequencer. If possible, the computer that runs the Sequencer should have the same hardware and software configurations as the computers that run the virtual applications.

> [!NOTE]
> If the system requirements of a locally installed application exceed the requirements of the Sequencer, you must meet the requirements of that application. Additionally, because the sequencing process is system resource-intensive, we recommend that the computer that runs the Sequencer has plenty of memory, a fast processor, and a fast hard drive. For more information, see [App-V 5.0 Supported Configurations](app-v-50-supported-configurations.md).

- [Visual C++ Redistributable Packages for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784). This prerequisite is required only if you have installed Hotfix Package 4 for Application Virtualization 5.0 SP2.

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)

- [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595)

- Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)

  > [!IMPORTANT]
  > You can download and install the previous KB article. However, it may have been replaced with a more recent version.

### Prerequisites for the App-V 5.0 server

> [!NOTE]
> The following prerequisites are already installed for computers that run Windows Server 2012:

-   Microsoft .NET Framework 4.5. This eliminates the Microsoft .NET Framework 4 requirement.

-   Windows PowerShell 3.0

-   Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)

    > [!IMPORTANT]
    > You can still download install the previous KB. However, it may have been replaced with a more recent version.

The account that you use to install the server components must have administrative rights on the computer that you're installing on. This account must also have the ability to query Active Directory (AD) Directory Services (DS). Before you install and configure the App-V 5.0 servers, you must specify a port where each component is hosted. You must also add the associated firewall rules to allow incoming requests to the specified ports.

> [!NOTE]
> Web Distributed Authoring and Versioning (WebDAV) is automatically disabled for the Management Service.

The App-V 5.0 server is supported for a standalone deployment, where all the components are deployed on the same server, and a distributed deployment. Depending on the topology that you use to deploy the App-V 5.0 server, the data that you'll need for each component will slightly change.

> [!IMPORTANT]
> The installation of the App-V 5.0 server on a computer that runs any previous version or component of App-V isn't supported. Additionally, the installation of the server components on a computer that runs Server Core or a Domain Controller is also not supported.

#### Management server

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)

- [Windows PowerShell 3.0](https://www.microsoft.com/download/details.aspx?id=34595)

  > [!NOTE]
  > Installing PowerShell 3.0 requires a restart.

- Windows Web Server with the IIS role enabled and the following features: **Common HTTP Features** (static content and default document), **Application Development** (ASP.NET, .NET Extensibility, ISAPI Extensions and ISAPI Filters), **Security** (Windows Authentication, Request Filtering), **Management Tools** (IIS Management Console).

- Download and install [KB2533623](https://support.microsoft.com/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)

  > [!IMPORTANT]
  > You can download and install the previous KB article. However, it may have been replaced with a more recent version.

- [Microsoft Visual C++ 2010 SP1 Redistributable Package (x64)](https://www.microsoft.com/download/details.aspx?id=13523)

- Microsoft Visual C++ 2010 SP1 Redistributable Package (x86)

- 64-bit ASP.NET registration

The App-V 5.0 server components are dependent, but they have varying requirements and installation options that must be deployed. Use the following information to prepare your environment to run the App-V 5.0 management server.

- Installation location - by default this component will be installed to: **%PROGRAMFILES%\Microsoft Application Virtualization Server**.

- Location of the App-V 5.0 management database - SQL Server Name, SQL Instance Name, Database Name.

- Access rights for the App-V 5.0 management console - This is the user or the group that should be granted access to the management console at the end of the deployment. After the deployment, only these users will have access to the management console until other administrators are added through the management console.

  > [!NOTE]
  > Security groups and single users aren't supported. You must specify an AD DS group.

- App-V 5.0 management service website name - specify a name for the website or use the default name.

- App-V 5.0 management service port binding - this should be a unique port number that isn't used by another website on the computer.

- Support for Microsoft Silverlight - Microsoft Silverlight must be installed before the management console is available. While this isn't a requirement for the deployment, the server must be able to support Microsoft Silverlight.

#### Management database

> [!NOTE]
> The database is required only when using the App-V 5.0 management server.

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)

- Microsoft Visual C++ 2010 SP1 Redistributable Package (x86)

The App-V 5.0 server components are dependent, but they have varying requirements and installation options that must be deployed. Use the following information to prepare your environment to run the App-V 5.0 management database.

- Installation location - by default this component will be installed to **%PROGRAMFILES%\Microsoft Application Virtualization Server**.

- Custom SQL Server instance name (if applicable) - the format should be **INSTANCENAME**, because the installation assumes that it is on the local machine. If you specify the name with the following format, **SVR\INSTANCE** will fail.

- Custom App-V 5.0 database name (if applicable) - you must specify a unique database name. The default value for the management database is **AppVManagement**.

- App-V 5.0 management server location - specifies the machine account on which the management server is deployed. This should be specified in the following format **Domain\MachineAccount**.

- App-V 5.0 management server installation administrator - specifies the account that is used to install the App-V 5.0 management server. You should use the following format: **Domain\AdministratorLoginName**.

- Microsoft SQL Server Service Agent - configure the computer running the App-V 5.0 Management Database so that Microsoft SQL Server Agent service is restarted automatically. For more information, see [Configure SQL Server Agent to Restart Services Automatically](/previous-versions/technet-magazine/gg313742(v=msdn.10)).

#### Reporting server

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)

- Microsoft Visual C++ 2010 SP1 Redistributable Package (x86)

> [!NOTE]
> To help reduce the risk of unwanted or malicious data being sent to the reporting server, you should restrict access to the Reporting Web Service per your corporate security policy.

Windows Web Server with the IIS role with the following features: **Common HTTP Features** (static content and default document), **Application Development** (ASP.NET, .NET Extensibility, ISAPI Extensions and ISAPI Filters), **Security** (Windows Authentication, Request Filtering), **Management Tools** (IIS Management Console)

- 64-bit ASP.NET registration
- Installation location - by default this component is installed to **%PROGRAMFILES%\Microsoft Application Virtualization Server**.
- App-V 5.0 reporting service website name - specifies the name of the website or the default name that will be used.
- App-V 5.0 reporting service port binding - This should be a unique port number that isn't already used by another website that runs on the computer.

#### Reporting database

> [!NOTE]
> The database is required only when using the App-V 5.0 reporting server.

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)

- Microsoft Visual C++ 2010 SP1 Redistributable Package (x86)

The App-V 5.0 server components are dependent, but they have varying requirements and installation options that must be deployed. Use the following information to prepare your environment to run the App-V 5.0 reporting database.

- Installation location - by default this component will be installed to **%PROGRAMFILES%\Microsoft Application Virtualization Server**.

- Custom SQL Server instance name (if applicable) - the format should be **INSTANCENAME**, because the installation assumes that it is on the local machine. If you specify the name with the following format, **SVR\INSTANCE** will fail.

- Custom App-V 5.0 database name (if applicable) - you must specify a unique database name. The default value for the reporting database is **AppVReporting**.

- App-V 5.0 reporting server location - specifies the machine account on which the reporting server is deployed. This should be specified in the following format **Domain\MachineAccount**.

- App-V 5.0 reporting server installation administrator - specifies the account that is used to install the App-V 5.0 reporting server. You should use the following format: **Domain\AdministratorLoginName**.

- Microsoft SQL Server Service and the Microsoft SQL Server Agent Service - these services must be associated with user accounts that have access to query AD.

#### Publishing server

- [Microsoft .NET Framework 4 (Full Package)](https://www.microsoft.com/download/details.aspx?id=17718)
- Microsoft Visual C++ 2010 SP1 Redistributable Package (x86)
- Windows Web Server with the IIS role with the following features: **Common HTTP Features** (static content and default document), **Application Development** (ASP.NET, .NET Extensibility, ISAPI Extensions and ISAPI Filters), **Security** (Windows Authentication, Request Filtering), **Management Tools** (IIS Management Console)
- 64-bit ASP.NET registration

The App-V 5.0 server components are dependent, but they have varying requirements and installation options that must be deployed. Use the following information to prepare your environment to run the App-V 5.0 publishing server.

- Installation location - by default this component is installed to **%PROGRAMFILES%\Microsoft Application Virtualization Server**.
- App-V 5.0 management service URL - specifies the URL of the App-V 5.0 management service. This is the port that the publishing server communicates with, and it should be specified using the following format: `https://localhost:12345`.
- App-V 5.0 publishing service website name - specifies the name of the website or the default name that will be used.
- App-V 5.0 publishing service port binding - This should be a unique port number that isn't already used by another website that runs on the computer.

## Related information

[Planning to Deploy App-V](planning-to-deploy-app-v.md)

[App-V 5.0 Supported Configurations](app-v-50-supported-configurations.md)
