# FLOOR {#concept_wrm_dgq_dgb .concept}

本文为您介绍如何使用实时计算数学函数FLOOR。

## 语法 {#section_dks_qgp_dgb .section}

```
B FLOOR(A)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|A|INT、BIGINT、FLOAT、DOUBLE|

## 功能描述 {#section_hks_qgp_dgb .section}

返回小于或等于A的最大整数数值，即舍去小数位的数值。B的数据类型与A的数据类型一致。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |in1\(DOUBLE\)|in2\(BIGINT\)|
    |-------------|-------------|
    |8.123|3|

-   测试语句

    ```
    SELECT 
    FLOOR(in1) as out1,
    FLOOR(in2) as out2
    FROM T1
    
    ```

-   测试结果

    |out1\(DOUBLE\)|out2\(BIGINT\)|
    |--------------|--------------|
    |8.0|3|


