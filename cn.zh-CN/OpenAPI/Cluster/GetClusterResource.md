# GetClusterResource {#concept_222287 .concept}

您可以使用GetClusterResource OpenAPI查看集群总资源的情况和当前已使用的资源情况。

## GetClusterResource请求参数 {#section_jjm_ihb_qpb .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|clusterId|String|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|

## GetClusterResource返回参数 {#section_jl1_aar_nxz .section}

|参数|类型|示例值|描述|
|RequestId|String|`FD0FF8C0-779A-45EB-9674-FF3E127B****`|请求ID|
|Resource.TotalMB|Long|2048|集群总内存|
|Resource.AllocatedMB|1024|已使用的内存|
|Resource.AvailableMB|1024|可使用的内存|
|Resource.TotalVirtualCores|200|集群总VCore数|
|Resource.AllocatedVirtualCores|100|已经使用的VCore数|
|Resource.AllocatedVirtualCores|100|可使用的VCore数|

## GetClusterResource请求示例 {#section_laf_0u0_4za .section}

```
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

-   JSON格式正常返回示例

    ``` {#codeblock_b7b_w6l_sce}
    {}
    ```

-   JSON格式异常返回示例

    ``` {#codeblock_5ou_x1u_462}
    null
    ```


```
http(s)://[Endpoint]/?clusterId=cmy99ugusuco66x9qc6k****
&RegionId=cn-hangzhou
&<公共请求参数>
```

