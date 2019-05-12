# TO\_TIMESTAMP {#concept_ibw_kyq_dgb .concept}

This topic describes how to use the date function TO\_TIMESTAMP in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
TIMESTAMP TO_TIMESTAMP(BIGINT time)
TIMESTAMP TO_TIMESTAMP(VARCHAR date)
TIMESTAMP TO_TIMESTAMP(VARCHAR date, VARCHAR format)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|time|BIGINT **Note:** The unit is millisecond.

 |
|date|VARCHAR **Note:** The default format is yyyy-MM-dd HH:mm:ss\[.SSS\]. \[DO NOT TRANSLATE\]

 |
|format|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function converts a date of the BIGINT or VARCHAR type to a date of the TIMESTAMP type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |timestamp1\(bigint\)|timestamp2\(VARCHAR\)|timestamp3\(VARCHAR\)|
    |--------------------|---------------------|---------------------|
    |1513135677000|2017-09-15 00:00:00|20170915000000|

-   Test statements

    ```language-sql
    SELECT TO_TIMESTAMP(timestamp1) as var1,
     TO_TIMESTAMP(timestamp2) as var2,
     TO_TIMESTAMP(timestamp3, 'yyyyMMddHHmmss') as var3
    FROM T1
    ```

-   Test results

    |var1\(TIMESTAMP\)|var2\(TIMESTAMP\)|var3\(TIMESTAMP\)|
    |-----------------|-----------------|-----------------|
    |2017-12-13 03:27:57.0|2017-09-15 00:00:00.0|2017-09-15 00:00:00.0|


