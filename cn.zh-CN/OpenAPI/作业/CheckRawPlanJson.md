# CheckRawPlanJson {#concept_ejb_fpq_tgb .concept}

您可以组合调用CheckRawPlanJson和GetRawPlanJson接口，来获取某个作业的planjson。CheckRawPlanJson接口发出调用请求后会返回一个session ID，GetRawPlanJson获取这个session ID后可以查询到planjson的详细情况。

**说明：** 建议循环调用CheckRawPlanJson方法直到成功获取。

## CheckRawPlanJson请求参数 {#section_nd5_qd1_rgb .section}

|参数|类型|是否必选|示例值|描述|
|jobName|String|是|job1|单个作业名称|
|projectName|String|是|project1|项目名称|
|sessionId|String|是|123456|当使用CheckRawPlanJson发送请求后，会返回一个sessionId，将该sessionId填在此处。|

## CheckRawPlanJson返回参数 {#section_lww_xd1_rgb .section}

|参数|类型|示例值|描述|
|RequestId|String|`FD0FF8C0-779A-45EB-9674-FF3E127B10D2`|请求ID|
|PlanJsonInfo| | |PlanJson详情|
|PlanJsonInfo.Status|String|success|GetRawPlanJson的执行状态： -   session in run：执行中
-   success ：成功
-   fail：失败

 |
|PlanJsonInfo.PlanJson|String|`{a:b}`|执行计划|
|PlanJsonInfo.ErrorMessage|String|error|错误信息|

## CheckRawPlanJson请求示例 {#section_gwg_121_rgb .section}

```language-java
http(s)://[Endpoint]/?Action=CheckRawPlanJson 
&<公共请求参数>
```

