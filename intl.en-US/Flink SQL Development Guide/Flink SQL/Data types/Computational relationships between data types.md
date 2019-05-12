# Computational relationships between data types {#concept_84965_zh .concept}

This topic describes mathematical and logical operations between different data types in Realtime Compute.

## Mathematical and logical operations {#section_dw1_xfx_bgb .section}

|Operation statement|Description|Data type supported by numeric1 and numeric2|Example|
|-------------------|-----------|--------------------------------------------|-------|
|numeric1 + numeric2|[Addition](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/Mathematical functions/Addition.md#)|INT, DOUBLE, DECIMAL, and BIGINT|`2 + 4.2`|
|numeric1 - numeric2|[Subtraction](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/Mathematical functions/Subtraction.md#)|`3 - 5.3`|
|numeric1 × numeric2|[Multiplication](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/Mathematical functions/Multiplication.md#)|`2 × 4`|
|numeric1/numeric2|[Division](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/Mathematical functions/Division.md#)|2.4/5|
|numeric1 \> numeric2|[Checks whether the first numeric is greater than the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/>.md#)|`2.4 > 5`|
|numeric1 < numeric2|[Checks whether the first numeric is less than the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/<.md#)|`2.4 < 5`|
|numeric1 \>= numeric2|[Checks whether the first numeric is greater than or equal to the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/>=.md#)|`2.4 >= 5`|
|numeric1 <= numeric2|[Checks whether the first numeric is less than or equal to the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/<=.md#)|`2.4 <= 5`|
|numeric1 = numeric2|[Checks whether the first numeric is equal to the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/=.md#)|INT, DOUBLE, DECIMAL, BIGINT, and VARCHAR|`‘iphone’ = 5`|
|numeric1 <\> numeric2|[Checks whether the first numeric is not equal to the second numeric.](intl.en-US/Flink SQL Development Guide/Flink SQL/Logical functions/<>.md#)|`'iphone' <> 5`|

**Note:** Data types of numeric1 and numeric2 in an operation statement must be the same.

