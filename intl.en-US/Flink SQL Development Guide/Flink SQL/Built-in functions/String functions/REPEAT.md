# REPEAT {#concept_62541_zh .concept}

This topic describes how to use the string function REPEAT in Realtime Compute.

## Syntax {#section_cl2_25p_dgb .section}

```language-sql
VARCHAR REPEAT(VARCHAR str, INT n)

```

## Input parameters {#REPEAT_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The string to be repeated.|
|n|INT|The number of times to repeat the string.|

## Function description {#REPEAT_OG_02 .section}

This function repeats a string a specified number of times and returns a new string. If str is NULL, the return value is NULL. If n is 0 or negative, the return value is an empty string.

## Examples {#REPEAT_OG_03 .section}

-   Test data

    |str\(VARCHAR\)|n\(INT\)|
    |--------------|--------|
    |J|9|
    |Hello|2|
    |Hello|-9|
    |null|9|

-   Test statements

    ```language-sql
    SELECT REPEAT(str,n) as var1
    FROM T1
    
    ```

-   Test results

    |var1\(VARCHAR\)|
    |---------------|
    |JJJJJJJJJ|
    |HelloHello|
    |Empty string|
    |null|


