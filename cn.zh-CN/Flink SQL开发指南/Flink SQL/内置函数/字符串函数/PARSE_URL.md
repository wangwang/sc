# PARSE\_URL {#concept_62551_zh .concept}

本文为您介绍如何使用实时计算字符串函数PARSE\_URL。

## 语法 {#section_sdq_5xq_dgb .section}

```language-sql
VARCHAR PARSE_URL(VARCHAR urlStr, VARCHAR partToExtract [, VARCHAR key])

```

## 入参 {#PARSE_URL-OG_01 .section}

|参数|数据类型|说明|
|--|----|--|
|urlStr|VARCHAR|链接|
|partToExtract|VARCHAR|指定链接中解析的部分。可取值如下：-   HOST
-   PATH
-   QUERY
-   REF
-   PROTOCOL
-   FILE
-   AUTHORITY
-   USERINFO

|
|key|VARCHAR|可选，指定截取部分中，具体的键。|

## 功能描述 {#PARSE_URL-OG_02 .section}

返回urlStr中指定的部分解析后的值。

**说明：** urlStr参数值为null，则返回值为null。

## 示例 {#PARSE_URL-OG_03 .section}

-   测试数据

    |url1\(VARCHAR\)|nullstr\(VARCHAR\)|
    |---------------|------------------|
    |http://facebook.com/path/p1.php?query=1|null|

-   测试语句

    ```language-sql
    SELECT PARSE_URL(url1, 'QUERY', 'query') as var1,
           PARSE_URL(url1, 'QUERY') as var2,
           PARSE_URL(url1, 'HOST') as var3,
           PARSE_URL(url1, 'PATH') as var4,
           PARSE_URL(url1, 'REF') as var5,
           PARSE_URL(url1, 'PROTOCOL') as var6,
           PARSE_URL(url1, 'FILE') as var7,
           PARSE_URL(url1, 'AUTHORITY') as var8,
           PARSE_URL(nullstr, 'QUERY') as var9,
           PARSE_URL(url1, 'USERINFO') as var10,
           PARSE_URL(nullstr, 'QUERY', 'query') as var11
    FROM T1
    
    ```

-   测试结果

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|var4\(VARCHAR\)|var5\(VARCHAR\)|var6\(VARCHAR\)|var7\(VARCHAR\)|var8\(VARCHAR\)|var9\(VARCHAR\)|var10\(VARCHAR\)|var11\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|----------------|----------------|
    |1|query=1|facebook.com|/path/p1.php|null|http|/path/p1.php?query=1|facebook.com|null|null|null|


