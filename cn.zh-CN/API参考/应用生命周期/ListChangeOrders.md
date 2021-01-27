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
|Key|String|Query|否|test|模糊查询值。 |
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
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |变更单列表信息。 |
|ChangeOrderList|Array of ChangeOrder| |变更单列表信息。 |
|AppId|String|164341c-9708-4967-b3ec-24933767\*\*\*\*|应用ID。 |
|BatchCount|Integer|1|分批数。 |
|BatchType|String|auto|分批类型。 |
|ChangeOrderId|String|7fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID。 |
|CoType|String|创建应用|变更单类型。 |
|CoTypeCode|String|CoCreateApp|变更单类型CODE。 |
|CreateTime|String|2019-07-11 15:54:49|创建时间。 |
|CreateUserId|String|sae-beta-test|阿里云账号名称。 |
|Description|String|版本：1.0 \| 镜像名称：nginx|描述信息。 |
|FinishTime|String|2019-07-11 20:12:58|结束时间。 |
|GroupId|String|c9ecd2-cf6c-46c3-9f20-525de202cf79|分组ID。 |
|Source|String|console|变更单操作入口来源。 |
|Status|Integer|2|变更单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|UserId|String|sae-beta-test|阿里云账号名称。 |
|CurrentPage|Integer|1|当前分页。 |
|PageSize|Integer|20|分页大小。 |
|TotalSize|Integer|1|变更单总数。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|65E1F-43BA-4D0C-8E61-E4D1337F\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取变更单列表是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |
|TraceId|String|0bb6f815638568884597879d\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/changeorder/ListChangeOrders?RegionId=cn-beijing&AppId=145341c-9708-4967-b3ec-24933767****
```

正常返回示例

`XML`格式

```
<ListChangeOrdersResponse>
	  <RequestId>65E1F-43BA-4D0C-8E61-E4D1337F****</RequestId>
	  <Message>success</Message>
	  <TraceId>0bb6f815638568884597879d****</TraceId>
	  <Data>
    	    <PageSize>20</PageSize>
    	    <CurrentPage>1</CurrentPage>
    	    <ChangeOrderList>
        	      <Status>2</Status>
        	      <Description>版本：1.0 | 镜像名称：nginx</Description>
        	      <CreateTime>2019-07-11 15:54:49</CreateTime>
        	      <ChangeOrderId>7fa5c0-9ebb-4bb4-b383-1f885447b109</ChangeOrderId>
        	      <CreateUserId>sae-beta-test</CreateUserId>
        	      <Source>console</Source>
        	      <BatchType>auto</BatchType>
        	      <GroupId>c9ecd2-cf6c-46c3-9f20-525de202cf79</GroupId>
        	      <FinishTime>2019-07-11 20:12:58</FinishTime>
        	      <CoTypeCode>CoCreateApp</CoTypeCode>
        	      <AppId>164341c-9708-4967-b3ec-24933767****</AppId>
        	      <UserId>sae-beta-test</UserId>
        	      <CoType>创建应用</CoType>
        	      <BatchCount>1</BatchCount>
    	    </ChangeOrderList>
    	    <TotalSize>1</TotalSize>
	  </Data>
	  <Code>200</Code>
	  <Success>true</Success>
</ListChangeOrdersResponse>
```

`JSON`格式

```
{
    "RequestId": "65E1F-43BA-4D0C-8E61-E4D1337F****",
    "Message": "success",
    "TraceId": "0bb6f815638568884597879d****",
    "Data": {
        "PageSize": 20,
        "CurrentPage": 1,
        "ChangeOrderList": {
            "Status": 2,
            "Description": "版本：1.0 | 镜像名称：nginx",
            "CreateTime": "2019-07-11 15:54:49",
            "ChangeOrderId": "7fa5c0-9ebb-4bb4-b383-1f885447b109",
            "CreateUserId": "sae-beta-test",
            "Source": "console",
            "BatchType": "auto",
            "GroupId": "c9ecd2-cf6c-46c3-9f20-525de202cf79",
            "FinishTime": "2019-07-11 20:12:58",
            "CoTypeCode": "CoCreateApp",
            "AppId": "164341c-9708-4967-b3ec-24933767****",
            "UserId": "sae-beta-test",
            "CoType": "创建应用",
            "BatchCount": 1
        },
        "TotalSize": 1
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源。|
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

