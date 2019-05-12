# NOT {#concept_62811_zh .concept}

This topic describes how to use the logical operation function NOT of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
NOT A

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|BOOLEAN|

## Function description {#section_cl2_v2w_cgb .section}

If A is `TRUE`, `FALSE` is returned. If A is `FALSE`, `TRUE` is returned.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |int2 \(INT\)|int3 \(INT\)|
    |------------|------------|
    |97|65|

-   Test statement

    ```
    SELECT int2 as aa
    FROM T1
    WHERE NOT int3=62;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |97|


