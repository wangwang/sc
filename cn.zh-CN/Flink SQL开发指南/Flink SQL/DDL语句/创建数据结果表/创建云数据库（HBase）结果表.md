# 创建云数据库（HBase）结果表 {#concept_91464_zh .concept}

本文为您介绍如何创建实时计算云数据库（HBase）结果表。

**说明：** 本文档仅适用于实时计算独享模式。

## DDL定义 {#section_l2m_q1g_cgb .section}

实时计算支持使用HBase作为结果输出。示例代码如下。

```
create table liuxd_user_behavior_test_front (
    row_key varchar,
    from_topic varchar,
    origin_data varchar,
    record_create_time varchar,
    primary key (row_key)
) with (
    type = 'cloudhbase',
    zkQuorum = '2',  
    columnFamily = 'yourColumnFamily',
    tableName = 'yourTableName',
    batchSize = '500'
)    
```

**说明：** 

-   `primary key`支持定义多个字段。多个字段会按照`rowkeyDelimiter`（默认为`:`）拼接起来作为`row_key`。
-   HBase做撤回删除操作时，如果Column定义了多版本，会把所有版本的值清空。

## WITH参数 {#section_zdt_m1g_cgb .section}

|参数|注释说明|备注|
|--|----|--|
|zkQuorum|HBase集群配置的zk地址|可以在hbase-site.xml文件中找到hbase.zookeeper.quorum相关配置|
|zkNodeParent|集群配置在zk上的路径|可以在hbase-site.xml文件中找到hbase.zookeeper.quorum相关配置|
|tableName|HBase表名|无|
|userName|用户名|无|
|password|密码|无|
|partitionBy|是否使用joinKey进行分区|可选，默认为False。设置为True时，使用joinKey进行分区，将数据分发到各JOIN节点，提高缓存命中率。|
|shuffleEmptyKey|是否将上游EMPTY KEY随机发送到下游节点|可选，默认为False。参数意义如下： -   False：如果上游有多个EMPTY KEY，将会将所有EMPTY KEY发送大同一个JOIN节点。
-   Te：如果上游有多个EMPTY KEY，将会将所有EMPTY KEY随机发送到各个JOIN节点。

 **说明：** shuffleEmptyKey在partitionedJoin生效后才是使用。

 |
|columnFamily|列族名|目前只支持插入同一列族|
|maxRetryTimes|最大尝试次数|可选，默认为10|
|bufferSize|流入多少条数据后进行去重|默认为5000|
|batchSize|一次批量写入的条数|可选，默认为100|
|flushIntervalMs|最长插入时间|可选，默认为2000|
|writePkValue|是否写入主键值|可选，默认为false|
|stringWriteMod|是否都按照string插入|可选，默认为false|
|rowkeyDelimiter|rowKey的分隔符|可选，默认为`:`|
|isDynamicTable|是否为动态表|可选，默认为false|

**说明：** 建议batchSize参数值设置在200到300之间。过大的batchSize值可能导致任务OOM（内存不足）报错。

## 动态表 {#section_3k6_x0r_gtp .section}

一些结果数据需要按某列的值作为动态列写入HBase。以每小时的成交数据作为动态列，保存在HBase中的示例如下。

|rowkey|cf:0|cf:1|...|
|------|----|----|---|
|20170707|100|200|...|

当isDynamicTable参数值为true时，表明该表为支持动态列的HBase表。

动态表仅支持3列输出，例如，rowkey, column和value。此时第2列（示例中的column）为动态列，其它参数与上述HBase参数一致。

**说明：** 使用动态表时，所有数据类型都会转换为STRING类型再进行输入。

``` {#codeblock_c5q_hwy_ko9 .language-SQL}
CREATE TABLE stream_test_hotline_agent (
  name varchar,
  age varchar,
  birthday varchar,
  primary key (name)
) WITH (
  type = 'cloudhbase',
  ...
columnFamily = 'cf',
 isDynamicTable ='true')
```

**说明：** 

-   以上声明中，会把birthday插入到以name为rowkey的cf:age列中。例如，一列数据是`（wang,18,2016-12-12)`，则这条数据会插入rowkey为`wang` 的行，`cf:18`列。
-   动态表严格按照rowkey column value的顺序，且必须在primary key中定义第1个字段为rowkey。

