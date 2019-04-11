# MULTI\_KEYVALUE {#concept_b2y_wly_zfb .concept}

本文为您介绍如何使用实时计算表值函数MULTI\_KEYVALUE。

**说明：** 仅支持实时计算2.2.2及以上版本。

## 语法 {#section_ezt_4my_zfb .section}

```
MULTI_KEYVALUE(VARCHAR str, VARCHAR split1, VARCHAR split2, VARCHAR key_name1, VARCHAR key_name2, ...)

```

## 入参 {#section_axr_sc5_jhb .section}

|参数|数据类型|说明|
|--|----|--|
|str|VARCHAR|字符串中的key-value（kv）对。|
|split1|VARCHAR|kv对的分隔符。当split1为null，表示按照whitespace作为kv对的分割符。当split1的长度\>1时，split1仅表示分隔符的集合，每个字符都表示一个有效的分隔符。|
|split2|VARCHAR|kv的分隔符。当split2为null，表示按照whitespace作为kv的分割符。当split2的长度\>1时，split2仅表示分隔符的集合，每个字符都表示一个有效的分隔符。|
|key\_name1, key\_name2, ...|VARCHAR|需要获取value的key值列表。|

## 功能描述 {#section_ymk_jd5_jhb .section}

解析str字符串中的key-value对，匹配有split1和split2的key-value对，并返回参数列表里key\_name1，key\_name2等对应的value值列表。key\_name值不存在时，对应的value值是null。

## 示例 {#section_vdy_pmy_zfb .section}

-   测试数据

    |str\(VARCHAR\)|split1\(VARCHAR\)|split2\(VARCHAR\)|key1\(VARCHAR\)|key2\(VARCHAR\)|
    |--------------|-----------------|-----------------|---------------|---------------|
    |k1=v1;k2=v2|;|=|k1|k2|
    |null|;|=|k1|k2|
    |k1:v1;k2:v2|;|:|k1|k3|
    |k1:v1;k2:v2|;|=|k1|k2|
    |k1:v1;k2:v2|,|:|k1|k2|
    |k1:v1;k2=v2|;|:|k1|k2|
    |k1:v1abck2:v2|cab|:|k1|k2|
    |k1:v1;k2=v2|;|:=|k1|k2|
    |k1:v1 k2:v2|null|:|k1|k2|
    |k1 v1;k2 v2|;|null|k1|k2|

-   测试语句

    ```language-sql
    SELECT c1, c2 
    FROM T1, lateral table(MULTI_KEYVALUE(str, split1, split2, key1, key2)) 
    as T(c1, c2)
    
    ```

-   测试结果

    |c1\(VARCHAR\)|c2\(VARCHAR\)|
    |-------------|-------------|
    |v1|v2|
    |null|null|
    |v1|null|
    |null|null|
    |null|null|
    |v1|null|
    |v1|v2|
    |v1|v2|
    |v1|v2|
    |v1|v2|


