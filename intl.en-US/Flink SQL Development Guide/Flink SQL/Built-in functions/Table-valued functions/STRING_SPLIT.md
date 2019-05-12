# STRING\_SPLIT {#concept_tsw_kwr_dgb .concept}

This topic describes how to use the table-valued function STRING\_SPLIT in Realtime Compute.

## Syntax {#section_dks_qgp_dgb .section}

```language-sql
string_split(varchar string, varchar separator)
```

## Input parameters {#section_eks_qgp_dgb .section}

|Parameter|Data type|
|---------|---------|
|string|VARCHAR|
|separator|VARCHAR|

## Function description {#section_hks_qgp_dgb .section}

This function splits a string into several substrings based on a separator.

## Examples {#section_iks_qgp_dgb .section}

-   Test data

    |d\(varchar\)|s\(varchar\)|
    |------------|------------|
    |abc-bcd|-|
    |hhh|-|

-   Test statements

    ```language-sql
    select d, v 
    from T1, 
    lateral table(string_split(d, s)) as T(v)
    ```

-   Test results

    |d\(varchar\)|v\(varchar\)|
    |------------|------------|
    |abc-bcd|abc|
    |abc-bcd|bcd|
    |hhh|hhh|

    **Note:** Currently, the separator must be a single character.


