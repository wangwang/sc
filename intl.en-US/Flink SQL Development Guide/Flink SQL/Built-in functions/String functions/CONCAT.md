# CONCAT {#concept_62537_zh .concept}

This topic describes how to use the string function CONCAT in Realtime Compute.

## Syntax {#section_gdf_klq_dgb .section}

```language-sql
 VARCHAR CONCAT(VARCHAR var1, VARCHAR var2, ...)

```

## Input parameters {#CONCAT_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|var1|VARCHAR|The string.|
|var2|VARCHAR|The string.|

## Function description {#CONCAT_OG_02 .section}

This function concatenates two or more strings into a single string. If any input parameter is NULL, the parameter is skipped.

## Examples {#CONCAT_OG_03 .section}

-   Test data

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|
    |---------------|---------------|---------------|
    |Hello|My|World|
    |Hello|null|World|
    |null|null|World|
    |null|null|null|

-   Test statements

    ```language-sql
    SELECT CONCAT(var1, var2, var3) as var
    FROM T1
    
    ```

-   Test results

    |var\(VARCHAR\)|
    |--------------|
    |HelloMyWorld|
    |HelloWorld|
    |World|
    |null|


