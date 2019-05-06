# UnbindQueue {#concept_227420 .concept}

您可以通过UnbindQueue OpenAPI将Queue中已经绑定的项目进行解绑。

**说明：** 执行UnbindQueue操作前，需要将项目上的作业全部下线。

## UnbindQueue请求参数 {#section_16a_3ep_11d .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|projectName|p1|项目的名称|
|queueName|queue1|要绑定的Queue的名称|

## UnbindQueue返回参数 {#section_20f_ty0_bem .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|

## 请求示例 {#section_y2v_ofo_6cv .section}

``` {#codeblock_5qj_gkv_5zv}
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&projectName=p1
&queueName=q1
&RegionId=cn-hangzhou
&<公共请求参数>
```

