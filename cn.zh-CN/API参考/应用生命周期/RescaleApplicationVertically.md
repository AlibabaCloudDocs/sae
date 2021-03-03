# RescaleApplicationVertically

调用RescaleApplicationVertically接口更改应用实例规格。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=RescaleApplicationVertically&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/app/rescaleApplicationVertically HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|0099b7be-5f5b-4512-a7fc-56049ef1\*\*\*\*|目标应用ID。 |
|Cpu|String|Query|是|1000|目标CPU规格，单位为毫核。 |
|Memory|String|Query|是|2048|目标内存规格，单位为MB。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|ffd8cd45-2b5f-415d-b4d0-1003e80bf354|发布单ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|AB521DBB-FA78-42E6-803F-A862EA4F\*\*\*\*|请求ID。 |
|Success|Boolean|true|更改实例规格是否成功。取值说明如下：

 -   **true**：表示更改成功。
-   **false**：表示更改失败。 |
|TraceId|String|0bc3b6f315637273629117900d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/sam/app/rescaleApplicationVertically?RegionId=cn-beijing&AppId=0099b7be-5f5b-4512-a7fc-56049ef1****&Cpu=1000&Memory=2048
```

正常返回示例

`XML`格式

```
<RescaleApplicationVerticallyResponse>
	  <Message>success</Message>
	  <RequestId>AB521DBB-FA78-42E6-803F-A862EA4F****</RequestId>
	  <TraceId>0bc3b6f315637273629117900d****</TraceId>
	  <Data>
		    <ChangeOrderId>ffd8cd45-2b5f-415d-b4d0-1003e80bf354</ChangeOrderId>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</RescaleApplicationVerticallyResponse>
```

`JSON`格式

```
{
	"Message": "success",
	"RequestId": "AB521DBB-FA78-42E6-803F-A862EA4F****",
	"TraceId": "0bc3b6f315637273629117900d****",
	"Data": {
		"ChangeOrderId": "ffd8cd45-2b5f-415d-b4d0-1003e80bf354"
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
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s。|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

