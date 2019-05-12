# Create an ElasticSearch result table {#concept_94716_zh .concept}

This topic describes how to create an ElasticSearch result table in Realtime Compute.

**Note:** This topic applies only to Realtime Compute deployed in exclusive mode.

## DDL definition {#section_ls1_qhg_cgb .section}

REST API is used to implement ElasticSearch result tables. Theoretically, REST API is compatible with all ElasticSearch versions. Realtime Compute supports creating an ElasticSearch table as the result table. The sample code is as follows:

```language-sql
create table es_stream_sink(
  field1 long, 
  field2 varbinary, 
  field3 varchar,
  PRIMARY KEY(field1)
) with (
  type ='elasticsearch',
  endPoint = '<yourEndPoint>',
  accessId = '<yourAccessId>',
  accessKey = '<yourAccessSecret>',
  index = '<yourIndex>',
  typeName = '<yourTypeName>'
);
```

**Note:** ElasticSearch supports data update based on the primary key. You can define only one field for the primary key.

-   When the primary key is specified, the document IDs are the values of the primary key field.
-   When the primary key is not specified, the document IDs are generated at random. For more information, see [Index API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html).
-   In full update mode, later documents overwrite earlier documents instead of updating fields in earlier documents.
-   In incremental update mode, the corresponding fields are updated based on the passed-in field values.
-   All updates use the upsert semantics by default, indicating insert or update.

## WITH parameters {#section_xgs_43g_cgb .section}

General configuration

|Name|Description|Default value|Required|
|----|-----------|-------------|--------|
|endPoint|The server address, for example: http://127.0.0.1:9211.|None|Yes|
|accessId|The AccessKey ID.|None|Yes|
|accessKey|The AccessKey Secret.|None|Yes|
|index|The index name, which is similar to the database name.|None|Yes|
|typeName|The type name, which is similar to the database table name.|None|Yes|
|bufferSize|The number of data records written at a time.|1000|No|
|maxRetryTimes|The maximum number of retries allowed in the case of an exception.|30|No|
|timeout|The read timeout period. Unit: millisecond.|600000|No|
|discovery|Indicates whether to enable operator discovery. If operator discovery is enabled, the client refreshes the server list every 5 minutes.|false|No|
|compression|Indicates whether to use GZIP to compress request bodies.|true|No|
|multiThread|Indicates whether to enable multithreading for JestClient.|true|No|
|ignoreWriteError|Indicates whether to ignore write exceptions.|false|No|
|Settings|The settings used to create indexes.|None|No|
|updateMode|The update mode after the primary key is specified.|full **Note:** 

-   full: full data overwriting
-   inc: incremental data update

 |No|

## Dynamic index-related WITH parameters {#section_pyd_qms_jgb .section}

|Name|Description|Default value|Required|
|dynamicIndex|Indicates whether to enable dynamic indexes.|false\(true/false\)|No|
|indexField|The field name of the index.|None|This parameter is required only when dynamicIndex is set to true. It supports only the TIMESTAMP \(in seconds\), DATE, and LONG data types.|
|indexInterval|The interval between index changes.|d|This parameter is required only when dynamicIndex is set to true. Valid values: -   d: Day
-   m: Month
-   w: Week

 |

**Note:** 

1.  When dynamicIndex is set to true, the `index` name in basic settings is used as the unified alias for indexes created subsequently. The alias and indexes have an one-to-many relationship.
2.  Actual index names corresponding to different values of `indexInterval` are as follows:
    -   d -\> Alias + "yyyyMMdd"
    -   m -\> Alias + "yyyyMM"
    -   w -\> Alias + "yyyyMMW"
3.  You can use Index API to modify an actual index, but you can only `get` the alias. If you want to modify the alias, see [Index Aliases](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-aliases.html).

