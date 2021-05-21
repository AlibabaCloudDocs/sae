# DescribeNamespaceResources

调用DescribeNamespaceResources接口查询命名空间内的资源信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaceResources&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/namespace/describeNamespaceResources HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|否|cn-shanghai:test|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |返回结果。 |
|VpcId|String|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |
|LastChangeOrderId|String|afedb3c4-63f8-4a3d-aaa3-2c30363f\*\*\*\*|发布单ID。 |
|BelongRegion|String|cn-shanghai|命名空间所属地域。 |
|NamespaceId|String|cn-shangha:test|命名空间ID。 |
|SecurityGroupId|String|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|UserId|String|test@aliyun.com|用户ID。 |
|NamespaceName|String|test|命名空间名称。 |
|LastChangeOrderStatus|String|success|命名空间最后一次发布单状态。 |
|VpcName|String|test|VPC名称。 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwp\*\*\*\*|VSwitch ID。 |
|Description|String|decs|命名空间描述信息。 |
|LastChangeOrderRunning|Boolean|true|命名空间是否有发布单运行。取值说明如下：

 -   **true**：表示有发布单运行。
-   **false**：表示没有发布单运行。 |
|AppCount|Long|1|应用个数。 |
|VSwitchName|String|test|VSwitch名称。 |
|NotificationExpired|Boolean|true|发布单通知是否过期。取值说明如下：

 -   **true**：表示发布单已过期。
-   **false**：表示发布单没有过期。 |
|TenantId|String|838cad95-973f-48fe-830b-2a8546d7\*\*\*\*|SAE命名空间租户ID。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Success|Boolean|true|查询命名空间资源信息是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/namespace/describeNamespaceResources?NamespaceId=cn-shanghai:test HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeNamespaceResourcesResponse>
    <Data/>
    <Code>200</Code>
    <Success>true</Success>
</DescribeNamespaceResourcesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Data" : { },
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

