# DescribeNamespaceResources

调用DescribeNamespaceResources接口查询命名空间内的资源信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaceResources&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/namespace/describeNamespaceResources HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-shanghai:test|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|AppCount|Long|1|应用个数。 |
|BelongRegion|String|cn-shanghai|命名空间所属地域。 |
|Description|String|decs|命名空间描述信息。 |
|LastChangeOrderId|String|afedb3c4-63f8-4a3d-aaa3-2c30363f\*\*\*\*|发布单ID。 |
|LastChangeOrderRunning|Boolean|true|命名空间是否有发布单运行。取值说明如下：

 -   **true**：表示有发布单运行。
-   **false**：表示没有发布单运行。 |
|LastChangeOrderStatus|String|success|命名空间最后一次发布单状态。 |
|NamespaceId|String|cn-shangha:test|命名空间ID。 |
|NamespaceName|String|test|命名空间名称。 |
|NotificationExpired|Boolean|true|发布单通知是否过期。取值说明如下：

 -   **true**：表示发布单已过期。
-   **false**：表示发布单没有过期。 |
|SecurityGroupId|String|sg-wz969ngg2e49q5i4\*\*\*\*|安全组ID。 |
|TenantId|String|838cad95-973f-48fe-830b-2a8546d7\*\*\*\*|SAE命名空间租户ID。 |
|UserId|String|test@aliyun.com|用户ID。 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwp\*\*\*\*|VSwitch ID。 |
|VSwitchName|String|test|VSwitch名称。 |
|VpcId|String|vpc-2ze0i263cnn311nvj\*\*\*\*|VPC ID。 |
|VpcName|String|test|VPC名称。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询命名空间资源信息是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/namespace/describeNamespaceResources?RegionId=cn-shanghai&NamespaceId=cn-shanghai%3Atest
```

正常返回示例

`XML`格式

```
<DescribeNamespaceResourcesResponse>
      <Message>success</Message>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <Description>decs</Description>
            <AppCount>1</AppCount>
            <SecurityGroupId>sg-wz969ngg2e49q5i4****</SecurityGroupId>
            <VSwitchId>vsw-2ze559r1z1bpwqxwp****</VSwitchId>
            <NotificationExpired>true</NotificationExpired>
            <BelongRegion>cn-shanghai</BelongRegion>
            <NamespaceName>test</NamespaceName>
            <TenantId>838cad95-973f-48fe-830b-2a8546d7****</TenantId>
            <VpcId>vpc-2ze0i263cnn311nvj****</VpcId>
            <LastChangeOrderRunning>true</LastChangeOrderRunning>
            <UserId>test@aliyun.com</UserId>
            <LastChangeOrderId>afedb3c4-63f8-4a3d-aaa3-2c30363f****</LastChangeOrderId>
            <VSwitchName>test</VSwitchName>
            <VpcName>test</VpcName>
            <NamespaceId>cn-shangha:test</NamespaceId>
            <LastChangeOrderStatus>success</LastChangeOrderStatus>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</DescribeNamespaceResourcesResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "Description": "decs",
        "AppCount": 1,
        "SecurityGroupId": "sg-wz969ngg2e49q5i4****",
        "VSwitchId": "vsw-2ze559r1z1bpwqxwp****",
        "NotificationExpired": true,
        "BelongRegion": "cn-shanghai",
        "NamespaceName": "test",
        "TenantId": "838cad95-973f-48fe-830b-2a8546d7****",
        "VpcId": "vpc-2ze0i263cnn311nvj****",
        "LastChangeOrderRunning": true,
        "UserId": "test@aliyun.com",
        "LastChangeOrderId": "afedb3c4-63f8-4a3d-aaa3-2c30363f****",
        "VSwitchName": "test",
        "VpcName": "test",
        "NamespaceId": "cn-shangha:test",
        "LastChangeOrderStatus": "success"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

