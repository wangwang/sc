# SUBSTRING {#concept_62542_zh .concept}

This topic describes how to use the string function SUBSTRING in Realtime Compute.

## Syntax {#section_qt1_fhq_dgb .section}

```language-sql
VARCHAR SUBSTRING(VARCHAR a, INT start)
VARCHAR SUBSTRING(VARCHAR a, INT start, INT len)

```

## Input parameters {#SUBSTRING_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|a|VARCHAR|The source string.|
|start|INT|The start position of the substring to be extracted from the source string.|
|len|INT|The length of the substring to be extracted.|

## Function description {#SUBSTRING_OG_02 .section}

This function returns a substring of the specified length from a string, starting from the specified position. If the length is not specified, this function returns the substring from the specified position to the end of the string. The value of start begins with 1. If the value is 0, it is regarded as 1. If the value is negative, this function counts backward from the end of the string to find the first character of the substring.

## Examples {#SUBSTRING_OG_03 .section}

-   Test data

    |str\(VARCHAR\)|nullstr\(VARCHAR\)|
    |--------------|------------------|
    |k1=v1;k2=v2|null|

-   Test statements

    ```language-sql
    SELECT SUBSTRING('', 222222222) as var1,
           SUBSTRING(str, 2) as var2,
           SUBSTRING(str, -2) as var3,
           SUBSTRING(str, -2, 1) as var4, 
           SUBSTRING(str, 2, 1) as var5,
           SUBSTRING(str, 22) as var6,
           SUBSTRING(str, -22) as var7,
           SUBSTRING(str, 1) as var8,
           SUBSTRING(str, 0) as var9,
           SUBSTRING(nullstr, 0) as var10
    FROM T1
    
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|var4\(VARCHAR\)|var5\(VARCHAR\)|var6\(VARCHAR\)|var7\(VARCHAR\)|var8\(VARCHAR\)|var9\(VARCHAR\)|var10\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|---------------|----------------|
    |Empty string|1=v1;k2=v2|v2|v|1|Empty string|Empty string|k1=v1;k2=v2|k1=v1;k2=v2|null|


