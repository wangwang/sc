# Result table overview {#concept_62524_zh .concept}

Realtime Compute uses the `CREATE TABLE` statement to define the format of the output data and to define how data is written to the destination data storage system.

Data can be written to the destination data storage system in two modes: append and update.

-   Append: If the output data is stored in a log system, a message system, or an RDS database with the primary key undefined, the output data is written to the data storage system in append mode. In this case, the original data in the data storage system is not modified.
-   Update: If the output data is stored in a database with the primary key declared, such as an RDS or HBase database with a primary key, the output data is written in the following two ways:
    -   If a data record queried based on the primary key does not exist in the destination database, the data record is inserted into the database.
    -   If a data record queried based on the primary key exists in the database, the data record is updated based on the primary key.

## Syntax {#section_mhh_zm2_cgb .section}

```language-sql
CREATE TABLE tableName
    (columnName dataType [, columnName dataType ]*)
    [ WITH (propertyName=propertyValue [, propertyName=propertyValue ]*) ];
				
```

## Examples {#section_aqn_pn2_cgb .section}

```language-sql
create table rds_output(
id int,
len int,
content VARCHAR,
primary key(id)
) with (
type='rds',
url='<yourDatabaseURL>',
tableName='<yourTableName>',
userName='<yourDatabaseUserName>',
password='<yourDatabasePassword>'
);
```

