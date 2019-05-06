# GetProject {#concept_226571 .concept}

您可以通过GetProject OpenAPI查看指定项目的详细信息。

## GetProject请求参数 {#section_ibg_f57_v4z .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|projectName|String|project1|项目名称|

## GetProject返回参数 {#section_zuo_sfu_hw7 .section}

|参数|类型|示例值|描述|
|--|--|---|--|
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

## 请求示例 {#section_7nx_f4s_3jw .section}

``` {#codeblock_kf7_q37_9ab}
http(s)://[Endpoint]/?projectName=project1
&RegionId=cn-hangzhou
&<公共请求参数>
```

