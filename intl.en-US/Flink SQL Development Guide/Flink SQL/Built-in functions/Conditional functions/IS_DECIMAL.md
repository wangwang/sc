# IS\_DECIMAL {#concept_zhx_ztr_dgb .concept}

This topic describes how to use the conditional function IS\_DECIMAL in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BOOLEAN IS_DECIMAL(VARCHAR str)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|str|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function checks whether the specified string can be converted to a decimal value. If yes, the return value is true. If not, the return value is false.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(VARCHAR\)|b\(VARCHAR\)|c\(VARCHAR\)|d\(VARCHAR\)|e\(VARCHAR\)|f\(VARCHAR\)|g\(VARCHAR\)|
    |------------|------------|------------|------------|------------|------------|------------|
    |1|123|2|11.4445|3|asd|null|

-   Test statements

    ```language-sql
    SELECT 
    IS_DECIMAL(a) as boo1,
    IS_DECIMAL(b) as boo2,
    IS_DECIMAL(c) as boo3,
    IS_DECIMAL(d) as boo4,
    IS_DECIMAL(e) as boo5,
    IS_DECIMAL(f) as boo6,
    IS_DECIMAL(g) as boo7
    FROM T1
    ```

-   Test results

    |boo1\(BOOLEAN\)|boo2\(BOOLEAN\)|boo3\(BOOLEAN\)|boo4\(BOOLEAN\)|boo5\(BOOLEAN\)|boo6\(BOOLEAN\)|boo7\(BOOLEAN\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|---------------|
    |true|true|true|true|true|false|false|


