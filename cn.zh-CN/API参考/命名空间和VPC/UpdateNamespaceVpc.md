# UpdateNamespaceVpc

调用UpdateNamespaceVpc接口更新命名空间绑定的VPC。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateNamespaceVpc&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
POST /pop/v1/sam/namespace/updateNamespaceVpc HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing:test|命名空间ID。 |
|VpcId|String|Query|是|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Success|Boolean|true|更新VPC信息是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |

## 示例

请求示例

```
POST /pop/v1/sam/namespace/updateNamespaceVpc?NamespaceId=cn-beijing:test&VpcId=vpc-2ze0i263cnn311nvj**** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<UpdateNamespaceVpcResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</UpdateNamespaceVpcResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|DeleteFail.NamespaceHasIngress|Ingress detected when deleting the namespace.|删除命名空间时，命名空间存在Ingress。|
|400|Namespace.AppExists|Please delete the application first.|请先删除应用。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

