# INSERT INTO statement {#concept_62509_zh .concept}

This topic describes the method and constraints for using an INSERT INTO statement in Realtime Compute.

## Syntax {#section_wb3_r14_cgb .section}

```language-sql
INSERT INTO tableName
      [ (columnName[ , columnName]*) ]
          queryStatement;

```

## Examples {#section_kdc_db4_cgb .section}

```language-sql
INSERT INTO LargeOrders
SELECT * FROM Orders WHERE units > 1000;

```

```language-sql
INSERT INTO Orders(z, v)
SELECT c,d FROM OO;
```

**Note:** 

-   A single Realtime Compute job allows one SQL job to contain multiple DML operations, data sources, data destinations, and dimension tables. For example, a job file can contain two paragraphs of SQL statements for independent businesses, which will write data to different data destinations.
-   Realtime Compute does not allow you to use a separate SELECT statement for query. A SELECT statement must be used together with a CREATE VIEW statement or be contained in an INSERT INTO statement.
-   An INSERT INTO statement supports updating information in an existing record. For example, you can insert a key value into an RDS table. If this key value exists, it will be updated. If it does not exist, a new key value will be inserted.

## Operation constraints {#section_hjn_db4_cgb .section}

|Table type|Operation constraint|
|----------|--------------------|
|Source table|Can only be referenced in a FROM statement and does not support INSERT.|
|Dimension table|Can only be referenced in a JOIN statement and does not support INSERT.|
|Result table|Supports only INSERT.|
|View|Can only be referenced in a FROM statement.|

