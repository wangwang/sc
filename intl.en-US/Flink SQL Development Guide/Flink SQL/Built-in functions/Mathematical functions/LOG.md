# LOG {#concept_ohl_zgq_dgb .concept}

This topic describes how to use the mathematical function LOG in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE LOG(DOUBLE base, DOUBLE x)
DOUBLE LOG(DOUBLE x)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|base|DOUBLE|
|x|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the logarithm of x to the specified base. The return value is a logarithm of the DOUBLE type. If base is not specified, this function returns the logarithm of x to base e.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |ID\(INT\)|BASE\(DOUBLE\)|X\(DOUBLE\)|
    |---------|--------------|-----------|
    |1|10.0|100.0|
    |2|2.0|8.0|

-   Test statements

    ```
    SELECT id, LOG(base, x) as dou1, LOG(2) as dou2
    FROM T1
    					
    ```

-   Test results

    |ID\(INT\)|dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |---------|--------------|--------------|
    |1|2.0|0.6931471805599453|
    |2|3.0|0.6931471805599453|


