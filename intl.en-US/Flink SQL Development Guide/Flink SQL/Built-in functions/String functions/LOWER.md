# LOWER {#concept_62805_zh .concept}

This topic describes how to use the string function LOWER in Realtime Compute.

## Syntax {#section_dbp_qvq_dgb .section}

```language-sql
VARCHAR LOWER(A)

```

## Input parameters {#LOWER_OG_01 .section}

-   A

    VARCHAR


## Function description {#LOWER_OG_02 .section}

This function converts all the letters in a string to lowercase.

## Examples {#LOWER_OG_03 .section}

-   Test data

    |var1\(VARCHAR\)|
    |---------------|
    |Ss|
    |yyT|

-   Test statements

    ```language-sql
    SELECT LOWER(var1) as aa
    FROM T1;
    
    ```

-   Test results

    |aa\(VARCHAR\)|
    |-------------|
    |ss|
    |yyt|


