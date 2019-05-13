# NOT BETWEEN AND {#concept_62828_zh .concept}

This topic describes how to use the logical operation function NOT BETWEEN AND of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
A NOT BETWEEN B AND C

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|
|B|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|
|C|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|

## Function description {#section_cl2_v2w_cgb .section}

This function selects a value not within a data range defined by two other values.``

## Example 1 {#section_qbd_hbp_dgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|int3 \(INT\)|
    |------------|------------|------------|
    |90|97|80|
    |11|10|7|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int1 NOT BETWEEN int2 AND int3;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |11|


## Example 2 {#section_ekm_zdw_cgb .section}

-   Test data

    |var1 \(VARCHAR\)|var2 \(VARCHAR\)|var3 \(VARCHAR\)|
    |----------------|----------------|----------------|
    |d|a|c|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE var1 NOT BETWEEN var2 AND var3;
    
    ```

-   Test result

    |aa \(VARCHAR\)|
    |--------------|
    |d|


## Example 3 {#section_d31_wcp_dgb .section}

-   Test data

    |TIMESTAMP1 \(TIMESTAMP\)|TIMESTAMP2 \(TIMESTAMP\)|TIMESTAMP3 \(TIMESTAMP\)|
    |------------------------|------------------------|------------------------|
    |1969-07-20 20:17:30|1969-07-20 20:17:40|1969-07-20 20:17:45|

-   Test statement

    ```
    SELECT TIMESTAMP1 as aa
    FROM T1
    WHERE TIMESTAMP1 NOT BETWEEN TIMESTAMP2 AND TIMESTAMP3;
    
    ```

-   Test result

    |aa \(TIMESTAMP\)|
    |----------------|
    |1969-07-20 20:17:30|


