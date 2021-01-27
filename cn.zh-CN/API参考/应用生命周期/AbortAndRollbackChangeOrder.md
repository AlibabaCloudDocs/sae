# AbortAndRollbackChangeOrder

调用AbortAndRollbackChangeOrder接口终止或回滚变更单。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=AbortAndRollbackChangeOrder&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/changeorder/AbortAndRollbackChangeOrder HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ChangeOrderId|String|Query|是|ba386059-69b1-4e65-b1e5-0682d9fa\*\*\*\*|变更单ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误 |
|Data|Struct| |变更单信息。 |
|ChangeOrderId|String|ba386059-69b1-4e65-b1e5-0682d9fa\*\*\*\*|变更单ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|终止变更单是否成功。取值说明如下：

 -   **true**：表示终止成功。
-   **false**：表示终止失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
PUT /pop/v1/sam/changeorder/AbortAndRollbackChangeOrder?RegionId=cn-hangzhou&ChangeOrderId=ba386059-69b1-4e65-b1e5-0682d9fa****
```

正常返回示例

`XML`格式

```
<AbortAndRollbackChangeOrder>
	  <Data>
		    <ChangeOrderId>ba386059-69b1-4e65-b1e5-0682d9fa****</ChangeOrderId>
	  </Data>
	  <Message>success</Message>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</AbortAndRollbackChangeOrder>
```

`JSON`格式

```
{
    "Data": {
        "ChangeOrderId": "xxx-xxxx-xxx-xxxx"
    },
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Success": true,
    "ErrorCode": "success",
    "Code": 200
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源。|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|InvalidChangeOrder.NotFound|The current change order does not exist.|变更单不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

```
xml
    <dependency>
    <groupId>com.aliyun.openservices</groupId>
    <artifactId>ons-client</artifactId>
    <version>1.2.1</version>
    </dependency>
   
```

