# ConfirmPipelineBatch

调用ConfirmPipelineBatch接口确认是否开始下一批次。

********\*

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ConfirmPipelineBatch&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/changeorder/ConfirmPipelineBatch HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|Confirm|Boolean|Query|是|true|是否开始下一批次。取值说明如下：

 -   **true**：表示开始下一批次。
-   **false**：表示不开始下一批次。 |
|PipelineId|String|Query|是|e2e-vds-feh-\*\*\*|批次ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |批次信息。 |
|PipelineId|String|e2e-vds-feh-\*\*\*|批次ID。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Success|Boolean|true|确认开启下一批次是否成功。取值说明如下：

 -   **true**：表示确认取成功。
-   **false**：表示确认失败。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |

## 示例

请求示例

```
GET /pop/v1/sam/changeorder/ConfirmPipelineBatch?RegionId=cn-beijing&PipelineId=e2e-vds-feh-***&Confirm=true
```

正常返回示例

`XML` 格式

```
<ConfirmPipelineBatchResponse>
      <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
      <Message>success</Message>
      <TraceId>0a98a02315955564772843261e****</TraceId>
      <Data>
            <PipelineId>e2e-vds-feh-***</PipelineId>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ConfirmPipelineBatchResponse>
```

`JSON` 格式

```
{
    "RequestId": "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
    "Message": "success",
    "TraceId": "0a98a02315955564772843261e****",
    "Data": {
        "PipelineId": "e2e-vds-feh-***"
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

