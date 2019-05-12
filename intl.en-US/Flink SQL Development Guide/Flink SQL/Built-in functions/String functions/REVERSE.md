# REVERSE {#concept_62543_zh .concept}

This topic describes how to use the string function REVERSE in Realtime Compute.

## Syntax {#section_rsf_k1q_dgb .section}

```language-sql
VARCHAR REVERSE(VARCHAR str)

```

## Input parameters {#REVERSE_OG_01 .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|str|VARCHAR|The string.|

## Function description {#REVERSE_OG_02 .section}

This function returns a string in the reverse order of the specified string. If any input parameter is NULL, the return value is NULL.

## Examples {#REVERSE_OG_03 .section}

-   Test data

    |str1\(VARCHAR\)|str2\(VARCHAR\)|str3\(VARCHAR\)|str4\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|
    |iPhoneX|Alibaba|World|null|

-   Test statements

    ```language-sql
    SELECT REVERSE(str1) as var1,REVERSE(str2) as var2,
            REVERSE(str3) as var3,REVERSE(str4) as var4
    FROM T1
    
    ```

-   Test results

    |var1\(VARCHAR\)|var2\(VARCHAR\)|var3\(VARCHAR\)|var4\(VARCHAR\)|
    |---------------|---------------|---------------|---------------|
    |XenohPi|ababilA|dlroW|null|


