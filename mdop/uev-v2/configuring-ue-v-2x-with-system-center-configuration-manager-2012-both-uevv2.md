---
title: Configuring UE-V 2.1 SP1 with System Center Configuration Manager 2012
description: The UE-V configuration pack provides a way for administrators to use the Compliance Settings feature of System Center Configuration Manager 2012 SP1 or later to apply consistent configurations across sites where UE-V and Configuration Manager are installed.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/02/2016
---

# Configuring UE-V 2.1 SP1 with System Center Configuration Manager 2012

After you install Microsoft User Experience Virtualization (UE-V) 2.1 SP1 and its required features, you need to configure UE-V. The UE-V configuration pack provides a way for administrators to use the Compliance Settings feature of System Center Configuration Manager 2012 SP1 or later to apply consistent configurations across sites where UE-V and Configuration Manager are installed.

## UE-V configuration pack supported features

The UE-V configuration pack includes tools to perform the following tasks:

- Create or update UE-V settings location template distribution baselines.

  - Define UE-V templates to be registered or unregistered
  - Update UE-V template configuration items and baselines as templates are added or updated
  - Distribute and register UE-V templates using standard Configuration Item remediation

- Create or update a UE-V agent policy configuration item to set or clear these settings.

    | Max package size               | Enable/disable Windows app sync | Wait for sync on application start |
    |--------------------------------|---------------------------------|------------------------------------|
    | Setting import delay           | Sync unlisted Windows apps      | Wait for sync on sign in             |
    | Settings import notification   | IT contact URL                  | Wait for sync timeout              |
    | Settings storage path          | IT contact descriptive text     | Settings template catalog path     |
    | Sync enablement                | Tray icon enabled               | Start/Stop UE-V agent service      |
    | Sync method                    | First use notification          | Define which Windows apps will roam settings |
    | Sync timeout                   |                                 |                                    |

- Verify compliance by confirming that UE-V is running.

## Generate a UE-V agent policy configuration item

All UE-V agent policy and configuration is distributed through a single configuration item that is generated using the UevAgentPolicyGenerator.exe tool. This tool reads the desired configuration from an XML configuration file and creates a CI containing the discovery and remediation settings needed to bring the machine into compliance.

The UE-V agent policy configuration item CAB file is created using the UevTemplateBaselineGenerator.exe command line tool, which has these parameters:

- Site &lt;site code&gt;

- PolicyName &lt;name&gt; Optional: Defaults to "UE-V agent Policy" if not present

- PolicyDescription &lt;description&gt; Optional: A description is provided if not present

- CabFilePath &lt;full path to configuration item .CAB file&gt;

- ConfigurationFile &lt;full path to agent configuration XML file&gt;

> [!NOTE]
> It might be necessary to change the PowerShell execution policy to allow these scripts to run in your environment. Do these steps in the Configuration Manager console:
>
> 1. Select **Administration &gt; Client Settings &gt; Properties**
>
> 2. In the **User Agent** tab, set the **PowerShell Execution Policy** to **Bypass**

## <a href="" id="create"></a> Create the first UE-V policy configuration item

1.  Copy the default settings configuration file from the UE-V configuration pack installation directory to a location visible to your Configuration Manager console:

    `C:\Program Files (x86)\Microsoft User Experience Virtualization\ConfigPack\AgentConfiguration.xml c:\<target path>`

    The default configuration file contains five sections:

    - **Computer Policy**: All UE-V machine level settings. The DesiredState attribute can be one of the following values:

        - **Set** to have the value assigned in the registry.

        - **Clear** to remove the setting.

        - **Unmanaged** to have the configuration item left at its current state.

    Don't remove lines from this section. Instead, set the DesiredState to 'Unmanaged' if you don't want Configuration Manager to alter current or default values.

    - **CurrentComputerUserPolicy**: All UE-V user level settings. These entries override the machine settings for a user. The DesiredState attribute can be one of the following values:

        - **Set** to have the value assigned in the registry.

        - **Clear** to remove the setting.

        - **Unmanaged** to have the configuration item left at its current state.

    Don't remove lines from this section. Instead, set the DesiredState to 'Unmanaged' if you don't want Configuration Manager to alter current or default values.

    - **Services**: Entries in this section control service operation. The default configuration file contains a single entry for the UevAgentService. The DesiredState attribute can be set to **Running** or **Stopped**.

    - **Windows8AppsComputerPolicy**: All machine level Windows app synchronization settings. Each PackageFamilyName listed in this section can be assigned a DesiredState of one of the following values:

        - **Enabled** to have settings roam.

        - **Disabled** to prevent settings from roaming.

        - **Cleared** to have the entry removed from UE-V control.

    You can add more lines to this section based on the list of installed Windows apps that can be viewed using the PowerShell cmdlet Get-AppxPackage.

    - **Windows8AppsCurrentComputerUserPolicy**: Identical to the Windows8AppsComputerPolicy with settings that override machine settings for an individual user.

2.  Edit the configuration file by changing the desired state and value fields.

3.  Run this command on a machine running the Configuration Manager console:

    ```command
    C:\Program Files (x86)\Microsoft User Experience Virtualization\ConfigPack\UevAgentPolicyGenerator.exe -Site ABC -CabFilePath "C:\MyCabFiles\UevPolicyItem.cab" -ConfigurationFile "c:\AgentConfiguration.xml"
    ```

4.  Import the CAB file using Configuration Manager console or PowerShell Import-CMConfigurationItem

## Update a UE-V policy configuration item

1.  Edit the configuration file by changing the desired state and value fields.

2.  Run the command from Step 3 in [Create the First UE-V Policy Configuration Item](#create). If you changed the name with the PolicyName parameter, make sure you enter the same name.

3.  Reimport the CAB file. The version in Configuration Manager is updated.

## Generate a UE-V template baseline

UE-V templates are distributed using a baseline containing multiple configuration items. Each configuration item contains the discovery and remediation scripts needed to install one UE-V template. The actual UE-V template is embedded within the remediation script for distribution using standard Configuration Item functionality.

The UE-V template baseline is created using the UevTemplateBaselineGenerator.exe command line tool, which has these parameters:

- Site &lt;site code&gt;

- BaselineName &lt;name&gt; (Optional: defaults to "UE-V Template Distribution Baseline" if not present)

- BaselineDescription &lt;description&gt; (Optional: a description is provided if not present)

- TemplateFolder &lt;UE-V template folder&gt;

- Register &lt;comma separated template file list&gt;

- Unregister &lt;comma separated template list&gt;

- CabFilePath &lt;Full path to baseline CAB file to generate&gt;

The result is a baseline CAB file that is ready for import into Configuration Manager. If at a future date, you update or add a template, you can rerun the command using the same baseline name. Importing the CAB results in CI version updates on the changed templates.

### <a href="" id="create2"></a>Create the first UE-V template baseline

1.  Create a primary set of UE-V templates in a stable folder location visible to the machine running your Configuration Manager console. As templates are added or updated, this folder is where they're pulled for distribution. The initial list of templates can be copied from a machine with UE-V installed. The default template location is C:\\Program Files\\Microsoft User Experience Virtualization\\Templates.

2.  Create a text.bat file where you can add the template generator command. This step is optional, but makes regeneration simpler if you save the command parameters.

3.  Add the command and parameters to the .bat file that will generate the baseline. The following example creates a baseline that distributes Notepad and Calculator:

    ```command
    C:\Program Files (x86)\Microsoft User Experience Virtualization\ConfigPack\UevTemplateBaselineGenerator.exe -Site "ABC" -TemplateFolder "C:\ProductionUevTemplates" -Register "MicrosoftNotepad.xml, MicrosoftCalculator.xml" -CabFilePath "C:\MyCabFiles\UevTemplateBaseline.cab"
    ```

4.  Run the .bat file to create UevTemplateBaseline.cab ready for import into Configuration Manager.

### Update a UE-V template baseline

The template generator uses the template version to determine if a template should be updated. If you make a template change and update the version, the baseline generator compares the template in your primary folder with the template contained in the CI on the Configuration Manager server. If a difference is found, the generated baseline and modified CI versions are updated.

To distribute a new Notepad template, you would perform these steps:

1.  Update the template and template version located in the &lt;Version&gt; element of the template.

2.  Copy the template to your primary template directory.

3.  Run the command in the .bat file that you created in Step 3 in [Create the First UE-V Template Baseline](#create2).

4.  Import the generated CAB file into Configuration Manager using the console or PowerShell Import-CMBaseline.

## Get the UE-V configuration pack

To download the UE-V configuration pack for Configuration Manager 2012 SP1, see [Get started with UE-V 2.1 SP1](get-started-with-ue-v-2x-new-uevv2.md).

## Related articles

[Manage configurations for UE-V 2.1 SP1](manage-configurations-for-ue-v-2x-new-uevv2.md)
