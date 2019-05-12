# CONCAT\_AGG {#concept_p1p_2yr_dgb .concept}

This topic describes how to use the aggregate function CONCAT\_AGG in Realtime Compute. In Flink SQL, the CONCAT\_AGG function concatenates the strings of all specified fields and returns a new string.

## Syntax {#section_dks_qgp_dgb .section}

```
CONCAT_AGG([linedelimiter,] value)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|linedelimiter \(optional\)|Only a string constant is currently supported.|

## Function description {#section_hks_qgp_dgb .section}

This function concatenates the strings of all specified fields and returns a new string. The default connector is `\n`. The return value is of the VARCHAR type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |c\(VARCHAR\)|
    |------------|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|
    |Hi|

-   Test statements

    ```language-sql
    SELECT 
    concat_agg(c) as var1, 
    concat_agg('-', c) as var2
    FROM MyTable
    GROUP BY c
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|
    |---------------|---------------|
    |Hi\\nHi\\nHi\\nHi\\nHi\\nHi\\nHi\\nHi\\nHi\\nHi|Hi-Hi-Hi-Hi-Hi-Hi-Hi-Hi-Hi-Hi|


