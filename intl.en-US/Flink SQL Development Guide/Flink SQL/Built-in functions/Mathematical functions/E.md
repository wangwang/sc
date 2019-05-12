# E {#concept_dly_4fq_dgb .concept}

This topic describes how to use the mathematical function E in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE E(A)
			
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|DOUBLE|

## Function description {#section_hks_qgp_dgb .section}

This function returns the DOUBLE type value of natural constant e.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |in1\(DOUBLE\)|
    |-------------|
    |8.0|
    |10.0|

-   Test statements

    ```
    SELECT id, e() as dou1, E() as dou2
    FROM T1
    					
    ```

-   Test results

    |id\(INT\)|dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |---------|--------------|--------------|
    |1|2.718281828459045|2.718281828459045|


