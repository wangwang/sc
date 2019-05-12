# BITAND {#concept_e1f_3yp_dgb .concept}

This topic describes how to use the mathematical function BITAND in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
INT BITAND(INT number1, INT number2)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|number1|INT|
|number2|INT|

## Function description {#section_hks_qgp_dgb .section}

This function performs a bitwise AND operation on the specified values. The input and output parameters are both of the INT type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(INT\)|b\(INT\)|
    |--------|--------|
    |2|3|

-   Test statements

    ```
    SELECT BITAND(a, b) as intt
    FROM T1
    
    ```

-   Test results

    |intt\(INT\)|
    |-----------|
    |2|


