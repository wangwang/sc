# Configure a data storage whitelist {#concept_92261_zh .concept}

This topic uses ApsaraDB for RDS as an example to describe how to configure a data storage whitelist.

## What is a whitelist {#section_j5h_tx4_yfb .section}

Some data storage services provide the whitelist feature to guarantee security. After you configure a whitelist, only IP addresses in the whitelist are allowed to access your data storage resources. Note that this feature also blocks data writing requests from other Alibaba Cloud products whose IP addresses are not in the whitelist.

## Configure a whitelist {#section_r2z_d2s_zfb .section}

The whitelist configuration method may vary depending on different data storage services. You need to configure the whitelist in the console of the corresponding data storage service. For more information, see the help document of the corresponding data storage service. For example, a new ApsaraDB for RDS instance blocks all external requests by default. You must add a whitelist to allow the specified IP addresses to access the ApsaraDB for RDS instance. When Realtime Compute uses ApsaraDB for RDS tables as dimension tables and result tables, it needs to read data from and write data to the ApsaraDB for RDS instance frequently. You must include the IP addresses of WebConsole and Worker of Realtime Compute to the whitelist to allow Realtime Compute to access your ApsaraDB for RDS instance.

Log on to the ApsaraDB for RDS console, and add the IP address of your Realtime Compute cluster to the whitelist, refer to [Set a whitelist](../../../../intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#). For more information about the IP address, see the following section of this topic.

## IP address {#section_ipr_gtl_bgb .section}

If you are using the exclusive mode, you only need to add the elastic network interface \(ENI\) IP address of your exclusive ECS cluster to the whitelist. To view the ENI IP address of your Realtime Compute cluster, choose **Project Management** \> **Clusters** \> **Cluster Name** \> **ENI**.

