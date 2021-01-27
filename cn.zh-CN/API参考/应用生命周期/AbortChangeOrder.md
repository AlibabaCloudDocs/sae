# AbortChangeOrder

调用AbortChangeOrder接口终止变更单。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=AbortChangeOrder&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/changeorder/AbortChangeOrder HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ChangeOrderId|String|Query|是|be2e1c76-682b-4897-98d3-1d8d6478\*\*\*\*|变更单ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |变更单信息。 |
|ChangeOrderId|String|be2e1c76-682b-4897-98d3-1d8d6478\*\*\*\*|变更单ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|终止变更单是否成功。取值说明如下：

 -   **true**：表示终止成功。
-   **false**：表示终止失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |

## 示例

请求示例

```
PUT /pop/v1/sam/changeorder/AbortChangeOrder?RegionId=cn-hangzhou&ChangeOrderId=be2e1c76-682b-4897-98d3-1d8d6478****
```

正常返回示例

`XML`格式

```
<AbortChangeOrder>
	  <Data>
		    <ChangeOrderId>be2e1c76-682b-4897-98d3-1d8d6478****</ChangeOrderId>
	  </Data>
	  <Message>success</Message>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <Success>true</Success>
	  <Code>200</Code>
</AbortChangeOrder>
```

`JSON`格式

```
{
    "Data": {
        "ChangeOrderId": "be2e1c76-682b-4897-98d3-1d8d6478****"
    },
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Success": true,
    "Code": 200
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源。|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

