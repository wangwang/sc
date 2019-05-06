# BindQueue {#concept_226948 .concept}

项目创建成功后，需要使用BindQueue将项目绑定在已经存在并且没有被其他项目绑定的Queue上后，才能在改项目上创建和运行作业。

**说明：** BindQueue仅适用于独享模式。

## BindQueue请求参数 {#section_5kw_pwg_skm .section}

|参数|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|clusterId|String|是|cmy99ugusuco66x9qc6k\*\*\*\*|集群ID|
|projectName|p1|项目的名称|
|queueName|queue1|要绑定的Queue的名称|

## BindQueue返回参数 {#section_qgc_a7w_aky .section}

|参数|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|FD0FF8C0-779A-45EB-9674-FF3E127B1\*\*\*\*|请求ID|

## 请求示例 {#section_gap_yq9_gi0 .section}

``` {#codeblock_mw5_duz_foc}
http(s)://[Endpoint]/?projectName=p1
&<公共请求参数>
```

