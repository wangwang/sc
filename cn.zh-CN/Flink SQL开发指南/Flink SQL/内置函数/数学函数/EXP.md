# EXP {#concept_kfv_ydq_dgb .concept}

本文为您介绍如何使用实时计算数学函数EXP。

## 语法 {#section_dks_qgp_dgb .section}

```
DOUBLE EXP(A)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|A|DOUBLE|

## 功能描述 {#section_hks_qgp_dgb .section}

返回自然常数e的A次幂的DOUBLE类型数值。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |in1\(DOUBLE\)|
    |-------------|
    |8.0|
    |10.0|

-   测试语句

    ```
    SELECT EXP(in1) as aa
    FROM T1
    
    ```

-   测试结果

    |aa\(DOUBLE\)|
    |------------|
    |2980.9579870417283|
    |22026.465794806718|


