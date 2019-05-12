# Create an HiTSDB result table {#concept_72779_zh .concept}

This topic describes how to create an High Performance Time Series Database \(HiTSDB\) result table in Realtime Compute.

## Introduction to HiTSDB {#section_xt2_mkg_cgb .section}

HiTSDB is a high performance, cost-effective, stable, and reliable online time series database service. HiTSDB provides a range of functions such as efficient read and write, storage with a high compression ratio, time series data interpolation, and aggregation. HiTSDB has been widely used in diversified industrial scenarios, such as Internet of Things \(IoT\) monitoring systems, enterprise-level energy management systems \(EMSs\), production safety monitoring systems, and electric power detection systems.

## DDL definition { .section}

Realtime Compute supports creating a HiTSDB table as the result table. The sample code is as follows:

**Note:** To reference an HiTSDB result table in Realtime Compute, you need to configure the data storage whitelist. For more information, see [Configure the data storage whitelist](intl.en-US/Flink SQL Development Guide/Data storage/Configure a data storage whitelist.md#).

```language-SQL
CREATE TABLE stream_test_hitsdb (
    metric varchar,
    timestamp INTEGER,
    value DOUBLE,
    tagk1 varchar
) WITH (
    type='hitsdb',
    host='<yourHostName>',
    virtualDomainSwitch = 'ture',
    httpConnectionPool = '20',
    batchPutSize = '1000'
);
```

The default format for table creation is described as follows:

-   Zeroth column: metric\(VARCHAR\).
-   First column: timestamp\(INTEGER\), in seconds.
-   Second column: value\(DOUBLE\)
-   Third column: tag\(VARCHAR\)
-   Fourth to Nth columns: Use the field name as the tag key and field value as the tag value.

**Note:** You must declare metric, timestamp, and value. Their data types must be the same as those in HiTSDB. Multiple tag columns are allowed.

## WITH parameters {#section_o3p_s4g_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|host|The IP address or virtual IP address.|Enter the host address of the registered instance. For more information, see [Connect to the instance](https://www.alibabacloud.com/help/doc-detail/56240.htm).|
|port|The port number.|Default value: 8242.|
|virtualDomainSwitch|Indicates whether to use the VIP server.|Default value: false. If you need to use the VIP server, set this parameter to true.|
|httpConnectionPool|The maximum number of HTTP connections in the HTTP connection pool.|Default value: 10.|
|httpCompress|Indicates whether to use GZIP to compress request bodies.|Default value: false, indicating no compression.|
|httpConnectTimeout|The HTTP connection timeout period.|Default value: 0.|
|ioThreadCount|The number of I/O threads.|Default value: 1.|
|batchPutBufferSize|The buffer size.|Default value: 10000.|
|batchPutRetryCount|The maximum number of write retries allowed.|Default value: 3.|
|batchPutSize|The data volume submitted at a time.|By default, 500 data points are submitted at a time.|
|batchPutTimeLimit|The wait time in the buffer. Unit: millisecond.|Default value: 200.|
|batchPutConsumerThreadCount|The number of serialized threads.|Default value: 1.|

## FAQ {#section_usr_vln_mgb .section}

Q: An error occurred during failover, indicating that the LONG type cannot be converted to the INT type. Why?

A: Realtime Compute versions earlier than V2.2.5 only support the INT type. Realtime Compute V2.2.5 and later support the BIGINT type.

