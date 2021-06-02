# ListChangeOrders

调用ListChangeOrders接口获取变更单列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListChangeOrders&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/changeorder/ListChangeOrders HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|145341c-9708-4967-b3ec-24933767\*\*\*\*|应用ID。 |
|CurrentPage|Integer|Query|否|1|当前分页。 |
|PageSize|Integer|Query|否|20|分页大小。 |
|Key|String|Query|否|test|针对发布单的**部署描述**的模糊查询值。 |
|CoType|String|Query|否|CoCreateApp|变更单类型。 |
|CoStatus|String|Query|否|2|变更单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|65E1F-43BA-4D0C-8E61-E4D1337F\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0bb6f815638568884597879d\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Object| |变更单列表信息。 |
|CurrentPage|Integer|1|当前分页。 |
|TotalSize|Integer|1|变更单总数。 |
|ChangeOrderList|Array of ChangeOrder| |变更单列表信息。 |
|Status|Integer|2|变更单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|FinishTime|String|2019-07-11 20:12:58|结束时间。 |
|CreateTime|String|2019-07-11 15:54:49|创建时间。 |
|UserId|String|sae-beta-test|阿里云账号名称。 |
|Source|String|console|变更单操作入口来源。 |
|BatchCount|Integer|1|分批数。 |
|CreateUserId|String|sae-beta-test|阿里云账号名称。 |
|CoTypeCode|String|CoCreateApp|变更单类型CODE。 |
|ChangeOrderId|String|7fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID。 |
|BatchType|String|auto|分批类型。 |
|GroupId|String|c9ecd2-cf6c-46c3-9f20-525de202cf79|分组ID。 |
|Description|String|版本：1.0 \| 镜像名称：nginx|描述信息。 |
|CoType|String|创建应用|变更单类型。 |
|AppId|String|164341c-9708-4967-b3ec-24933767\*\*\*\*|应用ID。 |
|PageSize|Integer|20|分页大小。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|获取变更单列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/changeorder/ListChangeOrders?AppId=145341c-9708-4967-b3ec-24933767****&CurrentPage=1&PageSize=20&Key=test&CoType=CoCreateApp&CoStatus=2 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListChangeOrdersResponse>
    <RequestId>65E1F-43BA-4D0C-8E61-E4D1337F****</RequestId>
    <Message>success</Message>
    <TraceId>0bb6f815638568884597879d****</TraceId>
    <Data>
        <CurrentPage>1</CurrentPage>
        <TotalSize>1</TotalSize>
        <ChangeOrderList>
            <Status>2</Status>
            <FinishTime>2019-07-11 20:12:58</FinishTime>
            <CreateTime>2019-07-11 15:54:49</CreateTime>
            <UserId>sae-beta-test</UserId>
            <Source>console</Source>
            <BatchCount>1</BatchCount>
            <CreateUserId>sae-beta-test</CreateUserId>
            <CoTypeCode>CoCreateApp</CoTypeCode>
            <ChangeOrderId>7fa5c0-9ebb-4bb4-b383-1f885447b109</ChangeOrderId>
            <BatchType>auto</BatchType>
            <GroupId>c9ecd2-cf6c-46c3-9f20-525de202cf79</GroupId>
            <Description>版本：1.0 | 镜像名称：nginx</Description>
            <CoType>创建应用</CoType>
            <AppId>164341c-9708-4967-b3ec-24933767****</AppId>
        </ChangeOrderList>
        <PageSize>20</PageSize>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListChangeOrdersResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "65E1F-43BA-4D0C-8E61-E4D1337F****",
  "Message" : "success",
  "TraceId" : "0bb6f815638568884597879d****",
  "Data" : {
    "CurrentPage" : 1,
    "TotalSize" : 1,
    "ChangeOrderList" : [ {
      "Status" : 2,
      "FinishTime" : "2019-07-11 20:12:58",
      "CreateTime" : "2019-07-11 15:54:49",
      "UserId" : "sae-beta-test",
      "Source" : "console",
      "BatchCount" : 1,
      "CreateUserId" : "sae-beta-test",
      "CoTypeCode" : "CoCreateApp",
      "ChangeOrderId" : "7fa5c0-9ebb-4bb4-b383-1f885447b109",
      "BatchType" : "auto",
      "GroupId" : "c9ecd2-cf6c-46c3-9f20-525de202cf79",
      "Description" : "版本：1.0 | 镜像名称：nginx",
      "CoType" : "创建应用",
      "AppId" : "164341c-9708-4967-b3ec-24933767****"
    } ],
    "PageSize" : 20
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源。|
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

