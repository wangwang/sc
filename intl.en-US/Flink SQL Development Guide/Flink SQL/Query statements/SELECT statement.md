# SELECT statement {#concept_62501_zh .concept}

A SELECT statement selects data from tables.

## Syntax {#section_ccz_zj4_cgb .section}

```language-sql
SELECT [ DISTINCT ]
{ * | projectItem [, projectItem ]* }
FROM tableExpression;
			
```

## Test data {#section_imd_ck4_cgb .section}

|a \(VARCHAR\)|b \(INT\)|c \(DATE\)|
|-------------|---------|----------|
|a1|211|1990-02-20|
|b1|120|2018-05-12|
|c1|89|2010-06-14|
|a1|46|2016-04-05|

## Example 1 {#section_emt_ck4_cgb .section}

-   Test statement

    ```language-sql
    SELECT * FROM Table name;
    ```

-   Test result

    |a \(VARCHAR\)|b \(INT\)|c \(DATE\)|
    |-------------|---------|----------|
    |a1|211|1990-02-20|
    |b1|120|2018-05-12|
    |c1|89|2010-06-14|
    |a1|46|2016-04-05|


## Example 2 {#section_qgc_bl4_cgb .section}

-   Test statement

    ```language-sql
    SELECT a, c AS d FROM Table name;
    ```

-   Test result

    |a \(VARCHAR\)|d \(DATE\)|
    |-------------|----------|
    |a1|1990-02-20|
    |b1|2018-05-12|
    |c1|2010-06-14|
    |a1|2016-04-05|


## Example 3 {#section_axp_bl4_cgb .section}

-   Test statement

    ```language-sql
    SELECT DISTINCT a FROM Table name;
    ```

-   Test result

    |a \(VARCHAR\)|
    |-------------|
    |a1|
    |b1|
    |c1|


## Subquery {#section_fk5_yk4_cgb .section}

Generally, a SELECT statement reads data from several tables, such as `SELECT column_1, column_2 … FROM table_name`. A SELECT statement can also read data from another SELECT statement, which is called a subquery.

**Note:** A subquery must use aliases, as shown in the following example.

-   SQL statement example:

    ```language-sql
    INSERT INTO result_table
    SELECT * FROM
                   (SELECT   t.a,
                             sum(t.b) AS sum_b
                    FROM     t1 t
                    GROUP BY t.a
                   ) t1 
    WHERE  t1.sum_b > 100;
    ```

-   Example result

    |a \(VARCHAR\)|b \(INT\)|
    |-------------|---------|
    |a1|211|
    |b1|120|
    |a1|257|


