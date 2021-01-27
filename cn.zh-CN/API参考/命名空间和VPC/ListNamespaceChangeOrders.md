# ListNamespaceChangeOrders

调用ListNamespaceChangeOrders接口获取命名空间发布单列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListNamespaceChangeOrders&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/changeorder/listNamespaceChangeOrders HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|NamespaceId|String|Query|是|cn-shanghai:test|命名空间ID。 |
|CoStatus|String|Query|否|2|发布单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|CoType|String|Query|否|CoBatchStartApplication|发布单类型。 |
|Key|String|Query|否|test|模糊查询值。 |
|CurrentPage|Integer|Query|否|20|分页大小。 |
|PageSize|Integer|Query|否|1|当前页。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |返回结果。 |
|ChangeOrderList|Array of ChangeOrder| |发布单列表。 |
|BatchCount|Integer|1|分批数。 |
|BatchType|String|自动|分批类型。 |
|ChangeOrderId|String|7fa5c0-9ebb-4bb4-b383-1f885447\*\*\*\*|发布单ID。 |
|CoType|String|批量启动应用|发布单类型。 |
|CoTypeCode|String|CoBatchStartApplication|发布单类型Code。 |
|CreateTime|String|2019-07-11 15:54:49|创建时间。 |
|CreateUserId|String|test@aliyun.com|创建用户ID。 |
|Description|String|批量启动应用|描述信息。 |
|FinishTime|String|2019-07-11 20:12:58|结束时间。 |
|GroupId|String|c9ecd2-cf6c-46c3-9f20-525de202\*\*\*\*|分组ID。 |
|NamespaceId|String|cn-shanghai:test|命名空间ID。 |
|Pipelines|String|xxxx|变更流水线。 |
|Source|String|console|变更单操作入口来源。 |
|Status|Integer|2|发布单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|UserId|String|xxx|用户ID。 |
|CurrentPage|Integer|1|当前分页。 |
|PageSize|Integer|20|分页大小。 |
|TotalSize|Integer|32|变更单总数。 |
|ErrorCode|String|200|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|5945C4F0-4505-476B-B668-CEDC4A0F\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取发布单列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0bc3915638507554994370d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/changeorder/listNamespaceChangeOrders?RegionId=cn-shanghai&NamespaceId=cn-shanghai%3Atest
```

正常返回示例

`XML` 格式

```
<ListNamespaceChangeOrdersResponse>
      <Message>success</Message>
      <RequestId>5945C4F0-4505-476B-B668-CEDC4A0F****</RequestId>
      <TraceId>0bc3915638507554994370d****</TraceId>
      <Data>
            <PageSize>20</PageSize>
            <CurrentPage>1</CurrentPage>
            <ChangeOrderList>
                  <Status>2</Status>
                  <Description>批量启动应用</Description>
                  <Pipelines>xxxx</Pipelines>
                  <CreateTime>2019-07-11 15:54:49</CreateTime>
                  <ChangeOrderId>7fa5c0-9ebb-4bb4-b383-1f885447****</ChangeOrderId>
                  <CreateUserId>test@aliyun.com</CreateUserId>
                  <Source>console</Source>
                  <BatchType>自动</BatchType>
                  <GroupId>c9ecd2-cf6c-46c3-9f20-525de202****</GroupId>
                  <FinishTime>2019-07-11 20:12:58</FinishTime>
                  <CoTypeCode>CoBatchStartApplication</CoTypeCode>
                  <UserId>xxx</UserId>
                  <NamespaceId>cn-shanghai:test</NamespaceId>
                  <CoType>批量启动应用</CoType>
                  <BatchCount>1</BatchCount>
            </ChangeOrderList>
            <TotalSize>32</TotalSize>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ListNamespaceChangeOrdersResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "5945C4F0-4505-476B-B668-CEDC4A0F****",
    "TraceId": "0bc3915638507554994370d****",
    "Data": {
        "PageSize": 20,
        "CurrentPage": 1,
        "ChangeOrderList": {
            "Status": 2,
            "Description": "批量启动应用",
            "Pipelines": "xxxx",
            "CreateTime": "2019-07-11 15:54:49",
            "ChangeOrderId": "7fa5c0-9ebb-4bb4-b383-1f885447****",
            "CreateUserId": "test@aliyun.com",
            "Source": "console",
            "BatchType": "自动",
            "GroupId": "c9ecd2-cf6c-46c3-9f20-525de202****",
            "FinishTime": "2019-07-11 20:12:58",
            "CoTypeCode": "CoBatchStartApplication",
            "UserId": "xxx",
            "NamespaceId": "cn-shanghai:test",
            "CoType": "批量启动应用",
            "BatchCount": 1
        },
        "TotalSize": 32
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

