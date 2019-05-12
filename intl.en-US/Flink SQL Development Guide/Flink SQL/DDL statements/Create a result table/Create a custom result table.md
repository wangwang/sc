# Create a custom result table {#concept_lkf_kdh_cgb .concept}

This topic describes how to create a custom result table in Realtime Compute.

**Note:** This topic applies only to Realtime Compute deployed in exclusive mode.

To meet diversified output requirements, Realtime Compute now allows you to customize the sink plug-in. The following dependency packages are required for a Maven project. The scope setting is `<scope>provided</scope>`.

## JAR package download {#section_dj1_vdh_cgb .section}

1.  [blink-connector-common-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/99987/cn_zh/1544614396864/blink-connector-custom-blink-2.2.4.jar)
2.  [blink-connector-custom-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/99987/cn_zh/1544614508576/blink-connector-common-blink-2.2.4.jar)
3.  [blink-table-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/99987/cn_zh/1544614551435/blink-table-blink-2.2.4.jar)
4.  [flink-table\_2.11-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/99987/cn_zh/1544614593263/flink-table_2.11-blink-2.2.4-20181102.033727-1.jar)
5.  [flink-core-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/99987/cn_zh/1547195750660/flink-core-blink-2.2.4.jar)

## Dependencies for Realtime Compute V2.0 and later {#section_fqw_b2h_cgb .section}

```language-java


   <dependencies> 
    <dependency> 
      <groupId>com.alibaba.blink</groupId> 
      <artifactId>blink-table</artifactId> 
      <version>blink-2.2.4-SNAPSHOT</version> 
      <scope>provided</scope> 
    </dependency>
    <dependency>
      <groupId>org.apache.flink</groupId>
      <artifactId>flink-table_2.11</artifactId>
      <version>blink-2.2.4-SNAPSHOT</version>
      <scope>provided</scope> 
    </dependency>
    <dependency> 
      <groupId>org.apache.flink</groupId> 
      <artifactId>flink-core</artifactId>
      <version>blink-2.2.4-SNAPSHOT</version>
      <scope>provided</scope> 
    </dependency> 
    <dependency> 
      <groupId>com.alibaba.blink</groupId>
      <artifactId>blink-connector-common</artifactId>
      <version>blink-2.2.4-SNAPSHOT</version> 
      <scope>provided</scope>
    </dependency> 
    <dependency> 
      <groupId>com.alibaba.blink</groupId> 
      <artifactId>blink-connector-custom</artifactId>
      <version>blink-2.2.4-SNAPSHOT</version>
      <scope>provided</scope>
    </dependency> 
  </dependencies>
			
```

## API description {#section_cnq_cfh_cgb .section}

The custom result table class needs to inherit the base class of the custom sink plug-in and implement the following methods:

```language-java
protected Map<String,String> userParamsMap;// The key-value pairs defined by you in the SQL WITH statement. All keys are in lowercase.
protected Set<String> primaryKeys;// The custom primary key fields.
protected List<String> headerFields;// The list of fields marked as header.
protected RowTypeInfo rowTypeInfo;// The field type and name.
/**
 * The initialization method. This method is called when you create a table for the first time or in the case of failover.
 *
 * @param taskNumber  // The ID of the current operator.
 * @param numTasks  // The total number of sink operators.
 * @throws IOException
 */
public abstract void open(int taskNumber,int numTasks) throws IOException;

/**
 * The close method, which is used to release resources.
 *
 * @throws IOException
 */
public abstract void close() throws IOException;

/**
 * Insert a single row of data.
 *
 * @param row
 * @throws IOException
 */
public abstract void writeAddRecord(Row row) throws IOException;

/**
 * Delete a single row of data.
 *
 * @param row
 * @throws IOException
 */
public abstract void writeDeleteRecord(Row row) throws IOException;

/**
 * If you want to use this method to insert multiple rows at a time, you need to load all data cached in threads to the downstream operator. If you do not want to insert multiple rows at a time, this method is not required.
 *
 * @throws IOException
 */
public abstract void sync() throws IOException;

/** 
* Return the class name. 
*/ 
public String getName();
			
```

After uploading JAR packages to Realtime Compute and referencing resources, you need to specify `type = 'custom'` for your custom sink plug-in. In addition, specify the class that implements the method. The following shows an example of a custom Redis result table \([download the demo here](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/110869/cn_zh/1552549477388/customsink_redis.tar.gz)\).

```language-sql
create table in_table(
    kv varchar 
)with(
    type = 'random'
);

create table out_table(
    `key` varchar,
    `value` varchar
)with(
    type = 'custom',
    class = 'com.alibaba.blink.connector.custom.demo.RedisSink',
    -- **You can define more user parameters, which can be obtained by using userParamsMap in the open() function.** 
    host = 'r-uf****.redis.rds.aliyuncs.com',
    port = '6379',
    db = '0',
    batsize = '10',
    password = '‘<yourDatabasePassword>'
);

insert into out_table
select
substring(kv,0,4) as `key`,
substring(kv,0,6) as `value`
from in_table;
```

The following table describes parameters of the Redis sink plug-in.

|Name|Description|Required|Remarks|
|----|-----------|--------|-------|
|host|The intranet connection address of the Redis instance.|Yes|None|
|port|The port number of the Redis instance.|Yes|None|
|password|The password used to connect to the Redis instance.|Yes|None|
|db|The database ID.|No|Default value: 0, indicating db0.|
|batchsize|The number of data records written at a time.|No|Default value: 1, indicating that writing multiple data records at a time is not supported.|

