# E {#concept_dly_4fq_dgb .concept}

本文为您介绍如何使用实时计算数学函数E。

## 语法 {#section_dks_qgp_dgb .section}

```
DOUBLE E()

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|A|DOUBLE|

## 功能描述 {#section_hks_qgp_dgb .section}

返回自然常数e的DOUBLE类型值。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |in1\(DOUBLE\)|
    |-------------|
    |8.0|
    |10.0|

-   测试语句

    ```
    SELECT  e() as dou1, E() as dou2
    FROM T1
    
    ```

-   测试结果

    |dou1\(DOUBLE\)|dou2\(DOUBLE\)|
    |--------------|--------------|
    |2.718281828459045|2.718281828459045|


