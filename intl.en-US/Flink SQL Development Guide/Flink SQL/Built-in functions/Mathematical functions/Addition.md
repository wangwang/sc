# Addition {#concept_62753_zh .concept}

This topic describes how to use the mathematical function addition in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
A + B
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|INT|
|B|INT|

## Function description {#section_hks_qgp_dgb .section}

This function returns the result of A plus B.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |int1\(INT\)|int2\(INT\)|int3\(INT\)|
    |-----------|-----------|-----------|
    |10|20|30|

-   Test statements

    ```
    SELECT int1+int2+int3 as aa
    FROM T1
    
    ```

-   Test results

    |aa\(int\)|
    |---------|
    |60|


