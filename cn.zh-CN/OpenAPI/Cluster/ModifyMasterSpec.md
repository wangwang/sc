# ModifyMasterSpec {#concept_226435 .concept}

您可以通过ModifyMasterSpec OpenAPI更改集群Master机型的规格，包括Master机型的升配和降配。

**说明：** ModifyMasterSpec仅支持在独享模式的按量付费模式下使用。

## ModifyMasterSpec请求参数 {#section_ryh_718_qbc .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|masterTargetModel|String|是|Ecs\_4c16g|Master机型变配的目标机器型号|

## ModifyMasterSpec返回参数 {#section_3d3_nuz_owy .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B\*\*\*\*|请求ID|

## 请求示例 {#section_qkh_23f_k5o .section}

``` {#codeblock_hgs_o4g_awy}
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

