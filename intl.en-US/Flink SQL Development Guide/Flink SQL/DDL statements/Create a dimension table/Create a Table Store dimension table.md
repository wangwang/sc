# Create a Table Store dimension table {#concept_62533_zh .concept}

This topic describes how to create a Table Store dimension table in Realtime Compute.

## Introduction to Table Store {#section_wd3_vxm_cgb .section}

Table Store is a distributed NoSQL data storage service built on Alibaba Cloud's Apsara system. It is designed to provide 99.99% high availability and 99.999999999% data reliability. By using data sharding and load balancing technologies, Table Store implements seamless scale-out in terms of data scale and access parallelism. It also supports the storage of and real-time access to large amounts of structured data.

## Examples {#section_ysz_xxm_cgb .section}

Realtime Compute supports creating a Table Store table as the dimension table. The sample code is as follows:

```language-sql
CREATE TABLE ots_dim_table (
 id int,
 len int,
 content VARCHAR,
 PRIMARY KEY (id),
 PERIOD FOR SYSTEM_TIME -- Define the change period of the dimension table, which indicates that the dimension table is changeable.
) WITH (
 type='ots',
 endPoint=‘<yourEndpoint>’,
 instanceName='<yourInstanceName>',
 tableName='<yourTableName>',
 accessId=‘<yourAccessId>’,
 accessKey=‘<yourAccessSecret>’
);
			
```

**Note:** When you declare a dimension table, you must specify the primary key. When you join a dimension table to another table, the ON condition must contain the equivalent conditions for all primary keys. The primary key of a Table Store table is the rowkey field of the table.

## WITH parameters {#section_nns_yxm_cgb .section}

|Name|Description|
|----|-----------|
|instanceName|The instance name.|
|tableName|The table name.|
|endPoint|The endpoint for accessing the instance.|
|accessId|The AccessKey ID.|
|accessKey|The AccessKey Secret.|

## Cache parameters {#section_tzp_zxm_cgb .section}

|Name|Description|Remarks|
|----|-----------|-------|
|cache|The cache policy.|Default value: `None`. Valid values: None and `LRU`.|
|cacheSize|The cache size, in lines.|When cache is set to LRU, this parameter specifies the cache size. Default value: 10000.|
|cacheTTLMs|The time before the cache expires, in milliseconds.|When cache is set to LRU, this parameter specifies the time before the cache expires.|

## Sample code {#section_frs_51n_cgb .section}

```language-SQL
CREATE TABLE datahub_input1 (
id            BIGINT, 
name        VARCHAR, 
age           BIGINT
) WITH (
type='datahub'
);

create table phoneNumber(
name VARCHAR,
phoneNumber bigint,
primary key(name),
PERIOD FOR SYSTEM_TIME -- Define the change period of the dimension table.
)with(
type='ots'
);

CREATE table result_infor(
id bigint,
phoneNumber bigint,
name VARCHAR
)with(
type='rds'
);

INSERT INTO result_infor
SELECT
t.id
,w.phoneNumber
,t.name
FROM datahub_input1 as t
JOIN phoneNumber FOR SYSTEM_TIME AS OF PROCTIME() as w -- This statement must be specified for joining the dimension table.
ON t.name = w.name;
			
```

For detailed syntax of dimension tables, see [Dimension table JOIN statement](intl.en-US/Flink SQL Development Guide/Flink SQL/Query statements/Dimension table JOIN statement.md#).

