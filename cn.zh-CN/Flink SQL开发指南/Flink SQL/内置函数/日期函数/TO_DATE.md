# TO\_DATE {#concept_egj_sxq_dgb .concept}

本文为您介绍如何使用实时计算日期函数TO\_DATE。

## 语法 {#section_dks_qgp_dgb .section}

```language-SQL
Date TO_DATE(INT time)
Date TO_DATE(VARCHAR date)
Date TO_DATE(VARCHAR date, VARCHAR format)
```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|time|INT **说明：** 表示从1970-1-1到所表示时间之间天数。

 |
|date|VARCHAR **说明：** 默认格式为yyyy-MM-dd。

 |
|format|VARCHAR|

## 功能描述 {#section_hks_qgp_dgb .section}

将INT类型的日期或者VARCHAR类型的日期转换成DATE类型。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |date1\(INT\)|date2\(VARCHAR\)|date3\(VARCHAR\)|
    |------------|----------------|----------------|
    |100|2017-09-15|20170915|

-   测试语句

    ```language-sql
    SELECT TO_DATE(date1) as var1,
     TO_DATE(date2) as var2,
     TO_DATE(date3,'yyyyMMdd') as var3
    FROM T1
    ```

-   测试结果

    |var1\(DATE\)|var2\(DATE\)|var3\(DATE\)|
    |------------|------------|------------|
    |1970-04-11|2017-09-15|2017-09-15|


