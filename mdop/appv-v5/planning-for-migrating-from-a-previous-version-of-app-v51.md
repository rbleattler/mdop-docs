---
title: Planning for migrating from a previous version of App-V
description: Use the following information to plan how to migrate to Microsoft Application Virtualization (App-V) 5.1 from previous versions of App-V.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/21/2016
---

# Planning for migrating from a previous version of App-V

Use the following information to plan how to migrate to Microsoft Application Virtualization (App-V) 5.1 from previous versions of App-V.

## Migration requirements

Before you start any upgrades, review the following requirements:

- If you are upgrading from a version earlier than App-V 4.6 SP2, upgrade to version App-V 4.6 SP3 first before upgrading to App-V 5.1 or later. In this scenario, upgrade the App-V clients first, and then upgrade the server components.
**Note:** App-V 4.6 has exited Mainstream support.

- App-V 5.1 supports only packages that are created using App-V 5.0 or App-V 5.1, or packages that have been converted to the **.appv** format.

- If you are upgrading the App-V Server from App-V 5.0 SP1, see [About App-V 5.1](about-app-v-51.md#bkmk-migrate-to-51) for instructions.

## Running the App-V 5.1 client concurrently with App-V 4.6

You can run the App-V 5.1 client concurrently on the same computer with the App-V 4.6 SP3 client.

When you run coexisting App-V clients, you can:

- Convert an App-V 4.6 SP3 package to the App-V 5.1 format and publish both packages, when you have both clients running.

- Define the migration policy for the converted package, which allows the converted App-V 5.1 package to assume the file type associations and shortcuts from the App-V 4.6 package.

### Supported coexistence scenarios

The following table shows the supported App-V coexistence scenarios. We recommend that you install the latest available updates of a given release when you are running coexisting clients.

| App-V 4.6 client type | App-V 5.1 client type |
|-----------------------|-----------------------|
| App-V 4.6 SP3         | App-V 5.1             |
| App-V 4.6 SP3 RDS     | App-V 5.1 RDS         |

### Requirements for running coexisting clients

To run coexisting clients, you must:

- Install the App-V 4.6 client before you install the App-V 5.1 client.

- Enable the **Enable Migration Mode** Group Policy setting, which is in the **App-V** &gt; **Client Coexistence** node. To deploy the .admx template, see [How to Download and Deploy MDOP Group Policy (.admx) Templates](../solutions/how-to-download-and-deploy-mdop-group-policy--admx--templates.md).

> [!NOTE]
> App-V 5.1 packages can run side by side with App-V 4.6 packages if you have coexisting installations of App-V 5.1 and 4.6. However, App-V 5.1 packages cannot interact with App-V 4.6 packages in the same virtual environment.

### Client downloads and documentation

The downloads include the App-V "regular" and RDS clients. For more information, see [About Microsoft Application Virtualization 5.1](about-app-v-51.md).

For more information about how to configure App-V 5.1 client coexistence, see:

- [How to Deploy the App-V 4.6 and the App-V 5.1 Client on the Same Computer](how-to-deploy-the-app-v-46-and-the-app-v--51-client-on-the-same-computer.md)

## <a href="" id="converting--previous-version--packages-using-the-package-converter-"></a>Converting "previous-version" packages using the package converter


Before migrating a package, created using App- 4.6 SP2 or earlier, to App-V 5.1, review the following requirements:

- You must convert the package to the **.appv** file format.

- The Package Converter supports only the direct conversion of packages that were created by using App-V 4.5 and later. To use the package converter on a package that was created using a previous version, you must use an App-V 4.5 or later version of the sequencer to upgrade the package, and then you can perform the package conversion.

For more information about using the package converter to convert a package, see [How to Convert a Package Created in a Previous Version of App-V](how-to-convert-a-package-created-in-a-previous-version-of-app-v51.md). After you convert the file, you can deploy it to target computers that run the App-V 5.1 client.

## Related topics

[App-V 5.1 supported configurations](app-v-51-supported-configurations.md)
