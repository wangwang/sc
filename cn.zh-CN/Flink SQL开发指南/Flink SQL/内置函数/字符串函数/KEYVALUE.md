# KEYVALUE {#concept_62547_zh .concept}

本文为您介绍如何使用实时计算字符串函数KEYVALUE。

## 语法 {#section_skk_j5q_dgb .section}

```language-sql
VARCHAR KEYVALUE(VARCHAR str, VARCHAR split1, VARCHAR split2, VARCHAR key_name)

```

## 入参 {#KEYVALUE_OG_01 .section}

|参数|数据类型|说明|
|--|----|--|
|str|VARCHAR|字符串中的key-value（kv）对。|
|split1|VARCHAR|kv对的分隔符。|
|split2|VARCHAR|kv的分隔符。|
|key\_name|VARCHAR|键的名称|

## 功能描述 {#KEYVALUE_OG_02 .section}

解析str字符串中，匹配有split1\(kv对的分隔符\)和split2\(kv的分隔符\)的key-value对，根据key\_name返回对应的数值。key\_name值不存在或者异常时返回NULL。

## 示例 {#KEYVALUE_OG_03 .section}

-   测试数据

    |str\(VARCHAR\)|split1\(VARCHAR\)|split2\(VARCHAR\)|key1\(VARCHAR\)|
    |--------------|-----------------|-----------------|---------------|
    |k1=v1;k2=v2|;|=|k2|
    |null|;|||:|
    |k1:v1|k2:v2|null|=|:|
    |k1:v1|k2:v2|||=|null|
    |k1:v1|k2:v2|||=|:|

-   测试语句

    ```language-sql
    SELECT  KEYVALUE(str, split1, split2, key1) as `result`
    FROM T1
    
    ```

-   测试结果

    |result\(VARCHAR\)|
    |-----------------|
    |v2|
    |null|
    |null|
    |null|
    |null|


