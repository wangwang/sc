# IS NOT NULL {#concept_62825_zh .concept}

This topic describes how to use the logical operation function IS NOT NULL of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
value IS NOT NULL

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|value|Any data type|

## Function description {#section_cl2_v2w_cgb .section}

If the value is `NULL`, `FALSE` is returned. Otherwise, `TRUE` is returned.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(VARCHAR\)|
    |------------|----------------|
    |97|NULL|
    |9|ww123|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int2 IS NOT NULL;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |9|


