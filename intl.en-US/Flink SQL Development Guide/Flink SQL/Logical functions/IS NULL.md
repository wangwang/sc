# IS NULL {#concept_62824_zh .concept}

This topic describes how to use the logical operation function IS NULL of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
value IS NULL

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|value|Any data type|

## Function description {#section_cl2_v2w_cgb .section}

If the value is `NULL`, `TRUE` is returned. Otherwise, `FALSE` is returned.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(VARCHAR\)|
    |------------|----------------|
    |97|NULL|
    |9|www|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int2 IS NULL;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |97|


