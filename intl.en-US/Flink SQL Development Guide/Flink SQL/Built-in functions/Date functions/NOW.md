# NOW {#concept_q4l_dvq_dgb .concept}

This topic describes how to use the date function NOW in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
BIGINT NOW()
			
```

## Input parameters {#section_eks_qgp_dgb .section}

If no input parameter is specified, the UNIX timestamp \(in seconds\) of the current system time is returned.

## Function description {#section_hks_qgp_dgb .section}

This function returns the UNIX timestamp \(in seconds\) in the current time zone. You can specify an INT type parameter as an offset \(in seconds\) and add the offset to the current timestamp to return a value. For example, the NOW\(100\) function adds 100 seconds to the current timestamp and returns a value of the BIGINT type.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |b\(VARCHAR\)|
    |------------|
    |null|

-   Test statements

    ```language-sql
    SELECT 
     NOW() as big1,
     NOW(b) as big2
    FROM T1
    					
    ```

-   Test results

    |big1\(BIGINT\)|big2\(BIGINT\)|
    |--------------|--------------|
    |1403006911|null|


