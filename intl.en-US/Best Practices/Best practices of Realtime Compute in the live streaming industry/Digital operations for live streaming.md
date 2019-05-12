# Digital operations for live streaming {#concept_65840_zh .concept}

This topic provides a use case to describe how to use Realtime Compute to implement digital operations for live streaming.

## Digital operations {#section_b22_ypm_2gb .section}

This topic focuses on digital operations. You can use Realtime Compute to monitor the operating status of streaming channels at your live streaming website in real time, such as popular videos and user viewing trends.

## Solution {#section_tfd_1qm_2gb .section}

-   Business objectives
    -   Collect statistics on the total number of users and user viewing trend at your website.
    -   Collect statistics on the total number of users and user viewing trend of a channel.
    -   Collect statistics on the top 10 popular channels, and top 10 popular channels in each category.
-   Data format

    Use the logs tracked in the client app as the raw data to collect statistics.

    The following table describes the data format of the tracked logs that the client app sends to the server.

    |Field name|Description|
    |----------|-----------|
    |ip|The IP address of the client.|
    |agent|The device type of the client.|
    |roomid|The ID of the channel.|
    |userid|The ID of the user.|
    |abytes|The audio bitrate.|
    |afcnt|The number of audio frames.|
    |adrop|The number of dropped audio frames.|
    |afts|The audio timestamp.|
    |alat|The E2E latency of audio frames.|
    |vbytes|The video bitrate.|
    |vfcnt|The number of video frames.|
    |vdrop|The number of dropped video frames.|
    |vfts|The video timestamp.|
    |vlat|The E2E latency of video frames.|
    |ublock|The number of upstream frame freezing times.|
    |dblock|The number of downstream frame freezing times.|
    |timestamp|The timestamp when a log was generated.|
    |region|The region where live streaming is performed.|

    Log Service uses semi-structured storage and displays the preceding fields in the following log format:

    ```language-json
    {
        "ip": "ip",
        "agent": "agent",
        "roomid": "123456789",
        "userid": "123456789",
        "abytes": "123456",
        "afcnt": "34",
        "adrop": "3",
        "afts": "1515922566",
        "alat": "123",
        "vbytes": "123456",
        "vfcnt": "34",
        "vdrop": "4",
        "vfts": "1515922566",
        "vlat": "123",
        "ublock": "1",
        "dblock": "2",
        "timestamp": "1515922566",
        "region": "hangzhou"
    }
    					
    ```

-   SQL statements
    -   Collect statistics on the total number of users and user viewing trend at your website.

        Use a new window every minute to collect statistics on the user viewing trend at your website. The statistical result of the last minute in the trend is the current total number of users at your website.

        ```language-sql
        CREATE VIEW view_app_total_visit_1min AS
        SELECT
            CAST(TUMBLE_START(app_ts, INTERVAL '1' MINUTE) as VARCHAR) as app_ts,
            COUNT(DISTINCT userid) as app_total_user_cnt
        FROM
            view_app_heartbeat_stream
        GROUP BY
            TUMBLE(app_ts, INTERVAL '1' MINUTE);
        							
        ```

    -   Collect statistics on the total number of users and user viewing trend of a channel.

        Similarly, use a new window every minute to collect statistics on the user viewing trend of a channel. The statistical result of the last minute in the trend is the current total number of users of the channel.

        ```language-sql
        CREATE VIEW view_app_room_visit_1min AS
        SELECT
            CAST(TUMBLE_START(app_ts, INTERVAL '1' MINUTE) as VARCHAR) as app_ts,
            roomid as room_id,
            COUNT(DISTINCT userid) as app_room_user_cnt
        FROM
            view_app_heartbeat_stream
        GROUP BY
            TUMBLE(app_ts, INTERVAL '1' MINUTE), roomid;
        							
        ```

    -   Rank the top 10 popular channels.

        Collect statistics on the top 10 popular channels and promote these channels on the homepage to increase your website traffic and clicks.

        ```language-sql
        CREATE VIEW view_app_room_visit_top10 AS
        SELECT
          app_ts,
          room_id,
          app_room_user_cnt,
          rangking
        FROM
        (
            SELECT 
                app_ts,
                room_id,
                app_room_user_cnt,
                ROW_NUMBER() OVER (PARTITION BY 1 ORDER BY app_room_user_cnt desc) AS ranking
            FROM
                view_app_room_visit_1min
        ) WHERE ranking <= 10;
        							
        ```

    -   Rank the top 10 popular channels in each category.

        To build a highly interactive user community and cover more live streaming scenarios to realize more profit, a platform operator usually establishes many diversified channels at their live streaming website to meet the requirements of different user groups. For example, Taobao Live covers multiple categories such as makeup, men's wear, autos, and fitness.

        Create an RDS dimension table dim\_category\_room to store the mappings between categories and channels.

        ```language-sql
        CREATE TABLE dim_category_room ( 
            id    BIGINT,
            category_id BIGINT,
            category_name VARCHAR,
            room_id    BIGINT
              PRIMARY KEY (room_id), 
              PERIOD FOR SYSTEM_TIME // Specify that this is a dimension table. 
         ) WITH ( 
             type= 'rds', 
             url = '<yourDatabaseURL>', // Your database URL. 
             tableName = '<yourDatabaseTableName>', // Your table name. 
             userName = '<yourDatabaseUserName>', // Your username. 
             password = '<yourDatabaseUserPassword>' // Your password. 
         );
        ```

        Join to the dim\_category\_room table based on the room ID and compute the rankings of channels in each category.

        ```language-sql
        CREATE VIEW view_app_room_visit_1min AS
        SELECT
            CAST(TUMBLE_START(app_ts, INTERVAL '1' MINUTE) as VARCHAR) as app_ts,
            roomid as room_id,
            COUNT(DISTINCT userid) as app_room_user_cnt
        FROM
            view_app_heartbeat_stream
        GROUP BY
            TUMBLE(app_ts, INTERVAL '1' MINUTE), roomid;
        
        // Join to the dim_category_room table.
        CREATE VIEW view_app_category_visit_1min AS
        SELECT 
            r.app_ts,
            r.room_id,
            d.category_id,
            d.category_name,
            r.app_room_user_cnt
        FROM
            view_app_room_visit_1min r
        JOIN
            dim_category_room d
        ON
            r.room_id = d.room_id;
        
        
        // Compute the rankings of channels in each category.
        CREATE VIEW view_app_category_visit_top10 AS
        SELECT
          app_ts,
          category_id,
          category_name,
          app_room_user_cnt,
          rangking
        FROM
        (
            SELECT 
                app_ts,
                room_id,
                category_id,
                category_name,
                app_room_user_cnt,
                ROW_NUMBER() OVER (PARTITION BY category_id ORDER BY app_room_user_cnt desc) AS ranking
            FROM
                view_app_category_visit_1min
        ) WHERE ranking <= 10;
        							
        ```


## Demo code and source code {#section_blr_yxx_ngb .section}

The Alibaba Cloud team has created demo code that contains a complete link applicable to the digital operation solution described above.

-   Upload a CSV file to a DataHub instance as the source table.
-   Create an RDS dimension table.
-   Create an RDS result table.

Refer to the complete demo code to register input and output data to develop your own digital operation solution. Click [Attachment](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/104071/cn_zh/1548210253178/%E8%A7%86%E9%A2%91%E7%9B%B4%E6%92%AD%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88%E4%B9%8B%20%E7%9B%B4%E6%92%AD%E6%95%B0%E5%AD%97%E5%8C%96%E8%BF%90%E8%90%A5.zip) to download the demo code.

