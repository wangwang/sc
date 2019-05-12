# GROUP BY statement {#concept_62503_zh .concept}

A GROUP BY statement groups a result set by one or more columns.

## Syntax {#section_tmz_dt4_cgb .section}

```language-sql
SELECT [ DISTINCT ]
{ * | projectItem [, projectItem ]* }
FROM tableExpression
[ GROUP BY { groupItem [, groupItem ]* } ];

```

## Example {#section_xq5_gt4_cgb .section}

-   Test data

    |Customer|OrderPrice|
    |--------|----------|
    |Bush|1000|
    |Carter|1600|
    |Bush|700|
    |Bush|300|
    |Adams|2000|
    |Carter|100|

-   Test statement

    ```language-SQL
    SELECT Customer,SUM(OrderPrice) FROM xxx
    GROUP BY Customer;
    
    ```

-   Test result

    |Customer|SUM\(OrderPrice\)|
    |--------|-----------------|
    |Bush|2000|
    |Carter|1700|
    |Adams|2000|


