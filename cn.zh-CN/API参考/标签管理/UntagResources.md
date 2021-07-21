# UntagResources

调用UntagResources接口解除指定资源和标签之间的绑定关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UntagResources&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
DELETE /tags HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|RegionId|String|Query|是|cn-beijing|地域ID。 |
|ResourceType|String|Query|是|application|资源类型，只支持`application`。 |
|ResourceIds|String|Query|是|\["d42921c4-5433-4abd-8075-0e536f8b\*\*\*\*"\]|资源ID列表，JSON字符串。 |
|TagKeys|String|Query|否|\["k1","k2"\]|标签键列表，JSON字符串。 |
|DeleteAll|Boolean|Query|否|false|是否删除所有标签，当且仅当未传入标签键时生效。取值说明如下：

 -   **true**：删除所有标签。
-   **false**：不删除所有标签。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Boolean|true|返回结果。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|删除标签是否成功。取值说明如下：

 -   **true**：表示删除成功。
-   **false**：表示删除失败。 |

## 示例

请求示例

```
DELETE /tags?RegionId=cn-beijing&ResourceType=application&ResourceIds=["d42921c4-5433-4abd-8075-0e536f8b****"]&TagKeys=["k1","k2"]&DeleteAll=false HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UntagResourcesResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>true</Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UntagResourcesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : true,
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|InvalidResourceType.NotFound|The specified resource type is not supported.|不支持指定的资源类型。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

