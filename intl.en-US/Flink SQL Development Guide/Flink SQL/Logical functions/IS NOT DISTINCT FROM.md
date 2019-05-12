# IS NOT DISTINCT FROM {#concept_85827_zh .concept}

This topic describes how to use the logical operation function IS NOT DISTINCT FROM of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
A IS NOT DISTINCT FROM B

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|Any data type|
|B|Any data type|

## Function description {#section_cl2_v2w_cgb .section}

-   `FALSE` is returned if the data types or values of A and B are different.
-   `TRUE` is returned if the data types and values of A and B are the same.
-   If both A and B are null, TRUE is returned even when their data types are different.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |A \(INT\)|B \(VARCHAR\)|
    |---------|-------------|
    |97|97|
    |null|sss|
    |null|null|

-   Test statement

    ```
    SELECT 
    A IS NOT DISTINCT FROM B as `result`
    FROM T1
    
    ```

-   Test result

    |result \(BOOLEAN\)|
    |------------------|
    |FALSE|
    |FALSE|
    |TRUE|


