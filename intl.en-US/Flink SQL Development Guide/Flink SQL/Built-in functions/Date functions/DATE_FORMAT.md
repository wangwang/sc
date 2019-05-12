# DATE\_FORMAT {#concept_qt5_kpq_dgb .concept}

This topic describes how to use the date function DATE\_FORMAT in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
VARCHAR DATE_FORMAT(TIMESTAMP time, VARCHAR to_format)
VARCHAR DATE_FORMAT(VARCHAR date, VARCHAR to_format)
VARCHAR DATE_FORMAT(VARCHAR date, VARCHAR from_format, VARCHAR to_format)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|date|VARCHAR **Note:** The default date format is yyyy-MM-dd HH:mm:ss.

 |
|time|TIMESTAMP|
|from\_format|VARCHAR|
|to\_format|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function converts a VARCHAR type date from the source format to the target format. The time or date parameter specifies the source string. The from\_format parameter is optional. It specifies the source format of the date. The default format is yyyy-MM-dd hh:mm:ss. The to\_format parameter specifies the target format of the date. The return value is a VARCHAR type date in the target format. If any input parameter is NULL or a parsing error occurs, the return value is NULL.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |date1\(VARCHAR\)|datetime1\(VARCHAR\)|nullstr\(VARCHAR\)|
    |----------------|--------------------|------------------|
    |0915-2017|2017-09-15 00:00:00|null|

-   Test statements

    ```language-sql
    SELECT DATE_FORMAT(datetime1, 'yyMMdd') as var1,
     DATE_FORMAT(nullstr, 'yyMMdd') as var2,
     DATE_FORMAT(datetime1, nullstr) as var3,
     DATE_FORMAT(date1, 'MMdd-yyyy', nullstr) as var4,
     DATE_FORMAT(date1, 'MMdd-yyyy', 'yyyyMMdd') as var5,
     DATE_FORMAT(TIMESTAMP '2017-09-15 23:00:00', 'yyMMdd') as var6
    FROM T1
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|var4\(VARCHAR\)|var5\(VARCHAR\)|var6\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|---------------|---------------|
    |170915|null|null|null|20170915|170915|


