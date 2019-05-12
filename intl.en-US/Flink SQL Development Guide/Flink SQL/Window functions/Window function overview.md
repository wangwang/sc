# Window function overview {#concept_62510_zh .concept}

This topic describes the window functions, time attributes, and window types that Flink SQL supports.

## Window functions {#section_pdk_kp5_cgb .section}

Flink SQL supports aggregation over infinite windows \(you do not need to explicitly add any windows in your SQL query statement\). In addition, Flink SQL supports aggregation over a specific window. For example, to count the number of users who clicked a specific URL in the past minute, you can define a window for collecting user clicks in the past minute. Then, you can compute the data in the window to obtain the result.

Flink SQL supports window aggregate and over aggregate. This topic describes window aggregate. Window aggregate supports the following two time attributes: event time and processing time. For each time attribute, Flink SQL supports the following three window types: tumbling window, sliding window, and session window.

## Time attributes {#section_vhy_mp5_cgb .section}

Flink SQL supports two time attributes. Realtime Compute aggregates data in windows based on these two time attributes.

-   [Event time](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#section_jf3_mhf_5fb): The event time that you provide in the table schema, which is generally the original creation time of the data.
-   [Processing time](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#section_lv4_5kf_5fb): The local time at which the system processes an event.

For more information about the time attributes supported by Realtime Compute, see [Time attributes](intl.en-US/Flink SQL Development Guide/Flink SQL/Basic concepts/Time attributes.md#).

