# ASIN {#concept_62749_zh .concept}

This topic describes how to use the mathematical function ASIN in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE ASIN(A)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the arcsine value of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |0.7173560908995228|
    |0.4|

-   Test statements

    ```
    SELECT ASIN(in1) as aa
    FROM T1
    
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |0.8|
    |0.41151684606748806|


