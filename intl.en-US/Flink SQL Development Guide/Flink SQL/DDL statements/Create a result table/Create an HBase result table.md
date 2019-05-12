# Create an HBase result table {#concept_91464_zh .concept}

This topic describes how to create an HBase result table in Realtime Compute.

**Note:** This topic applies only to Realtime Compute deployed in exclusive mode.

## DDL definition {#section_l2m_q1g_cgb .section}

Realtime Compute supports creating an HBase table as the result table. The sample code is as follows:

```
create table liuxd_user_behavior_test_front (
    row_key varchar,
    from_topic varchar,
    origin_data varchar,
    record_create_time varchar,
    PRIMARY KEY (row_key)
) with (
    type = 'cloudhbase',
    zkQuorum = '2'
    columnFamily = '<yourColumnFamily>',
    tableName = '<yourTableName>',
    batchSize = '500'
)
```

**Note:** 

-   You can define multiple fields for the `primary key`. Multiple fields are concatenated by the `rowkeyDelimiter` into a `row_key`. The default row key delimiter is a colon \(`:`\).
-   When you perform an undo operation in HBase, if a column stores multiple versions of a value, all versions of the value are deleted.

## WITH parameters {#section_zdt_m1g_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|zkQuorum|The ZooKeeper address of the HBase cluster.|You can find the configuration of hbase.zookeeper.quorum in the hbase-site.xml file.|
|zkNodeParent|The path of the cluster on the ZooKeeper server.|You can find the configuration of hbase.zookeeper.quorum in the hbase-site.xml file.|
|tableName|The name of the HBase table.|None|
|userName|The logon username.|None|
|password|The logon password.|None|
|partitionBy|When this parameter is set to true, Realtime Compute partitions the table based on joinKey and distributes data to the JOIN operator. This helps improve the cache hit ratio.|Optional. Default value: false.|
|shuffleEmptyKey|When this parameter is set to false, Realtime Compute distributes empty keys in the input data to the same JOIN operator. When this parameter is set to true, Realtime Compute distributes empty keys in the input data to random JOIN operators.|We recommend that you set this parameter to true.|
|columnFamily|The name of the column family.|Currently, Realtime Compute only supports inserting data of the same column family.|
|maxRetryTimes|The maximum number of insertion retries.|Optional. Default value: 10.|
|bufferSize|The maximum number of data records allowed before deduplication.|Default value: 5000.|
|batchSize|The number of data records written at a time.|Optional. Default value: 100.|
|flushIntervalMs|The maximum length of insertion time.|Optional. Default value: 2000.|
|writePkValue|Indicates whether to write the primary key value.|Optional. Default value: false.|
|stringWriteMod|Indicates whether to insert all data records as the STRING type.|Optional. Default value: false.|
|rowkeyDelimiter|The delimiter of row keys.|Optional. The default delimiter is a colon \(`:`\).|
|isDynamicTable|Indicates whether the table is a dynamic table.|Optional. Default value: false.|

