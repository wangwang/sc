# NULLIF {#concept_onp_t5r_dgb .concept}

This topic describes how to use the conditional function NULLIF in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
NULLIF(A,B)
			
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|INT|
|B|INT|

## Function description {#section_hks_qgp_dgb .section}

This function returns NULL if the two specified parameters have the same value, and returns the value of the first parameter if the parameters have different values.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(INT\)|var2\(INT\)|
    |-----------|-----------|
    |30|30|

-   Test statements

    ```language-sql
    SELECT NULLIF(var1,var2) as aa
    FROM T1
    ```

-   Test results

    |aa\(INT\)|
    |---------|
    |null|


