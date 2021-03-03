# DescribeChangeOrder

调用DescribeChangeOrder接口查询变更单信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeChangeOrder&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/changeorder/DescribeChangeOrder HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|ChangeOrderId|String|Query|是|76fa5c0-9ebb-4bb4-b383-1f885447\*\*\*\*|变更单ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |变更单信息。 |
|AppName|String|app-test|应用名称。 |
|Auto|Boolean|true|是否为自动分批。取值说明如下：

 -   **true**：表示自动分批变更。
-   **false**：表示不是自动分批变更。 |
|BatchCount|Integer|1|分批数。 |
|BatchType|String|Automatic|分批类型。 |
|BatchWaitTime|Integer|0|自动分批方式时，开始下一批次前的等待时间。单位：分钟 |
|ChangeOrderId|String|765fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID。 |
|CoType|String|Restart Instances|变更类型。 |
|CoTypeCode|String|CoRestartInstances|变更类型Code。 |
|CreateTime|String|2020-12-17 21:06:45|创建时间。 |
|CurrentPipelineId|String|0e4acf82-c9b1-4c1e-ac28-55776338\*\*\*\*|当前批次ID。 |
|Description|String|description|变更单描述信息。 |
|ErrorMessage|String|success|错误信息。 |
|Pipelines|Array of Pipeline| |批次信息。 |
|BatchType|Integer|0|分批类型。 |
|ParallelCount|Integer|0|分批内并行任务数。 |
|PipelineId|String|0e4acf82-c9b1-4c1e-ac28-55776338\*\*\*\*|批次ID。 |
|PipelineName|String|Batch 1 Change|批次名称。 |
|StartTime|Long|1562831689704|开始时间。 |
|Status|Integer|2|批次状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|UpdateTime|Long|1562847178007|最近更新时间。 |
|Status|Integer|2|变更单状态。取值说明如下：

 -   **0**：准备。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：终止。
-   **10**：系统异常执行失败。 |
|SupportRollback|Boolean|false|是否支持回滚。取值说明如下：

 -   **true**：表示支持回滚。
-   **false**：表示不支持回滚。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|查询变更单信息是否成功。取值说明如下：

 -   **true**：表示查询成功。
-   **false**：表示查询失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET pop/v1/sam/changeorder/DescribeChangeOrder?RegionId=cn-shanghai&ChangeOrderId=10261d92-e38a-4605-8be7-827dcaa1****
```

正常返回示例

`XML`格式

```
<DescribeChangeOrderResponse>
	  <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
	  <Message>success</Message>
	  <TraceId>0a98a02315955564772843261e****</TraceId>
	  <Data>
    	    <Status>2</Status>
    	    <Description>description</Description>
    	    <Pipelines>
        	      <Status>2</Status>
        	      <PipelineName>Batch 1 Change</PipelineName>
        	      <StartTime>1562831689704</StartTime>
        	      <UpdateTime>1562847178007</UpdateTime>
        	      <ParallelCount>0</ParallelCount>
        	      <PipelineId>0e4acf82-c9b1-4c1e-ac28-55776338****</PipelineId>
        	      <BatchType>0</BatchType>
    	    </Pipelines>
    	    <CreateTime>2020-12-17 21:06:45</CreateTime>
    	    <ChangeOrderId>765fa5c0-9ebb-4bb4-b383-1f885447b109</ChangeOrderId>
    	    <BatchType>Automatic</BatchType>
    	    <AppName>app-test</AppName>
    	    <Auto>true</Auto>
    	    <CurrentPipelineId>0e4acf82-c9b1-4c1e-ac28-55776338****</CurrentPipelineId>
    	    <CoTypeCode>CoRestartInstances</CoTypeCode>
    	    <SupportRollback>false</SupportRollback>
    	    <BatchWaitTime>0</BatchWaitTime>
    	    <ErrorMessage>success</ErrorMessage>
    	    <CoType>Restart Instances</CoType>
    	    <BatchCount>1</BatchCount>
	  </Data>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeChangeOrderResponse>
```

`JSON`格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "Status": 2,
        "Description": "description",
        "Pipelines": {
            "Status": 2,
            "PipelineName": "Batch 1 Change",
            "StartTime": 1562831689704,
            "UpdateTime": 1562847178007,
            "ParallelCount": 0,
            "PipelineId": "0e4acf82-c9b1-4c1e-ac28-55776338****",
            "BatchType": 0
        },
        "CreateTime": "2020-12-17 21:06:45",
        "ChangeOrderId": "765fa5c0-9ebb-4bb4-b383-1f885447b109",
        "BatchType": "Automatic",
        "AppName": "app-test",
        "Auto": true,
        "CurrentPipelineId": "0e4acf82-c9b1-4c1e-ac28-55776338****",
        "CoTypeCode": "CoRestartInstances",
        "SupportRollback": false,
        "BatchWaitTime": 0,
        "ErrorMessage": "success",
        "CoType": "Restart Instances",
        "BatchCount": 1
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
|400|InvalidChangeOrder.NotFound|The current change order does not exist.|变更单不存在。|
|404|InvalidAppId.NotFound|The specified AppId does not exist.|指定的AppId不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

