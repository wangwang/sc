# UUID {#concept_pb2_llx_dgb .concept}

This topic describes how to use the UUID function in Realtime Compute. In Flink SQL, the UUID function returns a universally unique identifier.

## Syntax {#section_dks_qgp_dgb .section}

```
VARCHAR UUID()
```

## Function description {#section_hks_qgp_dgb .section}

This function returns a universally unique identifier.

## Examples {#section_iks_qgp_dgb .section}

-   Test statements

    ```language-sql
    SELECT uuid() as `result`
    FROM T1
    ```

-   Test results

    |result\(VARCHAR\)|
    |-----------------|
    |a364e414-e68b-4e5c-9166-65b3a153e257|


