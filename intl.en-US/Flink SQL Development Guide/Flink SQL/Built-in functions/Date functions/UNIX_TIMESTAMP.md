# UNIX\_TIMESTAMP {#concept_xzs_wyq_dgb .concept}

This topic describes how to use the date function UNIX\_TIMESTAMP in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```language-sql
BIGINT UNIX_TIMESTAMP()
BIGINT UNIX_TIMESTAMP(VARCHAR date)
BIGINT UNIX_TIMESTAMP(TIMESTAMP timestamp)
BIGINT UNIX_TIMESTAMP(VARCHAR date, VARCHAR format)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|timestamp|TIMESTAMP|
|date|VARCHAR **Note:** The default date format is `yyyy-MM-dd HH:mm:ss`.

 |
|format|VARCHAR **Note:** The default format is `yyyy-MM-dd hh:mm:ss`.

 |

## Function description {#section_hks_qgp_dgb .section}

This function converts the specified date to a UNIX timestamp \(in seconds\) of the BIGINT type. If no input parameter is specified, the UNIX timestamp \(in seconds\) of the current time is returned. In this case, this function has the same semantics as NOW. If any input parameter is NULL or a parsing error occurs, the return value is NULL.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |nullstr\(VARCHAR\)|
    |------------------|
    |null|

-   Test statements

    ```language-sql
    SELECT UNIX_TIMESTAMP() as big1,
           UNIX_TIMESTAMP(nullstr) as big2
    FROM T1
    ```

-   Test results

    |big1\(BIGINT\)|big2\(BIGINT\)|
    |--------------|--------------|
    |1403006911|null|


