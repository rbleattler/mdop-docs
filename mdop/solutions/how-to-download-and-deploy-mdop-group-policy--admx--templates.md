---
title: How to Download and Deploy MDOP Group Policy (.admx) Templates
description: How to Download and Deploy MDOP Group Policy (.admx) Templates
author: aczechowski
ms.assetid: fdb64505-6c66-4fdf-ad74-a6a161191e3f
ms.reviewer:
ms.author: aaroncz
ms.pagetype: mdop
ms.mktglfcycl: deploy
ms.sitesec: library
ms.date: 06/15/2018
---


# How to Download and Deploy MDOP Group Policy (.admx) Templates


You can manage the feature settings of certain Microsoft Desktop Optimization Pack (MDOP) technologies (for example, App-V, UE-V, or MBAM) by using Group Policy templates, the .admx and .adml files. MDOP Group Policy templates are available for download in a self-extracting, compressed file, grouped by technology and version.

## MDOP Group Policy templates

**How to download and deploy the MDOP Group Policy templates**

1. Download the latest [MDOP Group Policy templates](https://www.microsoft.com/download/details.aspx?id=55531)

2. Expand the downloaded .cab file by running `expand <download_folder>\MDOP_ADMX_Templates.cab -F:* <destination_folder>`

   > [!WARNING]  
   > Do not extract the templates directly to the Group Policy deployment directory. Multiple technologies and versions are bundled in this file.

3. In the extracted folder, locate the technology-version .admx file. Certain MDOP technologies have multiple sets of Group Policy Objects (GPOs). For example, MBAM includes MBAM Management settings and MBAM User settings.

4. Locate the appropriate .adml file by language-culture (that is, *en-us* for English-United States).

5. Copy the .admx and .adml files to a policy definition folder. Depending on where you store the templates, you can configure Group Policy settings from the local device or from any computer on the domain.

   - **Local files:** To configure Group Policy settings from the local device, copy template files to the following locations:

     | File type                                 | File location                                            |
     | ----------------------------------------  | -------------------------------------------------------- |
     | Group Policy template (.admx)             | `%systemroot%\policyDefinitions\`                        |
     | Group Policy language file (.adml)        | `%systemroot%\policyDefinitions\[MUIculture]`            |

   - **Domain central store:** To enable Group Policy settings configuration by a Group Policy administrator from any computer on the domain, copy files to the following locations on the domain controller:

     | File type | File location |
     | --------- | ------------- |
     | Group Policy template (.admx) | `%systemroot%\sysvol\domain\policies\PolicyDefinitions\` |
     | Group Policy language file (.adml) | `%systemroot%\sysvol\domain\policies\PolicyDefinitions\[MUIculture]` <br> For example, the U.S. English ADML language-specific file will be stored in `%systemroot%\sysvol\domain\policies\PolicyDefinitions\en-us`. |

6. Edit the Group Policy settings using Group Policy Management Console (GPMC) or Advanced Group Policy Management (AGPM) to configure Group Policy settings for the MDOP technology.

### MDOP Group Policy by technology

For more information about supported MDOP Group Policy, see the specific documentation for the technology.

| MDOP Technology | Version bundles | Notes |
| --------------- | --------------- | ----- |
| **Application Virtualization (App-V)** | App-V 5.0 and App-V 5.0 Service Packs | [How to Modify App-V 5.0 Client Configuration Using the ADMX Template and Group Policy](../appv-v5/how-to-modify-app-v-50-client-configuration-using-the-admx-template-and-group-policy.md) |
| **User Experience Virtualization (UE-V)** | UE-V 2.0 and UE-V 2.1 | [Configuring UE-V 2.x with Group Policy Objects](../uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2.md) |
| &nbsp; | UE-V 1.0 including 1.0 SP1 | [Configuring UE-V with Group Policy Objects](../uev-v1/configuring-ue-v-with-group-policy-objects.md) |
| **Microsoft BitLocker Administration and Monitoring (MBAM)** | MBAM 2.5 | [Planning for MBAM 2.5 Group Policy Requirements](../mbam-v25/planning-for-mbam-25-group-policy-requirements.md) |
| &nbsp; | MBAM 2.0 including 2.0 SP1 | [Planning for MBAM 2.0 Group Policy Requirements](../mbam-v2/planning-for-mbam-20-group-policy-requirements-mbam-2.md) |
| &nbsp; | MBAM 1.0 | [How to Edit MBAM 1.0 GPO Settings](/previous-versions/windows/microsoft-desktop-optimization-pack/mbam-v1/how-to-edit-mbam-10-gpo-settings) |
