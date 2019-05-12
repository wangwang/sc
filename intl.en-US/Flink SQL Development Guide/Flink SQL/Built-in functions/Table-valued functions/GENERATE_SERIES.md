# GENERATE\_SERIES {#concept_ljm_bvr_dgb .concept}

This topic describes how to use the table-valued function GENERATE\_SERIES in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
GENERATE_SERIES(INT from, INT to)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|from|The lower bound of a consecutive series of values \(including the lower bound\) to be generated. This parameter is of the INT type.|
|to|The upper bound of a consecutive series of values \(excluding the upper bound\) to be generated. This parameter is of the INT type.|

## Function description {#section_hks_qgp_dgb .section}

This function generates a consecutive series of values from the lower bound to the upper bound minus one.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |s\(INT\)|e\(INT\)|
    |--------|--------|
    |1|3|
    |-2|1|

-   Test statements

    ```language-sql
    SELECT s, e, v 
    FROM T1, lateral table(GENERATE_SERIES(s, e)) 
    as T(v)
    ```

-   Test results

    |s\(INT\)|e\(INT\)|v\(INT\)|
    |--------|--------|--------|
    |1|3|1|
    |1|3|2|
    |-2|1|-2|
    |-2|1|-1|
    |-2|1|-0|


