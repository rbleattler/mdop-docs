---
title: Server event logs
description: The sections in this article provide information about MBAM server log event IDs.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
ms.topic: reference
---

# Server event logs

The sections in this article provide information about MBAM server log event IDs.

## Configuration

The following sections contain messages and troubleshooting information for event IDs that can occur on the MBAM server during configuration.

### Event ID 103

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: VssRegistrationException

#### ID 103 message

An exception was thrown during VSS registration.

### Event ID 104

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: VssDeregistrationException

#### ID 104 message

An exception was thrown during VSS deregistration.

### Event ID 300

Source: Microsoft-Windows-MBAM-Server/Admin

Event symbol: CmdletError

#### ID 300 message

Failed in removing folder.

#### ID 300 troubleshooting

Indicates that a terminating error occurred while performing a task. Inspect other event messages in the log to further diagnose MBAM setup.

### Event ID 301

Source: Microsoft-Windows-MBAM-Server/Admin

Event symbol: cmdletUnexpectedError

#### ID 301 message

Unexpected Cmdlet error.

### Event ID 302

Source: Microsoft-Windows-MBAM-Server/Admin

Event symbol: CmdletWarning

#### ID 302 message

Cmdlet warning.

### Event ID 303

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: CmdletInformation

#### ID 303 message

Cmdlet information.

#### ID 303 troubleshooting

Informational only, no troubleshooting required. The event indicates that a task is taking place by the cmdlets such as enabling or disabling a feature or canceling an operation.

### Event ID 400

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ConfiguratorError

#### ID 400 message

Configurator error.

#### ID 400 troubleshooting

Indicates that an error occurred while launching the MBAM Configurator. Ensure that the user has adequate privileges to launch the MBAM Configurator.

### Event ID 401

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ConfiguratorUnexpectedError

#### ID 401 message

Unexpected Configurator error.

#### ID 401 troubleshooting

Indicates that a terminating error has occurred while performing an MBAM Configurator task. The error message contains more details about the error. Inspect other error messages in the event log to further diagnose MBAM setup. Known errors include:

- Failure to retrieve or validate a certificate that the user selected
- Failure to parse the reports URL
- Failure to open event logs for the user

### Event ID 402

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ConfiguratorWarning

#### ID 402 message

Configurator warning.

#### ID 402 troubleshooting

Indicates that an MBAM Configurator task isn't complete as expected but didn't fail completely. Known tasks include missing certificate in the LocalMachine\My store that was configured in the web application feature, or a timeout for a pending task.

### Event ID 410

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: ConfiguratorInformation

#### ID 410 message

Configurator information.

#### ID 410 troubleshooting

Informational only, no troubleshooting required. The event indicates that the MBAM Configurator start a task.

Known tasks include:

- Launching the configurator
- Checking software prerequisites for an MBAM feature
- Validating parameters for an MBAM feature
- Enabling/disabling/committing an MBAM feature
- Generating a PowerShell script from the configurator

### Event ID 500

Source: Microsoft_Windows_MBAM_Server_Admin

Event symbol: WebProviderUnexpectedError

#### ID 500 message

Web application provider unexpected error.

#### ID 500 troubleshooting

Indicates that an error occurred while enabling and configuring an MBAM website or web service in IIS. Known errors include:

- Failure to find IIS WWW root folder
- Failure to access IIS configuration in `web.config` due to malformed files or missing settings
- Failure to create or remove a web application
- IIS access violation

This error is also logged if MBAM can't access Active Directory (AD) to validate user accounts. Verify that IIS is installed, correctly configured, and the IIS service is running. Verify that all the MBAM software prerequisite checks pass. Verify that the user has the correct permissions to create web applications on the IIS instance. Verify that the user has access to read user account objects in AD.

### Event ID 501

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: WebProviderError

#### ID 501 message

Web application provider unexpected error.

#### ID 501 troubleshooting

Indicates that an error occurred while enabling, disabling, or configuring an MBAM website or web service in IIS. Known errors include:

- Failure to read basic or WSHttp binding information from IIS
- Missing identity section or DNS entry in identity section in IIS config files
- Failure to open registry key `HKLM\SOFTWARE\Microsoft\InetStp`
- Failure to read value `PathWWWRoot` from registry key `HKLM\SOFTWARE\Microsoft\InetStp`
- User is trying to specify a virtual directory name with a reserved name for MBAM

Verify that IIS is installed and correctly configured. Verify that the registry key `HKLM\SOFTWARE\Microsoft\InetStp:PathWWWRoot` exists and is accessible. Verify that the binding information in IIS isn't corrupt.

### Event ID 502

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: WebProviderWarning

#### ID 502 message

Web application provider warning.

#### ID 502 troubleshooting

Indicates that a nonterminating error occurred while enabling an MBAM website or web service. Known errors include:

- Failure to access AD to validate the Service Principal Name (SPN) on the app pool account
- Failure to validate SPN because it's assigned to multiple accounts in AD
- Failure to register an SPN on the app pool account in AD
- SPN is registered on an account other than the app pool in AD
- Failure to remove SPN from the app pool account in AD during a rollback operation
- Failure to check if the IIS_IUSRS group is granted the **logon as batch** privilege on the IIS server

The event message contains more information about the specific error. Verify that AD is reachable from the server where MBAM setup is running. Verify that the user who is running the MBAM setup has permissions to read the app pool account in AD. If an SPN is already registered on the app pool account in AD, then make sure that it isn't registered on other accounts.

### Event ID 503

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: WebProviderInformation

#### ID 503 message

Web application provider information. {Description}

#### ID 503 troubleshooting

Informational only; no troubleshooting required. The event indicates that the MBAM Setup starts a task. Known tasks include getting IIS configuration such as binding information and root site, and configuring Service Principal Name (SPN).

### Event ID 600

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: SetupUnexpectedError

#### ID 600 message

Unexpected setup error.

#### ID 600 troubleshooting

Indicates that a terminating error occurred while enabling/disabling or configuring an MBAM feature. Known errors include:

- Failure to roll back a task after an error
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to read SQL version information
- Failure to register VSS writer in SQL

The event message contains more information about the specific error. Verify that all MBAM software prerequisite checks pass. Make sure the MBAM registry path, if it exists, `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM Server` and all the subkeys are readable. Verify that AD is reachable from the server where MBAM setup is running. Verify that the user who is running the MBAM setup has permissions to read in AD.

For a successful VSS writer registration, verify that a supported version of SQL is installed and an instance is accessible to the user who is running the MBAM setup. If disabling an MBAM feature or uninstalling MBAM, verify that all files such as log files and `web.config` files are closed so MBAM can remove its websites and web services.

### Event ID 601

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: SetupError

#### ID 601 message

Setup error.

#### ID 601 troubleshooting

Indicates that a terminating error occurred while enabling/disabling or configuring an MBAM feature. Known errors include:

- Failure to read MBAM configuration in IIS
- Corrupt appSettings section in IIS configuration or misconfigured settings
- Failure to validate host name
- Failure to read SQL version information
- Failure to register VSS writer in SQL

The event message contains more information about the specific error. Verify that IIS is installed and configured correctly. Verify that all MBAM software prerequisite checks pass. For a successful VSS writer registration, verify that a supported version of SQL is installed and an instance is accessible to the user who is running the MBAM setup.

### Event ID 602

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: SetupWarning

#### ID 602 message

Setup warning.

#### ID 602 troubleshooting

Indicates that a nonterminating error occurred while enabling\disabling or configuring an MBAM feature such as Configuration Manager (CM) Integration or MBAM web application. Known errors include: failure to delete MBAM Reports from SRS Role point in the CM, and failure to resolve a host name from the domain controller. The event message contains more information about the specific error.

Verify that AD is reachable from the server where MBAM setup is running. Verify that the user who is running the MBAM setup has remove permissions on the SSRS instance that is configured as an SRS Role point in CM.

### Event ID 603

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: SetupInformation

#### ID 603 message

Setup information.

#### ID 603 troubleshooting

Informational only, no troubleshooting required.

### Event ID 605

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: WebProviderSoftwareCheckFailure

#### ID 605 message

Web application cannot be enabled because one or more software dependencies are not being met.

#### ID 605 troubleshooting

During MBAM web site/web service installation, MBAM setup verifies if necessary prerequisites are in place. This message indicates that MBAM failed to install the requested web site/web service as the necessary prerequisite is missing. Refer to error messages preceding this message to get more information about missing prerequisites.

### Event ID 606

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: SetupParameterValidationFailure

#### ID 606 message

The parameter that is needed to enable the server feature was either not specified or it did not pass the validation.

#### ID 606 troubleshooting

Indicates that the parameter that is needed to configure an MBAM feature was either not specified or it didn't pass the validation.

### Event ID 607

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: SetupParameterValidationFailureWithError

#### ID 607 message

Error encountered while trying to validate specified parameter that is needed to enable the server feature.

#### ID 607 troubleshooting

Indicates that an error was encountered while trying to validate specified parameter that is needed to enable the server feature.

### Event ID 700

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: DbProviderUnexpectedError

#### ID 700 message

DB provider unexpected error.

### Event ID 701

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: DbProviderError

#### ID 701 message

DB provider error.

#### ID 701 troubleshooting

The message contained in the EventDetails section should provide more information about the actual error. Some of the areas to verify:

- MBAM Setup failed to connect to the database using the provided connection information. Verify the connection string details provided to MBAM setup.
- MBAM Setup couldn't connect to the given database using the supplied domain account credentials. Verify that the domain account username and password are valid.
- MBAM Setup couldn't connect to the given database using the supplied domain account credentials. Verify that the provided domain account has the necessary permissions in place to connect to the MBAM database.
- MBAM `dacpac` fails if a newer version of the MBAM database is already installed. Verify that a new version of MBAM databases doesn't exist on the given SQL server.

### Event ID 702

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: DbProviderWarning

#### ID 702 message

DB provider warning.

### Event ID 703

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: DbProviderInformation

#### ID 703 message

DB provider information.

#### ID 703 troubleshooting

Informational only, no troubleshooting required.

### Event ID 704

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: DbProviderDacError

#### ID 704 message

An error occurred while deploying the Data-Tier Application.

#### ID 704 troubleshooting

MBAM packages its databases as data tier applications and tries to register them using Microsoft.SqlServer.Dac.DacServices. The DAC service reports the error message in context. The event should contain detailed information about what caused it. To troubleshoot and fix the issue, read the information in the error message.

### Event ID 705

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: DbProviderDacWarning

#### ID 705 message

A warning occurred while deploying the Data-Tier Application.

#### ID 705 troubleshooting

MBAM packages its databases as data tier application and tries to register them using Microsoft.SqlServer.Dac.DacServices. The DAC service reports the warning message in context. The event should contain detailed information about what caused it. To troubleshoot and fix the issue, read the information in the error message.

### Event ID 706

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: DbProviderDacInformation

#### ID 706 message

A message was raised while deploying the Data-Tier Application.

#### ID 706 troubleshooting

Informational only, no troubleshooting required.

### Event ID 800

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ReportProviderUnexpectedError

#### ID 800 message

Report provider unexpected error.

#### ID 800 troubleshooting

##### Report provider unexpected error. {Description} {exceptionDetails}

Some of the possible exception details:

- An error occurred while getting the name of directory '{directoryName}'

- An exception occurred while getting files for directory '{directoryName}'

- An exception occurred while enumerating directories in directory '{directoryName}'

- An exception occurred while reading all bytes for file '{fileName}'

During MBAM installation, MBAM setup unzips all the report files to the specified installation path. As a part of report installation, the install module tries to access the unzipped report files at the installation path and communicates with SQL Reporting services to publish the report files. These errors occur when MBAM can't access the files/folders at the unzipped installation path.

Some tips to troubleshoot this issue:

- Verify that MBAM is installed.
- Verify that the registry key `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM Server\InstallationPath` is present and accessible to the executing user.
- Verify that the path to report files under MBAM InstallationPath doesn't exceed 248 characters.
- Verify that the MBAM setup folder or the files contained in the MBAM installation path weren't modified since installation.
- Verify that the user running the setup is authorized to read from/write to the MBAM installation folder.

##### Reporting Services connectivity failed. {exceptionDetails}

During MBAM reports installation, the module tries to communicate with SSRS web services to create folders and publish reports. This message indicates that MBAM couldn't find or communicate with SSRS web services.

Some tips to troubleshoot this issue:

- Verify that SSRS is installed on the specified machine.
- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user running the setup is authorized to access SSRS.

##### Failed to remove the MBAM Reports using Reporting Services instance URL '{SSRSInstanceUrl}'. Make sure the SSRS instance required for MBAM Reports is running and configured correctly

When MBAM installation fails or when the user disables MBAM Reporting features, the setup module removes SSRS reports. This message indicates that MBAM failed to remove SSRS reports.

Some tips to troubleshoot this issue:

- Verify that SSRS is installed on the specified machine.
- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user running the setup is authorized to access SSRS.

##### An error occurred while publishing reports. {exceptionDetails}

During MBAM reports installation, the module tries to communicate with SSRS web services to create folders and publish reports. This message indicates that the SSRS web service reported an exception while publishing reports.

Some tips to troubleshoot this issue:

- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user running the setup is authorized to access/publish reports to SSRS.

##### A policy for group user name '{userName}' already exists. In case this is not correct, manually revise the Reporting Service for duplicate or invalid policies

After MBAM setup publishes MBAM reports, it tries to create MBAM Report Users roles, if they don't exist already. It then sets the corresponding user policy. This error indicates that the SSRS web service threw an exception while setting up the report user role policy. Follow the instructions in the event message.

##### An error occurred while validating access to SSRS {exceptionDetails}

As part of the prerequisite check, MBAM setup verifies if the user has the necessary permissions to access/create folders under SSRS. The error message indicates that an exception occurred while verifying access to SSRS. For debugging tips, refer to the exception details.

##### Errors with SSRS URL

- **A SOAP error occurred while checking the SSRS URL. {exceptionDetails}**

- **A web error occurred while checking the SSRS URL. {exceptionDetails}**

- **An HTTP/HTTPS error occurred while checking the SSRS URL. {exceptionDetails}**

- **An error occurred while checking the SSRS URL. {exceptionDetails}**

As part of the prerequisite check, MBAM setup retrieves URLs associated with the supplied SSRS instance and tries to communicate with the SSRS web service. This error message indicates that the SSRS web service at the given URL threw an exception. For more information, see the exception details.

Some tips to resolve SSRS communication issues:

- Verify that SSRS is installed on the specified machine.
- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user running the setup is authorized to access SSRS.

##### An error occurred while retrieving the SSRS version. {exceptionDetails}

As part of the prerequisite check, MBAM setup queries WMI to retrieve the version number associated with the supplied SSRS instance. This error message indicates that an exception occurred while querying WMI. For more information, see the exception details.

Some checks you can perform:

- Verify that SSRS with the given instance name is installed on the specified machine.
- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user executing the setup is authorized to query the SSRS class under the WMI namespace.

##### Errors with WMI

- **The current user is not authorized to access the WMI namespace '{ssrsWMINamespace}'.**

- **An error occurred while enumerating the namespace '{ssrsWMINamespace}'. RPC server for SSRS WMI provider on the local host is not found.**

- **An error occurred while enumerating the namespace '{ssrsNamespace}'. Unable to find an instance of SSRS on the local host.**

- **An error occurred while accessing WMI. RPC server for instance '{ssrsInstance}' was not found.**

- **An error occurred while accessing WMI. Instance name '{ssrsInstanceName}' is not correct.**

- **An error occurred while accessing WMI. Unable to find instance '{ssrsInstanceName}' on the local host.**

As part of the prerequisite check, MBAM setup queries WMI to retrieve the WMI namespace associated with the given instance. This error message indicates that an exception occurred while querying WMI. For more information, see the exception details.

Some checks you can perform:

- Verify that SSRS with the given instance name is installed on the specified machine.
- Using the SSRS console, verify that SSRS is enabled and running.
- Verify that the user running the setup is authorized to access/query the SSRS class under the WMI namespace.

### Event ID 801

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ReportProviderError

#### ID 801 message

Report provider unexpected error.

#### ID 801 troubleshooting

Given the SQL server reporting services instance name, MBAM tries to find the WMI namespace corresponding to the reporting instance and connect to it. This error occurs if MBAM encounters an exception when MBAM searches for or tries to connect to SSRS WMI namespace. Read the information in the error messages logged in the MBAM setup channel before this message to get more details. Here are some things you can check:

- Verify that SSRS with the supplied instance name is up and running.
- Verify that the user account running MBAM installation has the necessary permissions to query/connect to the SSRS WMI namespace.

### Event ID 802

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: ReportProviderWarning

#### ID 802 message

Report provider warning.

### Event ID 803

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: ReportProviderInformation

#### ID 803 message

Report provider information.

#### ID 803 troubleshooting

Informational only, no troubleshooting required.

### Event ID 900

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: CMProviderUnexpectedError

#### ID 900 message

CM provider unexpected error.

#### ID 900 troubleshooting

Indicates that a terminating error occurred while enabling/disabling or configuring the Configuration Manager (CM) Integration feature in MBAM. Known errors include:

- Failure to connect to the CM site server via the SMS Provider
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to locate the Configuration Manager Console installation on the local machine
- Failure to retrieve information for the SSRS instance that is configured as an SRS Role point in CM

The event message contains more information about the specific error. Verify that all MBAM software prerequisite checks pass. Verify that the MBAM registry path, if it exists, `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM Server` and all the subkeys are readable. Verify that MBAM is being integrated with a supported version of Configuration Manager. Verify that the Configuration Manager Console is installed on the machine where the MBAM setup is being invoked and that the console can be used to connect to the target CM Site Server. Verify that a valid SSRS instance is configured as an SRS Role point in CM and that the user who is running the MBAM setup has read/write permissions on the SSRS instance.

### Event ID 901

Source: Microsoft-Windows-MBAM-Server /Admin

Event symbol: CMProviderError

#### ID 901 message

CM provider unexpected error.

#### ID 901 troubleshooting

Indicates that a terminating error occurred while enabling/disabling or configuring the Configuration Manager (CM) Integration feature in MBAM. Known errors include:

- Failure to connect to the CM Site Server via the SMS Provider
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to locate the Configuration Manager Console installation on the local machine
- Missing ConfigMgr folder in SSRS as the root folder for the SRS Role point reports
- Missing ConfigMgr shared data source in SSRS
- Failure to deploy SSRS reports in the SSRS instance that is configured as an SRS Role point in CM
- Failure to create Configuration Items and baselines in CM

The event message contains more information about the specific error. Verify that all MBAM software prerequisite checks pass. Verify that the MBAM registry path, if it exists, `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM Server` and all the subkeys are readable. Verify that MBAM is being integrated with a supported version of Configuration Manager. Verify that the Configuration Manager Console is installed on the machine where the MBAM setup is being invoked and that the console can be used to connect to the target CM Site Server. Verify that the user has the required read/write permissions to create Configuration Items, Baselines, and Collections in CM. Verify that a valid SSRS instance is configured as an SRS Role point in CM and that the user who is running the MBAM setup has read/write permissions on the SSRS instance.

### Event ID 902

Source: Microsoft_Windows_MBAM_Server_Admin

Event symbol: CMProviderWarning

#### ID 902 message

CM provider warning.

#### ID 902 troubleshooting

Indicates that a nonterminating error occurred while enabling the Configuration Manager (CM) Integration feature. Known errors include: failure to commit collection rules in the MBAM Supported Computers collection in CM, and other SSRS and network related errors.

The event message contains more information about the specific error. Some operations that caused this warning are retired after the warning. If after several retries the error persists, then MBAM might end with an actual error. Inspect other event messages in the log to further diagnose MBAM setup.

### Event ID 903

Source: Microsoft-Windows-MBAM-Server/Operational

Event symbol: CMProviderInformation

#### ID 903 message

CM provider information.

#### ID 903 troubleshooting

Informational only, no troubleshooting required.

## Operation

The following sections contain messages and troubleshooting information for event IDs that can occur while MBAM is running.

### Event ID 1

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: WebAppSpnError

#### ID 1 message

Application: {SiteName}{VirtualDirectory} is missing the following Service Principal Names (SPNs):{ListOfSpns} Register the required SPNs on the account: {ExecutionAccount}.

#### ID 1 troubleshooting

For Integrated Windows Authentication to succeed, necessary SPNs need to be in place. This message indicates that the SPN required for MBAM application isn't correctly configured. Details contained in this event should provide more information. For more information, see [MBAM 2.5 server prerequisites for stand-alone and configuration manager integration topologies](mbam-25-server-prerequisites-for-stand-alone-and-configuration-manager-integration-topologies.md#bkmk-prereqsams) |

### Event ID 4

Source: Microsoft-Windows-MBAM-Web/Operational

Event symbol: PerformanceCounterError

#### ID 4 message

An error occurred while retrieving a performance counter.

Message: {EventMessage}

Category: {CategoryOfPerformanceCounter}

Performance Counter: {NameOfPerformanceCounter}

Instance: {Name of performance counter category instance}

Exception: {ExceptionThrown}

Trace message contains the actual exception message, some of which are explained here:

- **ArgumentNullException**: This exception is thrown if the category, counter, or instance of requested Performance counter is invalid.

- **System.InvalidOperationException**:

  - categoryName is an empty string.
  - counterName is an empty string.
  - The read/write permission setting requested is invalid for this counter.
  - The category specified doesn't exist (if readOnly is true).
  - The category specified isn't a .NET Framework custom category (if readOnly is false).
  - The category specified is marked as multi-instance and requires the performance counter to be created with an instance name.
  - instanceName is longer than 127 characters.
  - categoryName and counterName are localized into different languages.

- **System.ComponentModel.Win32Exception**: An error occurred when accessing a system API.

- **System.PlatformNotSupportedException**: The platform is Windows 98 or Windows Millennium Edition (ME), which doesn't support performance counters.

- **System.UnauthorizedAccessException**: Code that is executing without administrative privileges attempted to read a performance counter.

#### ID 4 troubleshooting

The message contained in the event provides more details around the exception that was thrown. If a System.UnauthorizedAccessException was thrown, verify that MBAM execution account (app pool) has access to performance counter APIs.

### Event ID 100

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: AdminServiceRecoveryDbError

#### ID 100 message

**GetMachineUsers**: An error occurred while getting user information from the database. Message: {message} -or-

**GetRecoveryKey**: An error occurred while getting recovery key from the database. Message: {message} -or-

**GetRecoveryKey**: An error occurred while getting user information from the database. Message: {message} -or-

**GetRecoveryKeyIds**: An error occurred while getting recovery key Ids from the database. Message: {message} -or-

**GetTpmHashForUser**: An error occurred while getting TPM hash data from the recovery database. Message: {message} -or-

**GetTpmHashForUser**: An error occurred while getting TPM hash data from the recovery database. Message: {message} -or-

**QueryDriveRecoveryData**: An error occurred while getting drive recovery data from the database. Message: {message} -or-

**QueryRecoveryKeyIdsForUser**: An error occurred while getting recovery key Ids from the database. Message: {message} -or-

**QueryVolumeUsers**: An error occurred while getting user information from the database.

#### ID 100 troubleshooting

This message is logged whenever there's an exception while communicating with the MBAM recovery database. Read through the information contained in the trace to get specific details about the exception.

### Event ID 101

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: AdminServiceComplianceDbError

#### ID 101 message

**GetRecoveryKey**: An error occurred while logging an audit event to the compliance database. Message: {message} -or-

**GetRecoveryKeyIds**: An error occurred while logging an audit event to the compliance database. Message: {message} -or-

**GetTpmHashForUser**: An error occurred while logging an audit event to the compliance database. Message: {message} -or-

**QueryRecoveryKeyIdsForUser**: An error occurred while logging an audit event to the compliance database. Message: {message} -or-

**QueryDriveRecoveryData**: An error occurred while logging an audit event to the compliance database. Message: {message}

#### ID 101 troubleshooting

This message is logged whenever there's an exception while communicating the MBAM compliance database. Read through the information contained in the trace to get specific details about the exception.

### Event ID 102

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: AgentServiceRecoveryDbError

#### ID 102 troubleshooting

This message indicates an exception when MBAM Agent service tries to communicate with the recovery database. Read through the message contained in the event to get specific information about the exception.

### Event ID 103

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: AgentServiceError

#### ID 103 message

Unable to detect client machine account or data migration user account. -or-

Account verification failed for caller identity.

#### ID 103 troubleshooting

Whenever a call is made to the `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest`, or `GetTpmHash` web methods on MBAM Agent services, it retrieves the caller context to obtain caller credentials. If the caller context is null or empty, the MBAM Agent service logs "Unable to detect client machine account or data migration user account."

The message "Account verification failed for caller identity" is logged if the web method is expecting the caller to a be computer account and the caller isn't a computer account, or if the web method expects the caller to be a user account and the caller isn't a user account or member of data migration group account.

### Event ID 104

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: StatusServiceComplianceDbConfigError

#### ID 104 message

"The Compliance database connection string in the registry is empty."

#### ID 104 troubleshooting

This message is logged whenever the compliance database connection string is invalid.

Verify the value at the following registry key: `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`

### Event ID 105

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: StatusServiceComplianceDbError

#### ID 105 troubleshooting

This error indicates that MBAM websites/web services were unable to connect to the MBAMCompliance database.

### Event ID 106

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: HelpdeskError

#### ID 106 message

The request to URL {url} caused an internal error. -or-

An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration. -or-

An error occurred while verifying Service Principal Name (SPN) registration.

#### ID 106 troubleshooting

Indicates that Helpdesk application raised an unhandled exception. To find the specific exception, review the log entries in the MBAM Admin operational channel. -or-

During the initial Helpdesk website load operation, an SPN check is performed. To verify SPN, the Helpdesk requires execution account information, IIS Sitename, and ApplicationVirtualPath corresponding to Helpdesk website. This error message is logged when one or more of these SPNs are invalid or missing. -or-

This message indicates that a security exception is thrown while performing SPN verification. Refer to the exception contained in event details section.

### Event ID 107

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: SelfServicePortalError

#### ID 107 message

An error occurred while getting recovery key for a user. EventDetails:{ExceptionMessage} -or-

An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration. EventDetails: User: {username Identity} Application:{SiteName\ApplicationVirtualPath} -or-

An error occurred while verifying Service Principal Name (SPN) registration. EventDetails:{ExceptionMessage}

#### ID 107 troubleshooting

Indicates that an unexpected exception was thrown when a request was made to retrieve recovery key. Refer to the exception message contained in event details section. If tracing is enabled on MBAM Helpdesk, refer to trace data to obtain detailed exception messages. -or-

During an initial load operation, the Self-Service Portal (SSP) retrieves execution account information, IIS Sitename, and ApplicationVirtualPath corresponding to the Self-Service website to verify SPN. This error message is logged when one or more of these SPNs are invalid. -or-

This message indicates that a security exception was thrown while performing SPN verification. Refer to the exception contained in event details section.

### Event ID 108

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: DomainControllerError

#### ID 108 message

An error occurred while resolving domain name {DomainName}, A memory allocation failure occurred. -or-

Could not invoke DsGetDcName method. EventDetails:{ExceptionMessage}

#### ID 108 troubleshooting

To resolve domain name, MBAM uses the `DsGetDcName` Windows API. This message is logged when this API returns `ERROR_NOT_ENOUGH_MEMORY`, which indicates a memory allocation failure. -or-

This message indicates that `DsGetDcName` API method is unavailable on the hosting system.

### Event ID 109

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: WebAppRecoveryDbError

#### ID 109 message

An error occurred while reading the configuration of the Recovery database. The connection string to the Recovery database is not configured. Message: {message}

**DoesUserHaveMatchingRecoveryKey**: An error occurred while getting recovery key Ids for a user. Message: {message}

**QueryDriveRecoveryData**: An error occurred while getting drive recovery data. Message: {message}

**QueryRecoveryKeyIdsForUser**: An error occurred while getting recovery key Ids for a user. Message: {message}

An error occurred while getting TPM password hash from the Recovery database. EventDetails: {ExceptionMessage}

#### ID 109 troubleshooting

This message indicates that recovery database connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` is invalid. Verify the given registry key value.

### Event ID 110

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: WebAppComplianceDbError

#### ID 110 message

An error occurred while reading the configuration of the Compliance database. The connection string to the Compliance database is not configured. -or-

**GetRecoveryKeyForCurrentUser**: An error occurred while logging an audit event to the Compliance database. Message: {message} -or-

**QueryRecoveryKeyIdsForUser**: An error occurred while logging an audit event to the Compliance database. Message: {message} -or-

**QueryRecoveryKeyIdsForUser**: An error occurred while logging an audit event to the compliance database. Message: {message}

#### ID 110 troubleshooting

This message indicates that compliance db connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` is invalid. Verify the value corresponding to this registry key.

### Event ID 111

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: WebAppDbError

#### ID 111 troubleshooting

These errors indicate one of the following two conditions:

- MBAM websites/webservices were unable to either connect to MBAMCompliance OR MBAMRecovery database.
- MBAM websites/webservices execution account (app pool account) couldn't run the GetVersion stored procedure on MBAMCompliance OR MBAMRecovery database.

The message contained in the event provides more details about the exception.

### Event ID 112

Source: Microsoft-Windows-MBAM-Web/Admin

Event symbol: WebAppError

#### ID 112 message

An error occurred while verifying Service Principal Name (SPN) registration. EventDetails:{ExceptionMessage}

#### ID 112 troubleshooting

To perform SPN verification, MBAM queries Active Directory to retrieve a list of SPNs mapped to the execution account. MBAM also queries the `ApplicationHost.config` to obtain MBAM website bindings. This error message indicates that MBAM couldn't communicate with Active Directory or it couldn't load the `ApplicationHost.config` file.

Verify that the execution account (app pool account) has permissions to query AD or the `ApplicationHost.config` file. Also verify the site binding entries in the `ApplicationHost.config` file.

### Event ID 200

Source: Microsoft-Windows-MBAM-Web/Operational

Event symbol: HelpDeskInformation

#### ID 200 message

The administration website application successfully found and connected to a supported version of the Recovery database. -or-

The administration website application successfully found and connected to a supported version of the Compliance database.

#### ID 200 troubleshooting

Indicates successful connection to the Recovery/Compliance database from the MBAM Helpdesk website.

### Event ID 201

Source: Microsoft-Windows-MBAM-Web/Operational

Event symbol: SelfServicePortalInformation

#### ID 201 message

The Self-Service Portal application successfully found and connected to a supported version of the Recovery database. -or-

The Self-Service Portal application successfully found and connected to a supported version of the Compliance database.

#### ID 201 troubleshooting

Indicates successful connection to the Recovery/Compliance database from the MBAM Self-Service Portal.

### Event ID 202

Source: Microsoft-Windows-MBAM-Web/Operational

Event symbol: WebAppInformation

#### ID 202 message

Application has its SPNs registered correctly.

#### ID 202 troubleshooting

Indicates that the SPNs required for the MBAM Helpdesk website are correctly registered against the executing account.

## Related articles

[Client event logs](client-event-logs.md)
