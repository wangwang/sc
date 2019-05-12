# Subtraction {#concept_62757_zh .concept}

This topic describes how to use the mathematical function subtraction in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
A - B
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|INT|
|B|INT|

## Function description {#section_hks_qgp_dgb .section}

This function returns the result of A minus B.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |int1\(INT\)|int2\(INT\)|int3\(INT\)|
    |-----------|-----------|-----------|
    |10|10|30|

-   Test statements

    ```
    SELECT int3 - int2 - int1 as aa
    FROM T1
    
    ```

-   Test results

    |aa\(int\)|
    |---------|
    |10|


