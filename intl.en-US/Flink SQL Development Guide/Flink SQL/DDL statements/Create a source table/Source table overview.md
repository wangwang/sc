# Source table overview {#concept_62520_zh .concept}

In Realtime Compute, source tables are streaming data storage tables. Streaming data storage provides the input to drive the running of Realtime Compute. Therefore, at least one streaming data storage table is required for each Realtime Compute job.

## Syntax {#section_x2t_dhy_bgb .section}

```language-sql
  CREATE TABLE tableName
      (columnName dataType [, columnName dataType ]*)
      [ WITH (propertyName=propertyValue [, propertyName=propertyValue ]*) ];
			
```

## Examples {#section_m3g_fhy_bgb .section}

```language-sql
CREATE TABLE metaq_stream(
 x VARCHAR,
 y VARCHAR,
 z VARCHAR
) WITH (
 type='mq',
 topic='<yourTopicName>',
 endpoint='<yourEndpoint>',
 pullIntervalMs='1000',
 accessId='<yourAccessId>',
 accessKey='<yourAccessSecret>',
 startMessageOffset='1000',
 consumerGroup='yourConsumerGroup',
 fieldDelimiter='|'
);
```

## Obtain attribute fields of a source table {#section_v3l_32x_tgb .section}

-   Syntax for obtaining attribute fields of a source table 

    Realtime Compute provides the keyword `HEADER` in the DDL statement of a source table. You can use this keyword to obtain attribute fields of the source table.

    ```language-sql
    CREATE TABLE sourcetable
    (
     `timestamp`  VARCHAR HEADER,
      name        VARCHAR,
      MsgID       VARCHAR
    )WITH(
         type='sls'
    );
    ```

    The ``timestamp`` field in the preceding example is defined as `HEADER` to read values from data attribute fields. This field can be used as a common field subsequently.

    **Note:** Different types of source tables \(such as DataHub, Log Service, and MQ source tables\) have different default attribute fields. Some source tables also support custom attribute fields. For more information, see the documentation of the corresponding source table type.

-   Example for obtaining attribute fields of a source table 

    The following describes an example of how to obtain attribute fields of a Log Service source table. Currently, Log Service supports the following three attribute fields by default.

    |Field|Description|
    |-----|-----------|
    |`__source__`|The message source.|
    |`__topic__`|The message topic.|
    |`__timestamp__`|The time when the log was generated.|

    **Note:** To obtain attribute fields, you need to first declare the fields according to the normal logic. Then add the keyword `HEADER` to the end of the type declaration.

    Example:

    -   Test data

        ```language-json
        __topic__:  ens_altar_flow  
                result:  {"MsgID":"ems0a","Version":"0.0.1"} 
        ```

    -   Test statements

        ```language-sql
        CREATE TABLE sls_log (
          __topic__  VARCHAR HEADER, 
          result     VARCHAR   
        )WITH(
          type = 'sls'
        );
        CREATE TABLE sls_out (
          name     varchar, 
          MsgID    varchar, 
          Version  varchar  
        )WITH(
          type ='RDS'
        );
        INSERT INTO sls_out
        SELECT 
        __topic__,
        JSON_VALUE(result,'$. MsgID'),
        JSON_VALUE(result,'$. Version')
        FROM
        sls_log
        ```

    -   Test results

        |name\(VARCHAT\)|MsgID\(VARCHAT\)|Version\(VARCHAT\)|
        |---------------|----------------|------------------|
        |ens\_altar\_flow|ems0a|`0.0.1`|


## Source table with window functions {#section_rv1_4f1_chb .section}

Realtime Compute supports window aggregation over data based on two time attributes: Event Time and Processing Time. For Realtime Compute jobs that involve window functions, the [Watermark](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Watermark.md#)and [Computed column](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Computed column.md#)are required in the declaration of the source table. For more information about the time attribute-based aggregation operations in Realtime Compute, see [Time attributes](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#).

## Supported source table types {#section_zy5_3xg_chb .section}

Realtime Compute allows multiple types of source tables to be created. For more information, see the following topics:

-   [Create a Log Service source table](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a source table/Create a Log Service source table.md#)
-   [Create an MQ source table](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a source table/Create a MQ source table.md#)
-   [Create a Kafka source table](intl.en-US/Flink SQL Development Guide/Flink SQL/DDL statements/Create a source table/Create a Kafka source table.md#)

