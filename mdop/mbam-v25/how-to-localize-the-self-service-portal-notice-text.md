---
title: How to localize the Self-Service Portal notice text
description: You can configure localized notice text to display to users by default in the Self-Service Portal.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# How to localize the Self-Service Portal notice text

You can configure localized notice text to display to users by default in the Self-Service Portal. The Notice.txt file that displays the notice text is in the following root directory:

`<MBAM Self-Service Install Directory>\Self Service Website\`

To display localized notice text, you create a localized Notice.txt file, and then save it under a specific language folder in the following example directory:

`<MBAM Self-Service Install Directory>\Self Service Website\`

> [!NOTE]
> You can configure the path by using the **NoticeTextPath** item in **Application Settings**.



MBAM displays the notice text, based on the following rules:

- If you create a localized **Notice.txt** file in the appropriate language folder, MBAM displays the localized notice text if the default **Notice.txt** file exists. If the default **Notice.txt** file is missing, a message displays indicating that the default file is missing.

- If MBAM doesn't find a localized version of the Notice.txt file, it displays the text in the default Notice.txt file.

- If MBAM doesn't find a default Notice.txt file, it displays the default text in the Self-Service Portal.

> [!NOTE]
> If an user's browser is set to a language that doesn't have a corresponding language subfolder or Notice.txt, the text in the Notice.txt file in the following root directory is displayed:
>
> `<MBAM Self-Service Install Directory>\Self Service Website\`

## To create a localized Notice.txt file

1.  On the server where you configured the Self-Service Portal, create a <*Language*> folder in the following example directory, where <*Language*> represents the name of the localized language:

    `<MBAM Self-Service Install Directory>\Self Service Website\`

    > [!NOTE]
    > Some language folders already exist, so you might not have to create a folder. If you do have to create a language folder, see [Windows Language Code Identifier (LCID) Reference](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c) for a list of the valid names that you can use for the <*Language*> folder.

2.  Create a Notice.txt file that contains the localized notice text.

3.  Save the Notice.txt file in the `<Language>` folder. For example, to create a localized Notice.txt file in Spanish-Spain, save the localized Notice.txt file in the following example directory:

    `<MBAM Self-Service Install Directory>\Self Service Website\Es-es`

    The name of the Language folder can also be the language neutral name `es` instead of `es-es`. If the user's browser is set to `es-es` and that folder doesn't exist, the parent locale (as defined in .NET) is recursively retrieved and checked, resolving to `<MBAM Self-Service Install Directory>\SelfServiceWebsite\es\Notice.txt` before finally becoming the default Notice.txt file. This recursive fallback mimics the .NET resource loading rules.

## Related articles

[Customizing the Self-Service Portal for your organization](customizing-the-self-service-portal-for-your-organization.md)
