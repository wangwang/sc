# SPLIT\_INDEX {#concept_62544_zh .concept}

This topic describes how to use the string function SPLIT\_INDEX in Realtime Compute.

## Syntax {#section_ttn_xcq_dgb .section}

```language-sql
VARCHAR SPLIT_INDEX(VARCHAR str, VARCHAR sep, INT index)

```

## Input parameters {#SPLIT_INDEX-OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The source string to be split.|
|sep|VARCHAR|The separator.|
|index|INT|The index number of the substring to be extracted from the source string.|

## Function description {#SPLIT_INDEX-OG_02 .section}

This function uses the separator specified by `sep` to split the string specified by `str` into several substrings and returns the substring indexed as `index`. The value of `index` starts from 0. If the substring with the specified index number does not exist, the return value is NULL.

If any input parameter is NULL, the return value is NULL.

## Examples {#SPLIT_INDEX-OG_03 .section}

-   Test data

    |str\(VARCHAR\)|sep\(VARCHAR\)|index\(INT\)|
    |--------------|--------------|------------|
    |Jack,John,Mary|,|2|
    |Jack,John,Mary|,|3|
    |Jack,John,Mary|null|0|
    |null|,|0|

-   Test statements

    ```language-sql
    SELECT SPLIT_INDEX(str, sep, index) as var1
    FROM T1
    
    ```

-   Test results

    |var1\(VARCHAR\)|
    |---------------|
    |Mary|
    |null|
    |null|
    |null|


