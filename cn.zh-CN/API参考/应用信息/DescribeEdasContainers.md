# DescribeEdasContainers

调用DescribeEdasContainers接口获取应用微服务容器组件列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeEdasContainers&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/resource/edasContainers HTTP/1.1
```

## 请求参数

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Array of Data| |组件列表。 |
|Disabled|Boolean|false|微服务组件是否禁用。取值说明如下：

 -   **true**：表示组件被禁用。
-   **false**：表示组件未被禁用。 |
|EdasContainerVersion|String|3.5.3|容器版本。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用微服务容器组件列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/resource/edasContainers HTTP/1.1
公共请求头
```

正常返回示例

`XML`格式

```
<DescribeEdasContainersResponse>
	  <Data>
		    <EdasContainerVersion>3.5.3</EdasContainerVersion>
		    <Disabled>false</Disabled>
	  </Data>
	  <Message>success</Message>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Success>true</Success>
	  <Code>200</Code>
</DescribeEdasContainersResponse>
```

`JSON`格式

```
{
  "Data": [
    {
      "EdasContainerVersion": "3.5.3",
      "Disabled": false
    }
  ],
  "Message": "success",
  "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "TraceId": "0a98a02315955564772843261e****",
  "Success": true,
  "Code": 200
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

