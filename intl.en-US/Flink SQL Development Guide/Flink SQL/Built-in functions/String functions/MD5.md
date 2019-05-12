# MD5 {#concept_62549_zh .concept}

This topic describes how to use the string function MD5 in Realtime Compute.

## Syntax {#section_wmf_vwq_dgb .section}

```language-sql
VARCHAR MD5(VARCHAR str)

```

## Input parameters {#MD5_OG_01 .section}

-   str

    VARCHAR


## Function description {#MD5_OG_02 .section}

This function returns the MD5 value of the specified string. If the input parameter is an empty string \("\), the return value is an empty string.

## Examples {#MD5_OG_03 .section}

-   Test data

    |str1\(VARCHAR\)|str2\(VARCHAR\)|
    |---------------|---------------|
    |k1=v1;k2=v2|Empty string|

-   Test statements

    ```language-sql
    SELECT
       MD5(str1) as var1,
       MD5(str2) as var2
    FROM T1
    
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|
    |---------------|---------------|
    |19c17f42b4d6a90f7f9ffc2ea9bdd775|Empty string|


