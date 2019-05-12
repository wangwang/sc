# REGEXP {#concept_62550_zh .concept}

This topic describes how to use the string function REGEXP in Realtime Compute.

## Syntax {#section_rqy_fzq_dgb .section}

```language-sql
BOOLEAN REGEXP(VARCHAR str, VARCHAR pattern)

```

## Input parameters {#REGEXP_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The string.|
|pattern|VARCHAR|The regular expression pattern.|

## Function description {#REGEXP_OG_02 .section}

This function performs regular expression matching on a string to check whether it matches the specified pattern. If the string or pattern is empty or NULL, the return value is false.

## Examples {#REGEXP_OG_03 .section}

-   Test data

    |str1\(VARCHAR\)|pattern1\(VARCHAR\)|
    |---------------|-------------------|
    |k1=v1;k2=v2|k2\*|
    |k1:v1|k2:v2|k3|
    |null|k3|
    |k1:v1|k2:v2|null|
    |k1:v1|k2:v2|\(|

-   Test statements

    ```language-sql
    SELECT REGEXP(str1, pattern1) as result
    FROM T1
    
    ```

-   Test results

    |result\(BOOLEAN\)|
    |-----------------|
    |true|
    |false|
    |null|
    |null|
    |false|


