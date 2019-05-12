# MONTH {#concept_zrt_r5q_dgb .concept}

This topic describes how to use the date function MONTH in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BIGINT MONTH(TIMESTAMP timestamp) 
BIGINT MONTH(DATE date)

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|time|TIME|
|timestamp|TIMESTAMP|

## Function description {#section_hks_qgp_dgb .section}

This function returns the month in the specified time value as a number. The return value ranges from 1 to 12.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |datetime1\(VARCHAR\)|time1\(VARCHAR\)|time2\(TIME\)|timestamp1\(TIMESTAMP\)|
    |--------------------|----------------|-------------|-----------------------|
    |2017-10-15 11:12:13|22:23:24|22:23:24|2017-10-15 11:12:13|

-   Test statements

    ```language-sql
    SELECT MONTH(TIMESTAMP '2016-09-15 00:00:00') as int1,
     MONTH(DATE '2017-09-22') as int2,
     MONTH(tdate) as int3,
     MONTH(ts) as int4,
     MONTH(CAST(dateStr AS DATE)) as int5,
     MONTH(CAST(tsStr AS TIMESTAMP)) as int6
    FROM T1
    
    ```

-   Test results

    |int1\(BIGINT\)|int2\(BIGINT\)|int3\(BIGINT\)|int4\(BIGINT\)|int5\(BIGINT\)|int6\(BIGINT\)|
    |--------------|--------------|--------------|--------------|--------------|--------------|
    |9|9|11|10|9|10|


