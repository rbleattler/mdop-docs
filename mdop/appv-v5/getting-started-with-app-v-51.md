---
title: Getting Started with App-V 5.1
description: Microsoft Application Virtualization (App-V) 5.1 enables administrators to deploy, update, and support applications as services in real time, on an as-needed basis.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Getting Started with App-V 5.1

Microsoft Application Virtualization (App-V) 5.1 enables administrators to deploy, update, and support applications as services in real time, on an as-needed basis. Individual applications are transformed from locally installed products into centrally managed services and are available wherever you need, without the need to preconfigure computers or to change operating system settings.

App-V consists of the following elements:

|| Element | Description |
|--|--|
| App-V Management Server | - Provides a central location for managing the App-V infrastructure, which delivers virtual applications to both the App-V Desktop Client and the Remote Desktop Services (formerly Terminal Services) Client. <br> - Uses Microsoft SQL Server® for its data store, where one or more App-V Management servers can share a single SQL Server data store. <br> - Authenticates requests and provides security, metering, monitoring, and data gathering. The server uses Active Directory and supporting tools to manage users and applications. <br> - Has a management site that lets you configure the App-V infrastructure from any computer. You can add and remove applications, manipulate shortcuts, assign access permissions to users and groups, and create connection groups. <br> - Enables communication between the App-V Web Management Console and the SQL Server data store. These components can all be installed on a single server computer, or on one or more separate computers, depending on the required system architecture. |
| App-V Publishing Server | - Provides App-V Clients with entitled applications for the specific user <br> - Hosts the virtual application package for streaming. |
| App-V Desktop Client | - Retrieves virtual applications <br> - Publishes the applications on the clients <br> - Automatically sets up and manages virtual environments at runtime on Windows endpoints. <br> - Stores user-specific virtual application settings, such as registry and file changes, in each user's profile. |
| App-V Remote Desktop Services (RDS) Client | Enables Remote Desktop Session Host servers to use the capabilities of the App-V Desktop Client for shared desktop sessions. |
| App-V Sequencer | - Is a wizard-based tool that you use to transform traditional applications into virtual applications. <br> - Produces the application package, which consists of: <br>   1. a sequenced application (APPV) file <br>   2. a Windows Installer file (MSI) that can be deployed to clients configured for stand-alone operation <br>   3. Several XML files including Report.XML, PackageName_DeploymentConfig.XML, and PackageName_UserConfig.XML. The UserConfig and DeploymentConfig XML files are used to configure custom changes to the default behavior of the package. |

For more information about these elements, see [High Level Architecture for App-V 5.1](high-level-architecture-for-app-v-51.md).

If you are new to this product, we recommend that you read the documentation thoroughly. Before you deploy it to a production environment, we also recommend that you validate your deployment plan in a test network environment.

This section of the App-V 5.1 Administrator's Guide includes high-level information about App-V 5.1 to provide you with a basic understanding of the product before you begin the deployment planning.

## Next steps

[About App-V 5.1](about-app-v-51.md): Provides a high-level overview of App-V 5.1 and how it can be used in your organization.

[Evaluating App-V 5.1](evaluating-app-v-51.md): Provides information about how you can best evaluate App-V 5.1 for use in your organization.
