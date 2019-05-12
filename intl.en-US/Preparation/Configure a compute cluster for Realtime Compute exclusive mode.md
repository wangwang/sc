# Configure a compute cluster for Realtime Compute exclusive mode {#concept_c55_g5z_xfb .concept}

This topic describes how to configure a compute cluster for Realtime Compute exclusive mode.

## Background {#section_ubl_j5z_xfb .section}

If you purchase Realtime Compute exclusive mode, you exclusively own a distributed compute cluster that consists of master and slave nodes.

-   The master nodes manage the resources of the entire cluster and the interaction with the slave nodes. However, the master nodes do not provide the computation service.
-   The slave nodes are the nodes actually used for computation in the cluster. However, not every resource on a slave node is available for computation. This is because a slave node consumes some resources to run its operating system and communicate with other nodes.

## Purchasing principles {#section_t2s_k5z_xfb .section}

Realtime Compute exclusive mode uses the same CU concept as Realtime Compute shared mode, that is, 1 CU = 1Core CPU + 4 GB RAM. If you purchase Realtime Compute exclusive mode, you can also determine the models and quantities of master and slave nodes based on the number of CUs required. The master nodes are only used for management and do not participate in computation.

-   The minimum purchase quantity of slave nodes is two. That is, the minimum computing power in exclusive mode is 6 CUs \(3 CUs × 2\). The following table lists the empirical values for the number of available CUs that each slave model can actually provide for computation.

    **Note:** The empirical values are for your reference only.

    |Slave model|Number of CUs available for computation|
    |4 Core CPU and 16 GB RAM|3|
    |8 Cores CPU and 32 GB RAM|6|
    |16 Cores CPU and 64 GB RAM|13|
    |24 Cores CPU and 96 GB RAM|21|
    |32 Cores CPU and 128 GB RAM|28|
    |56 Cores CPU and 224 GB RAM|52|
    |64 Cores CPU and 256 GB RAM|60|

-   Select an appropriate master model depending on the maximum number of CUs in your cluster The following table lists the empirical number of CUs supported by each master model.

    **Note:** The empirical values are for your reference only.

    |Master model|Maximum number of CUs in the cluster|
    |4 Cores CPU and 16 GB RAM|80|
    |8 Cores CPU and 32 GB RAM|160|
    |16 Cores CPU and 64 GB RAM|800|
    |24 Cores CPU and 96 GB RAM|\> 800|


By using the preceding calculation logic, you can determine the combination of node models and quantities to build up a cluster. You can also log on to Realtime Compute Development Platform and go to the Pricing Calculator page to query the most cost-effective model combination.

**Note:** If you are a new user, you can first calculate the number of required CUs based on the number of queries per second \(QPS\) and the logic complexity of your business. Then use the preceding calculation logic to determine the node models and quantities. The logic for calculating the number of required CUs is as follows:

-   For simple business processing, such as single-stream filtering and character string conversion, 1 CU can process 10,000 records per second.
-   For complex business processing, such as join, window, and group by operations, 1 CU can process 1,000 to 5,000 records per second.

## Considerations {#section_i2k_v5z_xfb .section}

-   Once you have selected the slave model, you can only increase or decrease the required number of slave nodes of that model for possible future scale-out or scale-in. For example, if you have selected the slave model with an 8 Cores CPU and 32 GB RAM, you can add or remove several slave nodes of this model based on your scale-out or scale-in requirements. Consequently, the number of CUs available for computation increases or decreases by a multiple of 6 CUs.
-   To ensure stability of the cluster, we recommend that you purchase three master nodes to implement failover when a master node fails. If you purchase three master nodes, Alibaba Cloud provides you with a service-level agreement \(SLA\) guarantee.
-   Once you have specified the number of master nodes, you cannot change it during future use.

