# GetInstanceRunSummary {#concept_qrg_fwn_tgb .concept}

GetInstanceRunSummary OpenAPI是GetInstance接口的轻量级版本，返回作业运行时的部分信息。

## GetInstanceRunSummary请求参数 {#section_nd5_qd1_rgb .section}

|参数|类型|是否必选|示例值|描述|
|instanceId|Long|是|`-1`|实例ID。流作业只有一个运行实例，此处填`-1L`，指在线上运行的实例。批作业可以通过`ListInstance`、`Startjob`等接口获得实例ID|
|jobName|String|是|`job1`|作业名称|
|projectName|String|是|`project1`|项目名称|

## GetInstanceRunSummary返回参数 {#section_lww_xd1_rgb .section}

|参数|类型|示例值|描述|
|RequestId|String|`FD0FF8C0-779A-45EB-9674-FF3E127B10D2`|请求ID|
|RunSummary.Id|Long|`123`|InstanceID|
|RunSummary.ActualState|String|`RUNNING`|Instance的实际状态： -   WAITING：等待
-   RUNNING：运行中
-   PAUSED：暂停
-   TERMINATED：停止
-   SUCCESS：成功（批作业）
-   FAILED：失败（批作业）

 |
|RunSummary.ExpectState|String|`RUNNING`|期望状态： -   RUNNING ：运行中
-   PAUSED：暂停
-   TERMINATED： 停止
-   SUCCESS：成功（批作业）
-   FAILED：失败（流作业）

 |
|RunSummary.LastErrorTime|Long|`1548397575000`|最近错误时间|
|RunSummary.LastErrorMessage|String|`error`|最近错误信息|
|RunSummary.EngineJobHandler|String|`application_**** | ****`|Instance在YARN中的名称：`ApplicaitonID | jobID（JM分配的Job ID）`。|
|RunSummary.InputDelay|Long|`20`|业务延时（毫秒）|
|RunSummary.JobName|String|`job1`|作业名称|

## GetInstanceRunSummary请求示例 {#section_gwg_121_rgb .section}

```
http(s)://[Endpoint]/?Action=undefined
&<公共请求参数>
```

