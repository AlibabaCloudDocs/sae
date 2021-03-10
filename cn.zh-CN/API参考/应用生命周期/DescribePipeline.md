# DescribePipeline

调用DescribePipeline接口查看批次信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribePipeline&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/changeorder/DescribePipeline HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|PipelineId|String|Query|是|e2e-vds-feh-\*\*\*|批次ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|559B4247-C41C-4D9E-B866-B55D360B\*\*\*\*|请求ID。 |
|Message|String|null|调用结果的附加信息。 |
|TraceId|String|1344643016148440313321061f\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|object| |批次信息。 |
|ShowBatch|Boolean|false|是否可以开始下一批次执行。取值说明如下：

 -   **false**：不可以开始下一批次执行。
-   **true**：可以开始下一批次执行。 |
|PipelineStatus|Integer|2|批次状态，取值说明如下：

 -   **0**：准备就绪。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：中止。
-   **10**：系统异常执行失败。 |
|CurrentStageId|String|c3a55592-4c30-4d84-ac2d-e98c18ec\*\*\*\*|该批次正在执行的阶段ID。 |
|PipelineName|String|第1批变更|批次名称。 |
|StageList|Array of Stage| |批次的阶段信息列表。 |
|Status|Integer|2|阶段的状态，取值说明如下：

 -   **0**：准备就绪。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **6**：中止。 |
|StageId|String|c3a55592-4c30-4d84-ac2d-e98c18ec\*\*\*\*|阶段ID。 |
|ExecutorType|Integer|0|阶段类型，取值说明如下：

 -   **0**：串行。
-   **1**：并行。 |
|TaskList|Array of Task| |状态信息列表。 |
|Status|Integer|2|任务的状态，取值说明如下：

 -   **0**：准备就绪。
-   **1**：执行中。
-   **2**：执行成功。
-   **3**：执行失败。
-   **5**：等待重试。
-   **6**：中止。 |
|StageId|String|c3a55592-4c30-4d84-ac2d-e98c18ec\*\*\*\*|阶段ID。 |
|ErrorMessage|String|EDAS-10022 <a target='\_blank' href='https://help.aliyun.com/knowledge\_detail/106573.html\#EDAS-10022'\>应用启动时 READINESS 检查失败</a\>|任务执行的报错信息。如果任务执行成功，则不会返回该信息。 |
|ErrorCode|String|EDAS-10022|任务执行失败的错误码。如果任务执行成功，则不会返回该信息。 |
|TaskName|String|初始化环境|任务名称。 |
|ErrorIgnore|Integer|0|是否支持失败后执行后面任务，取值说明如下：

 -   **0**：不支持。
-   **1**：支持。 |
|Message|String|init Namespace success|任务执行信息。 |
|ShowManualIgnore|Boolean|false|是否支持手动跳过正在执行的任务，取值说明如下：

 -   **true**：支持。
-   **false**：不支持。 |
|TaskId|String|bef0122f-de9a-4ab0-8223-b88bf8ad\*\*\*\*|任务ID。 |
|StageName|String|部署应用|阶段的名称。 |
|NextPipelineId|String|b77b1c98-5772-4f05-95fc-c7bee5fa\*\*\*\*|下一批次ID。 |
|PipelineId|String|917660ba-5092-44ca-b8e0-80012c96\*\*\*\*|批次ID。 |
|CoStatus|String|执行成功|该批次所在的变更单的状态。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Success|Boolean|true|确认开启下一批次是否成功。取值说明如下：

 -   **true**：表示确认成功。
-   **false**：表示确认失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/changeorder/DescribePipeline?PipelineId=e2e-vds-feh-*** HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribePipelineResponse>
<RequestId>559B4247-C41C-4D9E-B866-B55D360B****</RequestId>
<Message>null</Message>
<TraceId>1344643016148440313321061f****</TraceId>
<Data>
    <ShowBatch>false</ShowBatch>
    <PipelineStatus>2</PipelineStatus>
    <CurrentStageId>c3a55592-4c30-4d84-ac2d-e98c18ec****</CurrentStageId>
    <PipelineName>第1批变更</PipelineName>
    <StageList>
        <Status>2</Status>
        <StageId>c3a55592-4c30-4d84-ac2d-e98c18ec****</StageId>
        <ExecutorType>0</ExecutorType>
        <TaskList>
            <Status>2</Status>
            <StageId>c3a55592-4c30-4d84-ac2d-e98c18ec****</StageId>
            <TaskName>初始化环境</TaskName>
            <ErrorIgnore>0</ErrorIgnore>
            <Message>init Namespace success</Message>
            <ShowManualIgnore>false</ShowManualIgnore>
            <TaskId>bef0122f-de9a-4ab0-8223-b88bf8ad****</TaskId>
        </TaskList>
        <StageName>部署应用</StageName>
    </StageList>
    <NextPipelineId>b77b1c98-5772-4f05-95fc-c7bee5fa****</NextPipelineId>
    <PipelineId>917660ba-5092-44ca-b8e0-80012c96****</PipelineId>
    <CoStatus>执行成功</CoStatus>
</Data>
<ErrorCode>success</ErrorCode>
<Code>200</Code>
<Success>true</Success>
</DescribePipelineResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "559B4247-C41C-4D9E-B866-B55D360B****",
  "Message" : "null",
  "TraceId" : "1344643016148440313321061f****",
  "Data" : {
    "ShowBatch" : false,
    "PipelineStatus" : 2,
    "CurrentStageId" : "c3a55592-4c30-4d84-ac2d-e98c18ec****",
    "PipelineName" : "第1批变更",
    "StageList" : [ {
      "Status" : 2,
      "StageId" : "c3a55592-4c30-4d84-ac2d-e98c18ec****",
      "ExecutorType" : 0,
      "TaskList" : [ {
        "Status" : 2,
        "StageId" : "c3a55592-4c30-4d84-ac2d-e98c18ec****",
        "TaskName" : "初始化环境",
        "ErrorIgnore" : 0,
        "Message" : "init Namespace success",
        "ShowManualIgnore" : false,
        "TaskId" : "bef0122f-de9a-4ab0-8223-b88bf8ad****"
      } ],
      "StageName" : "部署应用"
    } ],
    "NextPipelineId" : "b77b1c98-5772-4f05-95fc-c7bee5fa****",
    "PipelineId" : "917660ba-5092-44ca-b8e0-80012c96****",
    "CoStatus" : "执行成功"
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

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

