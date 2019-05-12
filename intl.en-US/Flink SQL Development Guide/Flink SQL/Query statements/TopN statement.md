# TopN statement {#concept_62508_zh .concept}

A TopN statement is used to compute the largest or smallest N data records of an indicator in real-time data. Flink SQL can use an `OVER` window function to flexibly implement TopN computing.

## Syntax {#section_pyl_tdt_cgb .section}

```language-sql
SELECT *
FROM (
  SELECT *,
    ROW_NUMBER() OVER ([PARTITION BY col1[, col2..]]
    ORDER BY col1 [asc|desc][, col2 [asc|desc]...]) AS rownum
  FROM table_name)
WHERE rownum <= N [AND conditions]

```

**Note:** 

-    `ROW_NUMBER()`: specifies an `OVER` window function for computing the number of a row. The value starts from 1.
-    `PARTITION BY col1[, col2..]`: specifies the columns used for partitioning. This parameter is optional.
-    `ORDER BY col1 [asc|desc][, col2 [asc|desc]...]`: specifies the columns used for sorting and the sorting order of each column.

As shown in the preceding syntax, TopN requires two levels of queries.

-   In the subquery, the `ROW_NUMBER()` window function is used to sort data by the specified columns and mark the data with rankings.
-   In the outer query, only the first N data records in a ranking list are obtained. For example, if N = 10, the first 10 data records are obtained.

During execution, Flink SQL sorts an input data stream based on the sort key. If the first N data records in a partition are changed, the updated data is sent downstream as an update steam.

**Note:** Therefore, if you want to export the TopN data to external storage, the target result table must contain primary keys.

Constraints of the WHERE condition

To enable Flink SQL to identify a TopN query, use the `rownum <= N` format in the outer loop to specify the first N data records. Do not place `rownum` in an expression such as `rownum - 5 <= N` for that purpose. The WHERE condition can also include other conditions that are joined with `AND`.

## Example 1 {#section_k54_xdt_cgb .section}

In the following example, the number of times each keyword is queried is computed by hour and city. Then, the top 100 most-queried keywords are exported. The hour, city, and ranking columns in the output table together identify a unique record. Therefore, the three columns must be declared as composite keys. \(The keys must also be set in the external storage.\)

```language-sql
CREATE TABLE rds_output (
  rownum BIGINT,
  start_time BIGINT,
  city VARCHAR,
  keyword VARCHAR,
  pv BIGINT,
  PRIMARY KEY (rownum, start_time, city)
) WITH (
  type = 'rds',
  ...
)

INSERT INTO rds_output
SELECT rownum, start_time, city, keyword, pv
FROM (
  SELECT *,
     ROW_NUMBER() OVER (PARTITION BY start_time, city ORDER BY pv desc) AS rownum
  FROM (
        SELECT SUBSTRING(time_str,1,12) AS start_time, 
            keyword,
            count(1) AS pv,
            city
        FROM tmp_search
        GROUP BY SUBSTRING(time_str,1,12), keyword, city
    ) a 
) 
WHERE rownum <= 100

```

## Example 2 {#section_y11_zdt_cgb .section}

-   Test data

    |ip \(VARCHAR\)|time \(VARCHAR\)|
    |--------------|----------------|
    |`192.168.1.1`|100000000|
    |`192.168.1.2`|100000000|
    |`192.168.1.2`|100000000|
    |`192.168.1.3`|100030000|
    |`192.168.1.3`|100000000|
    |`192.168.1.3`|100000000|

-   Test statements

    ```language-SQL
    CREATE TABLE source_table (
      IP VARCHAR,
      `TIME` VARCHAR 
    )WITH(
      type='datahub',
      endPoint='xxxxxxx',
      project='xxxxxxx',
      topic='xxxxxxx',
      accessId='xxxxxxx',
      accessKey='xxxxxxx'
    );
    
    CREATE TABLE result_table (
      rownum BIGINT,
      start_time VARCHAR,
      IP VARCHAR,
      cc BIGINT,
      PRIMARY KEY (start_time, IP)
    ) WITH (
      type = 'rds',
      url='xxxxxxx',
      tableName='blink_rds_test',
      userName='xxxxxxx',
      password='xxxxxxx'
    );
    INSERT INTO result_table
    SELECT rownum,start_time,IP,cc
    FROM (
      SELECT *,
         ROW_NUMBER() OVER (PARTITION BY start_time ORDER BY cc DESC) AS rownum
      FROM (
            SELECT SUBSTRING(`TIME`,1,2) AS start_time, -- You can specify a value based on the actual time. The data specified in this example is test data.
            COUNT(IP) AS cc,
            IP
            FROM  source_table
            GROUP BY SUBSTRING(`TIME`,1,2), IP
        )a
    ) 
    WHERE rownum <= 3 -- You can specify a value based on the number of data records you want to obtain. The data specified in this example is test data.
    
    
    
    ```

-   Test result

    |rownum \(BIGINT\)|start\_time \(VARCHAR\)|ip \(VARCHAR\)|cc \(BIGINT\)|
    |-----------------|-----------------------|--------------|-------------|
    |1|10|`192.168.1.3`|6|
    |2|10|`192.168.1.2`|4|
    |3|10|`192.168.1.1`|2|


## No ranking {#section_f3d_2ft_cgb .section}

-   No ranking solves the data bloat problem.
    -   Data bloat problem

        Based on the TopN syntax, the `rownum` field is written into a result table as one of the primary keys of the table. This may lead to data bloat. For example, if the ranking of a record is improved from the ninth to the first place after an update, the records ranked from the first to the ninth places are all changed. The changes must be updated in the result table. As a result, data bloat occurs. The update speed of the result table may decrease because an excessive amount of data is received.

    -   Method of no ranking

        To avoid data bloat, exclude `rownum` from the result table and compute `rownum` at the front-end. Generally, the amount of top N data records is not large, and the top 100 data records can be sorted quickly at the front-end. In this case, if the ranking of a record is improved from the ninth to the first place after an update, only this record needs to be delivered. This greatly improves the update speed of the result table.

-   Syntax of no ranking

    ```language-SQL
    SELECT col1, col2, col3
    FROM (
     SELECT col1, col2, col3
       ROW_NUMBER() OVER ([PARTITION BY col1[, col2..]]
       ORDER BY col1 [asc|desc][, col2 [asc|desc]...]) AS rownum
     FROM table_name)
    WHERE rownum <= N [AND conditions]
    
    
    ```

    The syntax is similar to the original TopN syntax. You only need to exclude the rownum field from the outer query.

    **Note:** If rownum is excluded, pay special attention to the definition of the primary keys of the result table. If the definition is incorrect, the TopN query result is incorrect. If rownum is excluded, the primary keys must be those in the key list at the GROUP BY node before the TopN statement.

-   Example of no ranking

    This example is a simplified case from a customer in the video industry. Heavy traffic is generated when each video is distributed. Based on the video traffic, you can identify the most popular videos. The following example identifies the top 5 videos that consume the most traffic per minute.

    -   Test statements

        ```
        -- Read the original data storage table from Log Service.
        CREATE TABLE sls_cdnlog_stream (
        vid VARCHAR, -- video id
        rowtime TIMESTAMP, -- Identify the time when the videos are watched.
        response_size BIGINT, -- Identify the traffic for watching the videos.
        WATERMARK FOR rowtime as withOffset(rowtime, 0)
        ) WITH (
        type='sls',
        ...
        );
        
        -- Compute the consumed bandwidth by video ID in the 1-minute window.
        CREATE VIEW cdnvid_group_view AS
        SELECT vid,
        TUMBLE_START(rowtime, INTERVAL '1' MINUTE) AS start_time,
        SUM(response_size) AS rss
        FROM sls_cdnlog_stream
        GROUP BY vid, TUMBLE(rowtime, INTERVAL '1' MINUTE);
        
        -- Create the result table.
        CREATE TABLE hbase_out_cdnvidtoplog (
        vid VARCHAR,
        rss BIGINT,
        start_time VARCHAR,
           -- Do not store the rownum field in the result table.
           -- Pay special attention to the definition of the primary keys. The primary keys must be those in the key list at the GROUP BY node before the TopN statement.
        PRIMARY KEY(start_time, vid)
        ) WITH (
        type='RDS',
        ...
        );
        
        -- Identify and export the IDs of the top 5 videos that consume the most traffic per minute.
        INSERT INTO hbase_out_cdnvidtoplog
        
        -- The outer query cannot include the rownum field.
        SELECT vid, rss, start_time FROM
        (
        SELECT
        vid, start_time, rss,
        ROW_NUMBER() OVER (PARTITION BY start_time ORDER BY rss DESC) as rownum,
        FROM
        cdnvid_group_view
        )
        WHERE rownum <= 5;
        
        
        ```

    -   Test data

        |vid \(VARCHAR\)|rowtime \(Timestamp\)|response\_size \(BIGINT\)|
        |---------------|---------------------|-------------------------|
        |10000|`2017-12-18 15:00:10`|2000|
        |10000|`2017-12-18 15:00:15`|4000|
        |10000|`2017-12-18 15:00:20`|3000|
        |10001|`2017-12-18 15:00:20`|3000|
        |10002|`2017-12-18 15:00:20`|4000|
        |10003|`2017-12-18 15:00:20`|1000|
        |10004|`2017-12-18 15:00:30`|1000|
        |10005|`2017-12-18 15:00:30`|5000|
        |10006|`2017-12-18 15:00:40`|6000|
        |10007|`2017-12-18 15:00:50`|8000|

    -   Test result

        |start\_time \(VARCHAR\)|vid \(VARCHAR\)|rss \(BIGINT\)|
        |-----------------------|---------------|--------------|
        |`2017-12-18 15:00:00`|10000|9000|
        |`2017-12-18 15:00:00`|10007|8000|
        |`2017-12-18 15:00:00`|10006|6000|
        |`2017-12-18 15:00:00`|10005|5000|
        |`2017-12-18 15:00:00`|10002|4000|


