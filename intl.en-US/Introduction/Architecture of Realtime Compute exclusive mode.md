# Architecture of Realtime Compute exclusive mode {#concept_73031_zh .concept}

This topic describes the architecture of Realtime Compute exclusive mode.

The following figure shows the architecture of Realtime Compute exclusive mode.

![](images/33597_en-US.png)

1.  In Realtime Compute exclusive mode, all your purchased ECS instances are fully hosted in the VPC of the compute cluster. Currently, Realtime Compute exclusive mode does not support logging on to ECS instances.
2.  When you create a compute cluster, Realtime Compute applies for an Elastic Network Interface \(ENI\) under your Realtime Compute account. You can use the ENI to access all resources in your VPC.
3.  To enable the compute cluster to access the Internet, you can bind an NAT gateway and an elastic IP address to the ENI. For more information, see the documentation on the Alibaba Cloud official website.
4.  The ENI that Realtime Compute applies for you belongs to an independent security group under your Realtime Compute account. To access services of another security group in the VPC, configure rules for the security group.

**Note:** You are charged for using the ENI only when the compute cluster accesses the Internet.

