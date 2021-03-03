# StopApplication

调用StopApplication接口停止应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=StopApplication&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/app/stopApplication HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|目标应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|4a815998-b468-4bea-b7d8-59f52a4421f5|发布单ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|停止应用是否成功。取值说明如下：

 -   **true**：表示停止成功。
-   **false**：表示停止失败。 |
|TraceId|String|0bc3b6e215637275918588187d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
PUT /pop/v1/sam/app/stopApplication?RegionId=cn-beijing&AppId=0099b7be-5f5b-4512-a7fc-56049ef1****
```

正常返回示例

`XML`格式

```
<StopApplicationResponse>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0bc3b6e215637275918588187d****</TraceId>
	  <Data>
		    <ChangeOrderId>4a815998-b468-4bea-b7d8-59f52a4421f5</ChangeOrderId>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</StopApplicationResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0bc3b6e215637275918588187d****",
    "Data": {
        "ChangeOrderId": "4a815998-b468-4bea-b7d8-59f52a4421f5"
    },
    "ErrorCode": "success",
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
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

