---
title: How to Deploy the App-V 5.1 Server
description: How to Deploy the App-V 5.1 Server
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to deploy the App-V 5.1 server

Use the following procedure to install the Microsoft Application Virtualization (App-V) 5.1 server. For information about deploying the App-V 5.1 Server, see [About App-V 5.1](about-app-v-51.md#bkmk-migrate-to-51).

## Before you start

- Ensure that you've installed prerequisite software. See [App-V 5.1 Prerequisites](app-v-51-prerequisites.md).

- Review the server section of [App-V 5.1 Security Considerations](app-v-51-security-considerations.md).

- Specify a port where each component will be hosted.

- Add firewall rules to allow incoming requests to access the specified ports.

- If you use SQL scripts, instead of the Windows Installer, to set up the Management database or Reporting database, you must run the SQL scripts before installing the Management Server or Reporting Server. See [How to Deploy the App-V Databases by Using SQL Scripts](how-to-deploy-the-app-v-databases-by-using-sql-scripts51.md).

## Install the App-V 5.0 server

1. Copy the App-V 5.1 server installation files to the computer on which you want to install it.

2. Start the App-V 5.1 server installation. Run `appv_server_setup.exe` as an administrator, and then select **Install**.

3. Review and accept the license terms, and choose whether to enable Microsoft updates.

4. On the **Feature Selection** page, select all of the following components.

    | Component | Description |
    |--|--|
    | Management server | Provides overall management functionality for the App-V infrastructure. |
    | Management database | Facilitates database predeployments for App-V management. |
    | Publishing server | Provides hosting and streaming functionality for virtual applications. |
    | Reporting server | Provides App-V 5.0 reporting services. |
    | Reporting database | Facilitates database predeployments for App-V reporting. |

5. On the **Installation Location** page, accept the default location where the selected components will be installed, or change the location by typing a new path on the **Installation Location** line.

6. On the initial **Create New Management Database** page, configure the **Microsoft SQL Server instance** and **Management Server database** by selecting the appropriate option below.

   - If you're using a *custom Microsoft SQL Server instance*:

     - Select **Use the custom instance**, and type the name of the instance.
     - Use the format **INSTANCENAME**. The assumed installation location is the local computer.
     - Not supported: A server name using the format `ServerName\INSTANCE`

   - If you're using a *custom database name*:

     - Select **Custom configuration** and type the database name.
     - The database name must be unique, or the installation will fail.

7. On the **Configure** page, accept the default value **Use this local computer**.

   > [!NOTE]
   > If you're installing the management server and management database side by side, some options on this page aren't available. In this case, the appropriate options are selected by default and can't be changed.

8. On the initial **Create New Reporting Database** page, configure the **Microsoft SQL Server instance** and **Reporting Server database** by selecting the appropriate option below.

   - If you're using a *custom Microsoft SQL Server instance*:

     - Select **Use the custom instance**, and type the name of the instance.
     - Use the format **INSTANCENAME**. The assumed installation location is the local computer.
     - Not supported: A server name using the format `ServerName\INSTANCE`

   - If you're using a *custom database name*:

     - Select **Custom configuration** and type the database name.
     - The database name must be unique, or the installation will fail.

9. On the **Configure** page, accept the default value: **Use this local computer**.

   > [!NOTE]
   > If you're installing the management server and management database side by side, some options on this page aren't available. In this case, the appropriate options are selected by default and can't be changed.

10. On the **Configure** (Management Server Configuration) page, specify the following:

    - Type the AD group with sufficient permissions to manage the App-V environment. For example: `MyDomain\MyUser`

      After installation, you can add more users or groups by using the Management console. However, global security groups and Active Directory Domain Services (AD DS) distribution groups aren't supported. **Domain local** or **Universal** groups are required to perform this action.

    - **Website name**: Specify the custom name that runs the publishing service. If you don't have a custom name, don't make any changes.

    - **Port binding**: Specify a unique port number that will be used by App-V. For example: `12345`. Make sure that the port specified isn't used by another website.

11. On the **Configure** **Publishing Server Configuration** page, specify the following:

    - Specify the URL for the management service. For example: `https://localhost:12345`

    - **Website name**: Specify the custom name that is used to run the publishing service. If you don't have a custom name, don't make any changes.

    - **Port binding**: Specify a unique port number that will be used by App-V. For example: `54321`. Make sure that the port specified isn't used by another website.

12. On the **Reporting Server** page, specify the following:

    - **Website name**: Specify the custom name that runs the reporting service. If you don't have a custom name, don't make any changes.

    - **Port binding**: Specify a unique port number that will be used by App-V. For example: `55555`. Make sure that the port specified isn't used by another website.

13. To start the installation, select **Install** on the **Ready** page, and then select **Close** on the **Finished** page.

14. To verify that the setup completed successfully, open a web browser, and type the following URL:

    `https://<Management server machine name>:<Management service port number>/Console.html`

    For example: `https://localhost:12345/console.html`. If the installation succeeded, the App-V Management console is displayed with no errors.

## Related information

[Deploying App-V 5.1](deploying-app-v-51.md)

[How to Install the Management and Reporting Databases on Separate Computers from the Management and Reporting Services](how-to-install-the-management-and-reporting-databases-on-separate-computers-from-the-management-and-reporting-services51.md)

[How to Install the Publishing Server on a Remote Computer](how-to-install-the-publishing-server-on-a-remote-computer51.md)

[How to Deploy the App-V 5.1 Server Using a Script](how-to-deploy-the-app-v-51-server-using-a-script.md)
