# NOT BETWEEN AND {#concept_62828_zh .concept}

本文为您介绍如何使用实时计算逻辑运算函数NOT BETWEEN AND。

## 语法 {#section_mnm_4dw_cgb .section}

```language-sql
A NOT BETWEEN B AND C
			
```

## 入参 {#section_qvx_tdw_cgb .section}

|参数|数据类型|
|--|----|
|A|DOUBLE、BIGINT、INT、VARCHAR、DATE、TIMESTAMP、TIME|
|B|DOUBLE、BIGINT、INT、VARCHAR、DATE、TIMESTAMP、TIME|
|C|DOUBLE、BIGINT、INT、VARCHAR、DATE、TIMESTAMP、TIME|

## 功能描述 {#section_cl2_v2w_cgb .section}

`NOT BETWEEN AND`操作符用于选取不存在与两个值之间的数据范围内的值。

## 示例1 {#section_qbd_hbp_dgb .section}

-   测试数据

    |int1\(INT\)|int2\(INT\)|int3\(INT\)|
    |-----------|-----------|-----------|
    |90|97|80|
    |11|10|7|

-   测试语句

    ```
    SELECT int1 as aa
    FROM T1
    WHERE int1 NOT BETWEEN int2 AND int3;
    					
    ```

-   测试结果

    |aa\(int\)|
    |---------|
    |11|


## 示例2 {#section_ekm_zdw_cgb .section}

-   测试数据

    |var1\(varchar\)|var2\(varchar\)|var3\(varchar\)|
    |---------------|---------------|---------------|
    |d|a|c|

-   测试语句

    ```
    SELECT int1 as aa
    FROM T1
    WHERE var1 NOT BETWEEN var2 AND var3;
    					
    ```

-   测试结果

    |aa\(varchar\)|
    |-------------|
    |d|


## 示例3 {#section_d31_wcp_dgb .section}

-   测试数据

    |TIMESTAMP1\(TIMESTAMP\)|TIMESTAMP2\(TIMESTAMP\)|TIMESTAMP3\(TIMESTAMP\)|
    |-----------------------|-----------------------|-----------------------|
    |1969-07-20 20:17:30|1969-07-20 20:17:40|1969-07-20 20:17:45|

-   测试语句

    ```
    SELECT TIMESTAMP1 as aa
    FROM T1
    WHERE TIMESTAMP1 NOT BETWEEN TIMESTAMP2 AND TIMESTAMP3;
    					
    ```

-   测试结果

    |aa\(TIMESTAMP\)|
    |---------------|
    |1969-07-20 20:17:30|


