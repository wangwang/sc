# ABS {#concept_62741_zh .concept}

This topic describes how to use the mathematical function ABS in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE ABS(A)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the absolute value of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |4.3|

-   Test statements

    ```
    SELECT ABS(in1) as aa
    FROM T1
    
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |4.3|


