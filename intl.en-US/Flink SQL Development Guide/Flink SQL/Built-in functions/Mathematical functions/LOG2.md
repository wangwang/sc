# LOG2 {#concept_vdc_qhq_dgb .concept}

This topic describes how to use the mathematical function LOG2 in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE LOG2(DOUBLE x)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|x|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the base-2 logarithm of x. If x is NULL, the return value is NULL. If x is negative, an exception occurs.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |id\(INT\)|X\(INT\)|
    |---------|--------|
    |1|8|
    |2|2|

-   Test statements

    ```
    SELECT id, log2(x) as dou1
    FROM T1
    
    ```

-   Test results

    |id\(INT\)|dou1\(DOUBLE\)|
    |---------|--------------|
    |1|3.0|
    |2|1.0|


