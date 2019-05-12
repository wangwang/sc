# IN {#concept_jf2_sdp_dgb .concept}

This topic describes how to use the logical operation function IN of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...)

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|value1|Constant|
|value2|Constant|

## Function description {#section_cl2_v2w_cgb .section}

This function queries records that match the input parameters.

## Example {#section_ekm_zdw_cgb .section}

-   Test data

    |id \(INT\)|LastName \(VARCHAR\)|
    |----------|--------------------|
    |1|Adams|
    |2|Bush|
    |3|Carter|

-   Test statement

    ```
    SELECT * 
    FROM T1
    WHERE LastName IN ('Adams','Carter')
    
    ```

-   Test result

    |id \(INT\)|LastName \(VARCHAR\)|
    |----------|--------------------|
    |1|Adams|
    |3|Carter|


