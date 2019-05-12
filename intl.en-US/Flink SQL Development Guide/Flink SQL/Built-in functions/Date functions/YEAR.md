# YEAR {#concept_ab3_d1r_dgb .concept}

This topic describes how to use the date function YEAR in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BIGINT YEAR(TIMESTAMP timestamp)
BIGINT YEAR(DATE date)
			
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|date|DATE|
|timestamp|TIMESTAMP|

## Function description {#section_hks_qgp_dgb .section}

This function returns the year in the specified time value.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |tsStr\(VARCHAR\)|dateStr\(VARCHAR\)|tdate\(DATE\)|ts\(TIMESTAMP\)|
    |----------------|------------------|-------------|---------------|
    |2017-10-15 00:00:00|2017-09-15|2017-11-10|2017-10-15 00:00:00|

-   Test statements

    ```language-sql
    SELECT YEAR(TIMESTAMP '2016-09-15 00:00:00') as int1,
     YEAR(DATE '2017-09-22') as int2,
     YEAR(tdate) as int3,
     YEAR(ts) as int4,
     YEAR(CAST(dateStr AS DATE)) as int5,
     YEAR(CAST(tsStr AS TIMESTAMP)) as int6
    FROM T1
    					
    ```

-   Test results

    |int1\(BIGINT\)|int2\(BIGINT\)|int3\(BIGINT\)|int4\(BIGINT\)|int5\(BIGINT\)|int6\(BIGINT\)|
    |--------------|--------------|--------------|--------------|--------------|--------------|
    |2016|2017|2017|2017|2015|2017|


