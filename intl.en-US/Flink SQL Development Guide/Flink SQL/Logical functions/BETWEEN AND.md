# BETWEEN AND {#concept_s4m_d3w_cgb .concept}

This topic describes how to use the logical operation function BETWEEN AND of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
 A BETWEEN AND B
			
```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|
|B|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|
|C|DOUBLE, BIGINT, INT, VARCHAR, DATE, TIMESTAMP, or TIME|

## Function description {#section_cl2_v2w_cgb .section}

This function selects a value within a data range defined by two other values.

## Example 1 {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|int3 \(INT\)|
    |------------|------------|------------|
    |90|80|100|
    |11|10|7|

-   Test statement

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int1 BETWEEN int2 AND int3;
    					
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |90|


## Example 2 {#section_wvp_p3w_cgb .section}

-   Test data

    |var1 \(VARCHAR\)|var2 \(VARCHAR\)|var3 \(VARCHAR\)|
    |----------------|----------------|----------------|
    |b|a|c|

-   Test statement

    ```
    SELECT var1 as aa
    FROM T1
    WHERE var1 BETWEEN var2 AND var3;
    					
    ```

-   Test result

    |aa \(VARCHAR\)|
    |--------------|
    |b|


## Example 3 {#section_chq_53w_cgb .section}

-   Test data

    |TIMESTAMP1 \(TIMESTAMP\)|TIMESTAMP2 \(TIMESTAMP\)|TIMESTAMP3 \(TIMESTAMP\)|
    |------------------------|------------------------|------------------------|
    |1969-07-20 20:17:30|1969-07-20 20:17:20|1969-07-20 20:17:45|

-   Test statement

    ```
    SELECT TIMESTAMP1 as aa
    FROM T1
    WHERE TIMESTAMP1 BETWEEN TIMESTAMP2 AND TIMESTAMP3;
    					
    ```

-   Test result

    |aa \(TIMESTAMP\)|
    |----------------|
    |1969-07-20 20:17:30|


