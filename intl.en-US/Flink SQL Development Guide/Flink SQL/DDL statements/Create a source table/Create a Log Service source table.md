# Create a Log Service source table {#concept_62521_zh .concept}

This topic describes how to create a Log Service source table in Realtime Compute. It also describes the attribute fields, WITH parameters, and field type mapping involved in the table creation process.

## Introduction to Log Service {#section_qr1_2wy_bgb .section}

Log Service is an all-in-one real-time data logging service that Alibaba Group has developed and tested in many big data scenarios. Based on Log Service, you can quickly finish tasks such as data ingestion, consumption, delivery, query, and analysis without any extra development work. This can help you improve O&M and operational efficiency, and build up the capability to process large amounts of logs in the data technology era. Log Service is a streaming data storage system. Realtime Compute supports creating a Log Service table as the source table. In Log Service, each data record is in a format similar to JSON. An example is as follows:

```language-json
{
    "a": 1000,
    "b": 1234,
    "c": "li"
}
			
```

Realtime Compute needs to define the following DDL \(in which sls indicates Log Service\):

```language-sql
create table sls_stream(
  a int,
  b int,
  c VARCHAR
) with (
  type ='sls',
  endPoint ='yourEndpoint',
  accessId ='yourAccessId',
  accessKey ='yourAccessKey',
  startTime = 'yourStartTime',
  project ='yourProjectName',
  logStore ='yourLogStoreName',
  consumerGroup ='yourConsumerGroupName'
);
			
```

## Attribute fields {#section_xhx_xxy_bgb .section}

Currently, Flink SQL supports obtaining the following three attribute fields of Log Service by default, and writing other custom fields.

|Field|Description|
|-----|-----------|
|`__source__`|The message source.|
|`__topic__`|The message topic.|
|`__timestamp__`|The time when the log was generated.|

 Notes on attribute fields 

To obtain attribute fields, you need to first declare the fields according to the normal logic. Then add the keyword `HEADER` to the end of the type declaration. Example:

-   Test data

    ```
         __topic__:  ens_altar_flow  
            result:  {"MsgID":"ems0a","Version":"0.0.1"}
    					
    ```

-   Test statements

    ```language-sql
    CREATE TABLE sls_log (
      __topic__  varchar HEADER,
      result     varchar  
    )
    WITH
    (
      type = 'sls'
    );
    
    CREATE TABLE sls_out (
      name     varchar,
      MsgID    varchar,
      Version  varchar 
    )
    WITH
    (
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

    |name\(VARCAHR\)|MsgID\(VARCAHR\)|Version\(VARCAHR\)|
    |---------------|----------------|------------------|
    |ens\_altar\_flow|ems0a|0.0.1|


## WITH parameters {#section_uz1_zxy_bgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|endPoint|The consumption endpoint information.|[Service endpoint](../../../../intl.en-US/API Reference/Service endpoint.md#)|
|accessId|The AccessKey ID of Log Service.|None|
|accessKey|The AccessKey Secret of Log Service.|None|
|project|The Log Service project to be accessed.|None|
|logStore|The LogStore in the Log Service project.|None|
|consumerGroup|The name of the consumer group.|You can customize the consumer group name \(with no fixed format\).|
|startTime|The start time that the log is consumed.|None|
|heartBeatIntervalMills|The heartbeat interval of the consumption client.|Optional. Default value: 10 seconds.|
|maxRetryTimes|The maximum number of read retries.|Optional. Default value: 5.|
|batchGetSize|The number of log items read at a time in a log group.|Optional. Default value: 10.|
|lengthCheck|The policy for checking the number of fields in a single line.|Optional. Default value: NONE. Valid values: NONE, SKIP, EXCEPTION, and PAD. -   SKIP: skips a data record when the number of fields in the record does not match the specified number.
-   EXCEPTION: throws an exception when the number of fields in the record does not match the specified number.
-   PAD: pads fields in sequence. Pad with null when a field does not exist.

 |
|columnErrorDebug|Indicates whether to enable debugging. If this parameter is set to true, logs about parsing exceptions are displayed.|Optional. Default value: false.|

**Note:** 

-   Log Service does not support data of the MAP type.
-   Fields can be unordered. However, we recommend that you use the same field order as that defined in the referenced table.
-   If the input data source is in JSON format, define a delimiter and use a built-in function to analyze JSON\_VALUE. Otherwise, the parsing fails and the following error information is generated:

    ```
    2017-12-25 15:24:43,467 WARN [Topology-0 (1/1)] com.alibaba.blink.streaming.connectors.common.source.parse.DefaultSourceCollector - Field missing error, table column number: 3, data column number: 3, data filed number: 1, data: [{"lg_order_code":"LP00000005","activity_code":"TEST_CODE1","occur_time":"2017-12-10 00:00:01"}]
    						
    ```

-   The batchGetSize value must not exceed 1000. Otherwise, an error is returned.
-   The batchGetSize parameter specifies the number of log items read at a time in a log group. If both the size of a single log item and the batchGetSize value are too large, frequent GC may be triggered. To avoid this, you need to set the parameters to smaller values.

## Field type mapping {#section_zgx_zxy_bgb .section}

The following table lists the mapping between Log Service field types and Realtime Compute field types. We recommend that you use the mapping in the DDL declaration.

|Log Service field type|Realtime Compute field type|
|----------------------|---------------------------|
|STRING|VARCHAR|

