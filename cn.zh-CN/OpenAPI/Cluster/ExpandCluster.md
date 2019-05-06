# ExpandCluster {#concept_222048 .concept}

ExpandCluster可对已有集群进行Slave机型的扩容。

**说明：** DestroyCluster仅适用于独享模式。

## ExpandCluster请求参数 {#section_ozp_xmt_q8i .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|count|Integer|是|5|扩容后的机器台数|
|model|String|否|Ecs\_4c16g|机器型号。 **说明：** 目前不支持混部，扩容机型只能和已有Slave机型一致。

 |
|clusterId|String|是|vsw-abcd|交换机名称。扩容提示vSwitch不足的时候需要填写。|

## ExpandCluster返回参数 {#section_s93_wap_aue .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|

## 请求示例 {#section_vab_zd0_dh1 .section}

``` {#codeblock_vc1_61r_ule}
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

