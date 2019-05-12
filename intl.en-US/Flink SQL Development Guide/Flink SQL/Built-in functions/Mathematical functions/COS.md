# COS {#concept_v35_4dq_dgb .concept}

This topic describes how to use the mathematical function COS in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE COS(A)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the cosine value of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |0.8|
    |0.4|

-   Test statements

    ```
    SELECT COS(in1) as aa
    FROM T1
    
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |0.6967067093471654|
    |0.9210609940028851|


