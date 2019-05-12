# CASE WHEN {#concept_62764_zh .concept}

This topic describes how to use the conditional function CASE WHEN in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
CASE WHEN a THEN b [WHEN c THEN d]* [ELSE e] END

```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|a|BOOLEAN|
|b|BOOLEAN|
|c|BOOLEAN|
|d|BOOLEAN|
|e|BOOLEAN|

## Function description {#section_hks_qgp_dgb .section}

If a is true, this function returns b. If a is false and c is true, this function returns d. If both a and c are false, this function returns e.

## Examples {#section_iks_qgp_dgb .section}

**Note:** 

When the CASE WHEN function returns a constant string, it pads spaces to the right-side of the string. In the following example, when the else condition is met, the return value is 'ios' followed by several spaces.

```
case when device_type = 'android' 
then 'android' 
else 'ios'
end as os
```

You can resolve this issue in the following two ways:

-   Use the TRIM function to remove spaces. For the preceding example, use trim\(os\).
-   Use the CAST function to convert a constant string to a string of the VARCHAR type.

-   Test data

    |device\_type\(VARCHAR\)|
    |-----------------------|
    |android|
    |ios|
    |win|

-   Test statement 1 \(using the TRIM function\)

```language-sql
SELECT 
   trim(os), // The trim() function is used here. 
   CHAR_LENGTH(trim(os)) // The trim() function is used here.
from(
   SELECT
     case when device_type = 'android'
     then 'android'
     else 'ios' 
end as os 
FROM T1
);
```

    Test statement 2 \(using the CAST function\)

    ```language-sql
    SELECT
     os, 
    CHAR_LENGTH(os) 
    from
    (SELECT 
     case when device_type = 'android'
     then cast('android' as varchar) // The CAST function is used here. 
     else cast('ios' as varchar) // The CAST function is used here. 
    end as os 
    FROM T1
    );
    ```

-   Test results

    |os\(VARCHAR\)|length\(INT\)|
    |-------------|-------------|
    |android|7|
    |ios|3|
    |ios|3|


