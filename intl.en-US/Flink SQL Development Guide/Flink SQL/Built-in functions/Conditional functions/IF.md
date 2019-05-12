# IF {#concept_wdg_2tr_dgb .concept}

This topic describes how to use the conditional function IF in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```
T IF(BOOLEAN testCondition, T valueTrue, T valueFalseOrNull)
			
```

**Note:** T represents a return value of any type.

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|testCondition|BOOLEAN|
|valueTrue|Any data type \(The valueTrue and valueFalseOrNull parameters must be of the same type.\)|
|valueFalseOrNull|Any data type \(The valueTrue and valueFalseOrNull parameters must be of the same type.\)|

## Function description {#section_hks_qgp_dgb .section}

This function uses the BOOLEAN value of testCondition as the judgment criterion. If testCondition is true, this function returns valueTrue. If testCondition is false, this function returns valueFalseOrNull. If testCondition is NULL, it is also regarded as false and this function returns valueFalseOrNull. If any other parameter is NULL, this function works based on normal semantics. The data type of the return value is determined by T.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |int1\(INT\)|int2\(INT\)|str1\(VARCHAR\)|str2\(VARCHAR\)|
    |-----------|-----------|---------------|---------------|
    |1|2|Jack|Harry|
    |1|2|Jack|null|
    |1|2|null|Harry|

-   Test statements

    ```language-sql
    SELECT IF(int1 < int2,str1, str2) as int1
    FROM T1
    ```

-   Test results

    |int1\(VARCHAR\)|
    |---------------|
    |Jack|
    |Jack|
    |null|


