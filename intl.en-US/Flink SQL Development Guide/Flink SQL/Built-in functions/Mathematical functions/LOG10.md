# LOG10 {#concept_mn3_jhq_dgb .concept}

This topic describes how to use the mathematical function LOG10 in Realtime Compute.

## Syntax {#section_w53_khq_dgb .section}

```
DOUBLE LOG10(DOUBLE x)
			
```

## Input parameters {#section_x53_khq_dgb .section}

|Parameter|Data type|
|---------|---------|
|x|DOUBLE|

## Function description {#section_z53_khq_dgb .section}

This function returns the base-10 logarithm of x. If x is NULL, the return value is NULL. If x is negative, an exception occurs.

## Examples {#section_av3_khq_dgb .section}

-   Test data

    |id\(INT\)|X\(INT\)|
    |---------|--------|
    |1|100|
    |2|10|

-   Test statements

    ```
    SELECT id, log10(x) as dou1
    FROM T1
    ```

-   Test results

    |id\(INT\)|dou1\(DOUBLE\)|
    |---------|--------------|
    |1|2.0|
    |2|1.0|


