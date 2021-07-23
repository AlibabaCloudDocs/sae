# UnbindSlb

调用UnbindSlb接口解绑私网或公网SLB。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UnbindSlb&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
DELETE /pop/v1/sam/app/slb HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|目标应用ID。 |
|Internet|Boolean|Query|否|true|是否解绑公网SLB。取值说明如下：

 -   **true**：表示解绑公网SLB。
-   **false**：表示不解绑公网SLB。 |
|Intranet|Boolean|Query|否|true|是否解绑私网SLB。取值说明如下：

 -   **true**：表示解绑私网SLB。
-   **false**：表示不解绑私网SLB。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|ChangeOrderId|String|4a815998-b468-4bea-b7d8-59f52a44\*\*\*\*|返回的发布单ID，用于查询任务执行状态。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|解绑内网或公网SLB是否成功。取值说明如下：

 -   **true**：表示解绑成功。
-   **false**：表示解绑失败。 |

## 示例

请求示例

```
DELETE /pop/v1/sam/app/slb?AppId=0099b7be-5f5b-4512-a7fc-56049ef1****&Internet=true HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UnbindSlbResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <ChangeOrderId>4a815998-b468-4bea-b7d8-59f52a44****</ChangeOrderId>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UnbindSlbResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : {
    "ChangeOrderId" : "4a815998-b468-4bea-b7d8-59f52a44****"
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.NotDeployYet|The application has not been deployed. Please deploy it and try again.|应用没有部署，请部署后重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

