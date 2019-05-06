# ListProject {#concept_226595 .concept}

您可以使用ListCluster OpenAPI，查询若干个项目的信息。查询的项目信息可根据参数选择，进行自由组合。

## ListProject请求参数 {#section_q41_4j0_o05 .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|deployType|String|是|cell|集群类型： -   独享集群：cell
-   共享集群： public

 |
|clusterId|String|否|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|name|String|p1|项目名称|
|pageIndex|Integer|2|分页选项。指定查询的页码。|
|pageSize|Integer|1|分页选项。每页显示的项目数。|
|region|String|cn-hangzhou|项目所属地区|

## ListProject返回参数 {#section_2p4_ni4_15g .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|
|PageIndex|Integer|1|分页选项。指定查询的页码。|
|PageSize|Integer|10|分页选项。每页显示的项目数。|
|TotalCount|Long|50|分页选项。总项目数。|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|
|Project.Name|String|project1|项目名称|
|Project.State|String|ENABLE|项目状态|
|Project.Creator|String|creator1|项目创建者的UID|
|Project.CreateTime|Long|1527494257000|项目创建时间|
|Project.Modifier|String|modifer1|项目修改者UID|
|Project.ModifyTime|Long|1527494257000|项目修改时间|
|Project.Description|String|project1|项目描述|
|Project.DeployType|String|cell|集群类型： -   独享集群：cell
-   共享集群： public

 |
|Project.ClusterId|String|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|Project.ManagerIds|String|m1|管理员ID列表。对个ID使用逗号（,）分隔|

## 请求示例 {#section_4a1_y7x_5jj .section}

``` {#codeblock_rkl_xb8_1n3}
http(s)://[Endpoint]/?deployType=cell
&name=p1
&RegionId=cn-hangzhou
&<公共请求参数>
```

