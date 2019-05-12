# AVG {#concept_h55_txr_dgb .concept}

本文为您介绍如何使用实时计算聚合函数AVG。Flink SQL中使用AVG函数返回指定表达式中所有值的平均值。

## 语法 {#section_dks_qgp_dgb .section}

```
AVG(A)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|A|TINYINT、SMALLINT、INT、BIGINT 、FLOAT 、DECIMAL 或DOUBLE|

## 功能描述 {#section_hks_qgp_dgb .section}

返回列的平均数。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |var1\(INT\)|var2\(INT\)|
    |-----------|-----------|
    |4|30|
    |6|30|

-   测试语句

    ```language-sql
    SELECT AVG(var1) as aa
    FROM T1
    
    ```

-   测试结果

    |aa\(INT\)|
    |---------|
    |5|


