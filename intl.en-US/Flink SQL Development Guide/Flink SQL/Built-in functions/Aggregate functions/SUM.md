# SUM {#concept_p51_m3x_dgb .concept}

This topic describes how to use the aggregate function SUM in Realtime Compute. In Flink SQL, the SUM function returns the sum of all input values.

## Syntax {#section_dks_qgp_dgb .section}

```
SUM(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|TINYINT, SMALLINT, INT, BIGINT, FLOAT, DECIMAL, or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the sum of all input values.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(INT\)|
    |-----------|
    |4|
    |4|

-   Test statements

    ```language-sql
    SELECT sum(var1) as aa
    FROM T1
    ```

-   Test results

    |aa\(INT\)|
    |---------|
    |8|


