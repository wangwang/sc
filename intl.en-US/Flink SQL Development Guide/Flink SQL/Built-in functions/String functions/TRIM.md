# TRIM {#concept_74511_zh .concept}

This topic describes how to use the string function TRIM in Realtime Compute.

## Syntax {#section_m2p_v3q_dgb .section}

```language-sql
VARCHAR TRIM( VARCHAR x )

```

## Input parameters {#TRIM_OG_01 .section}

|Parameter|Data type|
|---------|---------|
|x|VARCHAR|

## Function description {#TRIM_OG_02 .section}

This function removes leading and trailing characters from a string. The most common use is to remove leading and trailing spaces.

## Examples {#TRIM_OG_03 .section}

-   Test statements

    ```language-sql
    SELECT TRIM('   Sample   ') as result
    FROM T1
    
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |Sample|

    **Note:** The return value is 'Sample'.


