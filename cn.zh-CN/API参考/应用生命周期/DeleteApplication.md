# DeleteApplication

调用DeleteApplication接口删除应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DeleteApplication&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
DELETE /pop/v1/sam/app/deleteApplication HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|017f39b8-dfa4-4e16-a84b-1dcee4b1\*\*\*\*|要删除的应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88ab31|返回的发布单ID，用于查询任务执行状态。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|删除应用是否成功。取值说明如下：

 -   **true**：表示删除成功。
-   **false**：表示删除失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
DELETE /pop/v1/sam/app/deleteApplication?RegionId=cn-beijing&AppId=017f39b8-dfa4-4e16-a84b-1dcee4b1****
```

正常返回示例

`XML`格式

```
<DeleteApplicationResponse>
	  <Data>
		    <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88ab31</ChangeOrderId>
      </Data>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Success>true</Success>
	  <Code>200</Code>
</DeleteApplicationResponse>
```

`JSON`格式

```
{
    "Data": {
        "ChangeOrderId": "01db03d3-3ee9-48b3-b3d0-dfce2d88ab31"
    },
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a98a02315955564772843261e****",
    "Success": true,
    "Code": 200
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

