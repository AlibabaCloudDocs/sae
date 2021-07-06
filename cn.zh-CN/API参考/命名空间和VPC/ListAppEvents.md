# ListAppEvents

调用ListAppEvents接口查看应用事件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListAppEvents&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/listAppEvents HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|CurrentPage|Integer|Query|否|1|当前页数。 |
|PageSize|Integer|Query|否|10|分页大小。 |
|AppId|String|Query|否|f7730764-d88f-4b9a-8d8e-cd8efbfe\*\*\*\*|应用ID。 |
|ObjectKind|String|Query|否|Pod|对象类型。 |
|ObjectName|String|Query|否|errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-x\*\*\*\*|对象名。 |
|EventType|String|Query|否|Warning|事件类型。取值说明如下：

 -   **Warning**：告警。
-   **Normal**：正常。 |
|Reason|String|Query|否|Started|事件原因。 |
|Namespace|String|Query|是|cn-beijing|命名空间ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|B4D805CA-926D-41B1-8E63-7AD0C1ED\*\*\*\*|请求ID。 |
|Data|Object| |事件列表。 |
|CurrentPage|Integer|1|当前页。 |
|AppEventEntity|Array of AppEventEntity| |事件。 |
|ObjectKind|String|Pod|对象种类。 |
|EventType|String|Normal|事件类型。 |
|LastTimestamp|String|2020-02-19T05:01:28Z|最后出现时间。 |
|Message|String|Created container|事件信息。 |
|ObjectName|String|errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2\*\*\*\*|对象名称。 |
|Reason|String|Created|事件原因。 |
|FirstTimestamp|String|2020-02-19T05:01:28Z|首次出现时间。 |
|TotalSize|Integer|20|总页数。 |
|PageSize|Integer|10|分页大小。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|查看应用事件是否成功。取值说明如下：

 -   **true**：表示创建成功。
-   **false**：表示创建失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/listAppEvents?CurrentPage=1&PageSize=10&AppId=f7730764-d88f-4b9a-8d8e-cd8efbfe****&ObjectKind=Pod&ObjectName=errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-x****&EventType=Warning&Reason=Started&Namespace=cn-beijing HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListAppEventsResponse>
    <Message>success</Message>
    <RequestId>B4D805CA-926D-41B1-8E63-7AD0C1ED****</RequestId>
    <Data>
        <CurrentPage>1</CurrentPage>
        <AppEventEntity>
            <ObjectKind>Pod</ObjectKind>
            <EventType>Normal</EventType>
            <LastTimestamp>2020-02-19T05:01:28Z</LastTimestamp>
            <Message>Created container</Message>
            <ObjectName>errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2****</ObjectName>
            <Reason>Created</Reason>
            <FirstTimestamp>2020-02-19T05:01:28Z</FirstTimestamp>
        </AppEventEntity>
        <TotalSize>20</TotalSize>
        <PageSize>10</PageSize>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListAppEventsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "Message" : "success",
  "RequestId" : "B4D805CA-926D-41B1-8E63-7AD0C1ED****",
  "Data" : {
    "CurrentPage" : 1,
    "AppEventEntity" : [ {
      "ObjectKind" : "Pod",
      "EventType" : "Normal",
      "LastTimestamp" : "2020-02-19T05:01:28Z",
      "Message" : "Created container",
      "ObjectName" : "errew-b86bf540-b4dc-47d8-a42f-b4997c14bd8f-5595cbddd6-2****",
      "Reason" : "Created",
      "FirstTimestamp" : "2020-02-19T05:01:28Z"
    } ],
    "TotalSize" : 20,
    "PageSize" : 10
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|get.event.error|Failed to obtain event information.|获得事件信息失败。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s不能为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

