# DeleteQueue {#concept_227316 .concept}

您可以使用DeleteQueue OpenAPI删除已存在的Queue。

**说明：** 

-   DeleteQueue仅适用于独享模式。
-   需要删除的Queue已经被项目绑定，则需要先解绑项目，再使用DeleteQueue OpenAPI进行删除。

## DeleteQueue请求参数 {#section_1so_s7o_xe8 .section}

|参数|类型|是否必选|示例值|描述|
|clusterId|String|是|d6wxwo5tnrmuamx2ly3m\*\*\*\*|集群ID|
|queueName|String|是|root.default|Queue的名称|

## DeleteQueue返回参数 {#section_xf7_py6_van .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|

## 请求示例 {#section_efu_u4y_1p3 .section}

```
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&queueName=root.default
&<公共请求参数>
```

