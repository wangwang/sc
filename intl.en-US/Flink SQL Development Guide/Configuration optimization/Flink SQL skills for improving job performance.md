# Flink SQL skills for improving job performance {#concept_xdd_nbz_zfb .concept}

This topic describes the recommended Flink SQL statements, configuration, and functions that are helpful to significantly improve the job performance.

## Skills for improving Group Aggregate operations {#section_cwh_rcz_zfb .section}

-   Enable microBatch or miniBatch to improve the throughput

    Both microBatch and miniBatch are mini-batch processing methods. The only difference lies in their triggering mechanisms. In principle, they cache a specific amount of data before they trigger the processing. This reduces the frequency that Realtime Compute has to access the state, thus significantly improving the throughput and reducing the amount of data output.

    miniBatch triggers mini-batch processing by using the timer threads that are registered with each task. This involves some thread scheduling overheads. microBatch is an upgraded version of miniBatch. It triggers mini-batch processing by using event messages, which are inserted into the data sources at a specific interval. microBatch outperforms mini-batch in terms of data accumulation efficiency, back pressure control, throughput, and low latency.

    -   Scenarios

        Mini-batch processing is a policy that increases some latency to achieve greater throughput. We recommend that you disable mini-batch processing if you have high requirements on low latency. Generally, we recommend that you enable mini-batch processing, because it significantly improves the job performance in aggregation scenarios.

        **Note:** The microBatch mode is also helpful to solve the pain point of two-level aggregation data jitter.

    -   Enable mini-batch processing

        microBatch and miniBatch are disabled by default. To enable them, specify the following parameters:

        ```
        # This parameter specifies the interval at which data is accumulated. It must be specified when you use the microBatch policy. We recommend that you set this parameter to the same value as that of blink.miniBatch.allowLatencyMs.
        blink.microBatch.allowLatencyMs=5000
        # When you use the microBatch policy, you need to reserve the following miniBatch settings:
        blink.miniBatch.allowLatencyMs=5000
        # This parameter specifies the maximum number of data records that can be cached for each batch. The purpose is to avoid the out of memory (OOM) error.
        blink.miniBatch.size=20000
        ```

-   Enable LocalGlobal to solve common data hotspot problems

    The LocalGlobal optimization method divides the conventional aggregation process into two stages: local aggregation and global aggregation. This is similar to the Combine + Reduce processing method that is commonly used in the MapReduce model. In the first stage, Realtime Compute aggregates the first batch of data that is buffered locally at the input node \(LocalAgg\), and generates accumulators for this micro-batch. In the second stage, it merges the accumulators to obtain the final result \(globalAgg\).

    Essentially, LocalGlobal can eliminate data skew through LocalAgg and solve data hotspot problems during globalAgg to improve the job performance. The following diagram can help you understand how LocalGlobal solves data skew.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75347/155764128733642_en-US.png)

    -   Scenarios

        LocalGlobal is suitable for improving the performance of general aggregation operations such as SUM, COUNT, MAX, MIN, and AVG. It is also helpful to solve data hotspot problems when you perform such operations.

        **Note:** To enable LocalGlobal, you need to implement the merge method by using User Defined Aggregation Functions \(UDAFs\).

    -   Enable LocalGlobal

        Starting from Realtime Compute `V2.0`, LocalGlobal is enabled by default. When the value of the `blink.localAgg.enabled` parameter is set to true, LocalGlobal is enabled. However, this setting takes effect only when microBatch or miniBatch is enabled.

    -   Check whether the setting takes effect

        You can check whether the **GlobalGroupAggregate** or **LocalGroupAggregate** node exists in the final topology.

-   Enable PartialFinal to solve data hotspot problems when you run the CountDistinct function

    The LocalGlobal method can effectively improve the performance of general aggregation functions, such as SUM, COUNT, MAX, MIN, and AVG. However, its performance improvement effect for the CountDistinct function is limited. The reason is that the duplicate removal function of LocalAgg does not work well with distinct keys. As a result, a large amount of data is still stacked up at the global node.

    Typically, users who use earlier versions of Realtime Compute need to manually divide the aggregation process into two stages by adding a layer that scatters data by distinct key. This was a workaround to solve data hotspot problems when they run the CountDistinct function. Starting from `V2.2.0`, Realtime Compute offers PartialFinal, an automatic data scattering feature that saves your effort of manually dividing the aggregation process. The following diagram can help you understand the difference between LocalGlobal and PartialFinal.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/75347/155764128733643_en-US.png)

    -   Scenarios

        PartialFinal applies to scenarios where the CountDistinct function is used and the performance at the aggregation node cannot meet your requirements.

        **Note:** 

        -   The PartialFinal feature cannot be used in a Flink SQL statement that contains UDAFs.
        -   We recommend that you use PartialFinal when data volume is large. The PartialFinal feature automatically scatters data into two aggregation layers, and introduces additional network shuffling. When data volume is not large, it will be a waste of resources.
    -   Enable PartialFinal

        PartialFinal is disabled by default. You can explicitly enable it by setting the value of the `blink.partialAgg.enabled` parameter to true.

    -   Check whether the setting takes effect

        You can check whether the **Expand** node exists in the final topology, or whether the number of the aggregation layer changes from one to two.

-   Use the agg with filter syntax to significantly improve the job performance when you run the CountDistinct function

    **Note:** This method is supported by Realtime Compute `V2.2.2` and later.

    Some statistical jobs may record unique visitors \(UVs\) of different dimensions, such as UVs of all channels, UVs of the Taobao app, and UVs of the PC client. Many users choose to use the CASE WHEN statement to implement multi-dimensional statistical analysis. However, we recommend that you use the standard agg with filter syntax. The reason is that Realtime Compute has an SQL optimizer that can analyze the filter parameter. The SQL optimizer allows Realtime Compute to run the CountDisatinct function on the same field under different conditions by sharing the state. This reduces the read and write operations on the state. This syntax improves the job performance by one time based on the performance test.

    -   Scenarios

        We recommend that you replace the agg with CASE WHEN syntax with the agg with filter syntax. This is particularly helpful to improve the job performance when you run the CountDiscount function on the same field under different conditions.

    -   Original statement

        ```
        COUNT(distinct visitor_id)as UV1,COUNT(distinctcasewhen is_wireless='y'then visitor_id elsenullend)as UV2
        								
        ```

    -   Optimized statement

        ```
        COUNT(distinct visitor_id)as UV1,COUNT(distinct visitor_id) filter (where is_wireless='y')as UV2
        ```


## TopN optimization skills {#section_ncg_d3z_zfb .section}

When the input streams of TopN are non-update streams \(such as source\), TopN supports only one algorithm: AppendRank. When the input streams of TopN are update streams \(that have undergone Agg or Join operations\), TopN supports three algorithms. Ranked in a descending order of performance, these algorithms are UpdateFastRank, UnaryUpdateRank, and RetractRank \(\). The algorithm names will be displayed on the node names of the topology.

-   RetractRank is the algorithm with the lowest performance. We do not recommend that you use this algorithm in production. If you have to use this algorithm, check whether the input streams have the primary key \(PK\) information, and whether you can optimize the job performance.
-   UpdateFastRank is the optimal algorithm. The following conditions must be met if you want to use this algorithm: 1. The input streams must have the PK information. 2. The update of the ORDERBY field is monotonic, and the monotonic direction is opposite to the sorting order. For example, order by count, count\_distinct, sum \(positive\) desc.
-   The performance of the UnaryUpdateRank algorithm is only second to UpdateFastRank. One condition must be met if you want to use this algorithm: The input streams must have the PK information. No monotonic information is required. For example, order by avg.

-   In the case of order by sum \(positive\) desc, a positive filter condition must be added.

    In addition, the parameter value of sum must not be negative, and you need to inform the optimizer of such information by adding a positive filter. Then, you can use the UpdateFastRank algorithm. This algorithm is supported by Realtime Compute `V2.2.2` and later. See the following statements for reference \(pay attention to sum\(total\_fee\) filter ...\) \)

    ```
    SELECT cate_id, seller_id, stat_date, pay_ord_amt  # The rownum field is not included in the output. This reduces the amount of output data to be written into the result table.
    FROM(SELECT*
          ROW_NUMBER ()OVER(PARTITIONBY cate_id, stat_date   # Be sure to specify the stat_date field. Otherwise, the data will become disordered when the state expires.
    ORDERBY pay_ord_amt DESC## Sort by the sum of the input data) AS rownum
      FROM(SELECT cate_id, seller_id, stat_date,# Important! Parameters that are used to declare sum are all positive, so results of the sum() function are monotonically increasing. That's why TopN supports optimization algorithms. sum(total_fee) filter (where total_fee >=0)as pay_ord_amt
        FROMWHERE total_fee >=0GROUPBY cate_name, seller_id, stat_date)WHERE rownum <=100)) 
    ```

-   No-ranking optimization

    Do not include rownum in the output of TopN. We recommend that you sort the results when they are finally displayed in the front end. This can significantly reduce the amount of data that is to be written into the result table. For more information, see[TopN statement](intl.en-US/Flink SQL Development Guide/Flink SQL/Query statements/TopN statement.md#) .

-   Increase the cache size of TopN

    TopN has a state cache layer to improve the performance. The cache layer can improve the state access efficiency. The calculation formula of the TopN cache hit rate is:

    ```
    
    
    
    cache_hit = cache_size*parallelism/top_n/partition_key_num
    						
    ```

    Taking Top100 for example. Assume that the cache size is 10,000 and the parallelism is 50. If the number of keys for the partitionBy field is 100,000, the cache hit rate will be 10,000 × 50/100/100,000 = 5%. This value is very low, and large amounts of requests will access the state \(disk\), and the state seek metric would not be smooth. This also significantly affects the performance. Therefore, if the size of the partitionKey is very large, you may increase the cache size and heap memory of the TopN node. For more information, see [Manual configuration optimization](intl.en-US/Flink SQL Development Guide/Configuration optimization/Manual configuration optimization.md#).

    ```
    In this case, if you increase the TopN cache from the default value 10,000 to 200,000, the cache hit rate may reach 200,000 × 50/100/100,000 = 100%.
    blink.topn.cache.size=200,000
    ```

-   A time field must be included in the partitionBy field.

    For example, you need to include the day field in your statement for a daily ranking. Otherwise, the TopN result may become disordered due to the state time to live \(TTL\).


## Efficient deduplication solution {#section_yjb_nkz_zfb .section}

-   Use the FirstRow method to replace the first\_value function.

    **Note:** The FirstRow function is supported by Realtime Compute `V2.2.2` and later.

    The FirstRow method is used to perform deduplication, where it keeps the first occurrence of duplicate records under the specified primary key, and discards the rest duplicate records. After you replace the first\_value function with the FirstRow function, the state of the FirstRow function only stores keys, and the state access efficiency is significantly increased. This improves the Realtime Compute job performance by one time.

    **Note:** Difference between FirstRow and first\_value: The FirstRow method applies to an entire row, and reads data of the first row of the key, regardless of whether the field in this row is null. The first\_value function applies to the field, and reads the first non-null data record of the key.

    -   Original statement \(using first\_value to remove duplicates\):

        ```
        select biz_order_id, first_value(seller_id), first_value(buyer_id), first_value(total_fee)from tt_source
        groupby biz_order_id;
        ```

    -   Optimized statement \(by using the FirstRow method\): You need to add the PK property to the source table, and add the `fetchFirstRow='true'` configuration.

        ```
        CREATETABLE tt_source (
        biz_order_id varchar,
        seller_id varchar,
        buyer_id varchar,
        total_fee doublePRIMARYKEY(biz_order_id # 1. Declare the primary key that you want to remove duplicates with, which can be a composite key.
        )WITH(
        type='tt',fetchFirstRow='true' # 2. Set the value to true to only keep the first row. The default value is false, which means to keep the last row.)
        ```

-   Use the LastRow function to replace the last\_value function

    The LastRow function is used to perform deduplication, and it only keeps the last data record under the specified primary key. Its performance is slightly better than that of the last\_value function.

    **Note:** Difference between LastRow and last\_value: The LastRow function applies to an entire row, and reads data of the last row of the key, regardless of whether the field in this row is null. The last\_value function applies to the field, and reads the last non-null data record of the key.

    -   Original statement \(using last\_value to remove duplicates\):

        ```
        select biz_order_id,
         last_value(seller_id),
         last_value(buyer_id),
         last_value(total_fee)
        from tt_source
        group by biz_order_id;
        								
        ```

    -   Optimized statement \(using the LastRow function\): You need to add the Primary Key property to the source table, and add the `fetchFirstRow='false'` configuration.

        ```
        CREATETABLE tt_source (
        biz_order_id varchar,
        seller_id varchar,
        buyer_id varchar,
        total_fee doublePRIMARYKEY(biz_order_id)# 1. Declare the primary key that you want to remove duplicates with, which can be a composite key.
        )WITH(type='tt',
        fetchFirstRow='false',# 2. The default value is false, which means to keep the last row. Use the default value.)
        ```


## Efficient built-in functions {#section_qqb_clz_zfb .section}

-   Use built-in functions to replace UDXs

    Use built-in functions whenever possible. This is very important. Built-in functions of earlier Realtime Compute versions are incomplete. Many users had to use third-party User Defined Extensions \(UDXs\). In Realtime Compute V2.X, the built-in functions are greatly improved \(reduces message serialization or deserialization, and allows direct operations on Bytes\). However, UDXs cannot benefit from such improvements.

-   The KEY VALUE function uses single-character separators.

    The signature of the KEY VALUE function is: `KEYVALUE(content, keyValueSplit, keySplit, keyName)`. When keyValueSplit and KeySplit are single-character separators, such as `:` and `,`, Realtime Compute will use an optimized algorithm. Instead of segmenting the entire content, Realtime Compute directly looks for the required KeyName values among the binary data. This improves the job performance by approximately 30%.

-   MULTI\_KEYVALUE is used for scenarios with multiple key values.

    **Note:** This is supported by Realtime Compute `V2.2.2` and later.

    Sometimes, a query may involve multiple key value operations on the same content. For example, a content contains 10 key-value pairs, and you hope to extract all these 10 values to use them as fields. You may write 10 key value functions to parse the content 10 times. In this case, we recommend that you use the [MULTI\_KEYVALUE](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/Table-valued functions/MULTI_KEYVALUE.md#) function, which is a table-valued function. This function only requires one SPLIT parsing on the content. The performance is improved by 50%-100%.

-   Notes on LIKE operations
    -   If you want to perform startWith operations, use `LIKE 'xxx%'`.
    -   If you want to perform endWith operations, use `LIKE '%xxx'`.
    -   If you want to perform contains operations, use `LIKE '%xxx%'`.
    -   If you want to perform equals operations, use `LIKE 'xxx'`, which is equal to `str = 'xxx'`.
    -   If you want to match the `_` character, be sure to use `LIKE '%seller/id%' ESCAPE '/'`. Because `_` is a single-character wildcard in SQL, it can match any characters. If you declare it as `LIKE '% seller_id %'`, it matches a lot of characters such as `Seller_id`, `Seller # id`, `Sellerxid`, and `Seller1id`. The results may be unsatisfactory, and the efficiency may be rather low when regular expressions are used.
-   Use the regular expression functions sparingly

    Regular expression operations can be very time consuming, and may require a hundred more times of computing resources in comparison with other operations such as plus, minus, multiplication, and division. If you run regular expressions under some particular circumstances, your job [may be stuck in an infinite loop](https://stackoverflow.com/questions/4500507/infinite-loop-in-regex-in-java). Therefore, use LIKE whenever possible. For more information, see Notes on LIKE operations. Common regular expression functions include: [REGEXP](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/String functions/REGEXP.md#), [REGEXP\_EXTRACT](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/String functions/REGEXP_EXTRACT.md#), and [REGEXP\_REPLACE](intl.en-US/Flink SQL Development Guide/Flink SQL/Built-in functions/String functions/REGEXP_REPLACE.md#).


## Network transmission optimization {#section_hy1_gmz_zfb .section}

Commonly used Partitioner policies are:

-   KeyGroup/Hash: distributes data based on specified keys.
-   Rebalance: distributes data to each channel through round-robin scheduling.
-   Dynamic-Rebalance: dynamically distributes data to channels with lower load based on load status of output channels.
-   Forward: similar to Rebalance when unchained. When it is chained, it does one-to-one data distribution.
-   Rescale: distributes data in a one-to-many or many-to-one mode between input and output systems.

-   Use Dynamic-Rebalance to replace Rebalance

    Dynamic Rebalance can write data into subpartitions with lower load based on the amount of buffered data in each subpartition to achieve dynamic load balancing. In comparison with the static rebalance policy, when computing capacity of output computing nodes is unbalanced, Dynamic Rebalance can balance the load and improve the overall job performance. For example, if you find the load of your output nodes is unbalanced when you use rebalance, you may consider to use Dynamic-Rebalance. Parameter: `task.dynamic.rebalance.enabled=true`. Default value: false.

-   Use Rescale to replace Rebalance

    **Note:** Rescale is supported by Realtime Compute `V2.2.2` and later.

    Assume that you have five parallel input nodes and 10 parallel output nodes. When you use Rebalance, each input node distributes data to all 10 output nodes through round-robin scheduling. When you use Rescale, each input node only needs to distribute data to two output nodes through round-robin scheduling. This reduces the number of channels, increases the buffering speed of each subpartition, and thus improves the network efficiency. When input data is even and the number of parallel input and output nodes are in proportion, you can use Rescale to replace Rebalance. Parameter: `enable.rescale.shuffling=true`. Default value: false.


## Recommended configuration {#section_rfj_vmz_zfb .section}

To sum up, we recommend you use the following job configuration:

```
# excatly-once semantics
blink.checkpoint.mode=EXACTLY_ONCE
# The checkpoint interval, in milliseconds.
blink.checkpoint.interval.ms=180000
blink.checkpoint.timeout.ms=600000
# Realtime Compute V2.X uses Niagara as the state back-end, and uses it to set the lifecycle of the state data, in milliseconds.
state.backend.type=niagara
state.backend.niagara.ttl.ms=129600000
# Realtime Compute V2.X enables a 5-second micro-batch (You cannot set this parameter when you use a window function.)
blink.microBatch.allowLatencyMs=5000
# The allowed latency for a job.
blink.miniBatch.allowLatencyMs=5000
# The size of a batch.
blink.miniBatch.size=20000
# Local optimization. This feature is enabled by default in Realtime Compute V2.X, but you need to enable it manually if you use Realtime Compute V1.6.4.
blink.localAgg.enabled=true
# Realtime Compute V2.X allows you to enable PartialFinal to solve data hotspot problems when you run the CountDistinct function.
blink.partialAgg.enabled=true
# Union all optimization
blink.forbid.unionall.as.breakpoint.in.subsection.optimization=true
# Object reuse optimization. Enabled by default.
#blink.object.reuse=true
# GC optimization (You cannot set this parameter when you use a Log Service source table.)
blink.job.option=-yD heartbeat.timeout=180000 -yD env.java.opts='-verbose:gc -XX:NewRatio=3 -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:ParallelGCThreads=4'
# Time zone setting
blink.job.timeZone=Asia/Shanghai
```

