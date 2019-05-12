# TaskExecutor {#concept_62487_zh .concept}

This topic describes the role of TaskExecutor in the startup process of a Realtime Compute cluster, as well as its user interface.

## Background {#section_uk2_scs_bgb .section}

After a Realtime Compute cluster is started, one JobManger and one or more TaskExecutors are started. A client submits jobs to the JobManager, and the JobManager assigns tasks of the jobs to TaskExecutors. During task execution, TaskExecutors report the heartbeats and statistics to the JobManager. TaskExecutors transmit data to one another through data streams.

The number of slots is specified before a TaskExecutor is started. A TaskExecutor executes each task in each slot, and each task can be considered as a thread. A TaskExecutor receives tasks from the JobManager, and then establishes a Netty connection with its upstream to receive and process data.

## User interface of TaskExecutor {#section_xvx_wcs_bgb .section}

The TaskExecutor page provides you with a list of tasks and entries to their details.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41071/155764102034013_en-US.png)

