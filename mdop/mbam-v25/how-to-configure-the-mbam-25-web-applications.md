---
title: How to configure the MBAM 2.5 web applications
description: This article explains two methods to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 web applications for the recommended High-level architecture.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to configure the MBAM 2.5 web applications

This article explains how to configure the Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 web applications for the recommended [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md) by using one of the following methods:

- A Windows PowerShell cmdlet.

- The MBAM Server Configuration wizard.

The web applications comprise the following websites and their corresponding web services:

- **Administration and Monitoring Website**: Website where specified users can view reports and help users recover their computers when they forget their PIN or password.
- **Self-Service Portal**: Website that users can access to independently regain access to their computers if they forget their PIN or password.

## Before you start the configuration

- Review the recommended architecture for MBAM. For more information, see [High-level architecture for MBAM 2.5](high-level-architecture-for-mbam-25.md).
- Review the supported configurations for MBAM. For more information, see [MBAM 2.5 supported configurations](mbam-25-supported-configurations.md).
- Complete the required prerequisites on each server. Ensure that you configure SQL Server Reporting Services (SSRS) to use the Secure Sockets Layer (SSL) before you configure the Administration and Monitoring Website. Otherwise, the Reports feature uses HTTP instead of HTTPS. For more information, see [MBAM 2.5 server prerequisites for stand-alone and Configuration Manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md) and [MBAM 2.5 server prerequisites that apply only to the Configuration Manager integration topology](mbam-25-server-prerequisites-that-apply-only-to-the-configuration-manager-integration-topology.md) (if applicable).
- Register service principal names (SPNs) for the application pool account for the websites. You need to do this step only if you don't have administrative domain rights in Active Directory Domain Services (ADDS). If you do have these rights in ADDS, MBAM creates the SPNs for you. For more information, see [Planning how to secure the MBAM websites](planning-how-to-secure-the-mbam-websites.md#bkmk-regvirtualspn).
- Install the MBAM Server software on each server where you'll configure an MBAM Server feature. If you plan to install the websites on one server, and the web services on another, you can configure them only by using the **Enable-MbamWebApplication** Windows PowerShell cmdlet. The MBAM Server Configuration wizard doesn't support configuring these items on separate servers. For more information, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).
- Review the prerequisites for using Windows PowerShell if you plan to use cmdlets to configure MBAM Server features. For more information, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md).

## To configure the web applications by using Windows PowerShell

1.  Before you start the configuration, see [Configuring MBAM 2.5 server features by using Windows PowerShell](configuring-mbam-25-server-features-by-using-windows-powershell.md) to review the prerequisites for using Windows PowerShell.

2.  Use the **Enable-MbamWebApplication** cmdlet to configure the web applications using Windows PowerShell. To get information about this cmdlet, type **Get-Help Enable-MbamWebApplication**.

## To configure the settings for all web applications using the wizard

1. On the server where you want to configure the web applications, start the MBAM Server Configuration wizard. You can select **MBAM Server Configuration** from the **Start** menu to open the wizard.

2. Select **Add New Features**, select **Administration and Monitoring Website** and **Self-Service Portal**, and then select **Next**. The wizard checks that the server meets all prerequisites for the web applications.

3. If the prerequisite check is successful, select **Next** to continue. Otherwise, resolve any missing prerequisites, and then select **Check prerequisites again**.

4. Use the following descriptions to enter the field values in the wizard.

    | Field | Description |
    |--|--|
    | Security certificate | Select a previously created certificate to optionally encrypt the communication between the web services and the server on which you're configuring the websites. If you choose **Do not use a certificate**, your web communication might not be secure. |
    | Host name | Name of the host computer where you're configuring the websites. |
    | Installation path | Path where you're installing the websites. |
    | Port | Port number to use for website and service communication. **Note:** You must set a firewall exception to enable communication through the specified port. |
    | Web service application pool domain account and password | Domain user account and password for the web service application pool. If you enter a user name in the **Read/write access domain user or group** field on the **Configure Databases** page, you must enter that same value in this field. If you enter a group name in the **Read/write access domain user or group** field on the **Configure Databases** page, the value you enter in this field must be a member of that group. If you don't specify credentials, it uses the credentials that you specified for any previously enabled web application. All web applications must use the same application pool credentials. If you specify different credentials for different web applications, it uses the most recently specified value. **Important:** For improved security, set the account that's specified in the credentials to have limited user rights. Also, set the password of the account to never expire. |

5. Verify that the built-in IIS\_IUSRS account or the application pool account has been added to the **Impersonate a client after authentication** and the **Log on as a batch job** local security settings.

   To check whether it has been added to the local security settings, open the **Local Security Policy editor**, expand the **Local Policies** node, select the **User Rights Assignment** node, and double-click **Impersonate a client after authentication** and **Log on as a batch job** policies in the right pane.

## To configure connection information for the databases by using the wizard

1.  Use the following field descriptions to configure the connection information in the wizard for the Compliance and Audit Database.

   | Field                      | Description                                                   |
   |----------------------------|---------------------------------------------------------------|
   | SQL Server name            | Name of the server where the Compliance and Audit Database is configured. |
   | SQL Server database instance | SQL Server instance name where the Compliance and Audit Database is configured. |
   | Database name              | Name of the Compliance and Audit Database.                    |

2.  Use the following field descriptions to configure the connection information in the wizard for the Recovery Database.

   | Field                      | Description                                           |
   |----------------------------|-------------------------------------------------------|
   | SQL Server name            | Name of the server where the Recovery Database is configured. |
   | SQL Server database instance | SQL Server instance name where the Recovery Database is configured. |
   | Database name              | Name of the Recovery Database.                        |

## To configure the web applications by using the wizard

1. Use the following descriptions to enter the field values in the wizard to configure the Administration and Monitoring website.

   - **Advanced Helpdesk role domain group**: Domain user group whose members have access to all areas of the Administration and Monitoring website except the Reports area.
   - **Helpdesk role domain group**: Domain user group whose members have access to the **Manage TPM** and **Drive Recovery** areas of the Administration and Monitoring website.
   - **Use System Center Configuration Manager Integration**: If you're configuring MBAM with the Configuration Manager integration topology, select this option. It makes all reports, except the Recovery Audit report, appear in Configuration Manager instead of in the Administration and Monitoring website.
   - **Reporting role domain group**: Domain user group whose members have read-only access to the Reports area of the Administration and Monitoring website.
   - **SQL Server Reporting Services URL**: URL for the SSRS server where the MBAM Reports are configured. Examples of report URLs:

     | Type of host name                          | Example                                           |
     |--------------------------------------------|---------------------------------------------------|
     | Example with a fully qualified domain name | `https://MyReportServer.Contoso.com/ReportServer`   |
     | Example with a custom host name            | `https://MyReportServer/ReportServer`               |

   - **Virtual directory**: Virtual directory of the Administration and Monitoring Website. This name corresponds to the website's physical directory on the server and is appended to the website's host name, for example:
     - `https://<hostname>:<port>/HelpDesk/`
     - If you don't specify a virtual directory, it uses the value **HelpDesk**.
   - **Data Migration role domain group** (optional): Domain user group whose members have access to use the `Write-Mbam*Information` Cmdlets to write recovery information via this endpoint.

2. Use the following description to enter the field values in the wizard to configure the Self-Service Portal.

    | Field | Description |
    |--|--|
    | Virtual directory | Virtual directory of the web application. This name corresponds to the website's physical directory on the server, and is appended to the website's host name, for example: `https://<hostname>:<port>/SelfService/`. If you don't specify a virtual directory, it uses the value **SelfService**. |
    | Company name | Specify a company name for the Self-Service Portal, for example: Contoso IT. All Self-Service Portal users see this company name. |
    | Helpdesk URL text | Specify a text statement that directs users to your organization's Helpdesk website, for example: Contact Helpdesk or IT department. |
    | Helpdesk URL | Specify the URL for your organization's Helpdesk website, for example: `https://<companyHelpdeskURL>/`. |
    | Notice text file | Select a file that contains the notice you want displayed to users on the Self-Service Portal landing page. |
    | Don't display notice text to users | Select this check box to specify that the notice text isn't displayed to users. |

3. When you finish your entries, select **Next**.

    The wizard checks that the server meets all prerequisites for the web applications.

4. Select **Next** to continue.

5. On the **Summary** page, review the features that will be added.

    > [!NOTE]
    > To create a Windows PowerShell script for the entries you made, click **Export PowerShell Script** and save the script.

6. Select **Add** to add the web applications to the server, and then select **Close**.

    To customize the Self-Service Portal by adding custom notice text, your company name, pointers to more information, and so on, see [Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md).

## To configure the Self-Service Portal if client computers can't access the CDN

1.  Determine whether you're running Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1. If so, do nothing. Your Self-Service Portal configuration is complete.

    > [!NOTE]
    > Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 SP1 installs the JavaScript files in setup, and so doesn't need to be connected to the Microsoft content delivery network in order to configure the Self-Service Portal. The following steps are necessary only if you are using a version of Microsoft BitLocker Administration and Monitoring (MBAM) 2.5 previous to SP1.

2.  Determine if your client computers have access to the Microsoft content delivery network (CDN).

    The CDN gives the Self-Service Portal the access it requires to certain JavaScript files. If you don't configure the Self-Service Portal when client computers can't access the CDN, only the company name and the account under which the end user signed in will be displayed. No error message is shown.

3.  Do one of the following actions:

    -   If your client computers have access to the CDN, do nothing. Your Self-Service Portal configuration is complete.

    -   If your client computers don't have access to the CDN, complete the steps in [How to configure the Self-Service Portal when client computers can't access the Microsoft content delivery network](how-to-configure-the-self-service-portal-when-client-computers-cannot-access-the-microsoft-content-delivery-network.md).

## Related articles

[Server event logs](server-event-logs.md)

[Configuring the MBAM 2.5 server features](configuring-the-mbam-25-server-features.md)

[How to configure the Self-Service Portal when client computers can't access the Microsoft content delivery network](how-to-configure-the-self-service-portal-when-client-computers-cannot-access-the-microsoft-content-delivery-network.md)

[Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md)

[Validating the MBAM 2.5 server feature configuration](validating-the-mbam-25-server-feature-configuration.md)
