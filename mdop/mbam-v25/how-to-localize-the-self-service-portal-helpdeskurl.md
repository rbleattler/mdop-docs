---
title: How to localize the Self-Service Portal `HelpdeskURL`
description: You can configure a localized version of the Self-Service Portal URL to display to end users by default. The Self-Service Portal URL is represented by the parameter HelpdeskURL.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to localize the Self-Service Portal `HelpdeskURL`

You can configure a localized version of the Self-Service Portal URL to display to end users by default. The Self-Service Portal URL is represented by the parameter **HelpdeskURL**.

If you create a localized version, as described in the following instructions, Microsoft BitLocker Administration and Monitoring (MBAM) finds and displays the localized version. If MBAM doesn't find a localized version, it displays the URL that is configured for the parameter **HelpDeskURL**.

> [!NOTE]
> In the following instructions, *SelfService* is the default virtual directory name for the Self-Service Portal. You might have used a different name when you configured the Self-Service Portal.

## To localize the Self-Service Portal URL

1.  On the server where you configured the Self-Service Portal, browse to **Sites** &gt; **Microsoft BitLocker Administration and Monitoring** &gt; **SelfService** &gt; **Application Settings**.

2.  In the **Actions** pane, select **Add** to open the **Add Application Setting** dialog box.

3.  In the **Name** field, type `HelpdeskURL_<Language>`, where `<Language>` is the appropriate language code for the URL.

    For example, to create a localized version of the `HelpdeskURL` value in Spanish-Spain, name the parameter `HelpdeskURL_es-es`.

    The name of the Language folder can also be the language neutral name `es` instead of `es-es`. If the user's browser is set to `es-es` and that folder doesn't exist, the parent locale (as defined in .NET) is recursively retrieved and checked, resolving to `<MBAM Self-Service Install Directory>\SelfServiceWebsite\es\Notice.txt` before finally becoming the default Notice.txt file. This recursive fallback mimics the .NET resource loading rules.

    For a list of the valid language codes you can use, see [Windows Language Code Identifier (LCID) Reference](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).

4.  In the **Value** field, type the localized version of the `HelpdeskURL` value that you want to display to end users.

## Related articles

[Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md)
