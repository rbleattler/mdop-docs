---
title: Copying the MBAM 2.5 group policy templates
description: Before deploying the Microsoft BitLocker Administration and Monitoring (MBAM) client installation, you must download the MBAM group policy templates, which contain group policy settings that define MBAM implementation settings for BitLocker Drive Encryption.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/28/2017
---

# Copying the MBAM 2.5 group policy templates

Before deploying the Microsoft BitLocker Administration and Monitoring (MBAM) client installation, you must download the MBAM group policy templates, which contain group policy settings that define MBAM implementation settings for BitLocker Drive Encryption. After downloading the templates, you then set the group policy settings to implement across your enterprise.

## Downloading and deploying the MDOP group policy templates

MDOP group policy templates are available for download in a self-extracting, compressed file, grouped by technology and version.

### How to download and deploy the MDOP group policy templates

1. Download the MDOP group policy templates from [Microsoft Desktop Optimization Pack group policy administrative templates](https://www.microsoft.com/download/details.aspx?id=55531).

2. Run the downloaded file to extract the template folders.

    > [!WARNING]
    > Don't extract the templates directly to the group policy deployment directory. Multiple technologies and versions are bundled in this file.

3. In the extracted folder, locate the technology-version .admx file. Certain MDOP technologies have multiple sets of group policy objects (GPOs). For example, MBAM includes MBAM management settings and MBAM user settings.

4. Locate the appropriate .adml file by language-culture. For example, `en` for English-United States.

5. Copy the .admx and .adml files to a policy definition folder. Depending on where you store the templates, you can configure group policy settings from the local device or from any computer on the domain.

    - **Local files.** To configure group policy settings from the local device, copy template files to the following locations:

      | File type | File location |
      |--|--|
      | Group policy template (.admx) | `%systemroot%\policyDefinitions` |
      | Group policy language file (.adml) | `%systemroot%\policyDefinitions\[MUIculture]` |

    - **Domain central store.** To enable group policy settings configuration by a group policy administrator from any computer on the domain, copy files to the following locations on the domain controller:

      | File type | File location |
      |--|--|
      | group policy template (.admx) | `%systemroot%\sysvol\domain\policies\PolicyDefinitions` |
      | group policy language file (.adml) | `%systemroot%\sysvol\domain\policies\PolicyDefinitions\[MUIculture]\[MUIculture]`<br>For example, the U.S. English ADML language-specific file is stored in `%systemroot%\sysvol\domain\policies\PolicyDefinitions\en-us`. |

6. Edit the group policy settings using Group Policy Management Console (GPMC) or Advanced Group Policy Management (AGPM) to configure group policy settings for the MDOP technology. For more information, see [Editing the MBAM 2.5 group policy Settings](editing-the-mbam-25-group-policy-settings.md).

   For descriptions of the group policy settings, see [Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md).

## Related articles

[Deploying MBAM 2.5 group policy objects](deploying-mbam-25-group-policy-objects.md)
