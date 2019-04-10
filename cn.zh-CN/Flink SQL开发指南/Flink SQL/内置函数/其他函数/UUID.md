# UUID {#concept_pb2_llx_dgb .concept}

本文为您介绍如何使用实时计算UUID。Flink SQL中使用UUID函数返回通用唯一标识字符。

## 语法 {#section_dks_qgp_dgb .section}

```
VARCHAR UUID()

```

## 功能描述 {#section_hks_qgp_dgb .section}

返回通用唯一标识字符。

## 示例 {#section_iks_qgp_dgb .section}

-   测试语句

    ```language-sql
    SELECT uuid() as `result`
    FROM T1
    
    ```

-   测试结果

    |result\(VARCHAR\)|
    |-----------------|
    |a364e414-e68b-4e5c-9166-65b3a153e257|


