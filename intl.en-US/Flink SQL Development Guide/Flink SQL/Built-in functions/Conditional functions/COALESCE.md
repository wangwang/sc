# COALESCE {#concept_j1g_rsr_dgb .concept}

This topic describes how to use the conditional function COALESCE in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
COALESCE(A,B,...)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|A|Any data type|
|B|Any data type|

**Note:** All values must be of the same type or be NULL. Otherwise, an exception occurs.

## Function description {#section_hks_qgp_dgb .section}

This function returns the first non-NULL value in the specified list. The return value is of the same type as the input parameter values. If all values in the list are NULL, the return value is NULL.

**Note:** The list must contain at least one parameter. Otherwise, an exception occurs.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |var1\(VARCHAR\)|var2\(VARCHAR\)|
    |---------------|---------------|
    |null|30|

-   Test statements

    ```language-sql
    SELECT COALESCE(var1,var2) as aa
    FROM T1
    ```

-   Test results

    |aa\(VARCHAR\)|
    |-------------|
    |30|


