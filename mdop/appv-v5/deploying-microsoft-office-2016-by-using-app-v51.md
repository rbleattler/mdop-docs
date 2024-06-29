---
title: Deploying Microsoft Office 2016 by Using App-V
description: Deploying Microsoft Office 2016 by Using App-V
author: aczechowski
ms.reviewer:
ms.author: aaroncz
ms.collection: must-keep
ms.date: 04/19/2017
---

# Deploying Microsoft Office 2016 by Using App-V

Use the information in this article to use Microsoft Application Virtualization (App-V) 5.1, or later versions, to deliver Microsoft Office 2016 as a virtualized application to computers in your organization. For information about using App-V to deliver Office 2013, see [Deploying Microsoft Office 2013 by Using App-V](deploying-microsoft-office-2013-by-using-app-v51.md). For information about using App-V to deliver Office 2010, see [Deploying Microsoft Office 2010 by Using App-V](deploying-microsoft-office-2010-by-using-app-v51.md).

This article contains the following sections:

- [What to know before you start](#bkmk-before-you-start)

- [Creating an Office 2016 package for App-V with the Office Deployment Tool](#bkmk-create-office-pkg)

- [Publishing the Office package for App-V 5.1](#bkmk-pub-pkg-office)

- [Customizing and managing Office App-V packages](#bkmk-custmz-manage-office-pkgs)

## <a name="bkmk-before-you-start"></a>What to know before you start

Before you deploy Office 2016 by using App-V, review the following planning information.

### <a name="bkmk-supp-vers-coexist"></a>Supported Office versions and Office coexistence

For more information about supported versions of Office and about running coexisting versions of Office, see the following articles:

- [Supported versions of Microsoft Office](planning-for-using-app-v-with-office.md#bkmk-office-vers-supp-appv)
  - Supported versions of Office
  - Supported deployment types, for example, desktop, personal virtual desktop infrastructure (VDI), pooled VDI
  - Office licensing options
- [Planning for Using App-V with coexisting versions of Office](planning-for-using-app-v-with-office.md#bkmk-plan-coexisting): Considerations for installing different versions of Office on the same computer.

### <a name="bkmk-pkg-pub-reqs"></a>Packaging, publishing, and deployment requirements

Before you deploy Office by using App-V, review the following requirements.

| Task | Requirement |
|--|--|
| Packaging | - All of the Office applications that you want to deploy to users must be in a single package.<br>- In App-V 5.1 and later, you must use the Office Deployment Tool to create packages. You can't use the Sequencer.<br>- If you're deploying Microsoft Visio 2016 and Microsoft Project 2016 along with Office, you must include them in the same package with Office. For more information, see [Deploying Visio 2016 and Project 2016 with Office](#bkmk-deploy-visio-project). |
| Publishing | - You can publish only one Office package to each client computer.<br>- You must publish the Office package globally. You can't publish to the user. |
| Deploying any of the following products to a shared computer, for example, by using Remote Desktop Services: <br> - Microsoft 365 Apps for enterprise<br>- Visio Pro for Office 365<br>- Project Pro for Office 365 | You must enable [shared computer activation](/deployoffice/overview-shared-computer-activation). |

### Excluding Office applications from a package

The following table describes the recommended methods for excluding specific Office applications from a package.

| Task | Details |
|--|--|
| Use the **ExcludeApp** setting when you create the package by using the Office Deployment Tool. | - Enables you to exclude specific Office applications from the package when the Office Deployment Tool creates the package. For example, you can use this setting to create a package that contains only Microsoft Word.<br>- For more information, see [ExcludeApp element](/deployoffice/office-deployment-tool-configuration-options#bkmk-excludeappelement). |
| Modify the DeploymentConfig.xml file | - Modify the DeploymentConfig.xml file after the package has been created. This file contains the default package settings for all users on a computer that is running the App-V Client.<br>- For more information, see [Disabling Office 2016 applications](#bkmk-disable-office-apps). |

## <a name="bkmk-create-office-pkg"></a>Creating an Office 2016 package for App-V with the Office Deployment Tool

Complete the following steps to create an Office 2016 package for App-V 5.1 or later.

> [!IMPORTANT]
> In App-V 5.1 and later, you must use the Office Deployment Tool to create a package. You cannot use the Sequencer to create packages.

### Review prerequisites for using the Office Deployment Tool

The computer on which you're installing the Office Deployment Tool must have:

| Prerequisite | Description |
|--|--|
| Prerequisite software | .NET Framework 4 |
| Supported operating systems | - 64-bit version of Windows 10<br> - 64-bit version of Windows 8 or 8.1<br> - 64-bit version of Windows 7 |

> [!NOTE]
> In this article, the term "Office 2016 App-V package" refers to subscription licensing.

### Create Office 2016 App-V Packages Using Office Deployment Tool

You create Office 2016 App-V packages by using the Office Deployment Tool. The following instructions explain how to create an Office 2016 App-V package with Subscription Licensing.

Create Office 2016 App-V packages on 64-bit Windows computers. Once created, the Office 2016 App-V package runs on 32-bit and 64-bit Windows 7, Windows 8.1, and Windows 10 computers.

### Download the Office Deployment Tool

Office 2016 App-V Packages are created using the Office Deployment Tool, which generates an Office 2016 App-V Package. The package can't be created or modified through the App-V sequencer. To begin package creation:

1. Download the [Office 2016 Deployment Tool for Click-to-Run](https://www.microsoft.com/download/details.aspx?id=49117).

    > [!IMPORTANT]
    > You must use the Office 2016 Deployment Tool to create Office 2016 App-V Packages.

2. Run the .exe file and extract its features into the desired location. To make this process easier, you can create a shared network folder where the features will be saved.

    Example: `\\Server\Office2016`

3. Check that a setup.exe and a configuration.xml file exist and are in the location you specified.

### Download Office 2016 applications

After you download the Office Deployment Tool, you can use it to get the latest Office 2016 applications. After getting the Office applications, you create the Office 2016 App-V package.

The XML file that is included in the Office Deployment Tool specifies the product details, such as the languages and Office applications included.

#### 1. Customize the sample XML configuration file

Use the sample XML configuration file that you downloaded with the Office Deployment Tool to customize the Office applications:

1. Open the sample XML file in Notepad or your favorite text editor.

2. With the sample configuration.xml file open and ready for editing, you can specify products, languages, and the path to which you save the Office 2016 applications. The following is a basic example of the configuration.xml file:

```xml
<Configuration>
   <Add SourcePath= "\\Server\Office2016" OfficeClientEdition="32" >
    <Product ID="O365ProPlusRetail ">
      <Language ID="en-us" />
    </Product>
    <Product ID="VisioProRetail">
      <Language ID="en-us" />
    </Product>
  </Add>
</Configuration>
```

> [!NOTE]
> The configuration XML is a sample XML file. The file includes lines that are commented out. You can "uncomment" these lines to customize additional settings with the file. To "uncomment" these lines, remove the `<!--` from the beginning of the line, and the `-->` from the end of the line.

The above XML configuration file specifies that Office 2016 ProPlus 32-bit edition, including Visio ProPlus, will be downloaded in English to the `\\server\Office 2016` share, which is the location where Office applications will be saved to. The Product IDs of the applications don't affect the final licensing of Office. Office 2016 App-V packages with various licensing can be created from the same applications through specifying licensing in a later stage. The following table summarizes the customizable attributes and elements of XML file:

| Input | Description | Example |
|--|--|--|
| Add element | Specifies the products and languages to include in the package. | N/A |
| OfficeClientEdition (attribute of Add element) | Specifies the edition of Office 2016 product to use: 32-bit or 64-bit. The operation fails if **OfficeClientEdition** isn't set to a valid value. | `OfficeClientEdition="32"`<br>`OfficeClientEdition="64"` |
| Product element | Specifies the application. Project 2016 and Visio 2016 must be specified here as an added product to be included in the applications.<br>For more information about the product IDs, see [Product IDs that are supported by the Office Deployment Tool for Click-to-Run](/microsoft-365/troubleshoot/installation/product-ids-supported-office-deployment-click-to-run) | `Product ID="O365ProPlusRetail "`<br>`Product ID="VisioProRetail"`<br>`Product ID="ProjectProRetail"` |
| Language element | Specifies the language supported in the applications | `Language ID="en-us"` |
| Version (attribute of Add element) | Optional. Specifies a build to use for the package<br>Defaults to the latest advertised build (as defined in `v32.CAB` at the Office source). | `16.1.2.3` |
| SourcePath (attribute of Add element) | Specifies the location in which the applications will be saved to. | `Sourcepath = "\\Server\Office2016"` |
| Branch (attribute of Add element) | Optional. Specifies the update branch for the product that you want to download or install.<br>For more information about update branches, see Overview of update branches for Microsoft 365 Apps for enterprise. | `Branch = "Business"` |

After editing the configuration.xml file to specify the desired product, languages, and also the location that the Office 2016 applications will be saved onto, you can save the configuration file, for example, as Customconfig.xml.

#### 2. Download the applications into the specified location

Use an elevated command prompt and a 64-bit operating system to download the Office 2016 applications that will later be converted into an App-V package. Below is an example command with a description of details:

```cmd
\\server\Office2016\setup.exe /download \\server\Office2016\Customconfig.xml
```

In the example:

| Command | Description |
|--|--|
| `\\server\Office2016` | The network share location that contains the Office Deployment Tool and the custom Configuration.xml file, Customconfig.xml. |
| `Setup.exe` | The Office Deployment Tool. |
| `/download` | Downloads the Office 2016 applications that you specify in the customConfig.xml file. These bits can be later converted into an Office 2016 App-V package with Volume Licensing. |
| `\\server\Office2016\Customconfig.xml` | Passes the XML configuration file required to complete the download process, in this example, customconfig.xml. After using the download command, Office applications should be found in the location specified in the configuration XML file, in this example `\\Server\Office2016`. |

### Convert the Office applications into an App-V package

After you download the Office 2016 applications through the Office Deployment Tool, use the Office Deployment Tool to convert them into an Office 2016 App-V package. Complete the steps that correspond to your licensing model.

#### Summary of what you need to do

- Create the Office 2016 App-V packages on 64-bit Windows computers. However, the package runs on 32-bit and 64-bit Windows 7, Windows 8 or 8.1, and Windows 10 computers.

- Create an Office App-V package for Subscription Licensing package by using the Office Deployment Tool, and then modify the CustomConfig.xml configuration file.

The following table summarizes the values you need to enter in the CustomConfig.xml file for the licensing model you're using. The steps in the sections that follow the table specifies the exact entries you need to make.

> [!NOTE]
> You can use the Office Deployment Tool to create App-V packages for Microsoft 365 Apps for enterprise. Creating packages for the volume-licensed versions of Office Professional Plus or Office Standard is not supported.

| Product ID | Subscription Licensing |
|--|--|
| **Office 2016** | `O365ProPlusRetail` |
| **Office 2016 with Visio 2016** | `O365ProPlusRetail`<br>`VisioProRetail` |
| **Office 2016 with Visio 2016 and Project 2016** | `O365ProPlusRetail`<br>`VisioProRetail`<br>`ProjectProRetail` |

#### How to convert the Office applications into an App-V package

1. In Notepad, reopen the CustomConfig.xml file, and make the following changes to the file:

    - `SourcePath`: Point to the Office applications previously downloaded.
    - `ProductID`: Specify Subscription licensing, as shown in the following example:

      ```xml
      <Configuration>
        <Add SourcePath="\\server\Office 2016" OfficeClientEdition="32">
          <Product ID="O365ProPlusRetail">
            <Language ID="en-us" />
          </Product>
          <Product ID="VisioProRetail">
            <Language ID="en-us" />
          </Product>
        </Add>
      </Configuration>
      ```

      In this example, the following changes were made to create a package with Subscription licensing:

      - `Product ID` for Office was changed to `O365ProPlusRetail`.
      - `Product ID` for Visio was changed to `VisioProRetail`.

    - `ExcludeApp` (optional): Lets you specify Office programs that you don't want included in the App-V package that the Office Deployment Tool creates. For example, you can exclude Access and InfoPath.
    - `PACKAGEGUID` (optional): By default, all App-V packages created by the Office Deployment Tool share the same App-V Package ID. You can use PACKAGEGUID to specify a different package ID for each package, which allows you to publish multiple App-V packages, created by the Office Deployment Tool, and manage them by using the App-V Server.

      An example of when to use this parameter is if you create different packages for different users. For example, you can create a package with just Office 2016 for some users, and create another package with Office 2016 and Visio 2016 for another set of users.

      > [!NOTE]
      > Even if you use unique package IDs, you can still deploy only one App-V package to a single device.

2. Use the `/packager` command to convert the Office applications to an Office 2016 App-V package.

   For example:

   ```cmd
   \\server\Office2016\setup.exe /packager \\server\Office2016\Customconfig.xml \\server\share\Office2016AppV
   ```

   In the example:

    | Command | Description |
    |--|--|
    | `\\server\Office2016` | The network share location that contains the Office Deployment Tool and the custom Configuration.xml file, Customconfig.xml. |
    | `Setup.exe` | The Office Deployment Tool. |
    | `/packager` | Creates the Office 2016 App-V package with the type of licensing specified in the customConfig.xml file. |
    | `\\server\Office2016\Customconfig.xml` | Passes the configuration XML file (in this case customConfig) that has been prepared for the packaging stage. |
    | `\\server\share\Office 2016AppV` | Specifies the location of the newly created Office App-V package.

    After you run the `/packager` command, the following folders appear up in the directory where you specified the package should be saved:

     - **App-V Packages** - contains an Office 2016 App-V package and two deployment configuration files.

     - **WorkingDir**

    > [!NOTE]
    > To troubleshoot any issues, see the log files in the %temp% directory (default).

3. Verify that the Office 2016 App-V package works correctly:

   1. Publish the Office 2016 App-V package, which you created globally, to a test computer, and verify that the Office 2016 shortcuts appear.

   2. Start a few Office 2016 applications, such as Excel or Word, to ensure that your package is working as expected.

## <a name="bkmk-pub-pkg-office"></a>Publishing the Office package for App-V

Use the following information to publish an Office package.

### Methods for publishing Office App-V packages

Deploy the App-V package for Office 2016 by using the same methods you use for any other package:

- System Center Configuration Manager

- App-V Server

- Stand-alone through PowerShell commands

### Publishing prerequisites and requirements

| Prerequisite or requirement | Details |
|--|--|
| Enable PowerShell scripting on the App-V clients | To publish Office 2016 packages, you must run a script.<br>Package scripts are disabled by default on App-V clients. To enable scripting, run the following PowerShell command:<br>`Set-AppvClientConfiguration -EnablePackageScripts 1` |
| Publish the Office 2016 package globally | Extension points in the Office App-V package require installation at the computer level.<br>When you publish at the computer level, no prerequisite actions or redistributables are needed, and the Office 2016 package globally enables its applications to work like natively installed Office, eliminating the need for administrators to customize packages. |

### How to publish an Office package

Run the following command to publish an Office package globally:

- `Add-AppvClientPackage <Path_to_AppV_Package> | Publish-AppvClientPackage -global`

- From the Web Management Console on the App-V Server, you can add permissions to a group of computers instead of to a user group to enable packages to be published globally to the computers in the corresponding group.

## <a name="bkmk-custmz-manage-office-pkgs"></a>Customizing and managing Office App-V packages

To manage your Office App-V packages, use the same operations as you would for any other package, but there are a few exceptions, as outlined in the following sections.

- [Enabling Office plug-ins by using connection groups](#bkmk-enable-office-plugins)

- [Disabling Office 2016 applications](#bkmk-disable-office-apps)

- [Disabling Office 2016 shortcuts](#bkmk-disable-shortcuts)

- [Managing Office 2016 package upgrades](#bkmk-manage-office-pkg-upgrd)

- [Deploying Visio 2016 and Project 2016 with Office](#bkmk-deploy-visio-project)

### <a name="bkmk-enable-office-plugins"></a>Enabling Office plug-ins by using connection groups

Use the steps in this section to enable Office plug-ins with your Office package. To use Office plug-ins, you must use the App-V Sequencer to create a separate package that contains just the plug-ins. You can't use the Office Deployment Tool to create the plug-ins package. You then create a connection group that contains the Office package and the plug-ins package, as described in the following steps.

#### To enable plug-ins for Office App-V packages

1. Add a Connection Group through App-V Server, System Center Configuration Manager, or a PowerShell cmdlet.

2. Sequence your plug-ins using the App-V Sequencer. Ensure that Office 2016 is installed on the computer being used to sequence the plug-in. It's recommended you use Microsoft 365 Apps for enterprise(non-virtual) on the sequencing computer when you sequence Office 2016 plug-ins.

3. Create an App-V package that includes the desired plug-ins.

4. Add a Connection Group through App-V server, System Center Configuration Manager, or a PowerShell cmdlet.

5. Add the Office 2016 App-V package and the plug-ins package you sequenced to the Connection Group you created.

    > [!IMPORTANT]
    > The order of the packages in the Connection Group determines the order in which the package contents are merged. In your Connection group descriptor file, add the Office 2016 App-V package first, and then add the plug-in App-V package.

6. Ensure that both packages are published to the target computer and that the plug-in package is published globally to match the global settings of the published Office 2016 App-V package.

7. Verify that the Deployment Configuration File of the plug-in package has the same settings that the Office 2016 App-V package has.

    Since the Office 2016 App-V package is integrated with the operating system, the plug-in package settings should match. You can search the Deployment Configuration File for "COM Mode" and ensure that your plug-ins package has that value set as "Integrated" and that both "InProcessEnabled" and "OutOfProcessEnabled" match the settings of the Office 2016 App-V package you published.

8. Open the Deployment Configuration File and set the value for **Objects Enabled** to **false**.

9. If you made any changes to the Deployment Configuration file after sequencing, ensure that the plug-in package is published with the file.

10. Ensure that the Connection Group you created is enabled onto your desired computer. The Connection Group created will likely "pend" if the Office 2016 App-V package is in use when the Connection Group is enabled. If that happens, you have to reboot to successfully enable the Connection Group.

11. After you successfully publish both packages and enable the Connection Group, start the target Office 2016 application and verify that the plug-in you published and added to the connection group works as expected.

### <a name="bkmk-disable-office-apps"></a>Disabling Office 2016 applications

You may want to disable specific applications in your Office App-V package. For instance, you can disable Access, but leave all other Office application main available. When you disable an application, the end user will no longer see the shortcut for that application. You don't have to resequence the application. When you change the Deployment Configuration File after the Office 2016 App-V package has been published, you'll save the changes, add the Office 2016 App-V package, and then republish it with the new Deployment Configuration File to apply the new settings to Office 2016 App-V Package applications.

> [!NOTE]
> To exclude specific Office applications (for example, Access and InfoPath) when you create the App-V package with the Office Deployment Tool, use the **ExcludeApp** setting.

#### To disable an Office 2016 application

1. Open a Deployment Configuration File with a text editor such as **Notepad** and search for "Applications."

2. Search for the Office application you want to disable, for example, Access 2016.

3. Change the value of "Enabled" from "true" to "false."

4. Save the Deployment Configuration File.

5. Add the Office 2016 App-V Package with the new Deployment Configuration File.

    ```xml
    <Application Id="[{AppVPackageRoot}]\office16\lync.exe" Enabled="true">
      <VisualElements>
        <Name>Lync 2016</Name>
        <Icon />
        <Description />
      </VisualElements>
    </Application>
    <Application Id="[(AppVPackageRoot}]\office16\MSACCESS.EXE" Enabled="true">
      <VisualElements>
        <Name>Access 2016</Name>
        <Icon />
        <Description />
      </VisualElements>
    </Application>
    ```

6. Readd the Office 2016 App-V package, and then republish it with the new Deployment Configuration File to apply the new settings to Office 2016 App-V Package applications.

### <a name="bkmk-disable-shortcuts"></a>Disabling Office 2016 shortcuts

You may want to disable shortcuts for certain Office applications instead of unpublishing or removing the package. The following example shows how to disable shortcuts for Microsoft Access.

#### To disable shortcuts for Office 2016 applications

1. Open a Deployment Configuration File in Notepad and search for "Shortcuts".

2. To disable certain shortcuts, delete or comment out the specific shortcuts you don't want. You must keep the subsystem present and enabled. For example, in the example below, delete the Microsoft Access shortcuts, while keeping the subsystems `<shortcut> </shortcut>` intact to disable the Microsoft Access shortcut.

    ```xml
     <Shortcuts Enabled="true">
      <Extensions>
        <Extension Category="AppV.Shortcut">
          <Shortcut>
           <File>[{Common Programs}]\Microsoft Office 2016\Access 2016.lnk</File>
           <Target>[{AppvPackageRoot}])office16\MSACCESS.EXE</Target>
           <Icon>[{Windows}]\Installer\{90150000-000F-0000-0000-000000FF1CE)\accicons.exe.Ø.ico</Icon>
           <Arguments />
           <WorkingDirectory />
           <AppuserModelId>Microsoft.Office.MSACCESS.EXE.15</AppUserModelId>
           <AppUserModelExcludeFromShowInNewInstall>true</AppUserModelExcludeFromShowInNewInstall>
           <Description>Build a professional app quickly to manage data.</Description>
           <ShowCommand>l</ShowCommand>
           <ApplicationId>[{AppVPackageRoot}]\office16\MSACCESS.EXE</ApplicationId>
        </Shortcut>
    ```

3. Save the Deployment Configuration File.

4. Republish Office 2016 App-V Package with new Deployment Configuration File.

Many additional settings can be changed through modifying the Deployment Configuration for App-V packages, for example, file type associations, Virtual File System, and more. For more information on how to use Deployment Configuration Files to change App-V package settings, see the additional resources section at the end of this document.

### <a name="bkmk-manage-office-pkg-upgrd"></a>Managing Office 2016 package upgrades

To upgrade an Office 2016 package, use the Office Deployment Tool. To upgrade a previously deployed Office 2016 package, perform the following steps.

#### How to upgrade a previously deployed Office 2016 package

1. Create a new Office 2016 package through the Office Deployment Tool that uses the most recent Office 2016 application software. The most recent Office 2016 bits can always be obtained through the download stage of creating an Office 2016 App-V Package. The newly created Office 2016 package has the most recent updates and a new Version ID. All packages created using the Office Deployment Tool have the same lineage.

   > [!NOTE]
   > Office App-V packages have two Version IDs:
   >
   > - An Office 2016 App-V Package Version ID that is unique across all packages created using the Office Deployment Tool.
   > - A second App-V Package Version ID, x.x.x.x for example, in the AppX manifest that will only change if there is a new version of Office itself. For example, if a new Office 2016 release with upgrades is available, and a package is created through the Office Deployment Tool to incorporate these upgrades, the X.X.X.X version ID will change to reflect that the Office version itself has changed. The App-V server will use the X.X.X.X version ID to differentiate this package and recognize that it contains new upgrades to the previously published package, and as a result, publish it as an upgrade to the existing Office 2016 package.

2. Globally publish the newly created Office 2016 App-V Packages onto computers where you would like to apply the new updates. Since the new package has the same lineage of the older Office 2016 App-V Package, publishing the new package with the updates will only apply the new changes to the old package, and thus will be fast.

3. Upgrades are applied in the same manner of any globally published App-V Packages. Because applications will probably be in use, upgrades might be delayed until the computer is rebooted.

### <a name="bkmk-deploy-visio-project"></a>Deploying Visio 2016 and Project 2016 with Office

The following sections describe the requirements and options for deploying Visio 2013 and Project 2013 with Office.

#### How do I package and publish Visio 2013 and Project 2013 with Office?

You must include Visio 2013 and Project 2013 in the same package with Office.

If you aren't deploying Office, you can create a package that contains Visio and/or Project, as long as you follow the packaging, publishing, and deployment requirements described in this article.

#### How can I deploy Visio 2013 and Project 2013 to specific users?

If you want to *create two different packages and deploy each one to a different group of users*, create and deploy the following packages:

1. A package that contains only Office - deploy to computers whose users need only Office.

2. A package that contains Office, Visio, and Project - deploy to computers whose users need all three applications.

If you want *only one package for the whole organization, or if you have users who share computers*, follow these steps:

1. Create a package that contains Office, Visio, and Project.
2. Deploy the package to all users.
3. Use [Microsoft AppLocker](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd723678(v=ws.10)) to prevent specific users from using Visio and Project.

## Additional resources

[Deploying Microsoft Office 2013 by Using App-V](deploying-microsoft-office-2013-by-using-app-v.md)

[Deploying Microsoft Office 2010 by Using App-V](deploying-microsoft-office-2010-by-using-app-v.md)

[Office 2016 Deployment Tool for Click-to-Run](https://www.microsoft.com/download/details.aspx?id=49117)

[Managing Connection Groups](managing-connection-groups.md)

[About App-V 5.1 Dynamic Configuration](about-app-v-51-dynamic-configuration.md)
