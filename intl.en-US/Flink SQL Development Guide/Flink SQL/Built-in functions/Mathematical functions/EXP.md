# EXP {#concept_kfv_ydq_dgb .concept}

This topic describes how to use the mathematical function EXP in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE EXP()		
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns e raised to the power of the specified number. The constant e is the base of natural logarithms.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |8.0|
    |10.0|

-   Test statements

    ```
    SELECT EXP(in1) as aa
    FROM T1
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |2980.9579870417283|
    |22026.465794806718|


