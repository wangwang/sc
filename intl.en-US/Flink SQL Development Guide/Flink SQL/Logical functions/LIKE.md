# LIKE {#concept_62829_zh .concept}

This topic describes how to use the logical operation function LIKE of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
A LIKE B

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|VARCHAR|
|B|VARCHAR|

## Function description {#section_cl2_v2w_cgb .section}

TRUE is returned if A matches B. Otherwise, FALSE is returned.

**Note:** You can use the percent sign `(%)` as a wildcard.

## Example 1 {#section_qbd_hbp_dgb .section}

-   Test data

    |int1 \(INT\)|VARCHAR2 \(VARCHAR\)|VARCHAR3 \(VARCHAR\)|
    |------------|--------------------|--------------------|
    |90|ss97|97ss|
    |99|ss10|7ho7|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE VARCHAR2 LIKE 'ss%';
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |90|
    |99|


## Example 2 {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|VARCHAR2 \(VARCHAR\)|VARCHAR3 \(VARCHAR\)|
    |------------|--------------------|--------------------|
    |90|ss97|97ss|
    |99|ss10|7ho7|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE VARCHAR3 LIKE '%ho%';
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |99|


