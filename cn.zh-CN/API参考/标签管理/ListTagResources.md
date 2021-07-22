# ListTagResources

调用ListTagResources接口查询应用和标签的对应关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListTagResources&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /tags HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|RegionId|String|Query|是|cn-beijing|地域ID。 |
|ResourceType|String|Query|是|application|资源类型，仅支持`application`。 |
|NextToken|String|Query|否|A2RN|一次查询最多返回50条结果，当结果超过50条时，会同时返回一个Token，下一次查询使用该Token即可查询前50条结果之外的结果。 |
|ResourceIds|String|Query|否|\["d42921c4-5433-4abd-8075-0e536f8b\*\*\*\*"\]|应用ID列表，JSON字符串。 |
|Tags|String|Query|否|\[\{"key":"k1","value":"v1"\}\]|标签列表，JSON字符串。取值说明如下：

 -   **key**：表示标签键。
-   **value**：表示标签值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|7414187F-4F59-4585-9BCF-5F0804E4\*\*\*\*|请求ID。 |
|Message|String|success|附加信息。 |
|TraceId|String|0bc5f84e15916043198032146d\*\*\*\*|调用链ID，可用于精确查询调用信息。 |
|Data|Object| |返回数据。 |
|NextToken|String|""|一次查询最多返回50条结果，当结果超过50条时，会同时返回一个Token，下一次查询使用该Token即可查询前50条结果之外的结果。 |
|TagResources|Array of TagResource| |应用和标签的对应关系。 |
|ResourceType|String|ALIYUN::SAE::APPLICATION|资源类型，仅支持`application`。 |
|TagValue|String|v1|标签值。 |
|ResourceId|String|d42921c4-5433-4abd-8075-0e536f8b\*\*\*\*|应用ID。 |
|TagKey|String|k1|标签键。 |
|ErrorCode|String|MissingResourceType|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|查询应用和标签的对应关系是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |

## 示例

请求示例

```
GET /tags?RegionId=cn-beijing&ResourceType=application&NextToken=A2RN&ResourceIds=["d42921c4-5433-4abd-8075-0e536f8b****"]&Tags=[{"key":"k1","value":"v1"}] HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListTagResourcesResponse>
    <RequestId>7414187F-4F59-4585-9BCF-5F0804E4****</RequestId>
    <Message>success</Message>
    <TraceId>0bc5f84e15916043198032146d****</TraceId>
    <Data>
        <NextToken>""</NextToken>
        <TagResources>
            <ResourceType>ALIYUN::SAE::APPLICATION</ResourceType>
            <TagValue>v1</TagValue>
            <ResourceId>d42921c4-5433-4abd-8075-0e536f8b****</ResourceId>
            <TagKey>k1</TagKey>
        </TagResources>
    </Data>
    <ErrorCode>MissingResourceType</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListTagResourcesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "7414187F-4F59-4585-9BCF-5F0804E4****",
  "Message" : "success",
  "TraceId" : "0bc5f84e15916043198032146d****",
  "Data" : {
    "NextToken" : "\"\"",
    "TagResources" : [ {
      "ResourceType" : "ALIYUN::SAE::APPLICATION",
      "TagValue" : "v1",
      "ResourceId" : "d42921c4-5433-4abd-8075-0e536f8b****",
      "TagKey" : "k1"
    } ]
  },
  "ErrorCode" : "MissingResourceType",
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

