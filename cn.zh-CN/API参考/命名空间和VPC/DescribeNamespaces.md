# DescribeNamespaces

调用DescribeNamespaces接口查询命名空间列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaces&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/paas/namespaces HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|CurrentPage|Integer|Query|是|1|页码。 |
|PageSize|Integer|Query|是|10|翻页大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |命名空间信息列表。 |
|CurrentPage|Integer|1|页码。 |
|Namespaces|Array of Namespace| |命名空间列表。 |
|AccessKey|String|b34dbe3315c64f9f99b58ea447ec\*\*\*\*|AccessKey ID。 |
|NamespaceDescription|String|desc|命名空间描述。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|name|命名空间名称。 |
|RegionId|String|cn-beijing|地域。 |
|SecretKey|String|G/w6sseK7+nb3S6HBmANDBMD\*\*\*\*|AccessKey Secret。 |
|TenantId|String|838cad95-973f-48fe-830b-2a8546d7\*\*\*\*|租户ID。 |
|PageSize|Integer|10|翻页大小。 |
|TotalSize|Integer|100|总数。 |
|ErrorCode|String|InvalidParameter.NotEmpty|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询命名空间列表是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/paas/namespaces?RegionId=cn-hangzhou&CurrentPage=1&PageSize=10
```

正常返回示例

`XML` 格式

```
<DescribeNamespacesResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a981dd515966966104121683d****</TraceId>
      <Data>
            <Namespaces>
                  <NamespaceName>name</NamespaceName>
                  <SecretKey>G/w6sseK7+nb3S6HBmANDBMD****</SecretKey>
                  <TenantId>838cad95-973f-48fe-830b-2a8546d7****</TenantId>
                  <AccessKey>b34dbe3315c64f9f99b58ea447ec****</AccessKey>
                  <RegionId>cn-beijing</RegionId>
                  <NamespaceId>cn-beijing:test</NamespaceId>
                  <NamespaceDescription>desc</NamespaceDescription>
            </Namespaces>
            <PageSize>10</PageSize>
            <CurrentPage>1</CurrentPage>
            <TotalSize>100</TotalSize>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeNamespacesResponse>
```

`JSON` 格式

```
{
     "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
     "Message": "success",
    "TraceId": "0a981dd515966966104121683d****",
    "Data": {
        "Namespaces": {
            "NamespaceName": "name",
            "SecretKey": "G/w6sseK7+nb3S6HBmANDBMD****",
            "TenantId": "838cad95-973f-48fe-830b-2a8546d7****",
            "AccessKey": "b34dbe3315c64f9f99b58ea447ec****",
            "RegionId": "cn-beijing",
            "NamespaceId": "cn-beijing:test",
            "NamespaceDescription": "desc"
        },
        "PageSize": 10,
        "CurrentPage": 1,
        "TotalSize": 100
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

