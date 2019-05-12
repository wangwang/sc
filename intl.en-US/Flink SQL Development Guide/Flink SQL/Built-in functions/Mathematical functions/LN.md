# LN {#concept_frd_lgq_dgb .concept}

This topic describes how to use the mathematical function LN in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
DOUBLE ln(DOUBLE number)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|number|DOUBLE **Note:** If the input parameter is of the VARCHAR or BIGINT type, it is implicitly converted to the DOUBLE type for computation.

 |

## Function description {#section_hks_qgp_dgb .section}

This function returns the natural logarithm of the specified number. The return value is a logarithm of the DOUBLE type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |ID\(INT\)|X\(DOUBLE\)|
    |---------|-----------|
    |1|100.0|
    |2|8.0|

-   Test statements

    ```
    SELECT id, ln(x) as dou1, ln(e()) as dou2
    FROM T1
    ```

-   Test results

    |ID\(INT\)|dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |---------|--------------|--------------|
    |1|4.605170185988092|1.0|
    |2|2.0794415416798357|1.0|


