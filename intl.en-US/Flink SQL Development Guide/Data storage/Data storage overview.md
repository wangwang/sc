# Data storage overview {#concept_62474_zh .concept}

Realtime Compute provides a management page for various data storage systems, such as ApsaraDB for RDS and Table Store. It offers you an end-to-end cloud-based data storage management solution.

Data storage in Realtime Compute has two meanings. First, it refers to the data storage systems or database tables \(hereinafter referred to as "storage resources"\) at the input and output nodes of Realtime Compute. Second, it refers to how Realtime Compute manages the input and output storage resources \(hereinafter referred to as "the data storage feature"\). Realtime Compute supports two methods for using input and output storage resources: plaintext referencing and data storage resource registration.

**Note:** To allow Realtime Compute to access the data storage resources, you must grant Realtime Compute the permission to access these resources in advance. For more information about how to verify whether Realtime Compute already has the permission, and about how to grant the permission to Realtime Compute, see [Create a role for Realtime Compute exclusive mode and grant permissions to the role](../../../../intl.en-US/Preparation/Create a role for Realtime Compute exclusive mode and grant permissions to the role.md#).

## Plaintext referencing {#section_qx2_4tz_zfb .section}

You can explicitly reference the input and output storage resources by using AccessKey ID or AccessKey Secret in the WITH function of the DDL statement of your Realtime Compute job. For more information, see [EN-US\_TP\_40871.dita\#concept\_62515\_zh](EN-US_TP_40871.dita#concept_62515_zh). Plaintext referencing allows you to authorize Realtime Compute of both the same and different accounts \(including the Alibaba Cloud account and the RAM user\). Assume that user A \(including RAM users created under the Alibaba Cloud account of user A\) wants to use storage resources of user B in Realtime Compute. User A can reference storage resources of user B in plaintext mode by defining the reference in the DDL statement as follows:

```language-sql
CREATE TABLE in_stream(
  a varchar,
  b varchar,
  c timeStamp
)with(
type='datahub',
  endPoint='http://dh-cn-hangzhou.aliyuncs.com',
  project='blink_test',
  topic='ip_count02',
  accessId='<yourAccessSecret>', -- AccessKey ID granted by user B.
  accessKey='<yourProjectName> -- AccessKey Secret granted by user B.
);
```

## Data storage resource registration {#section_sx2_4tz_zfb .section}

To help you manage input and output storage resources, Realtime Compute offers the data storage management feature. This feature offers many conveniences, such as data preview, data sampling, and auto DDL generation, to help you manage your cloud-based storage resources. All you have to do is to register these resources on the Realtime Compute development platform in advance.

**Note:** The data storage resource registration feature of Realtime Compute currently supports only storage resources under the same Alibaba Cloud account. In other words, user A \(including RAM users created under the Alibaba Cloud account of user A\) can only register storage resources purchased by user A. This feature does not support registration of storage resources under different Alibaba Cloud accounts. To use storage resources of a different Alibaba Cloud account, use the plaintext referencing method.

-   Data storage resource registration

    In the left-side navigation pane of the Development Platform page, click **Data Storage**. Then, click **Registration and Connection** in the upper-right corner to go to the data storage resource registration page.

    Realtime Compute allows you to register three types of storage resources. For more information about the registration methods, click the following links:

    -   [Register Table Store resources](intl.en-US/Flink SQL Development Guide/Data storage/Data storage resource registration/Register Table Store resources.md#)
    -   [Register ApsaraDB for RDS resources](intl.en-US/Flink SQL Development Guide/Data storage/Data storage resource registration/Register ApsaraDB for RDS resources.md#)
    -   [Register Log Service resources](intl.en-US/Flink SQL Development Guide/Data storage/Data storage resource registration/Register Log Service resources.md#)
-   Data preview

    Realtime Compute offers a data preview feature for registered storage resources. Click **Data Storage** and select a data storage type to preview related data.

-   Data sampling

    Realtime Compute offers a data sampling feature for registered storage resources. Click **Data Storage**, select a data storage type, and click Data Sampling to enter the data sampling page. You can click **Download Data** in the upper-right corner to download the sampled data.

-   Auto DDL generation

    Realtime Compute offers an auto DDL generation feature for registered storage resources. On the job edit page, click **Data Storage**, select a data storage type, and click **Reference as Source Table**, **Reference as Result Table**, or **Reference as Dimension Table** to enable auto DDL generation.

    The automatically generated DDL statement contains only the basic WITH parameters to ensure the smooth connection between Realtime Compute and the storage resources. You can add other WITH parameters to the DDL statement as needed.

-   Network detection

    The data storage feature of Realtime Compute also provides a network detection feature. This feature is used to detect the network connectivity between Realtime Compute and the target storage resource. You can choose **Data Storage** \> **Registration and Connection**, and enable the network detection feature.


