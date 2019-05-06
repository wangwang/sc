# CreateCluster {#concept_189628 .concept}

您完成购买后，可以通过订单的实例ID，使用CreateCluster OpenAPI创建集群。

**说明：** CreateCluster仅适用于独享模式。

## CreateCluster请求参数 {#section_1f3_e7i_y4m .section}

|参数|类型|是否必选|示例值|描述|
|description|String|否|cluster1|集群描述|
|displayName|是|cluster\_name|您创建的集群的名称|
|orderId|blinkonecs\_1234|您下单生成的实例ID|
|userOssBucket|12345|用户OSS的Bucket名称|
|userVSwitch|vsw-abcd|您指定的交换机名称|
|userVpcId|vpc-abcd|集群所在VPC名称 **说明：** 实时计算需要和上下游数据存储处在同一个VPC内，否则会则会造成无法联通的问题。

 |
|zoneId|cn-shanghai-f|可用区区号|

## CreateCluster返回参数 {#section_fdf_zyj_aja .section}

|参数|类型|示例值|描述|
|ClusterId|String|cmy99ugusuco66x9qc6k\*\*\*\*|FOAS为创建完成的集群分配的ID|

## CreateCluster请求示例 {#section_spo_ltf_hk1 .section}

```
http(s)://[Endpoint]/?RegionId=cn-hangzhou
&<公共请求参数>
```

