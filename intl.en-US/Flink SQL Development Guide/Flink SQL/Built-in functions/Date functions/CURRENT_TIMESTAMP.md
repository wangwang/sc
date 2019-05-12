# CURRENT\_TIMESTAMP {#concept_ul5_hnq_dgb .concept}

This topic describes how to use the date function CURRENT\_TIMESTAMP in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
TIMESTAMP CURRENT_TIMESTAMP

```

## Function description {#section_hks_qgp_dgb .section}

This function returns the current UTC timestamp.

## Examples {#section_iks_qgp_dgb .section}

-   Test statements

    ```
    SELECT CURRENT_TIMESTAMP as var1
    FROM T1
    
    ```

-   Test results

    |var1\(TIMESTAMP\)|
    |-----------------|
    |2007-04-30 13:10:02.047|


