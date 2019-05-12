# Create a Table Store result table {#concept_62526_zh .concept}

This topic describes how to create a Table Store result table in Realtime Compute. It also describes the mapping between Table Store field types and Realtime Compute field types.

## Introduction to Table Store {#section_i4b_jrf_cgb .section}

Table Store is a distributed NoSQL data storage service built on Alibaba Cloud's Apsara system. It is designed to provide 99.99% high availability and 99.999999999% data reliability. By using data sharding and load balancing technologies, Table Store implements seamless scale-out in terms of data scale and access parallelism. It also supports the storage of and real-time access to large amounts of structured data.

## DDL definition {#section_pwl_qrf_cgb .section}

Realtime Compute supports creating a Table Store table as the result table. The sample code is as follows:

```language-sql
CREATE TABLE stream_test_hotline_agent (
 name varchar,
 age BIGINT,
 birthday BIGINT,
 primary key(name,age)
) WITH (
 type='ots',
 instanceName='<yourInstanceName>',
 tableName='<yourTableName>',
 accessId='<yourAccessId>',
 accessKey='<yourAccessSecret>',
 endPoint='<yourEndpoint>',
 valueColumns='birthday'
);
			
```

**Note:** 

-   We recommend that you use the data storage registration method to connect to Table Store. For more information, see [Register Table Store resources](intl.en-US/Flink SQL Development Guide/Data storage/Data storage resource registration/Register Table Store resources.md#).
-   The value of the valueColumns parameter must not be a declared primary key. It can be any field other than the primary key.

## WITH parameters {#section_jsj_rrf_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|instanceName|The instance name.|None|
|tableName|The table name.|None|
|endPoint|The endpoint for accessing the instance.|See [Endpoint](../../../../intl.en-US/Product Introduction/Terms/Endpoint.md#).|
|accessId|The AccessKey ID.|None|
|accessKey|The AccessKey Secret.|None|
|valueColumns|The column names of fields to be inserted. Separate multiple fields with commas \(`,`\).|The format of inserting two fields is `'ID,NAME'`.|
|bufferSize|The buffer size after deduplication.|Optional. Default value: 5000, indicating that the output starts once there are 5,000 input data records.|
|batchWriteTimeoutMs|The write timeout period. Unit: millisecond.|Optional. Default value: 5000. This value indicates that if no data is written to Table Store within 5000 milliseconds \(5 seconds\), all buffered data is written.|
|batchSize|The number of data records written at a time.|Optional. Default value: 100.|
|retryIntervalMs|The retry interval, in milliseconds.|Optional. Default value: 1000.|
|maxRetryTimes|The maximum number of retries allowed.|Optional. Default value: 100.|
|ignoreDelete|Indicates whether to ignore the delete operation.|Default value: false.|

## Field type mapping {#section_z2d_srf_cgb .section}

|Table Store field type|Realtime Compute field type|
|----------------------|---------------------------|
|INTEGER|BIGINT|
|STRING|VARCHAR|
|BOOLEAN|BOOLEAN|
|DOUBLE|DOUBLE|

**Note:** The Table Store result table must have a declared `primary key`. The output data is appended to the Table Store result table in Update mode.

