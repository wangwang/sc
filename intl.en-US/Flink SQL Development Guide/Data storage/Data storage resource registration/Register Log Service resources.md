# Register Log Service resources {#concept_62476_zh .concept}

This topic describes how to connect to Log Service by registering Log Service resources in Realtime Compute, and lists FAQs during the registration process.

## Register Log Service resources {#section_rxr_1hb_yfb .section}

Log Service \(LOG for short\) is formerly known as SLS. Log Service is an end-to-end log management solution. Log Service offers many features such as data collection, subscription, dumping, and query of large amounts of logs. Log Service is the log management platform of Alibaba Cloud. After you implement the management of ECS logs by using Log Service, Realtime Compute can directly connect to LogHub of Log Service. You do not need to migrate your data.

**Note:** When you use Log Service on Alibaba Cloud, you need to grant Realtime Compute the permission to access Log Service. For more information, see [Create a role for Realtime Compute exclusive mode and grant permissions to the role](../../../../intl.en-US/Preparation/Create a role for Realtime Compute exclusive mode and grant permissions to the role.md#). Otherwise, you may receive a `No Permission` error.

-   Enter the endpoint

    Enter the endpoint of Log Service. Log Service has different endpoints in different regions. For more information, see [Service endpoint](../../../../intl.en-US/API Reference/Service endpoint.md#).

    **Note:** 

    -   The endpoint must start with `http://` and cannot end with `/`, such as `http://cn-hangzhou-intranet.log.aliyuncs.com`.
    -   If your Realtime Compute and Log Service are both deployed in the intranet of Alibaba Cloud, we recommend that you enter a service endpoint of a classic network or VPC. To avoid consuming large amounts of Internet bandwidth and causing possible performance issues, we do not recommend that you enter an Internet endpoint.
    -   For more information about how to enter the endpoint of Log Service on Apsara Stack, contact your Apsara Stack system administrator.
-   Enter the project name

    Enter the Log Service project name.

    **Note:** You can only register data storage resources under the same Alibaba Cloud account. For example, user A owns Log Service project A, and user B wants to use project A in Realtime Compute. Realtime Compute does not allow user B to register project A, but user B can explicitly reference project A in the code. For more information, see [Plaintext referencing](intl.en-US/Flink SQL Development Guide/Data storage/Data storage overview.md#section_qx2_4tz_zfb).


## FAQ { .section}

Question: Why does an error \(error message XXX\) occur when I register data storage resources?

Answer: Realtime Compute uses a storage software development kit \(SDK\) to access different data storage systems. The Data Storage tab on the Realtime Compute development platform helps you manage data from different data storage systems by using this SDK. Therefore, in most cases, the errors are caused during your registration process. Please perform the following operations to troubleshoot the problem.

-   Check whether you have created the Log Service project and own the project. Log on to the [Log Service console](https://sls.console.aliyun.com/) with your Alibaba Cloud account, and check whether you can access the project.
-   Make sure that you are the owner of the Log Service project. You can only register data storage resources under the same Alibaba Cloud account.
-   Check whether you have entered the correct Log Service endpoint and project name. The endpoint must start with `http` and cannot end with `/`. For example, `http://cn-hangzhou.log.aliyuncs.com` is correct, but `http://cn-hangzhou.log.aliyuncs.com/` is incorrect.
-   Do not register the same data storage resource. Realtime Compute provides a registration check mechanism that prevents repeated registration of the same data storage resource.

Question: Why is only time-based data sampling supported?

Answer: Log Service is designed for streaming data storage, and APIs provided by it only support time parameters. Therefore, Realtime Compute only supports time-based data sampling. If you want to use the search feature of Log Service, log on to the [Log Service console](https://sls.console.aliyun.com/#/) and make sure that you have created and own a Log Service project.

