# DEGREES {#concept_zhx_4kq_dgb .concept}

This topic describes how to use the mathematical function DEGREES in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE DEGREES( double x )
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|x|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function converts a radian value x to a degree value.

## Examples {#section_iks_qgp_dgb .section}

-   Test statements

    ```
    SELECT DEGREES( PI() ) as result
    FROM T1
    ```

-   Test results

    |result\(DOUBLE\)|
    |----------------|
    |180.0|


