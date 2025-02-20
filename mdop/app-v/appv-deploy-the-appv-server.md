---
title: How to deploy the App-V Server (Windows 10/11)
description: Use these instructions to deploy the Application Virtualization (App-V) Server in App-V for Windows 10/11.
author: aczechowski
ms.date: 04/18/2018
---

# How to deploy the App-V Server (new installation)

>Applies to: Windows 10, Windows 11, Windows Server 2016

## Before you start

>[!IMPORTANT]
>If you're already using App-V 5.x, you don't need to re-deploy the App-V server components as they haven't changed since App-V 5.0 was released.

* Make sure that you install the [App-V prerequisites](appv-prerequisites.md).
* Review the server section of [App-V security considerations](appv-security-considerations.md).
* Specify a port where the server hosts each component.
* Add firewall rules to allow incoming requests to access the specified ports.
* If you use SQL scripts instead of the Windows Installer to set up the Management database or Reporting database, you must run the required SQL scripts before installing the Management Server or Reporting Server. See [How to deploy the App-V databases by using SQL scripts](appv-deploy-appv-databases-with-sql-scripts.md).

## Installing the App-V server

1. Download the App-V server components. All five App-V server components are included in the Microsoft Desktop Optimization Pack (MDOP) 2015 ISO package, which can be downloaded from either of the following locations:

    * If you have a Microsoft Visual Studio subscription, use the [Visual Studio subscriptions site](https://my.visualstudio.com/downloads) to download the MDOP ISO package.
    * If you're using [Windows client for Enterprise or Education](https://www.microsoft.com/windows/business), download it from the [Microsoft Microsoft 365 admin center](https://admin.microsoft.com/adminportal/home#/subscriptions/vlnew).

2. Copy the App-V server installation files to the computer on which you want to install it.

3. Start the App-V server installation by right-clicking and running **appv\_server\_setup.exe** as an administrator, and then select **Install**.

4. Review and accept the license terms, and choose whether to enable Microsoft updates.

5. On the **Feature Selection** page, select all components listed in the following table.

    | Component | Description |
    |---|---|
    | Management server | Provides overall management functionality for the App-V infrastructure. |
    | Management database | Facilitates database predeployments for App-V management. |
    | Publishing server | Provides hosting and streaming functionality for virtual applications. |
    | Reporting server | Provides App-V reporting services. |
    | Reporting database | Facilitates database predeployments for App-V reporting. |

6. On the **Installation Location** page, accept the default location where the selected components will be installed, or change the location by typing a new path on the **Installation Location** line.

7. On the initial **Create New Management Database** page, configure the **Microsoft SQL Server instance** and **Management Server database** by selecting the appropriate option from the following table:

    | Method | What you need to do |
    |---|---|
    | You use a custom Microsoft SQL Server instance. | Select **Use the custom instance**, then specify the instance name.<br/>Use the format **INSTANCENAME**. The assumed installation location is the local computer.<br/>Not supported: A server name using the format **ServerName**\\**INSTANCE**.|
    | You use a custom database name. | Select **Custom configuration** and type the database name.<br/>The database name must be unique, or the installation fails.|

8. On the **Configure** page, accept the default value, **Use this local computer**.

   > [!NOTE]
   > If you're installing the Management server and Management database side-by-side, the appropriate options are selected by default and cannot be changed.

9. On the initial **Create New Reporting Database** page, configure the **Microsoft SQL Server instance** and **Reporting Server database** by selecting the appropriate option from the following table:

    | Method | What you need to do |
    |---|---|
    | You use a custom Microsoft SQL Server instance. | Select **Use the custom instance**, and type the name of the instance.<br/>Use the format **INSTANCENAME**. The assumed installation location is the local computer.<br/>Not supported: A server name using the format **ServerName**\\**INSTANCE**.|
    | You use a custom database name. | Select **Custom configuration** and type the database name.<br/>The database name must be unique, or the installation fails.|

10. On the **Configure** page, accept the default value: **Use this local computer**.

    > [!NOTE]
    > If you're installing the Management server and Management database side-by-side, the appropriate options are selected by default and cannot be changed.

11. On the **Configure** (Management Server Configuration) page, specify the following:

    |  Item to configure | Description and examples |
    |---|---|
    | Specify AD group | Specify the AD group with sufficient permissions to manage the App-V environment. Example: MyDomain\MyUser<br><br/>After installation, you can add users or groups on the management console. However, global security groups and Active Directory Domain Services distribution groups aren't supported. You must use **Domain local** or **Universal** groups to perform this action.|
    |Website name | Specify the custom name that the server uses to run the publishing service.<br>If you don't have a custom name, you don't have to change it.|
    |Port binding | Specify a unique port number that App-V uses. Example: **12345**<br>Ensure that the port specified isn't used by another website. |

12. On the **Configure Publishing Server Configuration** page, specify the following:

    | Item to configure | Description and examples |
    |---|---|
    | Specify the management service URL | Example: http:<span></span>//localhost:12345 |
    | Website name | Specify the custom website name that the server uses to run the publishing service. <br>If you don't have a custom name, don't make any changes. |
    | Port binding | Specify a unique port number that App-V uses. Example: 54321<br>Ensure that the port specified isn't being used by another website. |

13. On the **Reporting Server** page, specify the following:

    | Item to configure | Description and examples |
    |---|---|
    | Website name | Specify the custom name that the server uses to run the Reporting Service.  <br>If you don't have a custom name, don't make any changes. |
    | Port binding | Specify a unique port number that App-V uses. Example: 55555<br/>Ensure that the port specified isn't being used by another website.|

14. To start the installation, select **Install** on the **Ready** page, and then select **Close** on the **Finished** page.

15. To verify that the setup completed successfully, open a web browser, and type the following URL with the bracketed variables adjusted according to your specifications in the earlier steps:

    `http://<Management server machine name>:<Management service port number>/console.html`

    Example: `http://localhost:12345/console.html`. If the installation succeeded, the App-V Management console displays with no errors.

## Related articles

* [App-V deployment checklist](appv-deployment-checklist.md)
* [How to install the management and reporting databases on separate computers from the management and reporting services](appv-install-the-management-and-reporting-databases-on-separate-computers.md)
* [How to install the publishing server on a remote computer](appv-install-the-publishing-server-on-a-remote-computer.md)
* [How to deploy the App-V server using a script](appv-deploy-the-appv-server-with-a-script.md)
