# Create a MaxCompute result table {#concept_pql_cdz_lgb .concept}

This topic describes how to create a MaxCompute result table in Realtime Compute and FAQs during the creation process.

## DDL definition {#section_jnb_3qf_cgb .section}

Realtime Compute supports creating a MaxCompute table as the result table. The sample code is as follows:

```language-sql
create table odps_output(
    id INT,
    user_name VARCHAR,
    content VARCHAR
) with (
    type = 'odps',
    endPoint = 'http://service.cn.maxcompute.aliyun-inc.com/api',
    project = '<projectName>',
    tableName = '<tableName>',
    accessId = '<yourAccessKeyId>',
    accessKey = '<yourAccessKeySecret>',
    `partition` = 'ds=2018****'
);
```

## WITH parameters {#section_glb_mqf_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|endPoint|The MaxCompute endpoint.|Required. For more information, see [Configure Endpoint](../../../../intl.en-US/Prepare/Configure Endpoint.md#).|
|project|The MaxCompute project name.|Required.|
|tableName|The table name.|Required.|
|accessId|The AccessKey ID.|Required|
|accessKey|The AccessKey Secret.|Required|
|partition|The partition name.|Optional. This parameter must be specified for a partition table. To view detailed partition information, log on to [Data Map](https://meta.dw.alibaba-inc.com/store/index.html). For example, if the partition name of a table is `ds=20180905`, you can specify the parameter as ``partition` = 'ds=20180905'`. Use commas \(,\) to separate multiple levels of partitions, for example, ``partition` = 'ds=20180912,dt=xxxyyy'`.|

**Note:** 

Realtime Compute writes the cached data to MaxCompute every time when it creates a checkpoint.

## FAQ {#section_lsc_fgz_lgb .section}

1.  Q: Does a Realtime Compute job clear the result table before it writes data to the MaxCompute sink that is in Stream mode when `isOverwrite` is set to `true`?

    A: The `isOverwrite` parameter is set to `true`by default. That is, Realtime Compute clears the result table and result data before it writes data to the sink. Every time Realtime Compute starts a job or resumes a paused job, it clears data of the existing result table or the result partition before it writes data. Data loss may occur when data is cleared after a paused Realtime Compute job is resumed.

2.  Q: What is the mapping between MaxCompute data types and Realtime Compute data types?

    A: The following table lists the mapping.

    |MaxCompute data type|Realtime Compute data type|
    |--------------------|--------------------------|
    |TINYINT|TINYINT|
    |SMALLINT|SMALLINT|
    |INT|INT|
    |BIGINT|BIGINT|
    |FLOAT|FLOAT|
    |DOUBLE|DOUBLE|
    |BOOLEAN|BOOLEAN|
    |DATETIME|TIMESTAMP|
    |TIMESTAMP|TIMESTAMP|
    |STRING|VARCHAR|
    |DECIMAL|DECIMAL|
    |BINARY|VARBINARY|

    **Note:** 

    -   Currently, MaxCompute connectors do not support converting other MaxCompute data types.
    -   VARCHAR is a new data type of MaxCompute. It is not currently supported by Realtime Compute connectors. We recommend that you set the VARCHAR type in the MaxCompute schema to the STRING type.

