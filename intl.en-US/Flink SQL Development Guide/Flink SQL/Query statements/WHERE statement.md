# WHERE statement {#concept_62502_zh .concept}

A WHERE statement can be used to filter data generated from a SELECT statement.

## Syntax {#section_ozy_b44_cgb .section}

```language-sql
SELECT [ ALL | DISTINCT ]
{ * | projectItem [, projectItem ]* }
FROM tableExpression
[ WHERE booleanExpression ];
```

The following table describes the operators can be used in a WHERE statement.

|Operator|Description|
|--------|-----------|
|=|Equal to|
|<\>|Not equal to|
|\>|Greater than|
|\>=|Greater than or equal to|
|<|Smaller than|
|<=|Smaller than or equal to|

## Example {#section_hvw_wq4_cgb .section}

-   Test data

    |Address|City|
    |-------|----|
    |Oxford Street|Beijing|
    |Fifth Avenue|Beijing|
    |Changan Street|Shanghai|

-   Test statement

    ```language-SQL
    SELECT * FROM table_a WHERE City='Beijing'
    ```

-   Test result

    |Address|City|
    |-------|----|
    |Oxford Street|Beijing|
    |Fifth Avenue|Beijing|


