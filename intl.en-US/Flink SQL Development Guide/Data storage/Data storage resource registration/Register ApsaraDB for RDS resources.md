# Register ApsaraDB for RDS resources {#concept_62478_zh .concept}

This topic describes how to access ApsaraDB for RDS by registering ApsaraDB for RDS resources in Realtime Compute.

ApsaraDB for RDS \(RDS for short\) is a stable, reliable, and scalable online database service. Realtime Compute supports several RDS engines such as MySQL.

**Note:** 

-   When you use ApsaraDB for RDS on Alibaba Cloud, you need to grant Realtime Compute the permission to access ApsaraDB for RDS. For more information, see [Create a role for Realtime Compute exclusive mode and grant permissions to the role](../../../../intl.en-US/Preparation/Create a role for Realtime Compute exclusive mode and grant permissions to the role.md#). Otherwise, a `No Permission` error may be returned.
-   Realtime Compute uses relational databases such as MySQL to store result data. The relational databases use Taobao Distributed Data Layer \(TDDL\) and RDS connectors. When Realtime Compute frequently writes data into a table or resource file, a deadlock may occur. In scenarios that require high queries per second \(QPS\), high transactions per second \(TPS\), or highly concurrent write operations, we recommend that you avoid using TDDL or RDS result tables. To prevent deadlocks, we recommend that you use [Table Store](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a result table/Create a Table Store result table.md#) result tables.

## Register ApsaraDB for RDS resources {#section_vnh_vgd_yfb .section}

**Note:** During the registration process, the system automatically configures the IP address whitelist for ApsaraDB for RDS.

Specify related information:

-   Region

    Select the region where your ApsaraDB for RDS instance is located.

-   Instance

    Enter the ID of the ApsaraDB for RDS instance.

    **Note:** Enter the instance ID, rather than the instance name.

-   DBName

    Enter the name of the database corresponding to the ApsaraDB for RDS instance.

    **Note:** The database name is not the instance name.

-   Username

    Enter the username that you use to log on to the database.

-   Password

    Enter the password that you use to log on to the database.

-   Whitelist Authorization

    ApsaraDB for RDS uses the whitelist feature to ensure data security. When you register ApsaraDB for RDS resources in Realtime Compute, the system automatically configures a whitelist for ApsaraDB for RDS.


