# CARDINALITY {#concept_ywb_fdq_dgb .concept}

This topic describes how to use the mathematical function CARDINALITY in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
CARDINALITY(str)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|number1|Array|

## Function description {#section_hks_qgp_dgb .section}

This function returns the number of elements in an array.

## Examples {#section_iks_qgp_dgb .section}

-   Test statements

    ```
    SELECT cardinality(array[1,2,3]) AS `result`
    FROM T1
    
    ```

-   Test results

    |result\(INT\)|
    |-------------|
    |3|


