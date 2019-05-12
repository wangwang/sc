# STR\_TO\_MAP {#concept_66820_zh .concept}

This topic describes how to use the string function STR\_TO\_MAP in Realtime Compute.

## Syntax {#section_sp3_rfq_dgb .section}

```
MAP STR_TO_MAP(VARCHAR text)
MAP STR_TO_MAP(VARCHAR text, VARCHAR listDelimiter, VARCHAR keyValueDelimiter)

```

## Function description {#section_nfl_qfq_dgb .section}

This function first uses the separator specified by listDelimiter to split the given text into key-value pairs. Then, this function uses the separator specified by keyValueDelimiter to separate the key and value in each key-value pair. Finally, this function assembles and returns a MAP. The default value of listDelimiter is a comma \(,\). The default value of keyValueDelimiter is an equal sign \(=\).

## Input parameters {#section_qw1_qfq_dgb .section}

|Parameter|Data type|Description|
|---------|---------|-----------|
|text|VARCHAR|The input text.|
|listDelimiter|VARCHAR|The separator between key-value pairs in the input text. The default value is a comma \(,\).|
|keyValueDelimiter|VARCHAR|The separator between the key and value in each key-value pair. The default value is an equal sign \(=\).|

**Note:** The listDelimiter and keyValueDelimiter parameters are defined by Java regular expressions. If a special character is used, it needs to be escaped.

## Test statements {#section_nst_kgq_dgb .section}

```
SELECT
  STR_TO_MAP('k1=v1,k2=v2')['k1'] as a
FROM T1
```

## Test results {#section_d2s_lgq_dgb .section}

|a\(VARCHAR\)|
|------------|
|v1|

