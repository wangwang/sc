# NOW {#concept_q4l_dvq_dgb .concept}

本文为您介绍如何使用实时计算日期函数NOW。

## 语法 {#section_dks_qgp_dgb .section}

```language-SQL
BIGINT NOW()
BIGINT NOW(a)
```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|a|INT|

## 功能描述 {#section_hks_qgp_dgb .section}

-   未指定参数时返回当前时区时间的时间戳，单位为秒。
-   可在括号内输入INT类型参数作为偏移值（单位：秒），返回偏移后的时间戳。例如，`now(100)`返回当前时间戳加100秒的时间戳。

    **说明：** 偏移值a为NULL时，NOW\(a\)返回值为NULL。


## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |a\(INT\)|
    |--------|
    |null|

-   测试语句

    ```language-sql
    SELECT 
     NOW() as now,
     NOW(100) as now_100,
     NOW(a) as now_null
    FROM T1
    ```

-   测试结果

    |now\(BIGINT\)|now\_100\(BIGINT\)|now\_null\(BIGINT\)|
    |-------------|------------------|-------------------|
    |1403006911|1403007011|null|


