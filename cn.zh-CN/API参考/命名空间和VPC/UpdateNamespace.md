# UpdateNamespace

调用UpdateNamespace接口更新命名空间信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateNamespace&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
PUT /pop/v1/paas/namespace HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|Query|否|name|命名空间名称。 |
|NamespaceDescription|String|Query|否|desc|命名空间描述。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |命名空间信息。 |
|NamespaceDescription|String|desc|命名空间描述。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|name|命名空间名称。 |
|RegionId|String|cn-beijing|地域。 |
|ErrorCode|String|InvalidNamespaceId.NotFound|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

-   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|更新命名空间信息是否成功。取值说明如下：

-   **true**：表示更新成功。
-   **false**：表示更新失败。 |

## 示例

请求示例

```
PUT /pop/v1/paas/namespace?NamespaceId=cn-beijing:test&NamespaceName=name&NamespaceDescription=desc HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UpdateNamespaceResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <NamespaceDescription>desc</NamespaceDescription>
        <NamespaceId>cn-beijing:test</NamespaceId>
        <NamespaceName>name</NamespaceName>
        <RegionId>cn-beijing</RegionId>
    </Data>
    <ErrorCode>InvalidNamespaceId.NotFound</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UpdateNamespaceResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : {
    "NamespaceDescription" : "desc",
    "NamespaceId" : "cn-beijing:test",
    "NamespaceName" : "name",
    "RegionId" : "cn-beijing"
  },
  "ErrorCode" : "InvalidNamespaceId.NotFound",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidNamespaceName.Format|The specified NamespaceName is invalid. The name of the namespace cannot exceed 63 characters in length.|指定的NamespaceName不合法。命名空间名称的长度不能超过63个字符。|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|Exceed.Namespace|Too many namespaces have been created.|创建的命名空间过多。|
|400|InvalidNamespaceId.Format|The specified NamespaceId is invalid.|指定的NamespaceId不合法。正确格式为\[所属regionId\]:\[命名空间标识\]，例如cn-beijing:test，并且长度不能超过32个字符。|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

