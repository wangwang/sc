# OVER window {#concept_62514_zh .concept}

An OVER window is a standard window used by traditional databases. It is different from the GROUP BY window. In a stream that applies the OVER window, each element corresponds to an OVER window, whose elements are a set of elements adjacent to the current element. Elements of a stream are distributed across multiple windows. In the implementation of Flink SQL windows, the row determined by each element that triggers computing is the last row of the window where the element is located.

In a stream that applies the OVER window, each element corresponds to an OVER window and triggers data computing once. In the underlying implementation of Realtime Compute, the OVER window data is managed in a global and unified manner \(only one copy of data is stored\). Logically, an OVER window is maintained to perform window computing for each element. Expired data will be cleared after the computing is completed.

## Syntax {#section_s3c_jxv_cgb .section}

```language-sql
SELECT
    agg1(col1) OVER (definition1) AS colName,
    ...
    aggN(colN) OVER (definition1) AS colNameN
FROM Tab1
			
```

**Note:** 

-   OVER \(definition1\) must be the same for agg1 through aggN.
-   The alias specified by AS can be queried by using an outer SQL statement.

## Type {#section_fnt_jxv_cgb .section}

In Flink SQL, the OVER window definition follows standard SQL syntax. Traditionally, OVER windows are not classified into finer-grained window types. To help you gain a better understanding of the OVER window semantics, we classify OVER windows into the following two types based on the ways of determining the computed row:

-   ROWS OVER window: Each row of elements is treated as a new computed row. That is, each row corresponds to a new window.
-   RANGE OVER window: All element rows with the same timestamp value are treated as the same computed row and belong to the same window.

## Attribute {#section_upy_nxv_cgb .section}

|Orthogonal attribute|proctime|eventtime|
|--------------------|--------|---------|
|rows|√|√|
|range|√|√|

-   rows: A window is determined based on the actual row of an element.
-   range: A window is determined based on the actual value \(timestamp value\) of an element.

## ROWS OVER window semantics {#section_kd5_2yv_cgb .section}

-   Window data

    In a ROWS OVER window, each element determines a window. ROWS OVER windows are classified into Unbounded and Bounded ROWS OVER windows.

    The following figure shows Unbounded ROWS OVER window data.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40915/155764436434339_en-US.png)

    **Note:** As shown in the preceding figure, elements of windows w7 and w8 of user 1 arrive at the same time, and so do elements of windows w3 and w4 of user 2. However, the elements are in different windows. In this regard, a ROWS OVER window is different from a RANGE OVER window.

    The following figure shows Bounded ROWS OVER window data, in which a window has three elements \(two elements in PRECEDING state\).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40915/155764436434340_en-US.png)

    **Note:** As shown in the preceding figure, windows w5 and w6 of user 1 have elements that arrive at the same time, and so do windows w2 and w3 of user 2. However, the elements are in different windows. In this regard, a ROWS OVER window is different from a RANGE OVER window.

-   Window syntax

    ```language-sql
    SELECT 
        agg1(col1) OVER(
         [PARTITION BY (value_expression1,..., value_expressionN)] 
         ORDER BY timeCol
         ROWS 
         BETWEEN (UNBOUNDED | rowCount) PRECEDING AND CURRENT ROW) AS colName, ... 
    FROM Tab1
    					
    ```

    -   value\_expression: specifies the value expression used for partitioning.
    -   timeCol: specifies the time field used for sorting elements.
    -   rowCount: specifies the number of rows to be traced before the current row.
-   Example

    Use a Bounded ROWS OVER window as an example. Here is a merchandise shelving table, which lists the ID, type, shelving time, and price of merchandises. Compute the highest price among three similar merchandises before the current merchandise hits shelves.

    **Test data**

    |itemID|itemType|onSellTime|price|
    |------|--------|----------|-----|
    |ITEM001|Electronic|`2017-11-11 10:01:00`|20|
    |ITEM002|Electronic|`2017-11-11 10:02:00`|50|
    |ITEM003|Electronic|`2017-11-11 10:03:00`|30|
    |ITEM004|Electronic|`2017-11-11 10:03:00`|60|
    |ITEM005|Electronic|`2017-11-11 10:05:00`|40|
    |ITEM006|Electronic|`2017-11-11 10:06:00`|20|
    |ITEM007|Electronic|`2017-11-11 10:07:00`|70|
    |ITEM008|Clothes|`2017-11-11 10:08:00`|20|

    **Test code**

    ```language-sql
    CREATE TABLE tmall_item(
       itemID VARCHAR,
       itemType VARCHAR,
       onSellTime TIMESTAMP,
       price DOUBLE,
       WATERMARK onSellTime FOR onSellTime as withOffset(onSellTime, 0) 
    ) 
    WITH (
      type = 'sls',
       ...
    ) ;
    
    SELECT  
        itemID,
        itemType, 
        onSellTime, 
        price,  
        MAX(price) OVER (
            PARTITION BY itemType 
            ORDER BY onSellTime 
            ROWS BETWEEN 2 preceding AND CURRENT ROW) AS maxPrice
      FROM tmall_item
    					
    ```

    **Test result**

    |itemID|itemType|onSellTime|price|maxPrice|
    |------|--------|----------|-----|--------|
    |ITEM001|Electronic|`2017-11-11 10:01:00`|20|20|
    |ITEM002|Electronic|`2017-11-11 10:02:00`|50|50|
    |ITEM003|Electronic|`2017-11-11 10:03:00`|30|50|
    |ITEM004|Electronic|2017-11-11 10:03:00|60|60|
    |ITEM005|Electronic|`2017-11-11 10:05:00`|40|60|
    |ITEM006|Electronic|`2017-11-11 10:06:00`|20|60|
    |ITEM007|Electronic|`2017-11-11 10:07:00`|70|70|
    |ITEM008|Clothes|`2017-11-11 10:08:00`|20|20|


## RANGE OVER window semantics {#section_o3z_syv_cgb .section}

-   Window data

    In a RANGE OVER window, all element rows with the same element value \(element timestamp\) determine a window. RANGE OVER windows are classified into Unbounded and Bounded RANGE OVER windows.

    The following figure shows Unbounded RANGE OVER window data.****

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40915/155764436534341_en-US.png)

    > As shown in the preceding figure, elements of the two w7 windows of user 1 arrive at the same time, and so do elements of the two w3 windows of user 2. The elements are in the same windows, respectively. In this regard, a RANGE OVER window is different from a ROWS OVER window.

    The following figure shows Bounded RANGE OVER window data, in which a 3-second window has an interval of 2 seconds.``

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40915/155764436534342_en-US.png)

    **Note:** As shown in the preceding figure, elements of the two w6 windows of user 1 arrive at the same time, and so do elements of the two w3 windows of user 2. The elements are in the same windows, respectively. In this regard, a RANGE OVER window is different from a ROWS OVER window.

-   Window syntax

    ```language-sql
    SELECT 
        agg1(col1) OVER(
         [PARTITION BY (value_expression1,..., value_expressionN)] 
         ORDER BY timeCol
         RANGE 
         BETWEEN (UNBOUNDED | timeInterval) PRECEDING AND CURRENT ROW) AS colName, 
    ... 
    FROM Tab1
    						
    ```

    -   value\_expression: specifies the value expression used for partitioning.
    -   timeCol: specifies the time field used for sorting elements.
    -   timeInterval: specifies the time span from the current element row to the earliest element row to be traced backwards.
-   Example

    Use a Bounded RANGE OVER window as an example. Here is a merchandise shelving table, which lists the ID, type, shelving time, and price of merchandises. Compute the highest price among similar merchandises that hit shelves 2 minutes earlier than the current merchandise.

    **Test data**

    |itemID|itemType|onSellTime|price|
    |------|--------|----------|-----|
    |ITEM001|Electronic|`2017-11-11 10:01:00`|20|
    |ITEM002|Electronic|`2017-11-11 10:02:00`|50|
    |ITEM003|Electronic|`2017-11-11 10:03:00`|30|
    |ITEM004|Electronic|`2017-11-11 10:03:00`|60|
    |ITEM005|Electronic|`2017-11-11 10:05:00`|40|
    |ITEM006|Electronic|`2017-11-11 10:06:00`|20|
    |ITEM007|Electronic|`2017-11-11 10:07:00`|70|
    |ITEM008|Clothes|`2017-11-11 10:08:00`|20|

    **Test code**

    ```language-sql
    CREATE TABLE tmall_item(
       itemID VARCHAR,
       itemType VARCHAR,
       onSellTime TIMESTAMP,
       price DOUBLE,
       WATERMARK onSellTime FOR onSellTime as withOffset(onSellTime, 0) 
    ) 
    WITH (
      type = 'sls',
       ...
    ) ;
    
    SELECT  
        itemID,
        itemType, 
        onSellTime, 
        price,  
        MAX(price) OVER (
            PARTITION BY itemType 
            ORDER BY onSellTime 
            RANGE BETWEEN INTERVAL '2' MINUTE preceding AND CURRENT ROW) AS maxPrice
      FROM tmall_item
    
    						
    ```

    **Test result**

    |itemID|itemType|onSellTime|price|maxPrice|
    |------|--------|----------|-----|--------|
    |ITEM001|Electronic|`2017-11-11 10:01:00`|20|20|
    |ITEM002|Electronic|`2017-11-11 10:02:00`|50|50|
    |ITEM003|Electronic|`2017-11-11 10:03:00`|30|50|
    |ITEM004|Electronic|`2017-11-11 10:03:00`|60|60|
    |ITEM005|Electronic|`2017-11-11 10:05:00`|40|60|
    |ITEM006|Electronic|`2017-11-11 10:06:00`|20|40|
    |ITEM007|Electronic|`2017-11-11 10:07:00`|70|70|
    |ITEM008|Clothes|`2017-11-11 10:08:00`|20|20|


