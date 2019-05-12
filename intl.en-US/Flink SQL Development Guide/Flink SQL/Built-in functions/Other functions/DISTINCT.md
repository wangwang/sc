# DISTINCT {#concept_mz3_bzx_ngb .concept}

This topic describes how to use the DISTINCT function in Realtime Compute. The DISTINCT function removes duplicate records from the query result of your `SELECT` statement and returns only unique records.

## DISTINCT syntax {#section_pmr_p1y_ngb .section}

```sql
SELECT DISTINCT expressions 
FROM tables
 ...
```

-   `DISTINCT` must be placed before expressions.
-   `expressions` can be one or more expressions, specific columns, or any other valid expressions such as functions.

## DISTINCT syntax examples {#section_dcr_1by_ngb .section}

-   Test statements

    The following provides an example of `DISTINCT` in Flink SQL:

    ```sql
    CREATE TABLE distinct_tab_source(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
       type='random'
    );
    CREATE TABLE distinct_tab_sink(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
        type = 'print'
    );
    INSERT INTO distinct_tab_sink 
    SELECT DISTINCT FirstName, LastName // Remove duplicate records based on the FirstName and LastName columns.
    FROM distinct_tab_source;
    ```

-   Test data

    |FirstName|LastName|
    |---------|--------|
    |SUNS|HENGRAN|
    |SUN|JINCHENG|
    |SUN|SHENGRAN|
    |SUN|SHENGRAN|

-   Test results

    |FirstName|LastName|
    |---------|--------|
    |SUNS|HENGRAN|
    |SUN|JINCHENG|
    |SUN|SHENGRAN|

    **Note:** 

    -   The test data contains four records.`DISTINCT FirstName, LastName` removes one duplicate record `SUN,SHENGRAN` and returns three unique records.
    -   The `SUNS,HENGRAN` and `SUN,SHENGRAN` records are retained. This indicates that `DISTINCT FirstName, LastName` processes the FirstName and LastName columns separately, instead of concatenating them for deduplication.
-   Alternative for DISTINCT

    `GROUP BY` in SQL statements also provides a deduplication function similar to that of `DISTINCT`. The `GROUP BY` syntax is as follows:

    ```sql
    SELECT expressions 
    FROM tables
    GROUP BY expressions 
    ;
    ```

    The following writes an SQL multi-insert query to reach the equivalent effect as the DISTINCT function:

    ```sql
    CREATE TABLE distinct_tab_source(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
       type='random'
    );
    CREATE TABLE distinct_tab_sink(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
        type = 'print'
    );
    CREATE TABLE distinct_tab_sink2(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
        type = 'print'
    );
    INSERT INTO distinct_tab_sink 
        SELECT DISTINCT FirstName, LastName // Remove duplicate records based on the FirstName and LastName columns.
            FROM distinct_tab_source;
    INSERT INTO distinct_tab_sink2 
        SELECT FirstName, LastName
            FROM distinct_tab_source
             GROUP BY FirstName, LastName; // Remove duplicate records based on the FirstName and LastName columns.
    							
    ```

    Given the same test data, the output of GROUP BY FirstName, LastName; is the same as that of the DISTINCT function in the preceding example. This indicates that the GROUP BY statement has the same semantics as the DISTINCT function.


## Use of DISTINCT in the aggregate function COUNT {#section_wqt_mhy_ngb .section}

The use of `DISTINCT` enables `COUNT` to count the number of records after deduplication.

```sql
COUNT(DISTINCT expression)
```

**Note:** Currently, only a single expression is supported.``

## COUNT DISTINCT syntax examples {#section_ahp_nvy_ngb .section}

-   Test statements

    ```sql
    CREATE TABLE distinct_tab_source(
        FirstName VARCHAR,
        LastName VARCHAR
    )WITH(
       type='random'
    );
    CREATE TABLE distinct_tab_sink(
        cnt BIGINT,
        distinct_cnt BIGINT
    )WITH(
        type = 'print'
    );
    INSERT INTO distinct_tab_sink 
        SELECT 
          COUNT(FirstName), // Do not remove duplicate records.
          COUNT(DISTINCT FirstName) // Remove duplicate records based on the FirstName column.
        FROM distinct_tab_source;
    						
    ```

-   Test data

    |FirstName|LastName|
    |---------|--------|
    |SUNS|HENGRAN|
    |SUN|JINCHENG|
    |SUN|SHENGRAN|
    |SUN|SHENGRAN|

-   Test results

    |cnt|distinct\_cnt|
    |---|-------------|
    |1|1|
    |2|2|
    |3|2|
    |4|2|


