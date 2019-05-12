# BITNOT {#concept_azd_ryp_dgb .concept}

本文为您介绍如何使用实时计算数学函数BITNOT。

## 语法 {#section_dks_qgp_dgb .section}

```
INT BITNOT(INT number)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|number|INT|

## 功能描述 {#section_hks_qgp_dgb .section}

按位取反。输入和输出类型均为整型，且类型一致。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |a\(INT\)|
    |--------|
    |7|

-   测试语句

    ```
    SELECT BITNOT(a) as var1
    FROM T1
    
    ```

-   测试结果

    |var1\(INT\)|
    |-----------|
    |0xfff8|


