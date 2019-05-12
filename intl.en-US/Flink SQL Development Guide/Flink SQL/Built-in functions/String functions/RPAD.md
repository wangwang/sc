# RPAD {#concept_62540_zh .concept}

This topic describes how to use the string function RPAD in Realtime Compute.

## Syntax {#section_yj3_jbq_dgb .section}

```language-sql
VARCHAR RPAD(VARCHAR str, INT len, VARCHAR pad)

```

## Input parameters {#RPAD_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The source string.|
|len|INT|The length of the new string after padding.|
|pad|VARCHAR|The string to be repeatedly padded to the source string.|

## Function description {#RPAD_OG_02 .section}

This function right-pads a source string with another string several times until the new string reaches the specified length.`` If any input parameter is NULL, the return value is NULL.

If `len` is negative, the return value is NULL.

If `pad` is an empty string and the value of `len` is less than or equal to the length of `str`, `str` is trimmed to the specified length. If pad is an empty string and the value of `len` is greater than the length of `str`, the return value is NULL.

## Examples {#RPAD_OG_03 .section}

-   Test data

    |str\(VARCHAR\)|len\(INT\)|pad\(VARCHAR\)|
    |--------------|----------|--------------|
    |Empty string|-2|Empty string|
    |HelloWorld|15|John|
    |John|2|C|
    |C|4|HelloWorld|
    |null|2|C|
    |c|2|null|
    |asd|2|Empty string|
    |Empty string|2|s|
    |asd|4|Empty string|
    |Empty string|0|Empty string|

-   Test statements

    ```language-sql
    SELECT RPAD(str, len, pad) as result
    FROM T1
    
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |null|
    |HelloWorldJohnJ|
    |Jo|
    |CHel|
    |null|
    |null|
    |as|
    |ss|
    |null|
    |Empty string|


