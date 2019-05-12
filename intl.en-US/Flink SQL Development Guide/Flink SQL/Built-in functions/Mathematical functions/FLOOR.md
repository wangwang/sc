# FLOOR {#concept_wrm_dgq_dgb .concept}

This topic describes how to use the mathematical function FLOOR in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
B FLOOR(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|INT, BIGINT, FLOAT, or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function rounds down the decimal portion of input parameter A and returns the largest integer less than or equal to input parameter A. The data type of output parameter B is the same as that of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|in2\(BIGINT\)|
    |-------------|-------------|
    |8.123|3|

-   Test statements

    ```
    SELECT 
    FLOOR(in1) as out1,
    FLOOR(in2) as out2
    FROM T1
    ```

-   Test results

    |out1\(DOUBLE\)|out2\(BIGINT\)|
    |--------------|--------------|
    |8.0|3|


