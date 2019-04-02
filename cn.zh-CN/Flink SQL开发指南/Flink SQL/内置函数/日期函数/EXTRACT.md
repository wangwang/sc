# EXTRACT {#concept_xwk_zqq_dgb .concept}

本文为您介绍如何使用实时计算日期函数EXTRACT。

## 语法 {#section_dks_qgp_dgb .section}

```
BIGINT EXTRACT(unit FROM time)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|time|任意日期表达式|
|unit|可取值如下。-   MICROSECOND
-   SECOND
-   MINUTE
-   HOUR
-   DAY
-   WEEK
-   MONTH
-   QUARTER
-   YEAR
-   SECOND\_MICROSECOND
-   MINUTE\_MICROSECOND
-   MINUTE\_SECOND
-   HOUR\_MICROSECOND
-   HOUR\_SECOND
-   HOUR\_MINUTE
-   DAY\_MICROSECOND
-   DAY\_SECOND
-   DAY\_MINUTE
-   DAY\_HOUR
-   YEAR\_MONTH

|

## 功能描述 {#section_hks_qgp_dgb .section}

返回日期/时间的单独部分，比如年、月、日、小时、分钟、周数等。

## 示例 {#section_iks_qgp_dgb .section}

-   测试语句

    ```
    EXTRACT(YEAR FROM CURRENT_TIMESTAMP) AS OrderYear,
    EXTRACT(MONTH FROM CURRENT_TIMESTAMP) AS OrderMonth,
    EXTRACT(DAY FROM CURRENT_TIMESTAMP) AS OrderDay,
    EXTRACT(WEEK FROM CURRENT_TIMESTAMP) AS OrderWeek
    
    ```

-   测试结果

    |OrderYear\(BIGINT\)|OrderMonth\(BIGINT\)|OrderDay\(BIGINT\)|OrderWeek\(BIGINT\)|
    |-------------------|--------------------|------------------|-------------------|
    |2018|10|11|41|


