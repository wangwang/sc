# Create a HybridDB for MySQL result table {#concept_63985_zh .concept}

This topic describes how to create a HybridDB for MySQL result table in Realtime Compute.

## Introduction to HybridDB for MySQL {#section_dtx_4sm_cgb .section}

HybridDB for MySQL is a relational hybrid transaction/analytical processing \(HTAP\) database that supports both online transaction processing \(OLTP\) and online analytical processing \(OLAP\). HTAP combines transaction processing \(TP\) and analytical processing \(AP\) to ensure real-time data processing and analysis.

HybridDB for MySQL is compatible with MySQL syntax and functions, and supports common Oracle analytic functions. HybridDB for MySQL is fully compatible with the TPC-H and TPC-DS benchmarks.

## DDL definition {#section_jvv_vsm_cgb .section}

Realtime Compute supports creating a HybridDB for MySQL table as the result table. The sample code is as follows:

```language-sql
create table petadata_output(
 id INT,
 len INT,
 content VARCHAR,
 primary key(id,len)
) with (
 type='petaData',
 url='<yourDatabaseURL>',
 tableName='<yourTableName>',
 userName='<yourDatabaseUserName>',
 password='<yourDatabasePassword>'
);
```

**Note:** 

-   Realtime Compute supports writing data to a HybridDB for MySQL result table. To do so, Realtime Compute concatenates a SQL statement based on each row of the result data, and then executes the SQL statement against the destination database.
-   The default value of bufferSize is 1000. If the bufferSize threshold \(buffer hashmap size\) is reached, data writing is triggered. Therefore, you need to set bufferSize together with batchSize. You can set bufferSize and batchSize to the same value.
-   The value of the batchSize parameter cannot be too large. We recommend you set the value as 4096.

## WITH parameters {#section_jkp_ysm_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|url|The address.|[Switch network type](../../../../intl.en-US/User Guide/Manage instances/Switch network type.md#)|
|tableName|The table name.|None|
|userName|The logon username.|None|
|password|The logon password.|None|
|maxRetryTimes|The maximum number of insertion retries.|Optional. Default value: 3.|
|batchSize|The number of data records written at a time.|Optional. Default value: 1000.|
|bufferSize|The buffer size after deduplication. This parameter takes effect only when the primary key is specified.|Optional.|
|flushIntervalMs|The write timeout period. Unit: millisecond.|Optional. Default value: 3000. This value indicates that if no data is written within 3 seconds, all buffered data is written.|
|ignoreDelete|Indicates whether to ignore the delete operation.|Default value: false.|

