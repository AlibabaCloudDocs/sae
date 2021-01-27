# CreateNamespace

调用CreateNamespace接口创建命名空间。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateNamespace&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/paas/namespace HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing:test|命名空间ID。仅允许小写英文字母和数字。 |
|NamespaceName|String|Query|是|name|命名空间名称。 |
|NamespaceDescription|String|Query|否|desc|命名空间描述信息。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |命名空间信息。 |
|NamespaceDescription|String|desc|命名空间描述信息。 |
|NamespaceId|String|cn-beijing:test|命名空间ID。 |
|NamespaceName|String|name|命名空间名称。 |
|RegionId|String|cn-beijing|命名空间所在地域。 |
|ErrorCode|String|InstanceExist.NamespaceId|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|创建命名空间是否成功。取值说明如下：

 -   **true**：表示创建成功。
-   **false**：表示创建失败。 |
|TraceId|String|0a981dd515966966104121683d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/paas/namespace?RegionId=cn-beijing&NamespaceId=cn-beijing%3Atest&NamespaceName=test
```

正常返回示例

`XML` 格式

```
<CreateNamespaceResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a981dd515966966104121683d****</TraceId>
      <Data>
            <NamespaceName>name</NamespaceName>
            <NamespaceId>cn-beijing:test</NamespaceId>
            <RegionId>cn-beijing</RegionId>
            <NamespaceDescription>desc</NamespaceDescription>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</CreateNamespaceResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a981dd515966966104121683d****",
    "Data": {
        "NamespaceName": "name",
        "NamespaceId": "cn-beijing:test",
        "RegionId": "cn-beijing",
        "NamespaceDescription": "desc"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InstanceExist.NamespaceId|The specified namespace ID already exists.|指定的命名空间ID已存在。|
|400|InvalidNamespace.WithUppercase|This namespace does not support creating SAE apps because it contains uppercase letters.|命名空间不支持创建SAE应用，因为它带有大写字母。|
|400|InvalidNamespaceId.Format|The specified NamespaceId is invalid.|指定的NamespaceId不合法。正确格式为\[所属regionId\]:\[命名空间标识\]，例如cn-beijing:test，并且长度不能超过32个字符。|
|400|InvalidNamespaceIdSuffix.Format|The specified NamespaceId is invalid. NamespaceId can only contain alphabetical letters or numbers.|指定的NamespaceId不合法。命名空间ID只能由字母或数字组成。|
|400|InvalidNamespaceName.Format|The specified NamespaceName is invalid. The name of the namespace cannot exceed 63 characters in length.|指定的NamespaceName不合法。命名空间名称的长度不能超过63个字符。|
|400|InvalidOperation.NamespaceClusterNotDeleted|The specified NamespaceId contains clusters.|指定的NamespaceId下还有集群。|
|400|Namespace.AppExists|Please delete the application first.|请先删除应用。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

