# POSITION {#concept_74509_zh .concept}

This topic describes how to use the string function POSITION in Realtime Compute.

## Syntax {#section_lwp_syq_dgb .section}

```language-sql
INTEGER POSITION( x IN y)

```

## Input parameters {#POSITION_OG_01 .section}

|Parameter|Data type|
|---------|---------|
|x|VARCHAR|
|y|VARCHAR|

## Function description {#POSITION_OG_02 .section}

This function returns the position of the first occurrence of string x in string y. This function is similar to LOCATE\(substr,str\).

## Examples {#POSITION_OG_03 .section}

-   Test statements

    ```language-sql
    POSITION('in' IN 'china') as result
    FROM T1
    
    ```

-   Test results

    |result\(INT\)|
    |-------------|
    |3|


