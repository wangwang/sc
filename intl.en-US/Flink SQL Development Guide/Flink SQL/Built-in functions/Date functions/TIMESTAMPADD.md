# TIMESTAMPADD {#concept_eq5_vvq_dgb .concept}

This topic describes how to use the date function TIMESTAMPADD in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
TIMESTAMP TIMESTAMPADD(interval,INT int_expr,TIMESTAMP datetime_expr)
DATE TIMESTAMPADD(interval,INT int_expr,DATE datetime_expr)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|interval|VARCHAR|
|int\_expr|INT|
|datetime\_expr|TIMESTAMP or DATE|

**Note:** 

The following table lists the valid units of interval.

|Unit of interval|Description|
|----------------|-----------|
|FRAC\_SECOND|Millisecond|
|SECOND|Second|
|MINUTE|Minute|
|HOUR|Hour|
|DAY|Day|
|WEEK|Week|
|MONTH|Month|
|QUARTER|Quarter|
|YEAR|Year|

## Function description {#section_hks_qgp_dgb .section}

This function adds the integer expression int\_expr to the date or datetime expression datetime\_expr, and returns the current time of the TIME type in the session time zone. The data type of the return value of this function is the same as that of datetime\_expr.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(TIMESTAMP\)|b\(DATE\)|
    |--------------|---------|
    |2018-07-09 10:23:56|1990-02-20|

-   Test statements

    ```language-sql
    SELECT 
    TIMESTAMPADD(HOUR,3,a) AS `result1`
    TIMESTAMPADD(DAY,3,b) AS `result2`
    FROM T1				
    ```

-   Test results

    |result1\(TIMESTAMP\)|result2\(DATE\)|
    |--------------------|---------------|
    |2018-07-09 13:23:56.0|1990-02-23|


