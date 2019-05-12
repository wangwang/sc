# TO\_DATE {#concept_egj_sxq_dgb .concept}

This topic describes how to use the date function TO\_DATE in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
Date TO_DATE(INT time)
Date TO_DATE(VARCHAR date)
Date TO_DATE(VARCHAR date, VARCHAR format)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|time|INT **Note:** This parameter specifies the number of days that have elapsed since 00:00:00 Thursday, 1 January, 1970.

 |
|date|VARCHAR **Note:** The default format is yyyy-MM-dd.

 |
|format|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function converts a date of the INT or VARCHAR type to a date of the DATE type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |date1\(INT\)|date2\(VARCHAR\)|date3\(VARCHAR\)|
    |------------|----------------|----------------|
    |100|2017-09-15|20170915|

-   Test statements

    ```language-sql
    SELECT TO_DATE(date1) as var1,
     TO_DATE(date2) as var2,
     TO_DATE(date3,'yyyy-MM-dd') as var3
    FROM T1
    					
    ```

-   Test results

    |var1\(DATE\)|var2\(DATE\)|var3\(DATE\)|
    |------------|------------|------------|
    |1970-04-11|2017-09-15|2017-09-15|


