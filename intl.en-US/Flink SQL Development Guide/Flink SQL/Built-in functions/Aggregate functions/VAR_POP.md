# VAR\_POP {#concept_cf1_x3x_dgb .concept}

This topic describes how to use the aggregate function VAR\_POP in Realtime Compute. In Flink SQL, the VAR\_POP function returns the population variance of all input values in the specified expression.

## Syntax {#section_dks_qgp_dgb .section}

```
T VAR_POP(T value)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|value|Numeric type, such as BIGINT or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the population variance of all input values.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(BIGINT\)|c\(VARCHAR\)|
    |-----------|------------|
    |2900|Hi|
    |2500|Hi|
    |2600|Hi|
    |3100|Hello|
    |11000|Hello|

-   Test statements

    ```language-sql
    SELECT 
    VAR_POP(a) as `result`,
     c
    FROM MyTable
    GROUP BY c
    ```

-   Test results

    |result\(BIGINT\)|c|
    |----------------|--|
    |28889|Hi|
    |15602500|Hello|


