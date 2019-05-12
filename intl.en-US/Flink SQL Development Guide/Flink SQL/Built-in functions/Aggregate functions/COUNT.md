# COUNT {#concept_r35_1zr_dgb .concept}

This topic describes how to use the aggregate function COUNT in Realtime Compute. In Flink SQL, the COUNT function returns the number of rows in a given column.

## Syntax {#section_dks_qgp_dgb .section}

```
COUNT(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A| -   Supported data types: TINYINT, SMALLINT, INT, BIGINT, FLOAT, DECIMAL, DOUBLE, BOOLEAN, and VARCHAR
-   Unsupported data types: DATE, TIME, TIMESTAMP, and VARBINARY

 |

## Function description {#section_hks_qgp_dgb .section}

This function returns the number of rows in a given column.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(VARCHAR\)|
    |---------------|
    |1000|
    |100|
    |10|
    |1|

-   Test statements

    ```language-sql
    SELECT COUNT(var1) as aa
    FROM T1
    					
    ```

-   Test results

    |aa\(BIGINT\)|
    |------------|
    |4|


