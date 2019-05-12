# LAST\_VALUE {#concept_xnc_1cs_dgb .concept}

This topic describes how to use the aggregate function LAST\_VALUE in Realtime Compute. In Flink SQL, the LAST\_VALUE function returns the last non-null record of a data stream.

## Syntax {#section_dks_qgp_dgb .section}

```
T LAST_VALUE(T value)
T LAST_VALUE(T value, Long order)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|value|Any data type \(The input parameters must be of the same type.\)|
|order|INT|

## Function description {#section_hks_qgp_dgb .section}

This function returns the last non-null record of a data stream. A record with the greatest order value is obtained as the last non-null record.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |a\(BIGINT\)|b\(INT\)|c\(VARCHAR\)|
    |-----------|--------|------------|
    |1L|1|"Hello"|
    |2L|2|"Hello"|
    |3L|3|"Hello"|
    |4L|4|"Hello"|
    |5L|5|"Hello"|
    |6L|6|"Hello"|
    |7L|7|"Hello World"|
    |8L|8|"Hello World"|
    |20L|20|"Hello World"|

-   Test statements

    ```language-sql
    SELECT c,
     last_value(b) 
    OVER (
    PARTITION BY c 
    ORDER BY PROCTIME() RANGE UNBOUNDED preceding
    ) as var1
    from T1
    					
    ```

-   Test results

    |c\(VARCHAR\)|var1\(INT\)|
    |------------|-----------|
    |Hello|1|
    |Hello|2|
    |Hello|3|
    |Hello|4|
    |Hello|5|
    |Hello|6|
    |Hello World|7|
    |Hello World|8|
    |Hello World|20|


