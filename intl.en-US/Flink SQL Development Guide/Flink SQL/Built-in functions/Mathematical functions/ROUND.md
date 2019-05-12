# ROUND {#concept_czf_blq_dgb .concept}

This topic describes how to use the mathematical function ROUND in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DECIMAL ROUND( DECIMAL x, INT n)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|x|DECIMAL|
|n|INT|

## Function description {#section_hks_qgp_dgb .section}

This function rounds the x parameter to n decimal places.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DECIMAL\)|
    |--------------|
    |0.7173560908995228|
    |0.4|

-   Test statements

    ```
    SELECT ROUND(in1,2) as `result`
    FROM T1
    
    ```

-   Test results

    |result\(DECIMAL\)|
    |-----------------|
    |0.72|
    |0.40|


