# ListAppEvents

调用ListAppEvents接口查看应用事件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListAppEvents&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/app/listAppEvents HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|f7730764-d88f-4b9a-8d8e-cd8efbfe\*\*\*\*|应用ID。 |
|CurrentPage|Integer|Query|是|1|当前页数。 |
|Namespace|String|Query|是|cn-beijing|命名空间ID。 |
|PageSize|Integer|Query|否|10|分页大小。 |
|ObjectKind|String|Query|否|Pod|对象类型。 |
|ObjectName|String|Query|否|errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-x\*\*\*\*|对象名。 |
|EventType|String|Query|否|Warning|事件类型。取值如下：

 -   **Warning**：告警。
-   **Normal**：正常。 |
|Reason|String|Query|否|Started|事件原因。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态。取值说明如下：

 -   2XX：成功。
-   3XX：重定向。
-   4XX：请求错误。
-   5XX：服务器错误。 |
|Data|Struct| |事件列表。 |
|AppEventEntity|Array of AppEventEntity| |事件。 |
|EventType|String|Normal|事件类型。 |
|FirstTimestamp|String|2020-02-19T05:01:28Z|首次出现时间。 |
|LastTimestamp|String|2020-02-19T05:01:28Z|最后出现时间。 |
|Message|String|Created container|事件信息。 |
|ObjectKind|String|Pod|对象种类。 |
|ObjectName|String|errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2\*\*\*\*|对象名称。 |
|Reason|String|Created|事件原因。 |
|CurrentPage|Integer|1|当前页。 |
|PageSize|Integer|10|分页大小。 |
|TotalSize|Integer|20|总页数。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|B4D805CA-926D-41B1-8E63-7AD0C1ED\*\*\*\*|请求ID。 |
|Success|Boolean|true|查看应用事件是否成功。取值说明如下：

 -   **true**：表示查看成功。
-   **false**：表示查看失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/listAppEvents?RegionId=cn-hangzhou&Namespace=cn-beijing&CurrentPage=1&AppId=f7730764-d88f-4b9a-8d8e-cd8efbfe****
```

正常返回示例

`XML` 格式

```
<ListAppEventsResponse>
      <Message>success</Message>
      <RequestId>B4D805CA-926D-41B1-8E63-7AD0C1ED****</RequestId>
      <Data>
            <PageSize>10</PageSize>
            <CurrentPage>1</CurrentPage>
            <TotalSize>20</TotalSize>
            <AppEventEntity>
                  <LastTimestamp>2020-02-19T05:01:28Z</LastTimestamp>
                  <Message>Created container</Message>
                  <EventType>Normal</EventType>
                  <ObjectKind>Pod</ObjectKind>
                  <FirstTimestamp>2020-02-19T05:01:28Z</FirstTimestamp>
                  <Reason>Created</Reason>
                  <ObjectName>errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2****</ObjectName>
            </AppEventEntity>
      </Data>
      <Code>200</Code>
      <Success>true</Success>
</ListAppEventsResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "B4D805CA-926D-41B1-8E63-7AD0C1ED****",
    "Data": {
        "PageSize": 10,
        "CurrentPage": 1,
        "TotalSize": 20,
        "AppEventEntity": {
            "LastTimestamp": "2020-02-19T05:01:28Z",
            "Message": "Created container",
            "EventType": "Normal",
            "ObjectKind": "Pod",
            "FirstTimestamp": "2020-02-19T05:01:28Z",
            "Reason": "Created",
            "ObjectName": "errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2****"
        }
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|get.event.error|Failed to obtain event information.|获得事件信息失败。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

