# FIRST\_VALUE {#concept_o2q_hzr_dgb .concept}

本文为您介绍如何使用实时计算聚合函数FIRST\_VALUE。Flink SQL中使用FIRST\_VALUE函数返回数据流的第一条非null数据。

## 语法 {#section_dks_qgp_dgb .section}

```
T FIRST_VALUE( T value )
T FIRST_VALUE( T value, Long order )

```

## 入参 {#section_eks_qgp_dgb .section}

|参数|数据类型|
|--|----|
|value|任意参数类型，但输入参数只能为同一种类型。|
|order|INT|

## 功能描述 {#section_hks_qgp_dgb .section}

获取数据流的第一条非null数据。根据order来决定FIRST\_VALUE是哪行，取order值最小的记录作为FIRST\_VALUE。

-   
## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |a\(BIGINT\)|b\(INT\)|c\(VARCHAR\)|
    |-----------|--------|------------|
    |1L|1|“Hello”|
    |2L|2|“Hello”|
    |3L|3|“Hello”|
    |4L|4|“Hello”|
    |5L|5|“Hello”|
    |6L|6|“Hello”|
    |7L|7|“Hello World”|
    |8L|8|“Hello World”|
    |20L|20|“Hello World”|

-   测试语句

    ```language-sql
    SELECT c,
     first_value(b) 
    OVER (
    PARTITION BY c 
    ORDER BY PROCTIME() RANGE UNBOUNDED preceding
    ) as var1
    from T1
    
    ```

-   测试结果

    |c\(VARCHAR\)|var1\(INT\)|
    |------------|-----------|
    |Hello|1|
    |Hello|1|
    |Hello|1|
    |Hello|1|
    |Hello|1|
    |Hello|1|
    |Hello World|7|
    |Hello World|7|
    |Hello World|7|


