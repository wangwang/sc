# Real-time situation awareness and geographic distribution of orders in e-commerce scenarios {#concept_stk_qcm_2gb .concept}

This topic provides a use case to describe how to use Realtime Compute to implement real-time situation awareness and geographic distribution of orders.

## Background {#section_nkg_wcm_2gb .section}

Real-time situation awareness and geographic order distribution help enterprises optimize the allocation and release of product categories in a timely manner. The following use case describes how a food e-commerce enterprise uses Realtime Compute to implement real-time situation awareness and geographic distribution of orders.

## Use case {#section_lbh_32m_2gb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41090/155763966934742_en-US.png)

**Note:** To focus on the core logic, we simplify the order data format to retain only the attributes related to the use case.

-   Create multiple tables to store data.

    In the e-commerce system, orders and shipping addresses are separately stored. A buyer can use multiple shipping addresses to place orders. No shipping address is specified when an order is created. The specific shipping address can be obtained only when the order is submitted. The shipping address table stores city IDs \(specified by city\_id\). You also need to create a city table to store the geographic information about cities. We create these tables to collect statistics on the distribution of orders \(GMV\) in different regions by day.

    -   Create an order table.

        ```
        CREATE TABLE source_order (
            id VARCHAR, // The ID of the order.
            seller_id VARCHAR, // The ID of the seller.
            account_id VARCHAR, // The ID of the buyer.
            receive_address_id VARCHAR, // The ID of the shipping address.
            total_price VARCHAR, // The order amount.
            pay_time VARCHAR, // The payment time of the order.
        ) WITH (
            type='datahub',
            endPoint='http://dh-cn-hangzhou.aliyun-inc.com',
            project='yourProjectName', // Your project name.
            topic='yourTopicName', // Your topic name.
            roleArn='yourRoleArn', // Your role ARN.
            batchReadSize='500'
        );
        ```

    -   Create a shipping address table.

        ```
        CREATE TABLE source_order_receive_address ( 
             id VARCHAR, // The ID of the shipping address. 
             full_name VARCHAR, // The full name of the consignee. 
             mobile_number VARCHAR, // The mobile number of the consignee. 
             detail_address VARCHAR, // The detailed shipping address. 
             province VARCHAR, // The province in the shipping address. 
             city_id VARCHAR, // The city in the shipping address. 
             create_time VARCHAR // The time when the order was created. 
         ) WITH ( 
             type='datahub', 
             endPoint='http://dh-cn-hangzhou.aliyun-inc.com', 
             project='yourProjectName', // Your project name. 
             topic='yourProjectName', // Your topic name. 
             roleArn='yourProjectName', // Your role ARN. 
             batchReadSize='500' 
         );                             
        ```

    -   Create a city table.

        ```
        CREATE TABLE dim_city ( 
             city_id varchar, 
             city_name varchar, // The name of the city. 
             province_id varchar, // The ID of the province to which the city belongs. 
             zip_code varchar, // The postal code. 
             lng varchar, // The longitude of the city. 
             lat varchar, // The latitude of the city. 
          PRIMARY KEY (city_id), 
          PERIOD FOR SYSTEM_TIME // Specify that this is a dimension table. 
         ) WITH ( 
             type= 'rds', 
             url = 'yourDatabaseURL', // Your database URL. 
             tableName = 'yourTableName', // Your table name. 
             userName = 'yourDatabaseName', // Your username. 
             password = 'yourDatabasePassword' // Your password. 
         );
        ```

    -   Collect statistics on the distribution of orders \(GMV\) in different regions by day.

        ```
        CREATE TABLE result_order_city_distribution ( 
             summary_date bigint, // The date when the statistics are collected. 
             city_id bigint, // The ID of the city. 
             city_name varchar, // The name of the city. 
             province_id bigint, // The ID of the province to which the city belongs. 
             gmv double, // The GMV. 
             lng varchar, // The longitude of the city. 
             lat varchar, // The latitude of the city. 
             primary key (summary_date,city_id) 
            ) WITH ( 
                type= 'rds',     
                url = 'yourDatabaseURL', // Your database URL. 
                tableName = 'yourTableName', // Your table name. 
                userName = 'yourDatabaseName', // Your username. 
                password = 'yourDatabasePassword' // Your password. 
            );
        ```

-   Edit business logic.

    ```
     insert into result_order_city_distribution 
     select 
     d.summary_date 
     ,cast(d.city_id as BIGINT) 
     ,e.city_name 
     ,cast(e.province_id as BIGINT) 
     ,d.gmv 
     ,e.lng 
     ,e.lat 
     ,e.lnglat 
     from 
     ( 
             select 
             DISTINCT 
             DATE_FORMAT(a.pay_time,'yyyyMMdd') as summary_date 
             ,b.city_id as city_id 
             ,round(sum(cast(a.total_price as double)),2) as gmv 
             from source_order as a 
             join source_order_receive_address as b on a.receive_address_id =b.id 
             group by DATE_FORMAT(a.pay_time,'yyyyMMdd'),b.city_id 
             // Join the order table with the shipping address table and compute the sales distribution by date and city ID. 
     )d join dim_city FOR SYSTEM_TIME AS OF PROCTIME() as e on d.city_id = e.city_id 
     // Join the dimension table to complete the geographic information about cities and obtain the final computing result. 
     ;
    ```


