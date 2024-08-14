---
title: Working with custom UE-V 2.1 SP1 templates and the UE-V 2.1 SP1 generator
description: To synchronize application settings between user computers, Microsoft User Experience Virtualization (UE-V) 2.1 SP1 uses settings location templates.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 08/30/2016
---

# Working with custom UE-V 2.1 SP1 templates and the UE-V 2.1 SP1 generator

To synchronize application settings between user computers, Microsoft User Experience Virtualization (UE-V) 2.1 SP1 uses *settings location templates*. Some settings location templates are included in User Experience Virtualization. You can also create, edit, or validate custom settings location templates by using the UE-V generator.

The UE-V generator monitors Windows desktop applications to discover and capture the locations where the application stores its settings. The application that is monitored must be a desktop application. The UE-V generator can't create a settings location template for the following application types:

- Virtualized applications

- Applications that are offered through Terminal Services

- Java applications

- Windows apps

**Standard and Nonstandard settings locations:** The UE-V generator helps you identify where applications search for settings files and registry settings that applications use to store settings information. The generator only discovers settings in locations that are accessible to a standard user. Settings that are stored in other locations are excluded. Discovered settings are grouped into two categories: **Standard** and **Non-standard**. Standard settings are recommended for synchronization, and UE-V can readily capture and apply them. Nonstandard settings can potentially synchronize settings but, because of the rules that UE-V uses, these settings might not consistently or dependably synchronize settings. These settings might depend on temporary files, result in unreliable synchronization, or might not be useful. These settings locations are presented in the UE-V generator. You can choose to include or exclude them on a case-by-case basis.

The UE-V generator opens the application as part of the discovery process. The generator can capture settings in the following locations:

- **Registry Settings** - Registry locations under **HKEY\_CURRENT\_USER**

- **Application Settings Files** - Files that are stored under \\ **Users** \\ \[User name\] \\ **AppData** \\ **Roaming**

The UE-V generator excludes locations, which commonly store application software files, but don't synchronize well between user computers or environments. The UE-V generator excludes these locations. Excluded locations are as follows:

- HKEY\_CURRENT\_USER registry keys and files to which the logged-on user can't write values

- HKEY\_CURRENT\_USER registry keys and files that are associated with the core functionality of the Windows operating system

- All registry keys that are located in the HKEY\_LOCAL\_MACHINE hive, which requires administrator rights and might require to set a User Account Control (UAC) agreement

- Files that are located in Program Files directories, which requires administrator rights and might require to set a UAC agreement

- Files that are located under Users \\ \[User name\] \\ AppData \\ LocalLow

- Windows operating system files that are located in %Systemroot%, which requires administrator rights and might require to set a UAC agreement

If registry keys and files that are stored in these locations are required to synchronize application settings, you can manually add the excluded locations to the settings location template during the template creation process
 (except for registry entries in the HKEY\_LOCAL\_MACHINE hive).

## <a href="" id="edit"></a>Edit settings location templates with the UE-V generator

Use the UE-V generator to edit settings location templates. When the revised settings are added to the templates by using the UE-V generator, the version information within the template is automatically updated to ensure that any existing templates that are deployed in the enterprise are updated correctly.

> [!NOTE]
> If you edit a UE-V 1.0 template by using the UE-V 2 generator, the template is automatically converted to a UE-V 2 template. UE-V 1.0 agents can no longer use the edited template.

### To edit a UE-V settings location template with the UE-V generator

1.  Select **Start**, select **All Programs**, select **Microsoft User Experience Virtualization**, and then select **Microsoft User Experience Virtualization Generator**.

2.  Select **Edit a settings location template**.

3.  In the list of recently used templates, select the template to be edited. Alternatively, select **Browse** to search for the settings template file. Select **Next** to continue.

4.  Review the **Properties**, **Registry** locations, and **Files** locations for the settings template. Edit as required.

    - On the **Properties** tab, you can view and edit the following properties:

        - **Application name**: The application name that is written in the description of the program file properties.

        - **Program name**: The name of the program that is taken from the program file properties. This name usually has the .exe file name extension.

        - **Product version**: The product version number of the .exe file of the application. This property, together with the **File version**, helps determine which applications are targeted by the settings location template. This property accepts a major version number. If this property is empty, then the settings location template applies to all versions of the product.

        - **File version**: The file version number of the .exe file of the application. This property, along with the **Product version**, helps determine which applications are targeted by the settings location template. This property accepts a major version number. If this property is empty, the settings location template applies to all versions of the program.

        - **Template author name** (optional): The name of the settings template author.

        - **Template author email** (optional): The email address of the settings location template author.

    - The **Registry** tab lists the **Key** and **Scope** of the registry locations that are included in the settings location template. You can edit the registry locations by using the **Tasks** drop-down menu. In the Tasks menu, you can add new keys, edit the name or scope of existing keys, delete keys, and browse the registry in which the keys are located. When you define the scope for the registry, you can use the **All Settings** scope to include all the registry settings under the specified key. Use **All Settings** and **Subkeys** to include all the registry settings under the specified key, subkeys, and subkey settings.

    - The **Files** tab lists the file path and file mask of the file locations that are included in the settings location template. You can edit the file locations by using the **Tasks** drop-down menu. In the **Tasks** menu for file locations, you can add new files or folder locations, edit the scope of existing files or folders, delete files or folders, and open the selected location in Windows Explorer. To include all files in the specified folder, leave the file mask empty.

5.  Select **Save** to save the changes to the settings location template.

6.  Select **Close** to close the Settings Template Wizard. Exit the UE-V generator application.

    After you edit the settings location template for an application, you should test the template. Deploy the revised settings location template in a lab environment before you put it into production in the enterprise.

### How to manually edit a settings location template

1.  Create a local copy of the settings location template `.xml` file. UE-V settings location templates are `.xml` files that identify the locations where application store settings values.

    > [!NOTE]
    > A settings location template is unique because of the template **ID**. If you copy the template and rename the `.xml` file, template registration fails. This behavior is because UE-V reads the template **ID** tag in the `.xml` file to determine the name, not the file name of the `.xml` file. UE-V also reads the **Version** number to know if anything has changed. If the version number is higher, UE-V updates the template.

2.  Open the settings location template file with an XML editor.

3.  Edit the settings location template file. All changes must conform to the UE-V schema file that is defined in [SettingsLocationTempate.xsd](application-template-schema-reference-for-ue-v-2x-both-uevv2.md). By default, a copy of the `.xsd` file is located in `\ProgramData\Microsoft\UEV\Templates`.

4.  Increment the **Version** number for the settings location template.

5.  Save the settings location template file, and then close the XML editor.

6.  Validate the modified settings location template file by using the UE-V generator.

7.  You must register the edited UE-V settings location template before it can synchronize settings between client computers. To register a template, open Windows PowerShell, and then run the following cmdlet: `update-uevtemplate [templatefilename]`. You can then copy the file to the settings storage catalog. The UE-V agent on users' computers should then update as scheduled in the scheduled task.

## <a href="" id="validate"></a>Validate settings location templates with the UE-V generator

You can create or edit settings location templates in an XML editor without using the UE-V generator. If you do, you can use the UE-V generator to validate that the new or revised XML matches the schema that has been defined for the template.

### To validate a UE-V settings location template with the UE-V generator

1.  Select **Start**, point to **All Programs**, select **Microsoft User Experience Virtualization**, and then select **Microsoft User Experience Virtualization Generator**.

2.  Select **Validate a settings location template**.

3.  In the list of recently used templates, select the template to be edited. Alternatively, you can **Browse** to the settings template file. Select **Next** to continue.

4.  Select **Validate** to continue.

5.  Select **Close** to close the Settings Template Wizard. Exit the UE-V generator application.

    After you validate the settings location template for an application, you should test the template. Deploy the template in a lab environment before you put it into a production environment in enterprise.

## Related articles

[Administering UE-V 2.1 SP1](administering-ue-v-2x-new-uevv2.md)

[Deploy UE-V 2.1 SP1 for custom applications](deploy-ue-v-2x-for-custom-applications-new-uevv2.md)
