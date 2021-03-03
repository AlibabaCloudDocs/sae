# DescribeNamespace

调用DescribeNamespace接口查询命名空间详细信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespace&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/paas/namespace HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing:test|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |命名空间信息。 |
|NamespaceDescription|String|desc|命名空间描述。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|name|命名空间名称。 |
|RegionId|String|cn-beijing|地域。 |
|ErrorCode|String|InvalidParameter.NotEmpty|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询命名空间信息是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/paas/namespace?RegionId=cn-hangzhou&NamespaceId=cn-beijing%3Atest
```

正常返回示例

`XML`格式

```
<DescribeNamespaceResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a981dd515966966104121683d****</TraceId>
      <Data>
            <NamespaceName>name</NamespaceName>
            <RegionId>cn-beijing</RegionId>
            <NamespaceId>cn-beijing:test</NamespaceId>
            <NamespaceDescription>desc</NamespaceDescription>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeNamespaceResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a981dd515966966104121683d****",
    "Data": {
        "NamespaceName": "name",
        "RegionId": "cn-beijing",
        "NamespaceId": "cn-beijing:test",
        "NamespaceDescription": "desc"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

