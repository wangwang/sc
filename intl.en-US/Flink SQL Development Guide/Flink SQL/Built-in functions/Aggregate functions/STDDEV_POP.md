# STDDEV\_POP {#concept_uhz_4hx_dgb .concept}

This topic describes how to use the aggregate function STDDEV\_POP in Realtime Compute. In Flink SQL, the STDDEV\_POP function returns the population standard deviation of a set of values.

## Syntax {#section_dks_qgp_dgb .section}

```
T STDDEV_POP(T value)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|value|BIGINT or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the population standard deviation of a set of values.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(DOUBLE\)|c\(VARCHAR\)|
    |-----------|------------|
    |0|Hi|
    |1|Hi|
    |2|Hi|
    |3|Hi|
    |4|Hi|
    |5|Hi|
    |6|Hi|
    |7|Hi|
    |8|Hi|
    |9|Hi|

-   Test statements

    ```language-sql
    SELECT c, STDDEV_POP(a) as dou1
    FROM MyTable
    GROUP BY c
    ```

-   Test results

    |c\(VARCHAR\)|dou1\(DOUBLE\)|
    |------------|--------------|
    |Hi|2.8722813232690143|


