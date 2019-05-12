# PARSE\_URL {#concept_62551_zh .concept}

This topic describes how to use the string function PARSE\_URL in Realtime Compute.

## Syntax {#section_sdq_5xq_dgb .section}

```language-sql
VARCHAR PARSE_URL(VARCHAR urlStr, VARCHAR partToExtract [, VARCHAR key])

```

## Input parameters {#PARSE_URL-OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|urlStr|VARCHAR|The URL string.|
|partToExtract|VARCHAR|The part to be parsed from the URL.|
|key \(optional\)|VARCHAR|The name of the key whose value is to be extracted.|

## Function description {#PARSE_URL-OG_02 .section}

This function parses a URL and returns the specified part from the URL. If the value of partToExtract is QUERY, this function returns the value of the specified key in the URL. Valid values of partToExtract include HOST, PATH, QUERY, REF, PROTOCOL, FILE, AUTHORITY, and USERINFO.

**Note:** If the input URL string is NULL, the return value is NULL.

## Examples {#PARSE_URL-OG_03 .section}

-   Test data

    |url1\(VARCHAR\)|nullstr\(VARCHAR\)|
    |---------------|------------------|
    |http://facebook.com/path/p1.php?query=1|null|

-   Test statements

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

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|var4\(VARCHAR\)|var5\(VARCHAR\)|var6\(VARCHAR\)|var7\(VARCHAR\)|var8\(VARCHAR\)|var9\(VARCHAR\)|var10\(VARCHAR\)|var11\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|----------------|----------------|
    |1|query=1|facebook.com|/path/p1.php|null|http|/path/p1.php? query=1|facebook.com|null|null|null|


