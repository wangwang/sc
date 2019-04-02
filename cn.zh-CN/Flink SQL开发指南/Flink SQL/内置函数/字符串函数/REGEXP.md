# REGEXP {#concept_62550_zh .concept}

本文为您介绍如何使用实时计算字符串函数REGEXP。

## 语法 {#section_rqy_fzq_dgb .section}

```language-sql
BOOLEAN REGEXP(VARCHAR str, VARCHAR pattern)

```

## 入参 {#REGEXP_OG_01 .section}

|参数|数据类型|说明|
|--|----|--|
|str|VARCHAR|指定的字符串。|
|pattern|VARCHAR|指定的匹配模式。|

## 功能描述 {#REGEXP_OG_02 .section}

指定str的字符串是否匹配指定的pattern进行正则匹配,str或者pattern为空或NULL返回false。

## 示例 {#REGEXP_OG_03 .section}

-   测试数据

    |str1\(VARCHAR\)|pattern1\(VARCHAR\)|
    |---------------|-------------------|
    |k1=v1;k2=v2|k2\*|
    |k1:v1|k2:v2|k3|
    |null|k3|
    |k1:v1|k2:v2|null|
    |k1:v1|k2:v2|\(|

-   测试语句

    ```language-sql
    SELECT  REGEXP(str1, pattern1) AS result
    FROM T1
    
    ```

-   测试结果

    |result\(BOOLEAN\)|
    |-----------------|
    |true|
    |false|
    |false|
    |false|
    |false|


