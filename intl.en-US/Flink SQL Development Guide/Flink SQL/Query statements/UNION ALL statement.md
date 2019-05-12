# UNION ALL statement {#concept_62507_zh .concept}

A UNION ALL statement is used to combine two data streams. The fields of the two data streams must be the same in terms of the field type and sequence.

## Syntax {#section_sgg_czs_cgb .section}

```language-sql
select_statement
UNION ALL
select_statement;

```

**Note:** Realtime Compute also supports the `UNION` function. `UNION ALL` allows duplicate values, whereas `UNION` does not. At the underlying layer of Realtime Compute, `UNION` is implemented as a combination of `UNION ALL` and `DISTINCT`. Due to its low execution efficiency, we recommend that you do not use `UNION`.

## Examples {#section_qgk_hzs_cgb .section}

-   Test data

    test\_source\_union1:

    |a \(VARCHAR\)|b \(BIGINT\)|c \(BIGINT\)|
    |-------------|------------|------------|
    |test1|1|10|

    test\_source\_union2:

    |a \(VARCHAR\)|b \(BIGINT\)|c \(BIGINT\)|
    |-------------|------------|------------|
    |test1|1|10|
    |test2|2|20|

    test\_source\_union3:

    |a \(VARCHAR\)|b \(BIGINT\)|c \(BIGINT\)|
    |-------------|------------|------------|
    |test1|1|10|
    |test2|2|20|
    |test1|1|10|

-   Test statements

    ```language-SQL
    SELECT
        a,
        sum(b),
        sum(c)
    FROM 
        (SELECT * from test_source_union1
        UNION ALL
        SELECT * from test_source_union2
        UNION ALL
        SELECT * from test_source_union3
        )t
     GROUP BY a;
    
    ```

-   Test result

    |d \(VARCHAR\)|e \(BIGINT\)|f \(BIGINT\)|
    |-------------|------------|------------|
    |test1|1|10|
    |test2|2|20|
    |test1|2|20|
    |test1|3|30|
    |test2|4|40|
    |test1|4|40|


