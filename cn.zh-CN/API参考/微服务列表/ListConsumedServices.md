# ListConsumedServices

调用ListConsumedServices接口获取订阅的微服务列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListConsumedServices&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/service/listConsumedServices HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|b2a8a925-477a-4ed7-b825-d5e22500\*\*\*\*|应用ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Array of ListConsumedServices| |微服务列表信息。 |
|AppId|String|b2a8a925-477a-4ed7-b825-d5e22500\*\*\*\*|应用ID。 |
|Group2Ip|String|\{\}|保留字段。 |
|Groups|List|HSF|消费的服务对应的组别。 |
|Ips|List|10.0.0.1|服务订阅地址。 |
|Name|String|com.alibaba.nodejs.ItemService|发布的服务名称。 |
|Type|String|RPC|发布的服务类型。 |
|Version|String|1.0.0|发布的服务版本。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取订阅的微服务列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1//sam/service/listConsumedServices?RegionId=cn-hangzhou&AppId=b2a8a925-477a-4ed7-b825-d5e22500****
```

正常返回示例

`XML`格式

```
<ListConsumedServicesResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <Type>RPC</Type>
            <Group2Ip>{}</Group2Ip>
            <Version>1.0.0</Version>
            <Name>com.alibaba.nodejs.ItemService</Name>
      </Data>
      <Data>
            <Ips>10.0.0.1</Ips>
            <Groups>HSF</Groups>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ListConsumedServicesResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": [
        {
            "Type": "RPC",
            "Group2Ip": "{}",
            "Version": "1.0.0",
            "Name": "com.alibaba.nodejs.ItemService"
        },
        {
            "Ips": "10.0.0.1",
            "Groups": "HSF"
        }
    ],
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

