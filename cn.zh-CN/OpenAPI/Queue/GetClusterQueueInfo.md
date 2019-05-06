# GetClusterQueueInfo {#concept_227340 .concept}

您可以通过GetClusterQueueInfo OpenAPI查询集群上已存在的Queue的信息。

## GetClusterQueueInfo请求参数 {#section_4hd_iot_qr7 .section}

**说明：** 公有云环境中，Queue的CPU、内存、GPU的最大值和最小值相同。

|参数|类型|是否必选|示例值|描述|
|clusterId|String|否|d6wxwo5tnrmuamx2ly3m\*\*\*\*|集群ID|

## GetClusterQueueInfo返回参数 {#section_tgv_uw0_3wv .section}

|参数|类型|示例值|描述|
|RequestId|String|`FD0FF8C0-779A-45EB-9674-FF3E127B****`|请求ID|
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

## GetClusterQueueInfo请求示例 {#section_2ny_z08_t73 .section}

```
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

