# Create a data view {#concept_62534_zh .concept}

You can create a data view in Realtime Compute to simplify the development process.

## Syntax {#section_alb_qk5_cgb .section}

If the computational logic is complex, you can create a data view by defining it in Realtime Compute to simplify the development process.

**Note:** The data view only helps describe the computational logic and does not lead to physical storage of data.

```language-sql
CREATE VIEW viewName[ (columnName[ , columnName]*
) ] AS queryStatement;

```

## Example 1 {#section_j1s_zk5_cgb .section}

```language-sql
CREATE VIEW LargeOrders (r, t, c, u) AS
SELECT
    rowtime,
    productId,
    c,
    units
FROM
    orders;
INSERT INTO
    rds_output
SELECT
    r,
    t,
    c,
    u
FROM
    LargeOrders;

```

## Example 2 {#section_zqj_1l5_cgb .section}

-   Test data

    |a\(VARCHAR\)|b \(BIGINT\)|c \(TIMESTAMP\)|
    |------------|------------|---------------|
    |test1|1|1506823820000|
    |test2|1|1506823850000|
    |test1|1|1506823810000|
    |test2|1|1506823840000|
    |test2|1|1506823870000|
    |test1|1|1506823830000|
    |test2|1|1506823860000|

-   Test statements

    ```language-SQL
    CREATE TABLE datahub_stream (
       a VARCHAR,
       b BIGINT,
       c TIMESTAMP,
       d AS PROCTIME()
    ) WITH (
      TYPE='datahub',
      ...
    );
    CREATE TABLE rds_output (
       a VARCHAR,
       b TIMESTAMP, 
       cnt BIGINT,
       PRIMARY KEY(a)
    )WITH(
      TYPE = 'rds',
      ...
    );
    CREATE VIEW rds_view AS
    SELECT a, 
       CAST(
          HOP_START(d, INTERVAL '5' SECOND, INTERVAL '30' SECOND) AS TIMESTAMP
       ) AS cc, 
       SUM(b) AS cnt
    FROM 
       datahub_stream 
    GROUP BY
        HOP(d, INTERVAL '5' SECOND, INTERVAL '30' SECOND),a;
    INSERT INTO 
       rds_output
    SELECT
       a,
       cc,
       cnt
    FROM 
       rds_view
    WHERE clause 
       cnt=4
    
    ```

-   Test results

    |a\(VARCHAR\)|b \(TIMESTAMP\)|cnt \(BIGINT\)|
    |------------|---------------|--------------|
    |test2|`2017-11-06 16:54:10`|4|


