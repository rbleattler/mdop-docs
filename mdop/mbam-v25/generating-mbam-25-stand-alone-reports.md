---
title: Generating MBAM 2.5 stand-alone reports
description: When you configure Microsoft BitLocker Administration and Monitoring (MBAM) with the stand-alone topology, you can generate reports to monitor BitLocker drive encryption usage and compliance.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/01/2016
---

# Generating MBAM 2.5 stand-alone reports

When you configure Microsoft BitLocker Administration and Monitoring (MBAM) with the stand-alone topology, you can generate reports to monitor BitLocker drive encryption usage and compliance.

For descriptions of the stand-alone reports, see [Understanding MBAM 2.5 stand-alone reports](understanding-mbam-25-stand-alone-reports.md).

> [!NOTE]
> To run the reports, you must be a member of the **MBAM Report Users** group, which you configure in Active Directory Domain Services. For more information, see [Planning for MBAM 2.5 groups and accounts](planning-for-mbam-25-groups-and-accounts.md).

## <a href="" id="bkmk-openadmin"></a> To open the Administration and Monitoring website

1.  Open a web browser and navigate to the Administration and Monitoring website. The default URL for the Administration and Monitoring website is:

    `https://<MBAMAdministrationServerName>:<port>/Helpdesk`

2.  In the left pane, select **Reports**. From the top menu bar, select the report you want to run.

    MBAM client data is retained in the Compliance and Audit Database for historical reference in case a computer is lost or stolen. When running enterprise reports, we recommend that you use appropriate start and end dates to scope the time frames for the reports from one to two weeks to increase reporting data accuracy.

    After you generate a report, you can save the results in different formats, such as HTML, Microsoft Word, and Microsoft Excel.

    > [!NOTE]
    > Configure SQL Server Reporting Services (SSRS) to use Secure Sockets Layer (SSL) before configuring the Administration and Monitoring website. If you don't configure SSRS to use SSL, when you configure the Administration and Monitoring website the URL for the Reports is set to HTTP instead of HTTPS. If you then go to the Administration and Monitoring website and select a report, the following message displays: "Only Secure Content is Displayed." To show the report, select **Show All Content**.

## <a href="" id="bkmk-enterprise"></a>To generate an Enterprise Compliance Report

1.  From the Administration and Monitoring Website, select the **Reports** node from the left navigation pane, select **Enterprise Compliance Report**, and select the filters that you want to use. The available filters for the Enterprise Compliance Report are:

    -   **Compliance Status**. Use this filter to specify the compliance status types of the report (for example, Compliant or Noncompliant).

    -   **Error State**. Use this filter to specify the error state types of the report (for example, No Error or Error).

2.  Select **View Report** to display the selected report.

3.  Select a computer name to view information about the computer in the Computer Compliance Report.

4.  To view information about the volumes on the computer, select the plus sign (`+`) next to the computer name.

## <a href="" id="bkmk-computercomp"></a>To generate a Computer Compliance Report

1.  From the Administration and Monitoring Website, select the **Report** node from the left navigation pane, and then select **Computer Compliance Report**. Use the Computer Compliance Report to search for **User name** or **Computer name**.

2.  Select **View Report** to view the Computer Compliance Report.

3.  Select a computer name to display more information about the computer in the Computer Compliance Report.

4.  To view information about the volumes on the computer, select the plus sign (`+`) next to the computer name.

    > [!NOTE]
    > If the computer matches or exceeds the requirements of the MBAM group policy settings, an MBAM client computer is considered compliant.

## <a href="" id="bkmk-recoverykey"></a> To generate a Recovery Key Audit Report

1.  From the Administration and Monitoring Website, select the **Report** node in the left navigation pane, and then select **Recovery Audit Report**. Select the filters for your Recovery Key Audit Report. The available filters for recovery key audits are as follows:

    -   **Helpdesk User**. This filter enables users to specify the user name of the requester. The requester is the person in the Help Desk who accessed the key on behalf of an end user.

    -   **End User**. This filter enables you to specify the user name of the user who called the Help Desk to obtain a recovery key.

    -   **Request Result**. This filter enables users to specify the request result types (for example, Success or Failed) that they want to base the report on. For example, users might want to view failed key access attempts.

    -   **Key Type**. This filter enables users to specify the key type that they want to base the report on. For example, for example, Recovery Key Password or TPM Password Hash.

    -   **Start Date**. This filter is used to define the Start Date part of the date range that the user wants to report on.

    -   **End Date**. This filter is used to define the End Date part of the date range that the users want to report on.

2.  Select **View Report** to view the report.

## Related articles

[Monitoring and reporting BitLocker compliance with MBAM 2.5](monitoring-and-reporting-bitlocker-compliance-with-mbam-25.md)

[Understanding MBAM 2.5 stand-alone reports](understanding-mbam-25-stand-alone-reports.md)
