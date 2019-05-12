# IS TRUE {#concept_62813_zh .concept}

This topic describes how to use the logical operation function IS TRUE of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
A IS TRUE

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|BOOLEAN|

## Function description {#section_cl2_v2w_cgb .section}

If A is TRUE, TRUE is returned. If A is FALSE, FALSE is returned.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|
    |------------|------------|
    |255|97|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int1=255 IS TRUE;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |97|


