# DATE\_SUB {#concept_kll_dqq_dgb .concept}

This topic describes how to use the date function DATE\_SUB in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
VARCHAR DATE_SUB(VARCHAR startdate, INT days)
VARCHAR DATE_SUB(TIMESTAMP time, INT days)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|startdate|VARCHAR **Note:** The format of a VARCHAR type date is yyyy-MM-dd or yyyy-MM-dd HH:mm:ss.

 |
|time|TIMESTAMP|
|days|INT|

## Function description {#section_hks_qgp_dgb .section}

This function subtracts an interval \(specified by days\) from the specified date and returns a new date. The return value is a VARCHAR type date in yyyy-MM-dd format. If any input parameter is NULL or a parsing error occurs, the return value is NULL.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |date1\(VARCHAR\)|nullstr\(VARCHAR\)|
    |----------------|------------------|
    |2017-10-15|null|

-   Test statements

    ```
    SELECT DATE_SUB(date1, 30) as var1,
     DATE_SUB(TIMESTAMP '2017-10-15 23:00:00',30) as var2,
     DATE_SUB(nullstr,30) as var3
    FROM T1
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|
    |---------------|---------------|---------------|
    |2017-09-15|2017-09-15|null|


