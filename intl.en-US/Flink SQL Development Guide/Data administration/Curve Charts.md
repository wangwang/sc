# Curve Charts {#concept_62483_zh .concept}

Realtime Compute provides an overview page of core metrics of the current job. You can diagnose the running status of the current job with one click based on curve charts. In the future, Realtime Compute will provide more deep analysis algorithms based on the current job status to assist you with smart and automatic diagnostics of errors.

The following figure shows the curve charts of the job diagnostic metrics.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086733954_en-US.png)

**Note:** The metrics shown in this figure are displayed only when the Realtime Compute job is in the running state. Realtime Compute asynchronously collects job metrics in the background, which results in delays. The metrics can be displayed properly only after a job has been running for more than 1 minute.

## Overview {#section_k5k_pjr_bgb .section}

-   Failover rate

    The failover rate refers to the failover \(caused by errors or exceptions\) frequency of the current job. Calculation method: Divide the accumulated failover count in the last minute by 60. For example, if one failover occurred in the last minute, the failover rate would be 1/60 = 0.01667.

    The trend of the failover rate allows you to better analyze problems of the job.

-   Delay
    -   fetched\_delay: Data pending time \(fetched\_delay\) = Time when data enters Flink - Data event time \(event time\). This metric indicates the actual processing capability of Realtime Compute.
    -   no\_data\_delay: Data arrival interval \(no\_data\_delay\) = Current system time - Time when the last data record arrives at Flink. This metric indicates the time required by a data record to flow from the data source to Flink.
    -   delay: Processing delay \(delay\) = Current system time - Current data event time \(event time\). This metric indicates the data processing progress.
-   Input TPS of Each Source

    Realtime Compute collects statistics about all streaming data input of a Realtime Compute job, and records the number of data blocks read from the source table every second. This allows you to intuitively view the transaction per second \(TPS\) information of the data storage system. Unlike TPS, records per second \(RPS\) indicates the number of data records that are parsed from data blocks of the source table. The unit is record/s. For example, Log Service reads N LogGroups and parses M log records every second. The number of log records parsed per second is the RPS of the data input system.

-   Data Output of Each Sink

    Realtime Compute collects statistics about all data output \(instead of only the streaming data output\) of a Realtime Compute job. This allows you to intuitively view the RPS information of the data storage system. Typically, if you cannot detect data output during system O&M, check both the data input and output systems.

-   Input RPS of Each Source

    Realtime Compute collects statistics about the streaming data input of a Realtime Compute job. This allows you to intuitively view the RPS information of the data storage system. Typically, if you cannot detect data output during system maintenance, check whether there is data input from the data source.

-   Input BPS of Each Source

    Realtime Compute collects statistics about the streaming data input of a Realtime Compute job, and records the traffic read from the source table every second. This allows you to intuitively view the byte per second \(BPS\) information of the data traffic.

-   Dirty data from Each Source

    This metric indicates whether dirty data exists in the source section of Realtime Compute.


## Advanced view { .section}

Realtime Compute provides a fault tolerance mechanism that allows you to restore data streams. This mechanism ensures that the data streams are consistent with the application. The core of this fault tolerance mechanism is to continuously create consistent snapshots for distributed data streams and their statuses. These snapshots act as consistency checkpoints for rollback in case of system failure.

One of the core concepts of distributed snapshots is the barrier. Barriers are inserted into data streams and flow together with the data streams to the output system. Barriers will not interfere with normal data. Instead, data streams are strictly ordered. A barrier cuts a data stream into two parts, one entering the current snapshot and the other the next snapshot. Each barrier has a snapshot ID. Data that flows before a barrier is included in the snapshot corresponding to this barrier. Barriers are lightweight, and do not interfere with the processing of data streams. Multiple barriers of different snapshots can simultaneously exist in the same data stream. This means that multiple snapshots may be created concurrently.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086733962_en-US.png)

Barriers are inserted at the data source. After barriers of snapshot n are inserted into all input data streams, the system records the current snapshot as Sn \(n indicates the snapshot position\). Then, the barriers keep flowing down. When operator A receives all barriers marked with snapshot n \(Sn barriers\) from its input streams, it inserts an Sn barrier into each of its output streams. The flow of data streams is similar to a Directed Acyclic Graph \(DAG\). Therefore, these streams are also known as DAG streams. When a sink operator \(operator B\), the destination of a DAG stream, receives all Sn barriers from its input streams, it reports to the checkpoint coordinator that the Sn snapshot is created. After all sink operators have reported that the Sn snapshot is created, this snapshot is marked created.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086733963_en-US.png)

The curve charts of various checkpoint metrics are as follows.

-   Checkpoint Duration

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086733964_en-US.png)

    This metric indicates the duration for creating a checkpoint, in milliseconds.

-   CheckpointSize

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086733965_en-US.png)

    This metric indicates the size of each checkpoint.

-   checkpointAlignmentTime

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833966_en-US.png)

    This metric indicates the duration required for all data streams to flow from the upstream nodes to the node at which you create a checkpoint. In other words, when a sink operator \(destination of a DAG stream\) receives all Sn barriers from its input streams, it reports to the checkpoint coordinator that the Sn snapshot is created. After all sink operators have reported that the Sn snapshot is created, this snapshot is marked created. This duration is known as the checkpoint alignment time.

-   checkpointCount

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833967_en-US.png)

-   Get

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833968_en-US.png)

    This metric indicates the longest time that a subtask spends on performing a GET operation on the RocksDB within a specific period.

-   Put

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833969_en-US.png)

    This metric indicates the longest time that a subtask spends on performing a PUT operation on the RocksDB within a specific period.

-   Seek

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833970_en-US.png)

    This metric indicates the longest time that a subtask spends on performing a SEEK operation on the RocksDB within a specific period.

-   State Size

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833971_en-US.png)

    This metric indicates the state size of a job. If the size increases too fast, the job is abnormal.

-   CMS GC Time

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833972_en-US.png)

    This metric indicates the time that the underlying container of a job spends on garbage collections \(GC\).

-   CMS GC Rate

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41067/155764086833973_en-US.png)

    This metric indicates the frequency that the underlying container of a job performs GC.


## WaterMark { .section}

-   WaterMark Delay

    This metric indicates the difference between the watermark time and the system time.

-   Dropped Records per Second

    When the time at which a data record reaches the window is later than the watermark time, the data record will be discarded. This metric indicates the number of late data records discarded per second.

-   Dropped Records

    When the time at which a data record reaches the window is later than the watermark time, the data record will be discarded. This metric indicates the accumulated number of discarded late data records at a specific time point.


## Delay { .section}

Top 15 Source Subtasks with the Longest Processing Delay

This metric indicates the processing delay of each source subtask.

## Throughput { .section}

-   Task Input TPS

    This metric indicates the data input of all tasks under the same Realtime Compute job.

-   Task Output TPS

    This metric indicates the data output of all tasks under the same Realtime Compute job.


## Queue { .section}

-   Input Queue Usage

    This metric indicates the data input queue of all tasks under the same Realtime Compute job.

-   Output Queue Usage

    This metric indicates the data output queue of all tasks under the same Realtime Compute job.


## Tracing { .section}

Advanced metrics are as follows:

-   Time Used In Processing Per Second

    This metric indicates the time that a task spends on processing data per second.

-   Time Used In Waiting Output Per Second

    This metric indicates the time that a task spends on waiting for the output per second.

-   TaskLatency Histogram Mean

    This metric indicates the computing latency curve of each task under the same job.

-   WaitOutput Histogram Mean

    This metric indicates the curve of the time that a task spends on waiting for the output.

-   WaitInput Histogram Mean

    This metric indicates the curve of the time that a task spends on waiting for the input.

-   PartitionLatency Mean

    This metric indicates the latency curve of each parallel subtask in a partition.


## Process { .section}

-   Process Memory RSS

    This metric indicates the memory usage curve of each process.

-   CPU Usage

    This metric indicates the CPU usage curve of each process.


## JVM { .section}

-   Memory Heap Used

    This metric indicates the Java Virtual Machine \(JVM\) heap memory usage of the job.

-   Memory Non-Heap Used

    This metric indicates the JVM non-heap memory usage of the job.

-   Threads Count

    This metric indicates the number of threads for the job.

-   GC \(CMS\)

    This metric indicates the number of garbage collections \(GC\) that have been performed for the job.


