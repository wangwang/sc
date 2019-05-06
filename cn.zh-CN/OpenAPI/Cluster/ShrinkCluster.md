# ShrinkCluster {#concept_226446 .concept}

您可以使用ShrinkCluster OpenAPI来减少集群Slave实例台数。

**说明：** 

-   ShrinkCluster仅支持在独享模式的按量付费模式下使用。
-   同时配置instanceIds参数和modelTargetCount参数时，以instanceIds为准。

## ShrinkCluster请求参数 {#section_t14_vsa_s8z .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|instanceIds|String|否|abcd|机器实例ID。指定需要去除的Slave实例。指定多个实例需用逗号（,）分割。|
|modelTargetCount|String|否|\{Ecs\_4c16g:2\}|指定缩容后，S实例的型号和台数。（缩容过程中随机去除Slave实例）。|

## ShrinkCluster返回参数 {#section_877_pmn_xlz .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B\*\*\*\*|请求ID|

## 请求示例 {#section_rs8_dup_akq .section}

``` {#codeblock_pya_6uu_k3s}
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

