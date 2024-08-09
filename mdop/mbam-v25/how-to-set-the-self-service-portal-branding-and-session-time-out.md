---
title: How to set the Self-Service Portal branding and session time-out
description: After you configure the Self-Service Portal, you can brand it with your company name, Help Desk URL, and "notice" text.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to set the Self-Service Portal branding and session time-out

After you configure the Self-Service Portal, you can brand it with your company name, Help Desk URL, and "notice" text. You can also change the Session Time-out setting to make the end user's session expire after a specified period of inactivity.

> [!NOTE]
> You can also brand the Self-Service Portal by using the **Enable-MbamWebApplication** Windows PowerShell cmdlet or the MBAM Server Configuration wizard. For instructions on using the wizard, see [How to configure the MBAM 2.5 web applications](how-to-configure-the-mbam-25-web-applications.md).

> [!NOTE]
> In the following instructions, *SelfService* is the default virtual directory name for the Self-Service Portal. You might have used a different name when you configured the Self-Service Portal.

## To set the session time-out and branding for the Self-Service Portal

1.  To set the time-out period for the end user's session, start the **Internet Information Services Manager**, or run **inetmgr.exe**.

2.  Browse to **Sites** &gt; **Microsoft BitLocker Administration and Monitoring** &gt; **SelfService** &gt; **ASP.NET** &gt; **Session State**, and change the **Time-out** value under **Cookie Settings** to the number of minutes after which the end user's Self-Service Portal session expires. The default value is **5**. To disable the setting so that there's no time-out, set the value to **0**.

3.  To set the branding items for the Self-Service Portal, start the **Internet Information Services Manager** or run **inetmgr.exe**.

4.  Browse to **Sites** &gt; **Microsoft BitLocker Administration and Monitoring** &gt; **SelfService** &gt; **Application Settings**.

5.  In the **Name** column, select the item that you want to change, and change the default value to reflect the name that you want to use. The following table lists the values that you can set.

    > [!CAUTION]
    > Don't change the value in the Name column (CompanyName\*), as it causes Self-Service Portal to stop working.

| Name | Default value |
|--|--|
| ClientValidationEnabled | true |
| CompanyName | Contoso IT |
| DisplayNotice | true |
| HelpdeskText | Contact Helpdesk or IT Department |
| HelpdeskUrl | `#` <br> **Note:** In MBAM 2.5 SP1, the HelpdeskUrl default value is empty. |
| jQueryPath | [Download jquery-1.10.2.min.js](https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js) <br> **Note:** In MBAM 2.5 SP1, this file is a local JavaScript file shipped with the product, located at `~/Scripts/jquery-1.10.2.min.js`. |
| jQueryValidatePath | [Download jquery.validate.min.js](https://ajax.aspnetcdn.com/ajax/jquery.validate/1.11.1/jquery.validate.min.js) <br> **Note:** In MBAM 2.5 SP1, this file is a local JavaScript file shipped with the product, located at `~/Scripts/jquery.validate.min.js`. |
| jQueryValidateUnobtrusivePath | [Download jquery.validate.unobtrusive.min.js](https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js) <br> **Note:** In MBAM 2.5 SP1, this file is a local JavaScript file shipped with the product, located at `~/Scripts/jquery.validate.unobtrusive.min.js`. |
| NoticeTextPath | Notice.txt <br> **Note:** You can edit the notice text either by using the Internet Information Services (IIS) Manager or by opening and changing the Notice.txt file in the installation directory. |
| UnobtrusiveJavaScriptEnabled | true |

## Related articles

[Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md)
