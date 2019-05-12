# HOUR {#concept_dt2_5tq_dgb .concept}

This topic describes how to use the date function HOUR in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BIGINT HOUR(TIME time)
BIGINT HOUR(TIMESTAMP timestamp)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|time|TIME|
|timestamp|TIMESTAMP|

## Function description {#section_hks_qgp_dgb .section}

This function returns the hours \(in 24-hour format\) in the specified time or timestamp value as a number. The return value ranges from 0 to 23.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |datetime1\(VARCHAR\)|time1\(VARCHAR\)|time2\(TIME\)|timestamp1\(TIMESTAMP\)|
    |--------------------|----------------|-------------|-----------------------|
    |2017-10-15 11:12:13|22:23:24|22:23:24|2017-10-15 11:12:13|

-   Test statements

    ```language-sql
    SELECT HOUR(TIMESTAMP '2016-09-20 23:33:33') as int1,
     HOUR(TIME '23:30:33') as int2,
     HOUR(time2) as int3,
     HOUR(timestamp1) as int4,
     HOUR(CAST(time1 AS TIME)) as int5,
     HOUR(CAST(datetime1 AS TIMESTAMP)) as int6
    FROM T1
    ```

-   Test results

    |int1\(BIGINT\)|int2\(BIGINT\)|int3\(BIGINT\)|int4\(BIGINT\)|int5\(BIGINT\)|int6\(BIGINT\)|
    |--------------|--------------|--------------|--------------|--------------|--------------|
    |23|23|22|11|22|11|


