# RAND {#concept_o2y_l3q_dgb .concept}

本文为您介绍如何使用实时计算数学函数RAND。

## 语法 {#section_dks_qgp_dgb .section}

```
DOUBLE RAND([BIGINT seed])

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|说明|
|--|----|--|
|seed|BIGINT|Seed取值为随机数，决定随机数序列的起始值。|

## 功能描述 {#section_hks_qgp_dgb .section}

返回大于等于0小于1的DOUBLE类型随机数。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |id\(INT\)|X\(INT\)|
    |---------|--------|
    |1|8|

-   测试语句

    ```
    SELECT id, rand(1) as dou1, rand(3) as dou2
    FROM T1
    
    ```

-   测试结果

    |id\(INT\)|dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |---------|--------------|--------------|
    |1|0.7308781907032909|0.731057369148862|


