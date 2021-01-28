# TagResources

调用TagResources接口为指定资源添加标签。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=TagResources&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /tags HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|RegionId|String|Body|是|cn-beijing|地域ID |
|ResourceIds|String|Body|是|\["d42921c4-5433-4abd-8075-0e536f8b\*\*\*\*"\]|资源ID，String数组的JSON序列化字符串。 |
|ResourceType|String|Body|是|application|资源类型，只支持`application`。 |
|Tags|String|Body|是|\[\{"key":"k1","value":"v1"\}\]|标签。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功
-   3XX：重定向
-   4XX：请求错误
-   5XX：服务器错误 |
|Data|Boolean|true|操作成功标识。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|为指定资源添加标签是否成功。取值说明如下：

 -   **true**：表示添加成功。
-   **false**：表示添加失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /tags HTTP/1.1
公共请求头
{
"RegionId": "cn-beijing",
"ResourceIds": "["d42921c4-5433-4abd-8075-0e536f8b****"]",
"ResourceType": "application",
"Tags": "[{"key":"k1","value":"v1"}]"
}
```

正常返回示例

`XML`格式

```
<TagResourcesResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>true</Data>
      <ErrorCode>success</ErrorCode>
      <Code>200</Code>
      <Success>true</Success>
</TagResourcesResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": true,
    "ErrorCode": "success",
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Duplicate.TagKey|The TagKey contains duplicate keys.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidParameter.TagKey|The specified TagKey is invalid.|标签键不合法。|
|400|InvalidParameter.TagValue|The specified TagValue is invalid.|标签值不合法。|
|400|Missing.TagKey|You must specify TagKey.|标签值不能为空。|
|400|NumberExceed.Tags|The maximum number of tags is exceeded.|资源标签已达上限。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

