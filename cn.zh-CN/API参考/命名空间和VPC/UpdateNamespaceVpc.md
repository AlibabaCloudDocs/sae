# UpdateNamespaceVpc

调用UpdateNamespaceVpc接口更新命名空间绑定的VPC。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateNamespaceVpc&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
POST /pop/v1/sam/namespace/updateNamespaceVpc HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-beijing:test|命名空间ID。 |
|VpcId|String|Query|是|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|更新VPC信息是否成功。取值说明如下：

 -   **true**：表示更新成功。
-   **false**：表示更新失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
POST /pop/v1/sam/namespace/updateNamespaceVpc?RegionId=cn-beijing&NamespaceId=cn-beijing%3Atest&VpcId=vpc-2ze0i263cnn311nvj****
```

正常返回示例

`XML` 格式

```
<UpdateNamespaceVpcResponse>.
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Code>200</Code>
      <Success>true</Success>
</UpdateNamespaceVpcResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a98a02315955564772843261e****",
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

