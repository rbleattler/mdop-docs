---
title: The connection group file
description: About the connection group file
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# The connection group file

This article contains the following sections:

-   [Connection group file purpose and location](#bkmk-cg-purpose-loc)

-   [Structure of the connection group XML file](#bkmk-define-cg-5-0sp3)

-   [Configuring the priority of packages in a connection group](#bkmk-config-pkg-priority-incg)

-   [Supported virtual application connection configurations](#bkmk-va-conn-configs)

## <a href="" id="bkmk-cg-purpose-loc"></a>Connection group file purpose and location

| Connection group purpose | A connection group is an App-V feature that enables you to group packages together to create a virtual environment in which the applications in those packages can interact with each other. <br> **Example:** You want to use plug-ins with Microsoft Office. You can create a package that contains the plug-ins, and create another package that contains Office, and then add both packages to a connection group to enable Office to use those plug-ins. |
|--|--|
| How the connection group file works | When you apply an App-V 5.1 connection group file, the packages that are enumerated in the file will be combined at runtime into a single virtual environment. Use the Microsoft Application Virtualization (App-V) 5.1 connection group file to configure existing App-V 5.1 connection groups. |
| Example file path | `%APPDATA%\Microsoft\AppV\Client\Catalog\PackageGroups{6CCC7575-162E-4152-9407-ED411DA138F4}{4D1E16E1-8EF8-41ED-92D5-8910A8527F96}` |

## <a href="" id="bkmk-define-cg-5-0sp3"></a>Structure of the connection group XML file

This section includes the following information:

-   [Parameters that define the connection group](#bkmk-params-define-cg)

-   [Parameters that define the packages in the connection group](#bkmk-params-define-pkgs-incg)

-   [App-V example connection group XML file](#bkmk-50sp3-exp-cg-xml)

-   [App-V 5.0 through App-V 5.0 SP2 example connection group XML file](#bkmk-50thru50sp2-exp-cg-xm)

### <a href="" id="bkmk-params-define-cg"></a>Parameters that define the connection group

The following table describes the parameters in the XML file that define the connection group itself, not the packages.

| Field | Description |
|--|--|
| Schema name | Name of the schema. <br> **Applicable starting in App-V 5.0 SP3**: If you want to use the new "optional packages" and "use any version" features that are described in this table, you must specify the following schema in the XML file: <br> `xmlns="https://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"` |
| AppConnectionGroupId | Unique GUID identifier for this connection group. The connection group state is associated with this identifier. Specify this identifier only when you create the connection group. <br> You can create a new GUID by typing: `[Guid]::NewGuid()`. |
| VersionId | Version GUID identifier for this version of the connection group. <br> When you update a connection group (for example, by adding or updating a new package), you must update the version GUID to reflect the new version. |
| DisplayName | Display name of the connection group. |
| Priority | Optional priority field for the connection group. <br> **"0"** - indicates the highest priority. <br> If a priority is required, but has not been configured, the package will fail because the correct connection group to use cannot be determined. |

### <a href="" id="bkmk-params-define-pkgs-incg"></a>Parameters that define the packages in the connection group

In the `<Packages>` section of the connection group XML file, you list the member packages in the connection group by specifying each package's unique package identifier and version identifier, as described in the following table. The first package in the list has the highest precedence.

| Field | Description |
|--|--|
| PackageId | Unique GUID identifier for this package. This GUID doesn't change when newer versions of the package are published. |
| VersionId | Unique GUID identifier for the version of the package. <br> **Applicable starting in App-V 5.0 SP3**: If you specify **"*"** for the package version, the GUID of the latest available package version is dynamically inserted. |
| IsOptional | **Applicable starting in App-V 5.0 SP3**: Parameter that enables you to make a package optional within the connection group. Valid entries are: <ul><li>**"true"** - package is optional in the connection group</li><li>**"false"** - package is required in the connection group</li></ul> See [How to Use Optional Packages in Connection Groups](how-to-use-optional-packages-in-connection-groups51.md). |

### <a href="" id="bkmk-50sp3-exp-cg-xml"></a>App-V example connection group XML file

The following example connection group XML file shows examples of the fields in the previous tables and highlights the items that are new starting in App-V 5.0 SP3.

```XML
<?xml version="1.0" encoding="UTF-16">
<appv:AppConnectionGroup
  xmlns="https://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"
  xmlns:appv="https://schemas.microsoft.com/appv/2014/virtualapplicationconnectiongroup"
  AppConnectionGroupId="61BE9B14-D2B4-41CE-A6E3-A1B658DE7000"
  VersionId="E6B6AA57-F2A7-49C9-ADF8-F2B5B3C8A42F"
  Priority="0"
  DisplayName="Sample Connection Group">
  <appv:Packages>
    <appv:Package
      PackageId="1DC709C8-309F-4AB4-BD47-F75926D04276"
      VersionId="*"
      IsOptional="true"
    />
    <appv:Package
      PackageId="04220DCA-EE77-42BE-A9F5-96FD8E8593F2"
      VersionId="E15EFFE9-043D-4C01-BC52-AD2BD1E8BAFA"
      IsOptional="false"
    />
  </appv:Packages>
</appv:AppConnectionGroup>
```

### <a href="" id="bkmk-50thru50sp2-exp-cg-xm"></a>App-V 5.0 through App-V 5.0 SP2 example connection group XML file

The following example connection group XML file applies to App-V 5.0 through App-V 5.0 SP2. It shows examples of the fields in the previous table, but it excludes the changes described above for App-V 5.0 SP3.

```XML
<?xml version="1.0" encoding="UTF-16">
<appv:AppConnectionGroup
  xmlns="https://schemas.microsoft.com/appv/2010/virtualapplicationconnectiongroup"
  xmlns:appv="https://schemas.microsoft.com/appv/2010/virtualapplicationconnectiongroup"
  AppConnectionGroupId="61BE9B14-D2B4-41CE-A6E3-A1B658DE7000"
  VersionId="E6B6AA57-F2A7-49C9-ADF8-F2B5B3C8A42F"
  Priority="0"
  DisplayName="Sample Connection Group">
  <appv:Packages>
    <appv:Package
      PackageId="1DC709C8-309F-4AB4-BD47-F75926D04276"
      VersionId="C7DF4F63-5288-439C-ACEF-EF06BF401EC5"
    />
    <appv:Package
     PackageId="04220DCA-EE77-42BE-A9F5-96FD8E8593F2"
     VersionId="E15EFFE9-043D-4C01-BC52-AD2BD1E8BAFA"
   />
 </appv:Packages>
<appv:AppConnectionGroup>
```

## <a href="" id="bkmk-config-pkg-priority-incg"></a>Configuring the priority of packages in a connection group

Package precedence is configured using the package list order. The first package in the document has the highest precedence. Subsequent packages in the list have descending priority.

Package precedence is the resolution for otherwise inevitable resource collisions during virtual environment initialization. For example, if two packages that are opening in the same virtual environment define the same registry DWORD value, the package with the highest precedence determines the value that is set.

You can use the connection group file to configure each connection group by using the following methods:

-   Specify runtime priorities for connection groups. To edit priority by using the App-V Management Console, click the connection group and then click **Edit**.

    > [!NOTE]
    > Priority is required only if the package is associated with more than one connection group.

-   Specify package precedence within the connection group.

The priority field is required when a running virtual application initiates from a native application request, for example, Microsoft Windows Explorer. The App-V client uses the priority to determine which connection group virtual environment the application should run in. This situation occurs if a virtual application is part of multiple connection groups.

If a virtual application is opened using another virtual application the virtual environment of the original virtual application will be used. The priority field is not used in this case.

For example:

The virtual application Microsoft Outlook is running in virtual environment **XYZ**. When you open an attached Microsoft Word document, a virtualized version Microsoft Word opens in the virtual environment **XYZ**, regardless of the virtualized Microsoft Word's associated connection groups or runtime priorities.

## <a href="" id="bkmk-va-conn-configs"></a>Supported virtual application connection configurations

The following sections provide example scenarios for each configuration.

### An. exe file and plug-in (.dll)

- You want to distribute Microsoft Office to all users, but distribute a Microsoft Excel plug-in to only a subset of users.
- Enable the connection group for the appropriate users.
- Update each package individually as required.

### An. exe file and a middleware application

- You have an application that requires a middleware application, or several applications that all depend on the same middleware runtime version.
- All computers that require one or more of the applications receive the connection groups with the application and middleware application runtime.
- You can optionally combine multiple middleware applications into a single connection group.

| Example | Example description |
|--|--|
| Virtual application connection group for the financial division | - Middleware application 1 <br> - Middleware application 2 <br> - Middleware application 3 <br> - Middleware application runtime |
| Virtual application connection group for HR division | - Middleware application 5 <br> - Middleware application 6 <br> - Middleware application runtime |

### An. exe file and an .exe file

You have an application that relies on another application, and you want to keep the packages separate for operational efficiencies, licensing restrictions, or rollout timelines.

For example:

If you deploy Microsoft Lync 2010, you can use three packages:

- Microsoft Office 2010
- Microsoft Communicator 2007
- Microsoft Lync 2010

You can manage the deployment using the following connection groups:

- Microsoft Office 2010 and Microsoft Communicator 2007
- Microsoft Office 2010 and Microsoft Lync 2010

When the deployment has completed, you can either create a single new Microsoft Office 2010 + Microsoft Lync 2010 package, or keep and maintain them as separate packages and deploy them by using a connection group.

## Related topics

[Managing connection groups](managing-connection-groups51.md)
