# IS NOT UNKNOWN {#concept_62816_zh .concept}

This topic describes how to use the logical operation function IS NOT UNKNOWN of Realtime Compute.

## Syntax {#section_mnm_4dw_cgb .section}

```language-sql
A IS NOT UNKNOWN

```

## Input parameter {#section_qvx_tdw_cgb .section}

|Name|Data type|
|----|---------|
|A|BOOLEAN|

## Function description {#section_cl2_v2w_cgb .section}

A is a logical comparison expression, such as 6 < 8.

In normal cases, when A compares two numbers, the value of A can be determined, which is either TRUE or FALSE. However, if either operand is not a number, the value of A cannot be determined. `IS NOT UNKNOWN` is used to determine whether this situation occurs. If the value of A cannot be determined \(that is, the value is neither `TRUE` nor `FALSE`\), `FALSE` is returned. If the value of A can be determined \(that is, the value is `TRUE` or `FALSE`\), `TRUE` is returned.

## Example 1 {#section_fzz_hy4_dgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|
    |------------|------------|
    |255|97|

-   Test statement

    ```
    SELECT int2 as aa
    FROM T1
    WHERE int1=25 IS NOT UNKNOWN;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |97|


## Example 2 {#section_ekm_zdw_cgb .section}

-   Test data

    |int1 \(INT\)|int2 \(INT\)|
    |------------|------------|
    |255|97|

-   Test statement

    ```
    SELECT int2 as aa
    FROM T1
    WHERE int1 < null IS NOT UNKNOWN;
    
    ```

-   Test result

    |aa \(INT\)|
    |----------|
    |null|


