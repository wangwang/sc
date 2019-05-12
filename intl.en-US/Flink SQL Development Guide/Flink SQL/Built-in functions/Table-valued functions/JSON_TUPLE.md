# JSON\_TUPLE {#concept_bcs_pvr_dgb .concept}

This topic describes how to use the table-valued function JSON\_TUPLE in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
JSON_TUPLE(str, path1, path2 ..., pathN)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The JSON string.|
|path1 to pathN|VARCHAR|The path string, which does not start with special characters such as a dollar sign \($\) or a period \(.\).``|

## Function description {#section_hks_qgp_dgb .section}

This function returns the value represented by each path string from the JSON string.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |d\(VARCHAR\)|s\(VARCHAR\)|
    |------------|------------|
    |\{"qwe":"asd","qwe2":"asd2","qwe3":"asd3"\}|qwe3|
    |\{"qwe":"asd4","qwe2":"asd5","qwe3":"asd3"\}|qwe2|

-   Test statements

    ```language-sql
    SELECT d, v 
    FROM T1, lateral table(JSON_TUPLE(d, 'qwe', s))
     as T(v)
    					
    ```

-   Test results

    |d\(VARCHAR\)|v\(VARCHAR\)|
    |------------|------------|
    |\{"qwe":"asd","qwe2":"asd2","qwe3":"asd3"\}|asd|
    |\{"qwe":"asd","qwe2":"asd2","qwe3":"asd3"\}|asd3|
    |\{"qwe":"asd4","qwe2":"asd5","qwe3":"asd3"\}|asd4|
    |\{"qwe":"asd4","qwe2":"asd5","qwe3":"asd3"\}|asd5|


