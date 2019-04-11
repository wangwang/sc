# IS\_DECIMAL {#concept_zhx_ztr_dgb .concept}

本文为您介绍如何使用实时计算条件函数IS\_DECIMAL。

## 语法 {#section_dks_qgp_dgb .section}

```
BOOLEAN IS_DECIMAL(VARCHAR str)

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|str|VARCHAR|

## 功能描述 {#section_hks_qgp_dgb .section}

str字符串如果可以转换为十进制数值返回TRUE；否则返回FALSE。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |a\(VARCHAR\)|b\(VARCHAR\)|c\(VARCHAR\)|d\(VARCHAR\)|e\(VARCHAR\)|f\(VARCHAR\)|g\(VARCHAR\)|
    |------------|------------|------------|------------|------------|------------|------------|
    |1|123|2|11.4445|3|asd|null|

-   测试语句

    ```language-sql
    SELECT 
    IS_DECIMAL(a) as boo1,
    IS_DECIMAL(b) as boo2,
    IS_DECIMAL(c) as boo3,
    IS_DECIMAL(d) as boo4,
    IS_DECIMAL(e) as boo5,
    IS_DECIMAL(f) as boo6,
    IS_DECIMAL(g) as boo7
    FROM T1
    
    ```

-   测试结果

    |boo1\(BOOLEAN\)|boo2\(BOOLEAN\)|boo3\(BOOLEAN\)|boo4\(BOOLEAN\)|boo5\(BOOLEAN\)|boo6\(BOOLEAN\)|boo7\(BOOLEAN\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|---------------|
    |true|true|true|true|true|false|false|


