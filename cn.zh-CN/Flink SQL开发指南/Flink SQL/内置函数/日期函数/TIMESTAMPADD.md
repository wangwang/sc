# TIMESTAMPADD {#concept_eq5_vvq_dgb .concept}

本文为您介绍如何使用实时计算日期函数TIMESTAMPADD。

## 语法 {#section_dks_qgp_dgb .section}

```
TIMESTAMP TIMESTAMPADD(interval,INT int_expr,TIMESTAMP datetime_expr)
DATE TIMESTAMPADD(interval,INT int_expr,DATE datetime_expr)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|interval|VARCHAR|
|int\_expr|INT|
|datetime\_expr|TIMESTAMP或DATE|

**说明：** 

interval可取值如下。

|interval参数|时间间隔单位|
|----------|------|
|FRAC\_SECOND|毫秒|
|SECOND|秒|
|MINUTE|分钟|
|HOUR|小时|
|DAY|天|
|WEEK|星期|
|MONTH|月|
|QUARTER|季度|
|YEAR|年|

## 功能描述 {#section_hks_qgp_dgb .section}

返回类型与datetime\_expr类型相同。

将整型表达式int\_expr添加到日期或日期时间表达式datetime\_expr中。以数据类型TIME的值返回会话时区中的当前时间。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |a\(TIMESTAMP\)|b\(DATE\)|
    |--------------|---------|
    |2018-07-09 10:23:56|1990-02-20|

-   测试语句

    ```language-sql
    SELECT 
    TIMESTAMPADD(HOUR,3,a) AS `result1`
    TIMESTAMPADD(DAY,3,b) AS `result2`
    FROM T1
    
    ```

-   测试结果

    |result1\(TIMESTAMP\)|result2\(DATE\)|
    |--------------------|---------------|
    |2018-07-09 13:23:56.0|1990-02-23|


