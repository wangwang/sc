# POWER {#concept_is4_d3q_dgb .concept}

This topic describes how to use the mathematical function POWER in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE POWER(A, B)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|
|B|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the result of A raised to the power of B. The result is a DOUBLE value.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|in2\(DOUBLE\)|
    |-------------|-------------|
    |2.0|4.0|

-   Test statements

    ```
    SELECT POWER(in1, in2) as aa
    FROM T1
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |16.0|


