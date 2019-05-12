# IS\_DIGIT {#concept_x4q_j5r_dgb .concept}

This topic describes how to use the conditional function IS\_DIGIT in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BOOLEAN IS_DIGIT(VARCHAR str)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|str|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function checks whether the specified string contains only digits. If yes, the return value is true. If not, the return value is false. The return value is of the BOOLEAN type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |e\(VARCHAR\)|f\(VARCHAR\)|g\(VARCHAR\)|
    |------------|------------|------------|
    |3|asd|null|

-   Test statements

    ```language-sql
    SELECT 
    IS_DIGIT(e) as boo1,
    IS_DIGIT(f) as boo2,
    IS_DIGIT(g) as boo3
    FROM T1
    ```

-   Test results

    |boo1\(BOOLEAN\)|boo2\(BOOLEAN\)|boo3\(BOOLEAN\)|
    |---------------|---------------|---------------|
    |true|false|false|


