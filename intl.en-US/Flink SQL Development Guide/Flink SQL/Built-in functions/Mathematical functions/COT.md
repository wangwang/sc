# COT {#concept_ilp_tdq_dgb .concept}

This topic describes how to use the mathematical function COT in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE COT(A)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the cotangent value of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |0.8|
    |0.4|

-   Test statements

    ```
    SELECT COT(in1) as aa
    FROM T1
    
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |1.0296385570503641|
    |0.4227932187381618|


