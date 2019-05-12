# OVERLAY {#concept_74514_zh .concept}

This topic describes how to use the string function OVERLAY in Realtime Compute.

## Syntax {#section_dkq_gxq_dgb .section}

```language-sql
VARCHAR OVERLAY ( (VARCHAR x PLACING VARCHAR y FROM INT start_position [ FOR INT length ]) )

```

## Input parameters {#OVERLAY_OG_01 .section}

|Parameter|Data type|
|---------|---------|
|x|VARCHAR|
|y|VARCHAR|
|start\_position|INT|
|length \(optional\)|INT|

## Function description {#OVERLAY_OG_02 .section}

This function replaces a substring of x with y. The replacement starts from the character position specified by start\_position. The total number of characters are to be replaced is the length value plus one.

## Examples {#OVERLAY_OG_03 .section}

-   Test statements

    ```language-sql
    OVERLAY('abcdefg' PLACING 'hij' FROM 2 FOR 2) as result
    FROM T1
    
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |ahijdefg|


