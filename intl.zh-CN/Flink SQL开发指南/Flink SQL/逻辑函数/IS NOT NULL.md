# IS NOT NULL {#concept_62825_zh .concept}

本文为您介绍如何使用实时计算逻辑运算函数IS NOT NULL。

## 语法 {#section_mnm_4dw_cgb .section}

```language-sql
value IS NOT NULL

```

## 入参 {#section_qvx_tdw_cgb .section}

|参数|数据类型|
|--|----|
|value|任意数据类型|

## 功能描述 {#section_cl2_v2w_cgb .section}

如果 value为`NULL`，返回`FALSE`，否则返回`TRUE`。

## 示例 {#section_ekm_zdw_cgb .section}

-   测试数据

    |int1\(INT\)|int2\(VARCHAR\)|
    |-----------|---------------|
    |97|无|
    |9|ww123|

-   测试语句

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int2 IS NOT NULL;
    
    ```

-   测试结果

    |aa\(int\)|
    |---------|
    |9|


