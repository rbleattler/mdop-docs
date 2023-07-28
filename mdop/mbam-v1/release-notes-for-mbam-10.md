---
title: Release Notes for MBAM 1.0
description: Release Notes for MBAM 1.0
author: aczechowski
ms.reviewer: 
manager: dansimp
ms.author: aaroncz
ms.prod: w10
ms.date: 08/30/2016
---


# Release Notes for MBAM 1.0

Read these release notes thoroughly before you install Microsoft BitLocker Administration and Monitoring (MBAM).

These release notes contain information that is required to successfully install MBAM. The release notes also contain information that isn't available in the product documentation. If there's a difference between these release notes and other MBAM documentation, the latest change should be considered authoritative. These release notes supersede the content that is included with this product.

## Known Issues with MBAM 1.0


This section contains release notes about the known issues with MBAM setup and installation.

### If you select the "Use a certificate to encrypt the network communication" option during Setup, existing database connections and dependent applications can stop functioning

You can configure MBAM for **Encrypted network communication** after you install either the Recovery and Hardware Database or the Compliance Status Database features. If you choose to configure MBAM for Encrypted network communication, MBAM Setup configures the instance of the SQL Server Database Engine to use Secure Sockets Layer (SSL) for communication between the applicable database and both the Administration and Monitoring Server and the Compliance and Audit Report Server features.

-   If the instance of the SQL Server Database Engine isn't already configured to use SSL, MBAM Setup configures it to do so. This can prevent applications that try to use non-MBAM databases on the instance of the SQL Server Database Engine from communicating with their databases.

-   If the instance of the SQL Server Database Engine is already configured to use SSL, it's configured to use the certificate that the user selected during setup. If this certificate differs from the one that was already in use, it can prevent applications that use SQL Server databases on the instance of the SQL Server Database Engine from running.

**WORKAROUND:** None

### MBAM Setup fails during installation when you use a local Administrator account

MBAM Setup fails when you use a local Administrator account. The log file contains the following information:

``` syntax
Locating group 'MBAM Report Users'
Adding <GUID>' to group 'MBAM Report Users'
Locating group 'MBAM Recovery and Hardware DB Access'
Adding 'S-1-5-20' to group 'MBAM Recovery and Hardware DB Access'
Exception: A new member could not be added to a local group because the member has the wrong account type.
 
  StackTrace: at System.DirectoryServices.AccountManagement.SAMStoreCtx.UpdateGroupMembership(Principal group, DirectoryEntry de, NetCred credentials, AuthenticationTypes authTypes)
   at System.DirectoryServices.AccountManagement.SDSUtils.ApplyChangesToDirectory(Principal p, StoreCtx storeCtx, GroupMembershipUpdater updateGroupMembership, NetCred credentials, AuthenticationTypes authTypes)
   at System.DirectoryServices.AccountManagement.SAMStoreCtx.Update(Principal p)
   at Microsoft.Windows.Mdop.BitlockerManagement.Setup.Groups.CreateGroupsDeferred(Session session)
  InnerException:Exception: A new member could not be added to a local group because the member has the wrong account type.
 
    InnerException:StackTrace: at System.DirectoryServices.AccountManagement.UnsafeNativeMethods.IADsGroup.Add(String bstrNewItem)
   at System.DirectoryServices.AccountManagement.SAMStoreCtx.UpdateGroupMembership(Principal group, DirectoryEntry de, NetCred credentials, AuthenticationTypes authTypes)
CustomAction MbamCreateGroupsDeferred returned actual error code 1603 (note this may not be 100% accurate if translation happened inside sandbox)
Action ended 11:41:29: InstallExecute. Return value 3.
```

**WORKAROUND:** Use a domain account with administrative credentials on the server computer when you install MBAM.

### MBAM Setup reconfigures the instance of the SQL Server Database Engine to not use SSL if you select "Don't encrypt network communication"

When you install either the Recovery and Hardware Database or the Compliance Status Database, you can use Setup to configure MBAM by selecting **Encrypted network communication**. If you decide not to encrypt the network communication, MBAM Setup reconfigures the instance of the SQL Server Database Engine so that it doesn't use SSL.

-   If the instance of the SQL Server Database Engine is already configured to use SSL, MBAM Setup disables SSL on the instance of the SQL Server Database Engine. This changes the communication security between the applications that use databases that aren't related to MBAM databases on the instance of the SQL Server Database Engine.

**WORKAROUND:** None

### Missing prerequisite for the Internet Information Services (IIS) Management Scripts and Tools web server feature

MBAM Setup is dependent on the IIS Management Scripts and Tools web server feature, but it isn't an enforced prerequisite. Server setup lets you install MBAM when this feature is missing. However, this causes the backup service MBAM VSS Writer to start and then stop, because it can't locate the Windows Management Instrumentation (WMI) and the Internet Information Services (IIS) provider. There's no error message for this condition, except that which occurs in the event log. Installation of MBAM without IIS Management Scripts and Tools causes the backup operations not to run for MBAM.

**WORKAROUND:** Ensure that the IIS Management Scripts and Tools web server feature is installed before you start the MBAM Setup.

### MBAM Setup stops responding during the "Installing selected features" phase when setup is configured to use a certificate

MBAM Setup stops responding during the **Installing selected features** phase of setup. This occurs during the installation of the Recovery and Hardware Database or the Compliance Status Database, after you select the **Use a certificate to encrypt the network communication** option. Furthermore, the MBAM Setup stops responding if the instance of the SQL Server Database Engine can't access the certificate that was specified during setup.

**WORKAROUND:** Update the permissions on the certificate, so that the Windows service for the applicable instance of the SQL Server Database Engine can access the certificate. You can also change the account under which the instance of the SQL Server Database Engine runs, for the database engine to use the certificate. To determine the permissions for the certificate, type the following command at the command prompt: **certutil -v -store MY**

### MBAM Setup pauses when you install SQL Server Reporting Services

During MBAM installation, when you select an instance of SQL Server Reporting Services (SSRS) and SSRS instance isn't available or it's configured incorrectly, the MBAM Setup might pause for up to one minute while it attempts to communicate with the SSRS instance.

**WORKAROUND:** Wait for at least one minute for MBAM Setup to resume while the Setup program attempts to contact the instance of SSRS.

### Administration and Monitoring Server doesn't run after setup

After MBAM Setup successfully installs the Administration and Monitoring Server feature, MBAM displays error messages when you try to access the MBAM administrator website. This issue occurs for one of the following reasons:

-   One or more prerequisites on the Administration and Monitoring Server were removed after the MBAM installation.

-   One or more prerequisites were installed on the server and later they were removed before running the MBAM Setup.

**WORKAROUND:** Review the MBAM documentation and confirm that all MBAM prerequisites are installed.

### Clicking documentation links during Setup results in an application error after Setup is finished

When you select a documentation link during setup and then close the Setup program by clicking **Cancel** or **Finish** after Setup has successfully finished, an application error message appears. The problem is caused by an access violation error in the Windows Task Scheduler.

**WORKAROUND:** None. You can ignore this error.

### Failed MBAM Setup doesn't remove new databases

If the MBAM Setup fails, Setup might not remove the newly created databases. This can cause failures during subsequent installations.

**WORKAROUND:** Choose a different name for the database instance during the subsequent installation.

### MBAM Setup doesn't recognize valid network load-balancing cluster certificates

During the MBAM Administration and Monitoring Server installation, with the network encryption option selected, the cluster certificate isn't recognized as a valid certificate. It's recognized as valid when the certificate for communication with the database is installed, but it's rejected for communication by the load-balancing cluster.

**WORKAROUND:** Confirm that the certificate revocation list (CRL) associated with the certificate is accessible, or use a certificate that doesn't require validation by using the CRL.

## Related information

[About MBAM 1.0](about-mbam-10.md)
