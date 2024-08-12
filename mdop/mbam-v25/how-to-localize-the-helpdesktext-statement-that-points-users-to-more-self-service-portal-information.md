---
title: How to localize the `HelpdeskText` statement that points users to more Self-Service Portal information
description: You can configure a localized version of the Self-Service Portal "HelpdeskText" statement, which informs users about how to get help when they use the Self-Service Portal.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to localize the `HelpdeskText` statement that points users to more Self-Service Portal information

You can configure a localized version of the Self-Service Portal "HelpdeskText" statement, which informs users about how to get help when they use the Self-Service Portal. If you configure localized text for the statement, as described in the following instructions, MBAM displays the localized version. If MBAM doesn't find the localized version, it displays the value that is in the **HelpdeskText** parameter.

> [!NOTE]
> In the following instructions, *SelfService* is the default virtual directory name for the Self-Service Portal. You might have used a different name when you configured the Self-Service Portal.

## To display a localized version of the `HelpdeskText` statement

1.  On the server where you configured the Self-Service Portal, browse to **Sites** &gt; **Microsoft BitLocker Administration and Monitoring** &gt; **SelfService** &gt; **Application Settings**.

2.  In the **Actions** pane, select **Add** to open the **Add Application Setting** dialog box.

3.  In the **Name** field, type **HelpdeskText**\_&lt;*Language*&gt;, where &lt;*Language*&gt; is the appropriate language code for the text.

    For example, to create a localized HelpdeskText statement in Spanish-Spain, name the parameter **HelpdeskText\_es-es**.

    The name of the Language folder can also be the language neutral name **es** instead of **es-es**. If the end user's browser is set to **es-es** and that folder doesn't exist, the parent locale (as defined in .NET) is recursively retrieved and checked, resolving to &lt;MBAM Self-Service Install Directory&gt;\\SelfServiceWebsite\\es\\Notice.txt before finally becoming the default Notice.txt file. This recursive fallback mimics the .NET resource loading rules.

    For a list of the valid language codes you can use, see [Windows Language Code Identifier (LCID) Reference](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).

4.  In the **Value** field, type the localized text that you want to display to end users.

## Related articles

[Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md)
