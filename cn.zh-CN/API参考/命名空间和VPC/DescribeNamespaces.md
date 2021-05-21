# DescribeNamespaces

调用DescribeNamespaces接口查询命名空间列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaces&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/paas/namespaces HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|CurrentPage|Integer|Query|是|1|页码。 |
|PageSize|Integer|Query|是|10|翻页大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |命名空间信息列表。 |
|CurrentPage|Integer|1|页码。 |
|TotalSize|Integer|100|总数。 |
|PageSize|Integer|10|翻页大小。 |
|Namespaces|Array of Namespace| |命名空间列表。 |
|NamespaceDescription|String|desc|命名空间描述。 |
|AccessKey|String|b34dbe3315c64f9f99b58ea447ec\*\*\*\*|AccessKey ID。 |
|SecretKey|String|G/w6sseK7+nb3S6HBmANDBMD\*\*\*\*|AccessKey Secret。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|name|命名空间名称。 |
|TenantId|String|838cad95-973f-48fe-830b-2a8546d7\*\*\*\*|租户ID。 |
|RegionId|String|cn-beijing|地域。 |
|ErrorCode|String|InvalidParameter.NotEmpty|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Success|Boolean|true|查询命名空间列表是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |

## 示例

请求示例

```
GET /pop/v1/paas/namespaces?CurrentPage=1&PageSize=10 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeNamespacesResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a981dd515966966104121683d****</TraceId>
    <Data>
        <CurrentPage>1</CurrentPage>
        <TotalSize>100</TotalSize>
        <PageSize>10</PageSize>
        <Namespaces>
            <NamespaceDescription>desc</NamespaceDescription>
            <AccessKey>b34dbe3315c64f9f99b58ea447ec****</AccessKey>
            <SecretKey>G/w6sseK7+nb3S6HBmANDBMD****</SecretKey>
            <NamespaceId>cn-beijing:test</NamespaceId>
            <NamespaceName>name</NamespaceName>
            <TenantId>838cad95-973f-48fe-830b-2a8546d7****</TenantId>
            <RegionId>cn-beijing</RegionId>
        </Namespaces>
    </Data>
    <ErrorCode>InvalidParameter.NotEmpty</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeNamespacesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a981dd515966966104121683d****",
  "Data" : {
    "CurrentPage" : 1,
    "TotalSize" : 100,
    "PageSize" : 10,
    "Namespaces" : [ {
      "NamespaceDescription" : "desc",
      "AccessKey" : "b34dbe3315c64f9f99b58ea447ec****",
      "SecretKey" : "G/w6sseK7+nb3S6HBmANDBMD****",
      "NamespaceId" : "cn-beijing:test",
      "NamespaceName" : "name",
      "TenantId" : "838cad95-973f-48fe-830b-2a8546d7****",
      "RegionId" : "cn-beijing"
    } ]
  },
  "ErrorCode" : "InvalidParameter.NotEmpty",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

