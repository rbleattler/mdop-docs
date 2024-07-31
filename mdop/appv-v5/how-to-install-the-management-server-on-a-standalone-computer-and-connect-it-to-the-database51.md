---
title: Install the management server on a standalone computer and connect it to the database
description: Use the following procedure to install the management server on a standalone computer and connect it to the database.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# Install the management server on a standalone computer and connect it to the database

Use the following procedure to install the management server on a standalone computer and connect it to the database.

## To install the management server on a standalone computer and connect it to the database

1.  Copy the App-V 5.1 server installation files to the computer on which you want to install it on. To start the App-V 5.1 server installation right-click and run **appv\_server\_setup.exe** as an administrator. Click **Install**.

2.  On the **Getting Started** page, review and accept the license terms, and click **Next**.

3.  On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, to enable Microsoft updates, select **Use Microsoft Update when I check for updates (recommended).** To disable Microsoft updates, select **I don't want to use Microsoft Update**. Click **Next**.

4.  On the **Feature Selection** page, select the **Management Server** checkbox and click **Next**.

5.  On the **Installation Location** page, accept the default location and click **Next**.

6.  On the **Configure Existing Management Database** page, select **Use a remote SQL Server**, and type the machine name of the computer running Microsoft SQL SQL, for example **SqlServerMachine**.

    > [!NOTE]
    > If the Microsoft SQL Server is deployed on the same server, select **Use local SQL Server**.


For the SQL Server Instance, select **Use the default instance**. If you are using a custom Microsoft SQL Server instance, you must select **Use a custom instance** and then type the name of the instance.

Specify the **SQL Server Database name** that this management server will use, for example **AppvManagement**.


7. On the **Configure Management Server Configuration** page, specify the AD group or account that will connect to the management console for administrative purposes for example **MyDomain\\MyUser** or **MyDomain\\AdminGroup**. The account or AD group you specify will be enabled to manage the server through the management console. You can add additional users or groups using the management console after installation

   Specify the **Website Name** that you want to use for the management service. Accept the default if you do not have a custom name. For the **Port Binding**, specify a unique port number to be used, for example **12345**.

8. Click **Install**.

9. To confirm that the setup has completed successfully, open a web browser, and type the following URL: http://managementserver:portnumber/Console. If the installation was successful, you should see the **Management Console** appear without any error messages or warnings being displayed.

## Related topics

[App-V 5.1 Deployment Checklist](app-v-51-deployment-checklist.md)
