# DDL overview {#concept_62515_zh .concept}

This topic describes the DDL syntax in Realtime Compute and the issues that require your attention during the DDL use, including field mapping and case sensitivity.

## Syntax {#section_stc_bhx_bgb .section}

```language-sql
CREATE TABLE tableName
      (columnName dataType [, columnName dataType ]*)
      [ WITH (propertyName=propertyValue [, propertyName=propertyValue ]*) ];
			
```

## Description { .section}

Realtime Compute does not provide a built-in data storage feature. Therefore, all DDL statements that involve table creation are reference declarations of external data tables or storage systems. The sample code is as follows:

```language-sql
CREATE TABLE mq_stream(
 a VARCHAR,
 b VARCAHR,
 c VARCAHR
) WITH (
 type='mq',
 topic='blink_mq_test',
 accessId='yourAccessId',
 accessKey='yourAccessKey'
);
```

The preceding code does not create a `topic` of the [MQ source table](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a source table/Create a MQ source table.md#) in Flink SQL. Instead, it declares a reference to a table named `mq_stream`. For all DML operations related to this MQ topic in downstream operators, the topic name can be replaced with the alias `mq_stream`.

-   The declaration of a table is valid only in the current job in Realtime Compute. A Realtime Compute job is generated after a SQL file is submitted. The preceding declaration of the `mq_stream` table is valid only in the current SQL file. Other SQL files in the same Realtime Compute project can also declare the `mq_stream` table.
-   According to the standard SQL definition, keywords, table names, and field names in DDL statements are case-insensitive.
-   Table and field names must start with a letter or digit, and can contain only letters, digits, and underscores \(\_\).
-   Depending on the nature of the upstream plug-in used, DDL declarations may establish the field mappings between the declaration table and external table based on other factors rather than solely on the field names. We recommend that you declare the same field names and number of fields as those in the referenced external tables. This can prevent data errors caused by confusing declarations.

    **Note:** If the upstream plug-in supports retrieving values based on keys of key-value pairs, the declaration table and its referenced external table do not need to have the same number of fields. However, the field names must be the same. If the upstream plug-in does not support retrieving values based on keys, the number of fields and their order must be the same between the declaration table and external table.


## Field mapping { .section}

Two field mapping methods are supported for a declaration table depending on whether the external data source has a schema.

-   Sequential mapping

    This method applies to data sources without a schema, for example, MQ. These data sources are usually unstructured storage systems that do not support retrieving values based on keys. We recommend that you customize field names in DDL SQL statements and use the same field types and number of fields in the declaration table as those in the external table.

    A sample record in MQ is provided as follows:

    ```
    asavfa,sddd32,sdfdsv
    ```

    Specify MQ field names according to the naming conventions.

    ```language-sql
    CREATE TABLE mq_stream(
     a VARCHAR,
     b VARCHAR,
     c VARCAHR
    ) WITH (
     type='mq',
     topic='blink_mq_test',
     accessId='yourAccessId',
     accessKey='yourAccessSecret'
    );
    ```

-   Name mapping

    This method applies to data sources with a schema. These data storage systems define field names and field types at the table storage level, and support retrieving values based on keys. We recommend that you use the same schema definition in Flink SQL declarations as that of the external data storage system. Specifically, the names, number, and order of fields in the declaration table must be the same as those in the external table.

    **Note:** If field names in the external data storage system are case-sensitive \(for example, [Table Store](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a result table/Create a Table Store result table.md#)\), enclose the case-sensitive field names in backticks \(```\). In the DDL syntax, field names in the declaration table must be the same as those in the external table.


## Case-sensitivity {#section_n3j_ckx_bgb .section}

In the standard SQL definition, fields are case-insensitive. For example, the following two statements have the same meaning:

```language-sql
create table stream_result (
    name varchar,
    value varchar
);
```

```language-sql
create table STREAM_RESULT (
    NAME varchar,
    VALUE varchar
);
```

However, most external data sources referenced by Realtime Compute are case-sensitive. For example, Table Store is case-sensitive. The following statement shows how to define the uppercase `NAME` field for Table Store:

```language-sql
create  table STREAM_RESULT (
    `NAME` varchar,
    `VALUE` varchar
);
```

In all subsequent DML statements, enclose the field in backticks \(```\) whenever it is referenced, as shown in the following statement:

```language-sql
INSERT INTO table_a
SELECT
  `NAME`,
  `VALUE`
FROM
  table_b;
```

## Related topics {#section_yxf_f3g_chb .section}

For more information about how to create source tables, dimension tables, and result tables in Realtime Compute, see the following topics:

-   [Source table overview](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a source table/Source table overview.md#)
-   [Result table overview](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a result table/Result table overview.md#)
-   [Dimension table overview](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a dimension table/Dimension table overview.md#)

