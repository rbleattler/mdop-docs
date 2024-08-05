---
title: How to install the management server on a standalone computer and connect it to the database
description: To install the management server on a standalone computer and connect it to the database, follow these steps.
author: aczechowski
ms.date: 04/18/2018
---

# How to install the management server on a standalone computer and connect it to the database

>Applies to: Windows 10, Windows 11, Windows Server 2016

To install the management server on a standalone computer and connect it to the database, follow these steps.

1. Copy the App-V server installation files to the computer on which you want to install it on. To start the App-V server installation, run **appv\_server\_setup.exe** as an administrator, then select **Install**.

1. On the **Getting Started** page, review and accept the license terms, then select **Next**.

1. On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, to enable Microsoft Update, select **Use Microsoft Update when I check for updates (recommended)**. To disable Microsoft Update, select **I don't want to use Microsoft Update**, then select **Next**.

1. On the **Feature Selection** page, select the **Management Server** checkbox, then select **Next**.

1. On the **Installation Location** page, accept the default location, then select **Next**.

1. On the **Configure Existing Management Database** page, select **Use a remote SQL Server**, then enter the computer running Microsoft SQL's machine name, such as ```SqlServerMachine```.

  > [!NOTE]
  >If the Microsoft SQL Server is deployed on the same server, select **Use local SQL Server**. For the SQL Server Instance, select **Use the default instance**. If you are using a custom Microsoft SQL Server instance, you must select **Use a custom instance**, then enter the instance's name. Specify the **SQL Server Database name** that this management server will use, such as ```AppvManagement```.

1. On the **Configure management server configuration** page, specify the following items:

   - The AD group or account that will connect to the management console for administrative purposes for example **MyDomain\\MyUser** or **MyDomain\\AdminGroup**. The account or AD group you specify will be enabled to manage the server through the management console. You can add additional users or groups using the management console after installation
   - The **Website Name** you want to use for the management service. Accept the default if you do not have a custom name.
   - For the **Port Binding**, specify a unique port number, such as **12345**.

1. Select **Install**.

1. To confirm that the setup has completed successfully, open a web browser and enter the following URL: `https://managementserver:portnumber/Console`. If the installation was successful, you should see the **Management Console** appear without any error messages or warnings displayed.

## Related articles

[Deploying App-V](appv-deploying-appv.md)
