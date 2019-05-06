# ListProjectBindQueueResource {#concept_zt4_sbr_tgb .concept}

ListProjectBindQueueResource API可以查询project关联的队列的资源信息，返回对应Queue资源情况的具体信息。

## ListProjectBindQueueResource请求参数 {#section_nd5_qd1_rgb .section}

|参数|类型|是否必选|示例值|描述|
|clusterId|String|否|d6wxwo5tnrmuamx2ly3m\*\*\*\*|集群ID|
|projectName|String|是|project1|项目名称|
|queueName|String|否|`root.default`|队列名称|

## ListProjectBindQueueResource返回参数 {#section_lww_xd1_rgb .section}

|参数|类型|示例值|描述|
|RequestId|String|`FD0FF8C0-779A-45EB-9674-FF3E127B10D2`|请求ID，方便foas定位问题|
|Queues.ClusterId|String|d6wxwo5tnrmuamx2ly3m\*\*\*\*|集群名称|
|Queues.QueueName|String|`root.default`|队列名称|
|Queues.MinGpu|Integer|2|最小GPU数|
|Queues.MaxGpu|Integer|10|GPU最大值|
|Queues.MinMem|Integer|1024|最小内存数（MB）|
|Queues.MaxMem|Integer|2048|内存最大值（MB）|
|Queues.MinVCore|Integer|50|最小Vcore数|
|Queues.MaxVCore|Integer|100|最大Vcore数|
|Queues.UsedVCore|Integer|50|已使用Vcore|
|Queues.UsedGpu|Integer|5|已使用GPU|
|Queues.UsedMem|Integer|512|已使用内存（MB）|

## ListProjectBindQueueResource请求示例 {#section_gwg_121_rgb .section}

```
http(s)://[Endpoint]/?Action=undefined
&<公共请求参数>
```

