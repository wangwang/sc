# LOCALTIME {#concept_pdb_25q_dgb .concept}

This topic describes how to use the date function LOCALTIME in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
TIME LOCALTIME
```

## Function description {#section_hks_qgp_dgb .section}

This function returns the current time of the TIME type in the session time zone. You can use LOCALTIME as a variable.

## Examples {#section_iks_qgp_dgb .section}

-   Test statements

    ```
    SELECT LOCALTIME as `result`
    FROM T1
    ```

-   Test results

    |result\(TIME\)|
    |--------------|
    |19:00:47|


