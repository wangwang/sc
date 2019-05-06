# ListCluster {#concept_222297 .concept}

您可以使用ListCluster OpenAPI，查询若干个集群的信息。查询的集群信息可根据参数选择，进行自由组合。

## ListCluster请求参数 {#section_21b_yfu_jop .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|否|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|displayName|String|clustera|集群名称|
|pageIndex|Integer|2|分页选项。指定查询的页码。|
|pageSize|Integer|1|分页选项。每页显示的集群数。|
|region|String|cn-hangzhou|集群所属地区|
|state|String|RUNNING|集群状态 -   集群创建中 ：STARTING
-   集群扩容中（增加Slave机型台数）： EXPANDING
-   集群变配中（提高或者降低Master型号） ：UPGRADING
-   集群注销中 ：DESTROYING
-   集群已销毁 ：DESTROYED
-   集群缩容中（减少Slave机型台数）：REDUCING
-   集群维护中：MAINTAINING

 |

## ListCluster返回参数 {#section_32y_vhw_xco .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|
|TotalCount|Long|50|总集群数|
|TotalPage|Integer|5|总页数|
|PageIndex|Integer|1|分页选项。指定查询的页码。|
|PageSize|Integer|10|分页选项。每页显示的集群数。|
|Clusters.ClusterId|String|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|Clusters.RegionId|String|cn-hangzhou|集群所属地区|
|Clusters.ZoneId|String|cn-hangzhou-a|可用地域ID|
|Clusters.State|String|RUNNING|集群状态 -   集群创建中 ：STARTING
-   集群扩容中（增加Slave机型台数）： EXPANDING
-   集群变配中（提高或者降低Master型号） ：UPGRADING
-   集群注销中 ：DESTROYING
-   集群已销毁 ：DESTROYED
-   集群缩容中（减少Slave机型台数）：REDUCING
-   集群维护中：MAINTAINING

 |
|Clusters.OwnerId|String|abcd|集群拥有者UID|
|Clusters.Operator|String|abcd|集群最后操作人UID|
|Clusters.DisplayName|String|abcd|集群名称|
|Clusters.Description|String|abcd|集群备注|
|Clusters.GmtCreate|Long|1527494257000|集群VPC创建时间|
|Clusters.GmtModified|Long|1527494257000|集群VPC修改时间|

## 请求示例 {#section_98f_ifk_5hj .section}

``` {#codeblock_dci_178_thq}
http(s)://[Endpoint]/?<公共请求http(s)://[Endpoint]/?RegionId=cn-hangzhou
&<公共请求参数>>
```

