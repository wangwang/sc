# GetClusterEngineVersions {#concept_222283 .concept}

您可以通过使用GetClusterEngineVersions OpenAPI，获取集群上可使用的引擎的版本号。

## GetClusterEngineVersions请求参数 {#section_slz_37k_5t8 .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|

## GetClusterEngineVersions返回参数 {#section_doz_y2g_r4z .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|
|EngineVersions|blink-2.2.7-1|引擎版本|

## 请求示例 {#section_96v_rkb_0qk .section}

``` {#codeblock_e7g_ech_m5t}
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6****
&RegionId=cn-hangzhou
&<公共请求参数>
```

