# REGEXP\_REPLACE {#concept_62545_zh .concept}

This topic describes how to use the string function REGEXP\_REPLACE in Realtime Compute.

## Syntax {#section_rmd_5rp_dgb .section}

```language-sql
VARCHAR REGEXP_REPLACE(VARCHAR str, VARCHAR pattern, VARCHAR replacement)

```

## Input parameters {#REGEXP_REPLACE_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The source string.|
|pattern|VARCHAR|The substring to be replaced in the source string.|
|replacement|VARCHAR|The replacement substring.|

**Note:** Comply with Java code conventions to write regular expression constants. When you run the codegen tool, it automatically converts SQL constant strings to Java code. Write the string \\d as '\\d' in the regular expression, just in the same way as you write a regular expression in Java.

## Function description {#REGEXP_REPLACE_02 .section}

This function replaces a substring that matches the specified regular expression pattern in the source string with another substring, and returns a new string. If any input parameter is NULL or the regular expression is invalid, the return value is NULL.

## Examples {#REGEXP_REPLACE_03 .section}

-   Test data

    |str1\(VARCHAR\)|pattern1\(VARCHAR\)|replace1\(VARCHAR\)|
    |---------------|-------------------|-------------------|
    |2014-03-13|-|Empty string|
    |null|-|Empty string|
    |2014-03-13|-|null|
    |2014-03-13|Empty string|s|
    |2014-03-13|\(|s|
    |100-200|\(\\d+\)|num|

-   Test statements

    ```language-sql
    SELECT REGEXP_REPLACE(str1, pattern1, replace1) as result
    FROM T1
    
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |20140313|
    |null|
    |null|
    |2014-03-13|
    |null|
    |num-num|


