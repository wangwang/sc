# MIN {#concept_ygx_fhx_dgb .concept}

This topic describes how to use the aggregate function MIN in Realtime Compute. In Flink SQL, the MIN function returns the minimum value among all input values.

## Syntax {#section_dks_qgp_dgb .section}

```
MIX(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|TINYINT, SMALLINT, INT, BIGINT, FLOAT, DECIMAL, DOUBLE, BOOLEAN, or VARCHAR **Note:** The following data types are not supported: DATE, TIME, TIMESTAMP, and VARBINARY.

 |

## Function description {#section_hks_qgp_dgb .section}

This function returns the minimum value among all input values.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(INT\)|
    |-----------|
    |4|
    |8|

-   Test statements

    ```language-sql
    SELECT MIX(var1) as aa
    FROM T1
    ```

-   Test results

    |aa\(INT\)|
    |---------|
    |4|


