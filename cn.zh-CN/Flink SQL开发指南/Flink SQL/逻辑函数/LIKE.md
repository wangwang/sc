# LIKE {#concept_62829_zh .concept}

本文为您介绍如何使用实时计算逻辑运算函数LIKE。

## 语法 {#section_mnm_4dw_cgb .section}

```language-sql
A LIKE B
			
```

## 入参 {#section_qvx_tdw_cgb .section}

|参数|数据类型|
|--|----|
|A|VARCHAR|
|B|VARCHAR|

## 功能描述 {#section_cl2_v2w_cgb .section}

如果匹配，返回TRUE，否则返回FALSE。

**说明：** `%`可用于定义通配符。

## 示例1 {#section_qbd_hbp_dgb .section}

-   测试数据

    |int1\(INT\)|VARCHAR2\(VARCHAR\)|VARCHAR3\(VARCHAR\)|
    |-----------|-------------------|-------------------|
    |90|ss97|97ss|
    |99|ss10|7ho7|

-   测试语句

    ```
    SELECT int1 as aa
    FROM T1
    WHERE VARCHAR2 LIKE 'ss%';
    					
    ```

-   测试结果

    |aa\(int\)|
    |---------|
    |90|
    |99|


## 示例2 {#section_ekm_zdw_cgb .section}

-   测试数据

    |int1\(INT\)|VARCHAR2\(VARCHAR\)|VARCHAR3\(VARCHAR\)|
    |-----------|-------------------|-------------------|
    |90|ss97|97ss|
    |99|ss10|7ho7|

-   测试语句

    ```
    SELECT int1 as aa
    FROM T1
    WHERE VARCHAR3 LIKE '%ho%';
    					
    ```

-   测试结果

    |aa\(int\)|
    |---------|
    |99|


