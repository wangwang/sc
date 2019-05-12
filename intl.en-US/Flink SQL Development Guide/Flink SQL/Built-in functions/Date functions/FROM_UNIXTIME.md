# FROM\_UNIXTIME {#concept_otj_bsq_dgb .concept}

This topic describes how to use the date function FROM\_UNIXTIME in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
VARCHAR FROM_UNIXTIME(BIGINT unixtime[, VARCHAR format])
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|unixtime|BIGINT|
|format|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

-   This function converts the timestamp \(in seconds\) specified by unixtime to a VARCHAR type date in the specified date format. The default format is yyyy-MM-dd HH:mm:ss.
-   If any input parameter is NULL or a parsing error occurs, the return value is NULL.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |unixtime1\(INT\)|nullstr\(VARCHAR\)|
    |----------------|------------------|
    |1505404800|null|

-   Test statements

    ```language-sql
    SELECT FROM_UNIXTIME(unixtime1) as var1, 
     FROM_UNIXTIME(unixtime1,'MMdd-yyyy') as var2,
     FROM_UNIXTIME(unixtime1,nullstr) as var3
    FROM T1
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|
    |---------------|---------------|---------------|
    |2017-10-15|2017-10-15|null|


