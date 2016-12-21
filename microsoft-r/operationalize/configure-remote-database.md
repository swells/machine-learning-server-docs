---

# required metadata
title: "Configure a remote database for operationalization | Microsoft R Server Docs"
description: "Configure a remote database for operationalization with Microsoft R Server"
keywords: ""
author: "j-martens"
manager: "jhubbard"
ms.date: "12/08/2016"
ms.topic: "article"
ms.prod: "microsoft-r"
ms.service: ""
ms.assetid: ""

# optional metadata
ROBOTS: ""
audience: ""
ms.devlang: ""
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.technology: 
  - deployr
  - r-server
ms.custom: ""
---

# Configuring an SQL Server or PostgreSQL Database

**Applies to:  Microsoft R Server 9.0.1**

The operationalization feature for R Server installs and uses a local SQLite database by default. Later, you can update the configuration to use another database locally or remotely. This is particularly useful when you want to use a remote database or when you have multiple web nodes. 

This feature uses a SQLite 3.7+ database by default, but can be configured to use:
+ On Windows: SQL Server Professional, Standard, or Express Version 2008 or greater
+ On Linux: PostgreSQL 9.2 or greater 

> [!Important]
> Any data that was saved in the default local SQLite database will be lost if you configure a different database.

<a name="sqlserver"></a>
<a name="postgresql"></a>

**To use a different local or remote database, do the following:**

> These steps assume that you have already set up SQL Server or PostgreSQL as described for that product.
>
> Create this database and register it in the configuration file below BEFORE the service for the control node is started.

1.  On each web node, [stop the service](admin-utility.md#startstop).

1.  Update the database properties to point to the new database as follows:

    1. Open the external configuration file, `appsettings.json` file. 

       + On Windows, this file is under `<MRS_home>\deployr\Microsoft.DeployR.Server.WebAPI\` where `<MRS_home>` is the path to the Microsoft R Server installation directory. To find this path, enter `normalizePath(R.home())` in your R console.

       + On Linux, this file is under `/usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/`.

    1. Locate the `ConnectionStrings` property block.

    1. Within that property block, locate the type of database you want to set up.
       + For SQL Server, look for `"sqlserver": {`.

       + For SQL Server, look for `"postgresql": {`.

    1. In the appropriate database section, enable that database type by adding the property `"Enabled": true,`. For example:
       ```
        "ConnectionStrings": {
                "sqlserver": {
                    "Enabled": true,
                    ...
       },
       ```

    1. Add the connection string.

       For SQL Server Database (**Integrated Security**), use:
       ``` 
       "Connection":  "Data Source=<DB-SERVER-IP-OR-FQDN>\\<INSTANCE-NAME>;Initial Catalog=<DB-NAME>;Integrated Security=True;"
       ```

       For SQL Server Database (**SQL authentication**), use: 
       ``` 
       "Connection":  "Data Source=<DB-SERVER-IP-OR-FQDN>\\<INSTANCE-NAME>;Initial Catalog=<DB-NAME>; Integrated Security=False; User Id=<USER-ID>;Password=<PASSWORD>;"
       ```

       For PostgreSQL Database, use:
       ``` 
       "Connection":  "User ID=<DB-USERNAME>;Password=<USER-PASSWORD>;Host=<DB-SERVER-IP-OR-FQDN>;Port=5432;Database=<DB-NAME>;Pooling=true;"
       ```       
    
    1. <a name="encrypt"></a>For better security, we recommend you encrypt the connection string for this database before adding the information to `appsettings.json`.
    
       1. Use the administration utility to [encrypt the connection string](admin-utility.md#encrypt).

       1. Copy the encrypted string returned by the administration utility into `"ConnectionStrings": {` property block and set `"Encrypted":` to `true`. For example:
            
       ```
        "ConnectionStrings": {
                "sqlserver": {
                    "Enabled": true,
                    "Encrypted": true,
                    "Connection": "eyJ0IjoiNzJFNDg5QUQ1RDQ4MEM1NURCMDRDMjM1MkQ1OTVEQ0I2RkQzQzE3QiIsInMiOiJFWkNhNUdJMUNSRFV0bXZHVEIxcmNRcmxXTE9QM2ZTOGtTWFVTRk5QSk9vVXRWVzRSTlh1THcvcDd0bCtQdFN3QVRFRjUvL2ZJMjB4K2xTME00VHRKZDdkcUhKb294aENOQURyZFY1KzZ0bUgzWG1TOWNVUkdwdjl3TGdTaUQ0Z0tUV0QrUDNZdEVMMCtrOStzdHB"
                },
                ...
       },
       ```       

    1. Save the changes you've made to `appsettings.json`.

1. Open the database port on the remote machine to the public IP of each web node as described in these articles: [SQL Server](https://technet.microsoft.com/en-us/library/ms175043(v=sql.130).aspx) | [PostgreSQL](https://www.postgresql.org/docs/current/static/auth-pg-hba-conf.html)
         
1. Launch the administrator's utility and:

   1. [Restart the web node](admin-utility.md#startstop) and the database is created upon restart.

   1. [Run the diagnostic tests](admin-diagnostics.md) to ensure the connection can be made to your new database.