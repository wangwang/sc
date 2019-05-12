# Watermark {#concept_lkg_hsy_bhb .concept}

Realtime Compute supports window aggregation over data based on time attributes. For a job that runs an Event Time-based window function, the watermark method must be used in the declaration of the source table.

Watermark is a mechanism that is used to measure the [Event Time](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#section_jf3_mhf_5fb) progress. It is a hidden data attribute. Watermark definition is a part of the source table DDL definition. Flink provides the following syntax to define a watermark:

**Note:** For more information about time attributes in Realtime Compute, see [Time attributes](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#).

```language-sql
WATERMARK [watermarkName] FOR <rowtime_field> AS withOffset(<rowtime_field>, offset)

```

|Name|Description|
|----|-----------|
|watermarkName|The name of the watermark. This parameter is optional.|
|<rowtime\_field\>|The column used to generate the watermark. This column is identified as the Event Time column and can be used to define a window in a subsequent query. The parameter value must be a column defined in the table. Only columns of the TIMESTAMP type are supported.|
|withOffset|The watermark generation policy. The watermark value is generated based on the following formula: `<rowtime_field> - offset`. The first parameter in `withOffset`must be `<rowtime_field>`.|
|offset|The offset between the watermark value and Event Time value. Unit: millisecond.|

Generally, a field in a data record indicates the time when the record is generated. For example, a table has a `rowtime` field of the TIMESTAMP type, and one field value is `1501750584000 (2017-08-03 08:56:24.000)`. If you want to define a watermark based on the `rowtime` field and configure a 4-second offset in the watermark policy, add the following definition:

```
WATERMARK FOR rowtime AS withOffset(rowtime, 4000)

```

In this example, the watermark time of the data record is `1501750584000 - 4000 = 1501750580000 (2017-08-03 08:56:20.000)`. It means that all data whose timestamp is earlier than `1501750580000 (2017-08-03 08:56:20.000)` has arrived.

**Note:** 

-   When you use an Event Time-based watermark, note that the `rowtime` field must be of the TIMESTAMP type. Currently, Realtime Compute supports a 13-digit UNIX timestamp in milliseconds. If the rowtime field is of another type or the UNIX timestamp is not 13 digits in length, we recommend that you use a [computed column](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Computed column.md#) to convert the time.
-   The [Event Time](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#section_jf3_mhf_5fb) and [Processing Time](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#section_lv4_5kf_5fb) can only be declared in the source table.

Summary

-   A watermark indicates that all the events whose timestamp \(t'\) is earlier than the watermark time t \(`t'< t`\) have occurred. After the watermark time `t` has taken effect, all subsequently received records whose Event Time is earlier than `t` will be discarded. This is the current mechanism used in Realtime Compute. In the future, Realtime Compute will allow you to change configurations to ensure that later data can also be updated.
-   The watermark is particularly important for out-of-order data streams because it maximizes the chance that a window is correctly computed even when the arrival of some events is delayed.
-   When an operator has multiple input data streams for parallel processing, the Event Time of the data stream with the shortest time is used as the Event Time at the operator.

    ![](images/40782_en-US.svg)


