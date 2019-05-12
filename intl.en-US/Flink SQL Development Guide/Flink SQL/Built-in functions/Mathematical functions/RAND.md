# RAND {#concept_o2y_l3q_dgb .concept}

This topic describes how to use the mathematical function RAND in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE RAND([BIGINT seed])
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|seed|BIGINT|

**Note:** The value of seed is a random number, which determines the start value of a random number sequence.

## Function description {#section_hks_qgp_dgb .section}

This function returns a random number between 0 \(inclusive\) and 1 \(exclusive\). The return value is of the DOUBLE type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |id\(INT\)|X\(INT\)|
    |---------|--------|
    |1|8|

-   Test statements

    ```
    SELECT id, rand(1) as dou1, rand(3) as dou2
    FROM T1
    ```

-   Test results

    |id\(INT\)|dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |---------|--------------|--------------|
    |1|0.7308781907032909|0.731057369148862|


