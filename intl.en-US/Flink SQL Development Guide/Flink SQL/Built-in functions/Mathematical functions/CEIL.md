# CEIL {#concept_lk4_xjq_dgb .concept}

This topic describes how to use the mathematical function CEIL in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
B CEIL(A)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|INT, BIGINT, FLOAT, or DOUBLE|
|B|INT, BIGINT, FLOAT, or DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function rounds input parameter A up to the nearest integer greater than or equal to A. The data type of output parameter B is the same as that of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(INT\)|in2\(DOUBLE\)|
    |----------|-------------|
    |1|2.3|

-   Test statements

    ```language-SQL
    SELECT
    CEIL(in1) as out1
    CEIL(in2) as out2
    FROM T1
    ```

-   Test results

    |out1\(INT\)|out2\(DOUBLE\)|
    |-----------|--------------|
    |1|3.0|


