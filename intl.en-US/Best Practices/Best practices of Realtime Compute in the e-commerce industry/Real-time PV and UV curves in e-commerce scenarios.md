# Real-time PV and UV curves in e-commerce scenarios {#concept_65669_zh .concept}

This topic provides a use case of Gegejia, a partner of Realtime Compute, to describe how to use Realtime Compute to create real-time page view \(PV\) and unique visitor \(UV\) curves.

## Background {#section_ich_bq2_2gb .section}

With the rise of new retail, competition in the Internet e-commerce industry is becoming increasingly fierce. Real-time data is particularly important to the e-commerce industry, such as collecting statistics on the total PVs and UVs to a website.

## Use case {#section_stq_fq2_2gb .section}

-   Business architecture

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41088/155763960634588_en-US.png)

-   Business process
    1.  Use the SDK provided by DataHub to synchronize the binlog file to DataHub.
    2.  Use Realtime Compute to subscribe to data in DataHub for real-time computing.
    3.  Insert real-time data into RDS.
    4.  Display data in Alibaba Cloud DataV or other visual dashboards.
-   Preparations

    The following table describes the fields in a log source table.

    |Field name|Data type|Description|
    |----------|---------|-----------|
    |account\_id|VARCHAR|The ID of the user.|
    |client\_ip|VARCHAR|The IP address of the client.|
    |client\_info|VARCHAR|The model of the device.|
    |platform|VARCHAR|The operating system type of the device.|
    |imei|VARCHAR|The International Mobile Equipment Identity \(IMEI\) number of the device.|
    |version|BIGINT|The operating system version of the device.|
    |action|BIGINT|The page jump description.|
    |gpm|VARCHAR|The tracking path.|
    |c\_time|VARCHAR|The time when the request was made.|
    |target\_type|VARCHAR|The type of requested data.|
    |target\_id|VARCHAR|The ID of requested data.|
    |udata|VARCHAR|The extended information.|
    |session\_id|VARCHAR|The ID of the session.|
    |product\_id\_chain|VARCHAR|The string of product IDs.|
    |cart\_product\_id\_chain|VARCHAR|The ID string of the products added to the cart.|
    |tag|VARCHAR|The special tag.|
    |position|VARCHAR|The location of the user.|
    |network|VARCHAR|The network type of the user.|
    |p\_dt|VARCHAR|The time partition by day.|
    |p\_platform|VARCHAR|The partition system version.|

    The following table describes the fields in an RDS result table.

    |Field name|Data type|Description|
    |----------|---------|-----------|
    |summary\_date|BIGINT|The date when the statistics are collected.|
    |summary\_min|VARCHAR|The minute when the statistics are collected.|
    |pv|BIGINT|The number of clicks on the specified website.|
    |uv|BIGINT|The number of visitors who click the specified website. **Note:** Only one UV is counted for multiple clicks by the same visitor within one day.

 |
    |currenttime|TIMESTAMP|The current system time.|

-   Business logic

    ```language-SQL
    
     // Create source tables.
    
    CREATE TABLE source_ods_fact_log_track_action (
        account_id                        VARCHAR, // The ID of the user.
        client_ip                         VARCHAR, // The IP address of the client.
        client_info                       VARCHAR, // The model of the device.
        platform                          VARCHAR, // The operating system type of the device.
        imei                              VARCHAR, // The IMEI number of the device.
        `version`                         VARCHAR, // The operating system version of the device.
        `action`                          VARCHAR, // The page jump description.
        gpm                               VARCHAR, // The tracking path.
        c_time                            VARCHAR, // The time when the request was made.
        target_type                       VARCHAR, // The type of requested data.
        target_id                         VARCHAR, // The ID of requested data.
        udata                             VARCHAR, // The extended information in JSON format.
        session_id                        VARCHAR, // The ID of the session.
        product_id_chain                  VARCHAR, // The string of product IDs.
        cart_product_id_chain             VARCHAR, // The ID string of the products added to the car.
        tag                               VARCHAR, // The special tag.
        `position`                        VARCHAR, // The location of the user.
        network                           VARCHAR, // The network type of the user.
        p_dt                              VARCHAR, // The time partition by day.
        p_platform                        VARCHAR // The partition system version.
    
    
    ) WITH (    
        type='datahub',
        endPoint='yourEndpointURL',
        project='yourProjectName',
        topic='yourTopicName',
        accessId='yourAccessId',
        accessKey='yourAccessSecret',
        batchReadSize='1000'
    );
    
    CREATE TABLE result_cps_total_summary_pvuv_min (
        summary_date              BIGINT, // The date when the statistics are collected.
        summary_min               VARCHAR, // The minute when the statistics are collected.
        pv                        BIGINT, // The number of clicks on the specified website.
        uv                        BIGINT, // The number of visitors who click the specified website. Only one UV is counted for multiple clicks by the same visitor within one day.
        currenttime               TIMESTAMP, // The current system time.
        primary key (summary_date,summary_min)
    ) WITH (    
        type= 'rds',
        url = 'yourRDSDatabaseURL',
        userName = 'yourDatabaseUserName',
        password = 'yourDatabasePassword',
        tableName = 'yourTableName'
    );
    
    CREATE VIEW result_cps_total_summary_pvuv_min_01 AS
    select 
    cast(p_dt as BIGINT) as summary_date // The time partition by day.
    ,count(client_ip) as pv // Compute the number of PVs by client IP address.
    ,count(distinct client_ip) as uv // Deduplicate visitors by client IP address.
    ,cast(max(c_time ) as TIMESTAMP)  as c_time // The time when the request was made.
    from source_ods_fact_log_track_action
    group by p_dt;
    
    INSERT into  result_cps_total_summary_pvuv_min
    select 
    a.summary_date, // The time partition by day.
    cast(DATE_FORMAT(c_time,'HH:mm')  as VARCHAR) as summary_min, // Obtain the time string representing the hour and minute.
    a.pv,
    a.uv,
    CURRENT_TIMESTAMP  as currenttime // The current system time.
    from result_cps_total_summary_pvuv_min_01 AS a
    ;
    ```

-   Key points

    To help you understand structured code and facilitate code maintenance, we recommend that you use views to split the business logic into two modules. For more information about views, see [Create a data view](../../../../intl.en-US/Flink SQL Development Guide/Flink SQL/Create a data view.md#).

    -   Module 1

        ```language-SQL
        CREATE VIEW result_cps_total_summary_pvuv_min_01 AS
        select 
        cast(p_dt as BIGINT) as summary_date // The time partition by day.
        ,count(client_ip) as pv // Compute the number of PVs by client IP address.
        ,count(distinct client_ip) as uv // Deduplicate visitors by client IP address.
        ,cast(max(c_time ) as TIMESTAMP)  as c_time // The time when the request was made.
        from source_ods_fact_log_track_action
        group by p_dt;
        ```

        -   Compute the number of clicks on the website by client IP address and use it as the number of PVs. Deduplicate visitors by client IP address to compute the number of UVs.
        -   `cast(max(c_time) as TIMESTAMP)` // The time when the last request was made.
        -   This snippet of business logic code groups data by `p_dt` \(specifying the time partition by `day`\) and uses `max(c_time)` to determine the last access time in the time partition. Finally, Realtime Compute inserts the numbers of PVs and UVs into the database.
        The following table describes the output results.

        |p\_dt|pv|uv|`max(c_time)`|
        |-----|--|--|-------------|
        |2017-12-12|1000|100|`2017-12-12 9:00:00`|
        |2017-12-12|1500|120|`2017-12-12 9:01:00`|
        |2017-12-12|2200|200|`2017-12-12 9:02:00`|
        |2017-12-12|3300|320|`2017-12-12 9:03:00`|

    -   Module 2

        ```language-SQL
        INSERT into  result_cps_total_summary_pvuv_min
        select 
        a.summary_date, // The time partition by day.
        cast(DATE_FORMAT(c_time,'HH:mm')  as VARCHAR) as summary_min, // Obtain the time string representing the hour and minute.
        a.pv,
        a.uv,
        CURRENT_TIMESTAMP  as currenttime // The current system time.
        from result_cps_total_summary_pvuv_min_01 AS a
        ```

        Extract the data in module 1 by hour and minute and obtain the PV and UV growth curves, as shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41088/155763960734589_en-US.png)


