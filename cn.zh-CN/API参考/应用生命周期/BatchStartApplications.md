# BatchStartApplications

调用BatchStartApplications接口批量启动应用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=BatchStartApplications&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
PUT /pop/v1/sam/app/batchStartApplications HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppIds|String|Query|是|ebf491f0-c1a5-45e2-b2c4-710dbe2a\*\*\*\*|应用ID，多个ID时使用半角逗号（,）分割。 |
|NamespaceId|String|Query|是|cn-shanghai|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88\*\*\*\*|变更流程ID。 |
|ErrorCode|String|System.Upgrading|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D5557|请求ID。 |
|Success|Boolean|true|批量启动应用是否成功。取值说明如下：

 -   **true**：表示批量启动应用成功。
-   **false**：表示批量启动应用失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
PUT /pop/v1/sam/app/batchStartApplications?RegionId=cn-shanghai&NamespaceId=cn-shanghai&AppIds=ebf491f0-c1a5-45e2-b2c4-710dbe2a****
```

正常返回示例

`XML`格式

```
<BatchStartApplicationsResponse>
  <Message>success</Message>
  <TraceId>0a98a02315955564772843261e****</TraceId>
  <Data>
        <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88****</ChangeOrderId>
  </Data>
  <Code>200</Code>
  <Success>true</Success>
</BatchStartApplicationsResponse>
```

`JSON`格式

```
{
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "ChangeOrderId": "01db03d3-3ee9-48b3-b3d0-dfce2d88****"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|System.Upgrading|The system is being upgraded. Please try again later.|系统正在升级，请稍后操作。|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}。|
|400|Mamespace.Have.No.Applications|There are no applications in this namespace.|该命名空间中没有应用。|
|400|Invalid.App.List.Not.Same.Namespace|The selected applications do not belong to the same namespace.|所选择的应用不属于同一个命名空间。|
|400|user.indebt|The user has an outstanding payment.|您处于欠费状态。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

