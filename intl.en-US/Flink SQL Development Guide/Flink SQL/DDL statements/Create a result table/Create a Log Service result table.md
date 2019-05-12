# Create a Log Service result table {#concept_62529_zh .concept}

This topic describes how to create a Log Service result table in Realtime Compute.

## Introduction to Log Service {#section_fzz_tnf_cgb .section}

As an all-in-one real-time data logging service, Log Service allows you to quickly finish tasks such as data ingestion, consumption, delivery, query, and analysis without any extra development work. This can help you improve O&M and operational efficiency, and build up the capability to process large amounts of logs in the data technology era.

## DDL definition {#section_ivj_wnf_cgb .section}

Realtime Compute supports creating a Log Service table as the result table.

```language-sql
create table sls_stream(
 name varchar,
 age BIGINT,
 birthday BIGINT
)with(
 type='sls',
 endPoint=‘<yourEndpoint>’,
 accessId=‘<yourAccessId>’,
 accessKey=‘<yourAccessSecret>’,
 project=‘<yourProjectName>’,
 logStore='<yourLogstoreName>'
);
```

**Note:** We recommend that you use the data storage registration method to connect to Log Service. For more information, see [Log Service]().

## WITH parameters {#section_njl_xnf_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|endPoint|The endpoint.|[Service endpoint](../../../../intl.en-US/API Reference/Service endpoint.md#)|
|project|The project name.|None|
|topic|The table name of the topic.|None|
|accessId|The AccessKey ID.|None|
|accessKey|The AccessKey Secret.|None|
|mode|The write mode.|Optional. Default value: `random`. If this parameter is set to `partition`, data is written by partition.|
|partitionColumn|The partition column.|This parameter is required if `mode` is set to `partition`.|
|topic|The Log Service topic.|Optional. This parameter is left empty by default.|
|source|The source of the log. For example, you can set this parameter to the IP address of the machine where the log was generated.|Optional. This parameter is left empty by default.|

