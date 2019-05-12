# REPLACE {#concept_93504_zh .concept}

This topic describes how to use the string function REPLACE in Realtime Compute.

## Syntax {#section_rg5_fzp_dgb .section}

```language-sql
VARCHAR REPLACE(str1, str2, str3)

```

## Input parameters {#REPLACE_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str1|VARCHAR|The source string.|
|str2|VARCHAR|The substring to be replaced in the source string.|
|str3|VARCHAR|The replacement substring.|

## Function description {#REPLACE_OG_02 .section}

This function replaces a substring of a string with another substring.

## Examples {#REPLACE_OG_03 .section}

-   Test data

    |str1\(INT\)|str2\(INT\)|str3\(INT\)|
    |-----------|-----------|-----------|
    |alibaba blink|blink|flink|

-   Test statements

    ```language-sql
    SELECT REPLACE(str1, str2, str3) as `result`
    FROM T1
    
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |alibaba flink|


