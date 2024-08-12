---
title: How to move the MBAM 2.5 databases
description: Use these procedures to move the Compliance and Audit database and Recovery database from one computer to another.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/15/2018
---

# How to move the MBAM 2.5 databases

Use these procedures to move the Compliance and Audit database and Recovery database from one computer to another. For example, from Server A to Server B.

> [!NOTE]
> It's important that the databases be restored to Machine B PRIOR to running the MBAM Configuration Wizard to update/configure them.

> [!IMPORTANT]
> Before proceeding with configuring MBAM, install the latest MDOP servicing release update. Otherwise your database server isn't recognized or supported. When trying to validate the database configuration, the configuration wizard reports an error:
>
> "An error occurred deploying the Data Tier Application ---> Microsoft.SqlServer.Dac.DacServicesException: database source is not a supported version of SQL Server"
>
> [October 2020 servicing release for Microsoft Desktop Optimization Pack](https://support.microsoft.com/topic/october-2020-servicing-release-for-microsoft-desktop-optimization-pack-9c509089-51d3-0877-15c5-04b83313b7c9)

If the databases are NOT present, the Configuration Wizard creates NEW, empty, databases. When your existing databases are then restored, this process breaks the MBAM configuration.

Restore the databases first, then run the MBAM Configuration Wizard. Choose the database option and the Configuration Wizard connects to the databases you restored. It  upgrades them if needed as part of the process.

If you move multiple features, move them in the following order:

1.  Recovery database

2.  Compliance and Audit database

3.  Reports

4.  Administration and Monitoring website

5.  Self-Service Portal

>[!NOTE]
>To run the example Windows PowerShell scripts provided in this topic, you must update the Windows PowerShell execution policy to enable scripts to be run. For more information, see [Get started with PowerShell](/powershell/scripting/learn/ps101/01-getting-started#execution-policy).

## Move the Recovery database

The high-level steps for moving the Recovery database are:

1.  Stop all instances of the MBAM Administration and Monitoring website.

2.  Back up the Recovery database on Server A.

3.  Move the Recovery database from Server A to Server B.

4.  Restore the Recovery database on Server B.

5.  Configure access to the database on Server B and update connection data.

6.  Install MBAM Server software and run the MBAM Server Configuration wizard on Server B.

7.  Resume the instance of the Administration and Monitoring website.

### How to move the Recovery database

**Stop all instances of the MBAM Administration and Monitoring website.** On each server that is running the MBAM Administration and Monitoring Server website, use the Internet Information Services (IIS) Manager console to stop the Administration and Monitoring website.

To automate this procedure, you can use Windows PowerShell to enter a command that's similar to the following command:

```powershell
Stop-website "Microsoft BitLocker Administration and Monitoring"
```

>[!NOTE]
>To run this command, you must add the Internet Information Services (IIS) module for Windows PowerShell to the current instance of Windows PowerShell.

### Back up the Recovery database on Server A

1.  Use the **Back Up** task in SQL Server Management Studio to back up the Recovery database on Server A. By default, the database name is **MBAM Recovery database**.

2.  To automate this procedure, create a SQL file (.sql) that contains the following SQL script, and change the MBAM Recovery database to use the full recovery mode:

    ```sql
    USE master;

    GO

    ALTER database "MBAM Recovery and Hardware"

    SET RECOVERY FULL;

    GO

    -- Create MBAM Recovery database Data and MBAM Recovery logical backup devices.

    USE master

    GO

    EXEC sp_addumpdevice 'disk', 'MBAM Recovery and Hardware database Data Device',

    'Z:\MBAM Recovery database Data.bak';

    GO

    -- Back up the full MBAM Recovery database.

    BACKUP database [MBAM Recovery and Hardware] TO [MBAM Recovery and Hardware database Data Device];

    GO

    BACKUP CERTIFICATE [MBAM Recovery Encryption Certificate]

    TO FILE = 'Z:\SQLServerInstanceCertificateFile'

    WITH PRIVATE KEY

    (

    FILE = ' Z:\SQLServerInstanceCertificateFilePrivateKey',

    ENCRYPTION BY PASSWORD = '$PASSWORD$'

    );

    GO
    ```

3.  Use the following value to replace the values in the code example with values that match your environment:

    `$PASSWORD$` - password that you use to encrypt the Private Key file.

4.  In Windows PowerShell, run the script that is stored in the file and similar to the following example:

    ```powershell
    Invoke-Sqlcmd -InputFile
    'Z:\BackupMBAMRecoveryandHardwarDatabaseScript.sql' -ServerInstance $SERVERNAME$\$SQLINSTANCENAME$
    ```

5.  Use the following value to replace the values in the code example with values that match your environment:

    `$SERVERNAME$\$SQLINSTANCENAME$` - server name and instance from which the Recovery database will be backed up.

### Move the Recovery database from Server A to Server B

Use Windows Explorer to move the **MBAM Recovery database Data.bak** file from Server A to Server B.

To automate this procedure, you can use Windows PowerShell to run a command that is similar to the following example:

```powershell
Copy-Item "Z:\MBAM Recovery database Data.bak"
\\$SERVERNAME$\$DESTINATIONSHARE$

Copy-Item "Z:\SQLServerInstanceCertificateFile"
\\$SERVERNAME$\$DESTINATIONSHARE$

Copy-Item "Z:\SQLServerInstanceCertificateFilePrivateKey"
\\$SERVERNAME$\$DESTINATIONSHARE$
```

Use the information in the following table to replace the values in the code example with values that match your environment.

| Parameter        | Description  |
|----------------------|------------------|
| `$SERVERNAME$`       | Name of the server to which the files will be copied. |
| `$DESTINATIONSHARE$` | Name of the share and path to which the files will be copied. |

### Restore the Recovery database on Server B

1.  Restore the Recovery database on Server B by using the **Restore database** task in SQL Server Management Studio.

2.  When the previous task finishes, select **From Device**, and then select the database backup file.

3.  Use the **Add** command to select the **MBAM Recovery database Data.bak** file, and select **OK** to complete the restoration process.

4.  To automate this procedure, create a SQL file (.sql) that contains the following SQL script:

    ```sql
    -- Restore MBAM Recovery database.

    USE master

    GO

    -- Drop certificate created by MBAM Setup.

    DROP CERTIFICATE [MBAM Recovery Encryption Certificate]

    GO

    --Add certificate

    CREATE CERTIFICATE [MBAM Recovery Encryption Certificate]

    FROM FILE = 'Z:\SQLServerInstanceCertificateFile'

    WITH PRIVATE KEY

    (

    FILE = ' Z:\SQLServerInstanceCertificateFilePrivateKey',

    DECRYPTION BY PASSWORD = '$PASSWORD$'

    );

    GO

    -- Restore the MBAM Recovery database data and log files.

    RESTORE database [MBAM Recovery and Hardware]

    FROM DISK = 'Z:\MBAM Recovery database Data.bak'

    WITH REPLACE
    ```

5.  Use the following value to replace the values in the code example with values that match your environment.

    `$PASSWORD$` - password that you used to encrypt the Private Key file.

6.  In Windows PowerShell, run the script that is stored in the file and similar to the following:

    ```powershell
    Invoke-Sqlcmd -InputFile 'Z:\RestoreMBAMRecoveryandHardwarDatabaseScript.sql' -ServerInstance $SERVERNAME$\$SQLINSTANCENAME$
    ```

7.  Use the following value to replace the values in the code example with values that match your environment.

    `$SERVERNAME$\$SQLINSTANCENAME$` - Server name and instance to which the Recovery database will be restored.

### Configure access to the database on Server B and update connection data

1. Verify that the Microsoft SQL Server user login that enables Recovery database access on the restored database is mapped to the access account that you provided during the configuration process.

   >[!NOTE]
   >If the login isn't the same, create a login by using SQL Server Management Studio, and map it to the existing database user.

2. On the server that is running the Administration and Monitoring website, use the Internet Information Services (IIS) Manager console to update the connection string information for the MBAM websites.

3. Edit the following registry key:

   `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString`

4. Update the **Data Source** value with the name of the server and instance (for example, `$SERVERNAME$\$SQLINSTANCENAME`) to which the Recovery database was moved.

5. Update the **Initial Catalog** value with the recovered database name.

6. To automate this process, you can use the Windows PowerShell command prompt to enter a command line on the Administration and Monitoring Server that is similar to the following example:

   ```powershell
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\\Microsoft\MBAM Server\\Web" /v
   RecoveryDBConnectionString /t REG_SZ /d "Integrated Security=SSPI;Initial
   Catalog=$database$;Data Source=$SERVERNAME$\$SQLINSTANCENAME$" /f

   Set-WebConfigurationProperty
   'connectionStrings/add[@name="KeyRecoveryConnectionString"]' -PSPath
   "IIS:\sites\Microsoft Bitlocker Administration and
   Monitoring\MBAMAdministrationService" -Name "connectionString" -Value "Data
   Source=$SERVERNAME$\$SQLINSTANCENAME$;Initial Catalog=MBAM Recovery and
   Hardware;Integrated Security=SSPI;"

   Set-WebConfigurationProperty
   'connectionStrings/add[\@name="Microsoft.Mbam.RecoveryAndHardwareDataStore.ConnectionString"]'
   -PSPath "IIS:\sites\Microsoft Bitlocker Administration and
   Monitoring\MBAMRecoveryAndHardwareService" -Name "connectionString" -Value
   "Data Source=$SERVERNAME$\$SQLINSTANCENAME$;Initial Catalog=MBAM Recovery
   and Hardware;Integrated Security=SSPI;"
   ```

   >[!NOTE]
   >This connection string is shared by all local MBAM web applications. Therefore, it needs to be updated only once per server.

7. Use the following table to replace the values in the code example with values that match your environment.

   |Parameter|Description|
   |---------|-----------|
   |`$SERVERNAME$/$SQLINSTANCENAME$`|Server name and instance of SQL Server where the Recovery database is located.|
   |`$database$`|Name of the Recovery database.|

### Install MBAM Server software and run the MBAM Server Configuration wizard on Server B

1.  Install the MBAM 2.5 Server software on Server B. For details, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

2.  On Server B, start the MBAM Server Configuration wizard, select **Add New Features**, and then select only the **Recovery database** feature. For details on how to configure the databases, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).

    >[!TIP]
    >Alternatively, you can use the **Enable-MbamDatabase** Windows PowerShell cmdlet to configure the Recovery database.

### Resume the instance of the Administration and Monitoring website

On the server that is running the Administration and Monitoring website, use the Internet Information Services (IIS) Manager console to start the Administration and Monitoring website.

To automate this procedure, you can use Windows PowerShell to run a command that is similar to the following example:

```powershell
Start-website "Microsoft BitLocker Administration and Monitoring"
```

>[!NOTE]
>To run this command, you must add the IIS module for Windows PowerShell to the current instance of Windows PowerShell.

## Move the Compliance and Audit database

The high-level steps for moving the Compliance and Audit database are:

1.  Stop all instances of the MBAM Administration and Monitoring website

2.  Back up the Compliance and Audit database on Server A

3.  Move the Compliance and Audit database from Server A to Server B

4.  Restore the Compliance and Audit database on Server B

5.  Configure access to the database on Server B and update connection data

6.  Install MBAM Server software and run the MBAM Server Configuration wizard on
    Server B

7.  Resume the instance of the Administration and Monitoring website

### How to move the Compliance and Audit database

**Stop all instances of the MBAM Administration and Monitoring website.**  On each server that is running the MBAM Administration and Monitoring Server website, use the Internet Information Services (IIS) Manager console to stop the Administration and Monitoring website.

To automate this procedure, you can use Windows PowerShell to enter a command that is similar to the following example:

```powershell
Stop-website "Microsoft BitLocker Administration and Monitoring"
```

>[!NOTE]
>To run this command, you must add the Internet Information Services (IIS) module for Windows PowerShell to the current instance of Windows PowerShell.

### Back up the Compliance and Audit database on Server A

1.  Use the **Back Up** task in SQL Server Management Studio to back up the Compliance and Audit database on Server A. By default, the database name is **MBAM Compliance Status database**.

2.  To automate this procedure, create a SQL file (.sql) that contains the following SQL script:

    ```sql
    USE master;

    GO

    ALTER database "MBAM Compliance Status"

    SET RECOVERY FULL;

    GO

    -- Create MBAM Compliance Status Data logical backup devices.

    USE master

    GO

    EXEC sp_addumpdevice 'disk', 'MBAM Compliance Status database Data Device',

    'Z: \MBAM Compliance Status database Data.bak';

    GO

    -- Back up the full MBAM Compliance Recovery database.

    BACKUP database [MBAM Compliance Status] TO [MBAM Compliance Status database Data Device];

    GO

    ```

3.  Run the script that is stored in the .sql file by using a Windows PowerShell command that is similar to the following example:

    ```powershell
    Invoke-Sqlcmd -InputFile "Z:\BackupMBAMComplianceStatusDatabaseScript.sql" -ServerInstance $SERVERNAME$\$SQLINSTANCENAME$
    ```

4.  Using the following value, replace the values in the code example with values that match your environment:

    `$SERVERNAME$\$SQLINSTANCENAME$` - server name and instance from which the Compliance and Audit database will be backed up.

### Move the Compliance and Audit database from Server A to Server B**

1.  Use Windows Explorer to move the **MBAM Compliance Status database Data.bak** file from Server A to Server B.

2.  To automate this procedure, you can use Windows PowerShell to run a command that is similar to the following example:

    ```powershell
    Copy-Item "Z:\MBAM Compliance Status database Data.bak"
    \\$SERVERNAME$\$DESTINATIONSHARE$
    ```

3.  Using the following table, replace the values in the code example with values that match your environment.

    | Parameter        | Description                                               |
    |----------------------|---------------------------------------------------------------|
    | `$SERVERNAME$`       | Name of the server to which the files will be copied.         |
    | `$DESTINATIONSHARE$` | Name of the share and path to which the files will be copied. |

### Restore the Compliance and Audit database on Server B

1.  Restore the Compliance and Audit database on Server B by using the **Restore database** task in SQL Server Management Studio.

2.  When the previous task finishes, select **From Device**, and then select the database backup file.

3.  Use the **Add** command to select the **MBAM Compliance Status database Data.bak** file and select **OK** to complete the restoration process.

4.  To automate this procedure, create a SQL file (.sql) that contains the following SQL script:

    ```sql
    -- Create MBAM Compliance Status database Data logical backup devices.

    Use master

    GO

    -- Restore the MBAM Compliance Status database data files.

    RESTORE database [MBAM Compliance Status]

    FROM DISK = 'C:\test\MBAM Compliance Status database Data.bak'

    WITH REPLACE

    ```

5.  In Windows PowerShell, run the script that is stored in the file and similar to the following example:

    ```powershell
    Invoke-Sqlcmd -InputFile "Z:\RestoreMBAMComplianceStatusDatabaseScript.sql" -ServerInstance $SERVERNAME$\$SQLINSTANCENAME$
    ```

6.  Using the following value, replace the values in the code example with values that match your environment.

    `$SERVERNAME$\$SQLINSTANCENAME$` - Server name and instance to which the Compliance and Audit database will be restored.

### Configure access to the database on Server B and update connection data

1. Verify that the Microsoft SQL Server user login that enables Compliance and Audit database access on the restored database is mapped to the access account that you provided during the configuration process.

   >[!NOTE]
   >If the login is not the same, create a login by using SQL Server Management Studio, and map it to the existing database user.

2. On the server that is running the Administration and Monitoring website, use the Internet Information Services (IIS) Manager console to update the connection string information for the website.

3. Edit the following registry key:

   `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`

4. Update the **Data Source** value with the name of the server and instance (for example, `$SERVERNAME$\$SQLINSTANCENAME$`) to which the Recovery database was moved.

5. Update the **Initial Catalog** value with the recovered database name.

6. To automate this process, you can use the Windows PowerShell command prompt to enter a command line on the Administration and Monitoring Server that is similar to the following example:

   ```powershell
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MBAM Server\Web" /v
   ComplianceDBConnectionString /t REG_SZ /d "Integrated Security=SSPI;Initial
   Catalog=$database$;Data Source=$SERVERNAME$\$SQLINSTANCENAME$" /f
   ```

   >[!NOTE]
   >This connection string is shared by all local MBAM web applications. Therefore, it needs to be updated only once per server.

7. Using the following table, replace the values in the code example with values that match your environment.

   |Parameter | Description |
   |---------|------------|
   |`$SERVERNAME$\$SQLINSTANCENAME$` | Server name and instance of SQL Server where the Recovery database is located.|
   |`$database$`|Name of the recovered database.|

### Install MBAM Server software and run the MBAM Server Configuration wizard on Server B

1.  Install the MBAM 2.5 Server software on Server B. For details, see [Installing the MBAM 2.5 server software](installing-the-mbam-25-server-software.md).

2.  On Server B, start the MBAM Server Configuration wizard, select **Add New Features**, and then select only the **Compliance and Audit database** feature. For details on how to configure the databases, see [How to configure the MBAM 2.5 databases](how-to-configure-the-mbam-25-databases.md).

    >[!TIP]
    >Alternatively, you can use the **Enable-MbamDatabase** Windows PowerShell cmdlet to configure the Compliance and Audit database.

### Resume the instance of the Administration and Monitoring website

On the server that is running the Administration and Monitoring website, use the Internet Information Services (IIS) Manager console to start the Administration and Monitoring website.

To automate this procedure, you can use Windows PowerShell to run a command that is similar to the following example:

```powershell
Start-website "Microsoft BitLocker Administration and Monitoring"
```

>[!NOTE]
>To run this command, you must add the IIS module for Windows PowerShell to the current instance of Windows PowerShell.
