# JobManager {#concept_62486_zh .concept}

This topic describes the usage of JobManager and its role in the startup process of a Realtime Compute cluster.

JobManager is essential to the startup process of a Realtime Compute cluster. The startup process of a Realtime Compute cluster is described as follows:

1.  The Realtime Compute cluster starts one JobManager and one or more TaskExecutors.
2.  A client submits jobs to the JobManager.
3.  The JobManager assigns tasks of the jobs to TaskExecutors.
4.  TaskExecutors report the heartbeats and statistics to the JobManager.

## Usage of JobManager {#section_jzt_5yr_bgb .section}

Similar to Storm Nimbus, a JobManager receives jobs, and arranges for TaskExecutors to create checkpoints. The JobManager receives jobs and resources, such as JAR packages, from a client. Then, the JobManager generates an optimized execution plan, and assigns tasks to TaskExecutors.

## JobManager parameters {#section_mj1_fzr_bgb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41070/155764096334011_en-US.png)

