# UDF {#concept_69472_zh .concept}

This topic describes how to build the development environment, write business code, and publish a user defined function \(UDF\) for Realtime Compute.

**Note:** Currently, Realtime Compute does not support UDXs in shared mode. UDXs are supported only in exclusive mode.

## Definition {#section_qrh_dpx_dgb .section}

A UDF maps zero, one, or multiple scalar values to a new scalar value.

## Build the development environment {#section_ikd_3px_dgb .section}

For more information, see [Build the development environment](intl.en-US/Flink SQL Development Guide/Flink SQL/UDX/UDX overview.md#section_ck2_gcm_cgb).

## Write business logic code {#section_hsh_jpx_dgb .section}

A UDF needs to implement the `eval` method in the ScalarFunction class. The `open` and `close` methods are optional. The following sample code is written in Java:

```language-java
package com.hjc.test.blink.sql.udx;


import org.apache.flink.table.functions.FunctionContext;
import org.apache.flink.table.functions.ScalarFunction;

public class StringLengthUdf extends ScalarFunction {
    // The open method is optional.
    // To write the open method, you must import org.apache.flink.table.functions.FunctionContext.
    @Override
    public void open(FunctionContext context) {
        }
    public long eval(String a) {
        return a == null ? 0 : a.length();
    }
    public long eval(String b, String c) {
        return eval(b) + eval(c);
    }
    // The close method is optional.
    @Override
    public void close() {
        }
}
			
```

## Publish {#section_cwx_jpx_dgb .section}

Locate the required class, write SQL statements, and click **Publish**. On the Administration page, click **Start** to run the function.

``` {#codeblock_to2_gzk_dmw .language-sql}
-- udf str.length()
CREATE FUNCTION stringLengthUdf AS 'com.hjc.test.blink.sql.udx.StringLengthUdf';
create table sls_stream(
    a int,
    b int,
    c varchar
) with (
    type='sls',
    endPoint='yourEndpoint',
    accessKeyId='yourAccessId',
    accessKeySecret='yourAccessSecret',
    startTime = '2017-07-04 00:00:00',
    project='yourProjectName',
    logStore='yourLogStoreName',
    consumerGroup='consumerGroupTest1'
);
create table rds_output(
    id int,
    len bigint,
    content VARCHAR
) with (
    type='rds',
    url='yourDatabaseURL',
    tableName='yourDatabaseTableName',
    userName='yourDatabaseUserName',
    password='yourDatabasePassword'
);
insert into rds_output
select
    a,
    stringLengthUdf(c),
    c as content
from sls_stream
```

## FAQ {#section_m5p_kpx_dgb .section}

Q: Why does a user defined random number generator always generate the same value at run time?

A: If a UDF has no parameters and you do not declare the function as nondeterministic, the function may be optimized to be a constant value during compilation. To avoid this, you can override `isDeterministic()` to make it return `false` in the UDF.

