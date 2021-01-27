# BatchStopApplications

调用BatchStopApplications接口批量停止应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=BatchStopApplications&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/app/batchStopApplications HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-shanghai|命名空间ID。 |
|AppIds|String|Query|否|ebf491f0-c1a5-45e2-b2c4-710dbe2a\*\*\*\*，ebf491f0-c1a5-45e2-b2c4-71025e2a\*\*\*\*|需要停止的应用ID，多个ID时使用半角逗号（,）分割。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|4a815998-b468-\*\*\*\*-b7d8-59f52a4421f5|变更单ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|7BD8F4C7-D84C-4D46-9885-8212997E24D6|请求ID。 |
|Success|Boolean|true|批量停止应是否成功。取值说明如下：

 -   **true**：表示停止成功。
-   **false**：表示停止失败。 |
|TraceId|String|0bc3b6e215637275918588187d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
PUT /pop/v1//sam/app/batchStopApplications?RegionId=cn-hangzhou&NamespaceId=cn-shanghai
```

正常返回示例

`XML`格式

```
<BatchStopApplicationsResponse>
      <Message>success</Message>
      <RequestId>7BD8F4C7-D84C-4D46-9885-8212997E****</RequestId>
      <TraceId>0bc3b6e215637275918588187d****</TraceId>
      <Data>
            <ChangeOrderId>4a815998-b468-****-b7d8-59f52a4421f5</ChangeOrderId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</BatchStopApplicationsResponse>
```

`JSON`格式

```
{
	"Message": "success",
	"RequestId": "7BD8F4C7-D84C-4D46-9885-8212997E****",
	"TraceId": "0bc3b6e215637275918588187d****",
	"Data": {
		"ChangeOrderId": "4a815998-b468-****-b7d8-59f52a4421f5"
	},
	"Code": 200,
	"Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

