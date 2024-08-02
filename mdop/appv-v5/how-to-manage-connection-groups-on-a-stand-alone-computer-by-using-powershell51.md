---
title: Manage connection groups on a stand-alone computer by using Windows PowerShell
description: An App-V connection group allows you to run all the virtual applications as a defined set of packages in a single virtual environment.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 11/01/2016
---

# Manage connection groups on a stand-alone computer by using Windows PowerShell

An App-V connection group allows you to run all the virtual applications as a defined set of packages in a single virtual environment. For example, you can virtualize an application and its plug-ins by using separate packages, but run them together in a single connection group.

A connection group XML file defines the connection group that runs on the computer where you've installed the App-V client. For information about the connection group XML file and how to configure it, see [About the Connection Group File](about-the-connection-group-file51.md).

## <a href="" id="bkmk-add-pub-pkgs-in-cg"></a> To add and publish the App-V packages in the connection group

1.  To add and publish the App-V 5.1 packages to the computer running the App-V client, type the following command:

    Add-AppvClientPackage -path c:\\tmpstore\\quartfin.appv | Publish-AppvClientPackage

2.  Repeat **step 1** of this procedure for each package in the connection group.

## <a href="" id="bkmk-add-enable-cg-on-clt"></a> To add and enable the connection group on the App-V client

1.  Add the connection group by typing the following command:

    Add-AppvClientConnectionGroup -path c:\\tmpstore\\financ.xml

2.  Enable the connection group by typing the following command:

    Enable-AppvClientConnectionGroup -name "Financial Applications"

    When any virtual applications that are in the member packages are run on the target computer, they will run inside the connection group's virtual environment and will be available to all the virtual applications in the other packages in the connection group.

## <a href="" id="bkmk-enable-cg-for-user-poshtopic"></a> To enable or disable a connection group for a specific user

1.  Review the parameter description and requirements:

    -   The parameter enables an administrator to enable or disable a connection group for a specific user.

    -   You must use App-V 5.0 SP2 Hotfix Package 5 or later to use this parameter.

    -   You can run this cmdlet from the user or administrator session.

    -   You must be logged in with administrative credentials to use the parameter.

    -   The end user must be logged in.

    -   You must provide the end user's security identifier (SID).

2.  Use the following cmdlets, and add the optional **-UserSID** parameter, where **-UserSID** represents the end user's security identifier (SID):

    | Cmdlet                          | Examples                                                                                   |
    |---------------------------------|--------------------------------------------------------------------------------------------|
    | Enable-AppVClientConnectionGroup| Enable-AppVClientConnectionGroup "ConnectionGroupA" -UserSID S-1-2-34-56789012-3456789012-345678901-2345 |
    | Disable-AppVClientConnectionGroup| Disable-AppVClientConnectionGroup "ConnectionGroupA" -UserSID S-1-2-34-56789012-3456789012-345678901-2345 |

## <a href="" id="bkmk-admin-only-posh-topic-cg"></a> To allow only administrators to enable connection groups

1.  Review the description and requirement for using this cmdlet:

    -   Use this cmdlet and parameter to configure the App-V client to allow only administrators (not end users) to enable or disable connection groups.

    -   You must be using at least App-V 5.0 SP3 to use this cmdlet.

2.  Run the following cmdlet and parameter:

    | Cmdlet                      | Parameter and values                              | Example                                                |
    |-----------------------------|---------------------------------------------------|--------------------------------------------------------|
    | Set-AppvClientConfiguration | -RequirePublishAsAdmin                            | Set-AppvClientConfiguration -RequirePublishAsAdmin 1   |
    |                             | - 0 - False                                       |                                                        |
    |                             | - 1 - True                                        |                                                        |

## Related topics

[Operations for App-V 5.1](operations-for-app-v-51.md)

[Administering App-V 5.1 by Using PowerShell](administering-app-v-51-by-using-powershell.md)
