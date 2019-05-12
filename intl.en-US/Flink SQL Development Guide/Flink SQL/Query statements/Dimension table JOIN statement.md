# Dimension table JOIN statement {#concept_62506_zh .concept}

A dimension table is constantly changing. Therefore, when joining a record to a dimension table, you must specify the time the record is associated with the dimension table snapshot. Currently, a record can be associated with the dimension table snapshot taken only at the current moment. \(In the future, we will allow a record to be associated with the dimension table snapshot taken at the time specified by rowtime in the left table.\)

## Dimension table JOIN syntax {#section_syw_j1p_cgb .section}

```language-sql
SELECT column-names
FROM table1  [AS <alias1>]
[LEFT] JOIN table2 FOR SYSTEM_TIME AS OF PROCTIME() [AS <alias2>]
ON table1.column-name1 = table2.key-name1

```

For example, the following SQL statement joins an event stream to a whitelist dimension table:

```language-sql
SELECT e.*, w. *
FROM event AS e
JOIN white_list FOR SYSTEM_TIME AS OF PROCTIME() AS w
ON e.id = w.id

```

**Note:** 

-   Dimension tables support `INNER JOIN` and `LEFT JOIN`, and do not support `RIGHT JOIN` or `FULL JOIN`.
-   You must append `FOR SYSTEM_TIME AS OF PROCTIME()` to the end of the dimension table. Then, the data in the dimension table that can be viewed at the current moment is joined.
-   The JOIN operation is performed only in processing time. Therefore, even if data in the dimension table is added, updated, or deleted, the associated data is not revoked or changed.
-   The ON condition must contain an equivalent condition for the primary key of the dimension table \(and must be the consistent with the definition of the table that is actually referenced\). In addition to the required equivalent condition, the ON condition can contain other equivalent conditions.
-   Two dimension tables cannot be joined.

## Example {#section_jrp_m1p_cgb .section}

-   Test data

    nameinfo:

    |id \(BIGINT\)|name \(VARCHAR\)|age \(BIGINT\)|
    |-------------|----------------|--------------|
    |1|lilei|22|
    |2|hanmeimei|20|
    |3|libai|28|

    phoneNumber:

    |name \(VARCHAR\)|phoneNumber \(BIGINT\)|
    |----------------|----------------------|
    |dufu|18867889855|
    |baijuyi|18867889856|
    |libai|18867889857|
    |lilei|18867889858|

-   Test statements

    ```language-sql
    CREATE TABLE datahub_input1 (
    id            BIGINT,
    name        VARCHAR,
    age           BIGINT
    ) WITH (
    type='datahub'
    );
    
    create table phoneNumber(
    name VARCHAR,
    phoneNumber bigint,
    primary key(name),
    PERIOD FOR SYSTEM_TIME
    )with(
    type='rds'
    );
    
    CREATE table result_infor(
    id bigint,
    phoneNumber bigint,
    name VARCHAR
    )with(
    type='rds'
    );
    
    INSERT INTO result_infor
    SELECT
    t.id,
    w.phoneNumber,
    t.name
    FROM datahub_input1 as t
    JOIN phoneNumber FOR SYSTEM_TIME AS OF PROCTIME() as w
    ON t.name = w.name;
    
    ```

-   Test result

    |id \(BIGINT\)|phoneNumber \(BIGINT\)|name \(VARCHAR\)|
    |-------------|----------------------|----------------|
    |1|18867889858|lilei|
    |3|18867889857|libai|


