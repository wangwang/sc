# BITNOT {#concept_azd_ryp_dgb .concept}

This topic describes how to use the mathematical function BITNOT in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
INT BITNOT(INT number)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|number|INT|

## Function description {#section_hks_qgp_dgb .section}

This function performs a bitwise NOT operation on the specified value. The input and output parameters are both of the INT type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(INT\)|
    |--------|
    |7|

-   Test statements

    ```
    SELECT BITNOT(a) as var1
    FROM T1
    
    ```

-   Test results

    |var1\(INT\)|
    |-----------|
    |0xfff8|


