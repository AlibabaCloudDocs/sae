# BindSlb

调用BindSlb接口为应用绑定SLB。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=BindSlb&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/app/slb HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|需要绑定SLB的目标应用ID。 |
|Internet|String|Query|否|\[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]|绑定公网SLB。例如: \[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]，表示将容器的8080端口通过SLB的80端口暴露服务，协议为TCP。 |
|Intranet|String|Query|否|\[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]|绑定私网SLB。例如: \[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]，表示将容器的8080端口通过SLB的80端口暴露服务，协议为TCP。 |
|InternetSlbId|String|Query|否|lb-bp1tg0k6d9nqaw7l1\*\*\*\*|使用指定的已购买的公网SLB，目前只支持非共享型实例。 |
|IntranetSlbId|String|Query|否|lb-bp1tg0k6d9nqaw7l1\*\*\*\*|使用指定的已购买的私网SLB，目前只支持非共享型实例。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88\*\*\*\*|返回的发布单ID，用于查询任务执行状态。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|绑定SLB是否成功。取值说明如下：

 -   **true**：表示绑定成功。
-   **false**：表示绑定失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，可用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/sam/app/slb HTTP/1.1
公共请求头
{
  "AppId": "0099b7be-5f5b-4512-a7fc-56049ef1****"
}
```

正常返回示例

`XML` 格式

```
<BindSlbResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88****</ChangeOrderId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</BindSlbResponse>
```

`JSON` 格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "ChangeOrderId": "01db03d3-3ee9-48b3-b3d0-dfce2d88****"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.NotDeployYet|The application has not been deployed. Please deploy it and try again.|应用没有部署，请部署后重试。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParam.ProtocolNotSupport|Only TCP protocol is supported.|不支持指定的协议，只支持TCP协议。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|Slb.NotFound|The SLB instance does not exist: slbId \[%s\]|SLB不存在：slbId\[%s\]。|
|400|SlbAppVSwitch.NotMatch|The SLB instance does not match the VSwitch of the current application.|SLB与应用VSwitch不匹配。|
|400|SlbHttpsCert.NotConsistent|The HTTPS listening certificate for each listener must match.|SLB设置HTTPS监听证书配置必须一致。|
|400|SlbHttpsCert.NotFound|You must configure the certificate before you configure HTTPS listening for the SLB instance.|SLB设置HTTPS监听必须有证书配置。|
|400|SLBInstanceQuota.OverQuota|The total number of SLB instances exceeds the quota. Please reduce the instances and try again.|SLB总实例数超过了限额，请您减少数量后重试。|
|400|SlbListenerPort.NotAvailable|The SLB listening port is unavailable: slbId \[%s\], port \[%s\]|SLB监听端口被占用：slbId\[%s\], port\[%s\]。|
|400|SlbListenerType.Invalid|An SLB listener type error occurred. Only HTTPS and TCP are supported.|SLB监听类型异常，只支持HTTPS和TCP类型。|
|400|SlbSpec.NotSupport|Shared performance SLB instances are not supported.|不支持性能共享型SLB实例。|
|400|SlbType.Invalid|An SLB network type error occurred.|SLB网络类型异常。|
|400|SSLCert.NotFound|The specified SSL certificate cannot be found.|找不到对应的SSL证书。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

