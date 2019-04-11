# NOW {#concept_q4l_dvq_dgb .concept}

本文为您介绍如何使用实时计算日期函数NOW。

## 语法 {#section_dks_qgp_dgb .section}

```
BIGINT NOW()

```

## 入参 {#section_eks_qgp_dgb .section}

未指定参数时为当前系统时间的秒数。

## 功能描述 {#section_hks_qgp_dgb .section}

返回当前时区时间的时间戳，单位为秒。可在括号内输入整型参数作为偏移值（单位：秒），返回偏移后的时间戳。例如，`now(100)`返回当前时间戳加100秒的时间戳。

## 示例 {#section_iks_qgp_dgb .section}

-   测试数据

    |b\(VARCHAR\)|
    |------------|
    |null|

-   测试语句

    ```language-sql
    SELECT 
     NOW() as big1,
     NOW(100) as big2,
     NOW(b) as big3
    FROM T1
    
    ```

-   测试结果

    |big1\(BIGINT\)|big2\(BIGINT\)|big3\(BIGINT\)|
    |--------------|--------------|--------------|
    |1403006911|1403007011|null|


