# AVG {#concept_h55_txr_dgb .concept}

This topic describes how to use the aggregate function AVG in Realtime Compute. In Flink SQL, the AVG function returns the average value of all values in the specified expression.

## Syntax {#section_dks_qgp_dgb .section}

```
AVG(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|TINYINT, SMALLINT, INT, BIGINT, FLOAT, DECIMAL, or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the average value of a column.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(INT\)|var2\(INT\)|
    |-----------|-----------|
    |4|30|
    |6|30|

-   Test statements

    ```language-sql
    SELECT AVG(var1) as aa
    FROM T1
    ```

-   Test results

    |aa\(INT\)|
    |---------|
    |5|


