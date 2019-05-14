# Hop window {#concept_r3r_jqv_cgb .concept}

This article describes how to use the real-time calculation sliding window function.

**Note:** Real-time computing HOP window \(HOP\) cannot be used together with last\_value, first\_value, or TopN functions.

## What is a sliding window? {#section_mfx_kqv_cgb .section}

A hop window is also called a sliding window. Unlike tumble windows, hop windows can overlap each other.

The sliding window has two parameters: slide and size. The slide parameter specifies the length of the sliding step, and the size parameter specifies the size of the window.

-   Slide <Size:The windows overlap each other, and each element is assigned to multiple windows.
-   Slide = Size:The windows are tumbling windows.
-   Slide \> Size:The windows do not overlap each other but are separated by gaps.

Generally, most elements match multiple windows, and the windows overlap. Sliding windows are useful in computing moving averages. For example, to compute the data average in the past 5 minutes every 10 seconds, you can set slide to 10 seconds and size to 5 minutes. The following figure shows sliding windows whose slide is 30 seconds and size is 1 minute.

![Hop window](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/40913/155781895334327_en-US.png)

## Sliding Window function syntax {#section_dhc_y1v_cgb .section}

The HOP function is used to define a sliding window in a GROUP BY clause.

```language-sql
HOP (<time-attr>, <slide-interval>, <size-interval>)
<slide-interval>: INTERVAL 'string' timeUnit
<size-interval>: INTERVAL 'string' timeUnit
			
```

**Note:** 

The `<time-attr>` parameter must be a valid time attribute in a stream to specify whether the time is the processing time or event time. Refer [Window function overview](intl.en-US/Flink SQL Development Guide/Flink SQL/Window functions/Window function overview.md#)to learn how to define [Time attributes](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#) and [Watermark](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Watermark.md#).

## Window identifier functions {#section_dtr_rdv_cgb .section}

A window identifier function specifies the start or end time of a window, or the window time attribute for aggregation of lower-level windows.

|Window identifier function|Return type|Description|
|--------------------------|-----------|-----------|
|`HOP_START (<time-attr>, <slide-interval>, <size-interval>)`|TIMESTAMP|Return the start time \(include border value\) of the window. For example, if the window is `[00:10, 00:15)`, `00:10` is returned.|
|`HOP_END (<time-attr>, <slide-interval>, <size-interval>)`|TIMESTAMP|Return the end time \(include border value\) of the window. For example, if the window is `[00:00, 00:15)`, `00:15` is returned.|
|`HOP_ROWTIME (<time-attr>, <slide-interval>, <size-interval>)`|TIMESTAMP \(rowtime-attr\)|Return the end time \(exclude the border value\) of the window. For example, if the window is`[00:00, 00:15)`, `00:14:59.999` is returned. The return value is a rowtime attribute, based on which time type operations can be performed. The function is applicable only to windows based on event time.|
|`HOP_PROCTIME (<time-attr>, <slide-interval>, <size-interval>)`|TIMESTAMP \(rowtime-attr\)|Return the end time \(exclude the border value\) of the window. For example, if the window is `[00:00, 00:15)`\], `00:14:59.999` is returned. The return value is a proctime attribute, based on which time type operations can be performed. It can only be used in a window based on processing time.|

## Example {#section_lpl_sdv_cgb .section}

The following example describes how to compute the number of clicks per user over the past minute every 30 seconds. That is, the 1-minute window slides every 30 seconds.

-   Test data

    |username\(VARCHAR\)|click\_url\(VARCHAR\)|ts\(TIMESTAMP\)|
    |-------------------|---------------------|---------------|
    |Jark|`http://taobao.com/xxx`|`2017-10-10 10:00:00.0`|
    |Jark|`http://taobao.com/xxx`|`2017-10-10 10:00:10. 0`|
    |Jark|`http://taobao.com/xxx`|`2017-10-10 10:00:49. 0`|
    |Jark|`http://taobao.com/xxx`|`2017-10-10 10:01:05. 0`|
    |Jark|`http://taobao.com/xxx`|`2017-10-10 10:01:58. 0`|
    |Timo|`http://taobao.com/xxx`|`2017-10-10 10:02:10. 0`|

-   Test statement

    ```language-SQL
    Create table user_clicks (
        Username VARCHAR,
        Click_url VARCHAR,
        Ts TIMESTAMP,
        WATERMARK wk FOR ts as withoffset (ts, 2000) -- Define a watermark for rowtime.
    ) WITH (TYPE = 'datahub ',
            ...) ;
    CREATE TABLE hop_output (
        window_start TIMESTAMP,
        window_end TIMESTAMP,
        username VARCHAR,
        clicks BIGINT
    ) WITH (TYPE = 'rds ',
            ...) ;
    INSERT INTO
        hop_output
    SELECT statement
        HOP_START (ts, INTERVAL '30' SECOND, INTERVAL '1' MINUTE ),
        HOP_END (ts, INTERVAL '30' SECOND, INTERVAL '1' MINUTE ),
        username,
        COUNT (click_url)
    FROM
        user_clicks
    GROUP BY
        HOP (ts, INTERVAL '30' SECOND, INTERVAL '1' MINUTE ),
        username
    					
    ```

-   Test results

    |window\_start\(TIMESTAMP\)|window\_end\(TIMESTAMP\)|username\(VARCHAR\)|clicks\(BIGINT\)|
    |--------------------------|------------------------|-------------------|----------------|
    |`2017-10-10 10:00:00.0`|`2017-10-10 10:01:00. 0`|Jark|3|
    |`2017-10-10 10:00:30. 0`|`2017-10-10 10:01:30. 0`|Jark|2|
    |`2017-10-10 10:01:00. 0`|`2017-10-10 10:02:00. 0`|Jark|2|
    |`2017-10-10 10:01:30. 0`|`2017-10-10 10:02:30. 0`|Jark|1|
    |`2017-10-10 10:01:30. 0`|`2017-10-10 10:02:30. 0`|Timo|1|
    |`2017-10-10 10:02:00. 0`|`2017-10-10 10:03:00. 0`|Timo|1|


