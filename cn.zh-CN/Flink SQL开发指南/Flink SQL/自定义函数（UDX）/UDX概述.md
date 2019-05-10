# UDX概述 {#concept_69463_zh .concept}

本文为您介绍如何为实时计算自定义函数搭建环境和使用。

**说明：** 目前阿里云实时计算共享模式暂不支持自定义函数，仅独享模式支持自定义函数。

## UDX分类 {#section_190_h60_4it .section}

实时计算支持以下3类自定义函数：

|UDX分类|描述|
|-----|--|
|UDF（User Defined Function）|用户自定义标量值函数（User Defined Scalar Function）。其输入与输出是一对一的关系，即读入一行数据，写出一条输出值。|
|UDAF（User Defined Aggregation Function）|自定义聚合函数，其输入与输出是多对一的关系， 即将多条输入记录聚合成一条输出值。可以与SQL中的GROUP BY语句联用。具体语法请参见[聚合函数](../../../../cn.zh-CN/用户指南/SQL/内建函数/聚合函数.md#)。|
|UDTF（User Defined Table-valued Function）|自定义表值函数，调用一次函数输出多行或多列数据。|

## 环境搭建 {#section_ck2_gcm_cgb .section}

自定义函数（UDX）的开发需要依赖实时计算的相关JAR包，为了便于用户快速的搭建环境，我们提供了一个UDX开发DEMO（`RealtimeCompute-udxDemo.gz`），该DEMO为Maven的Project，您可使用IntelliJ IDEA直接打开，并在此基础上进行开发。

DEMO中已经分别有3个简单的UDF、UDAF和UDTF的实现，供参考。

`[RealtimeCompute-udxDemo.gz](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/69463/cn_zh/1535104736459/RealtimeCompute-udxDemo.gz)`

以上Demo主要使用的依赖JAR包如下，如您需要单独使用，可以直接下载：

-   共享模式（基于实时计算3.0以下版本）

    -   [flink-streaming-java\_2.11](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1543327398632/flink-streaming-java_2.11-blink-2.2.4.jar)
    -   [flink-table\_2.11](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1543327437386/flink-table_2.11-blink-2.2.4.jar)
    -   [flink-core-blink-2.2.4](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1543326995841/flink-core-blink-2.2.4.jar)
    **说明：** 上文中的DEMO包下载后，要将`pom.xml`按照下边示例进行更改。您可以下载基于共享模式的[单例测试案例](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1557294154462/RealtimeCompute-udxDemo.zip)。

    ``` {#codeblock_m93_8xh_puo .language-java}
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-core</artifactId>
        <version>blink-2.2.4-SNAPSHOT</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
         <groupId>org.apache.flink</groupId>
         <artifactId>flink-table_2.11</artifactId>
         <version>blink-2.2.4-SNAPSHOT</version>
         <scope>provided</scope>
    </dependency> 
    <dependency>
         <groupId>org.apache.flink</groupId>
         <artifactId>flink-streaming-java_2.11</artifactId>
         <version>blink-2.2.4-SNAPSHOT</version>
         <scope>provided</scope>
    </dependency>
    
    <!-- 单例测试使用 -->
    <!-- https://mvnrepository.com/artifact/junit/junit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.8.1</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.scala-lang</groupId>
        <artifactId>scala-library</artifactId>
        <version>2.11.12</version>
    </dependency> 
    ```

-   独享模式（基于实时计算3.0及以上版本）

    -   [flink-core-blink-3.2.1.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1557279822540/flink-core-blink-3.2.1.jar)
    -   [flink-streaming-java\_2.11-blink-3.2.1.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1557279865869/flink-streaming-java_2.11-blink-3.2.1.jar)
    -   [flink-core-blink-3.2.1.jar](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/98378/cn_zh/1557279936582/flink-table_2.11-blink-3.2.1.jar)
    **说明：** 上文中的Demo包下载后，要将`pom.xml`按照下边示例进行更改。

    ``` {#codeblock_lj9_1sg_sqq .language-java}
    <dependency>
      <groupId>com.alibaba.blink</groupId>
      <artifactId>flink-core</artifactId>
      <version>blink-3.2.1-SNAPSHOT</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>com.alibaba.blink</groupId>
      <artifactId>flink-table_2.11</artifactId>
      <version>blink-3.2.1-SNAPSHOT</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>com.alibaba.blink</groupId>
      <artifactId>flink-streaming-java_2.11</artifactId>
      <version>blink-3.2.1-SNAPSHOT</version>
      <scope>provided</scope>
    </dependency>     
    
    <!-- 单例测试使用 -->
    <!-- https://mvnrepository.com/artifact/junit/junit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.8.1</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.scala-lang</groupId>
        <artifactId>scala-library</artifactId>
        <version>2.11.12</version>
    </dependency> 
    ```


## 注册使用 {#section_5q4_9pi_lny .section}

1.  [登录实时计算控制台](https://stream.console.aliyun.com)。
2.  单击顶部菜单中的开发，进入开发页面。
3.  在左侧的导航栏中单击**资源引用**。
4.  在**资源引用**页签的右上角，单击**新建资源**。
5.  在上传资源页面输入资源配置信息。

    |参数名称|说明|
    |----|--|
    |上传方式|当前仅支持本地上传。|
    |资源选择|单击**选择资源**，选择需要引用的资源。|
    |资源名称|输入资源名称。|
    |资源备注|输入资源备注信息。|
    |资源类型|选择引用资源类型，JAR、DICTIONARY或PYTHON。|

6.  在**资源引用**页签中，将鼠标悬停在对应作业的右侧的**更多**上。
7.  选择下拉列表中的**引用**，将资源中的代码输入实时计算作业编辑窗口。
8.  在作业的编辑窗口的顶部，输入自定义函数声明，示例如下。

    ``` {#codeblock_jpv_uww_av5 .language-SQL}
    CREATE FUNCTION stringLengthUdf AS 'com.hjc.test.blink.sql.udx.StringLengthUdf';
    ```


## 参数与返回值类型 {#section_584_qiv_6ll .section}

实时计算支持定义Java UDX时，使用Java类型作为参数和返回值。下面为实时计算类型和Java类型的映射关系。

|实时计算数类型|Java类型|
|-------|------|
|TINYINT|java.lang.Byte|
|SAMLLINT|java.lang.Short|
|INT|java.lang.Integer|
|BIGINT|java.lang.Long|
|FLOAT|java.lang.Float|
|DOUBLE|java.lang.Double|
|DECIMAL|java.math.BigDecimal|
|BOOLEAN|java.lang.Boolean|
|DATE|java.sql.Date|
|TIME|java.sql.Time|
|TIMESTAMP|java.sql.Timestamp|
|CHAR|java.lang.Character|
|STRING|java.lang.String|
|VARBINARY|java.lang.byte\[\]|
|ARRAY|java.util.List|
|MAP|暂不支持|

## 自定义函数参数获取 {#section_zjd_fbn_jhb .section}

在`UDX`中提供了可选的`open(FunctionContext context)` 方法，`FunctionContext`具备参数传递功能，自定义配置项可以通过此对象来传递。

假设需要在作业中添加如下2个参数。

```language-java
testKey1=lincoln
test.key2=todd
```

以UDTF为例，在open方法中通过`context.getJobParameter`即可获取。示例如下。

```language-java
public void open(FunctionContext context) throws Exception {
      String key1 = context.getJobParameter("testKey1", "empty");
      String key2 = context.getJobParameter("test.key2", "empty");
      System.err.println(String.format("end open: key1:%s, key2:%s", key1, key2));
}
```

**说明：** 具体的作业参数可参见[作业参数](cn.zh-CN/Flink SQL开发指南/配置调优/手动配置调优.md#ul_r1g_lhm_bgb)。

