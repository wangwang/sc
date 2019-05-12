# SIN {#concept_dg5_x3q_dgb .concept}

This topic describes how to use the mathematical function SIN in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE SIN(A)
			
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the sine value of input parameter A.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |8.0|
    |0.4|

-   Test statements

    ```
    SELECT SIN(in1) as aa
    FROM T1
    ```

-   Test results

    |aa\(DOUBLE\)|
    |------------|
    |0.9893582466233818|
    |0.3894183423086505|


