# AND {#concept_pxr_4gw_cgb .concept}

This topic describes how to use the logical operation function AND of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
 A AND B

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|BOOLEAN|
|B|BOOLEAN|

## Function description {#section_cl2_v2w_cgb .section}

TRUE is returned if both A and B are TRUE. Otherwise, FALSE is returned.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|int3 \(INT\)|
    |------------|------------|------------|
    |255|97|65|

-   Test statement

    ```
    SELECT int2 as aa
    FROM T1
    WHERE int1=255 AND int3=65;
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |97|


