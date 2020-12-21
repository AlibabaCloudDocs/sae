# ListApplications

调用ListApplications接口获取应用列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListApplications&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法

```
GET /pop/v1/sam/app/listApplications HTTPS|HTTP
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|CurrentPage|Integer|Query|否|1|当前页数。 |
|PageSize|Integer|Query|否|20|页面大小。 |
|AppName|String|Query|否|demo-app|应用名称。 |
|NamespaceId|String|Query|否|cn-beijing:demo|命名空间ID。 |
|Tags|String|Query|否|\[\{"key":"key","value":"value"\}\]|标签列表，JSON字符串。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或POP错误码。 |
|Data|Struct| |应用列表。 |
|Applications|Array of Application| |应用列表。 |
|AppDeletingStatus|Boolean|false|是否正在删除应用。取值说明如下：

 -   **true**：表示应用正在被删除。
-   **false**：表示应用没有被删除。 |
|AppId|String|f7730764-d88f-4b9a-8d8e-cd8efbfe\*\*\*\*|应用ID。 |
|AppName|String|demo-app|应用名称。 |
|Instances|Integer|2|应用实例个数。 |
|NamespaceId|String|cn-beijing:demo|命名空间ID。 |
|RegionId|String|cn-beijing|地域ID。 |
|RunningInstances|Integer|2|运行中的实例个数。 |
|Tags|Array of Tags| |应用标签。 |
|Key|String|key|标签键。 |
|Value|String|value|标签值。 |
|CurrentPage|Integer|1|当前页数。 |
|PageSize|Integer|20|页面大小。 |
|TotalSize|Integer|2|应用总个数。 |
|ErrorCode|String|success|错误码。 |
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|B4D805CA-926D-41B1-8E63-7AD0C1ED\*\*\*\*|请求ID。 |
|Success|Boolean|true|获取应用列表。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/listApplications?RegionId=cn-beijing&CurrentPage=1
```

正常返回示例

`XML` 格式

```
<ListApplicationsResponse>
    <Message>success</Message>
    <RequestId>B4D805CA-926D-41B1-8E63-7AD0C1ED****</RequestId>
    <Data>
        <PageSize>20</PageSize>
        <Applications>
            <Instances>2</Instances>
            <AppId>f7730764-d88f-4b9a-8d8e-cd8efbfe****</AppId>
            <RunningInstances>2</RunningInstances>
            <NamespaceId>cn-beijing:demo</NamespaceId>
            <RegionId>cn-beijing</RegionId>
            <AppDeletingStatus>false</AppDeletingStatus>
            <AppName>demo-app</AppName>
        </Applications>
        <Applications>
            <Tags>
                <Value>value</Value>
            <   Key>key</Key>
            </Tags>
        </Applications>
        <CurrentPage>1</CurrentPage>
        <TotalSize>2</TotalSize>
    </Data>
    <Code>200</Code>
    <Success>true</Success>
</ListApplicationsResponse>
```

`JSON` 格式

```
{
    "Message": "success",
    "RequestId": "B4D805CA-926D-41B1-8E63-7AD0C1ED****",
    "Data": {
        "PageSize": 20,
        "Applications": [
            {
                "Instances": 2,
                "AppId": "f7730764-d88f-4b9a-8d8e-cd8efbfe****",
                "RunningInstances": 2,
                "NamespaceId": "cn-beijing:demo",
                "RegionId": "cn-beijing",
                "AppDeletingStatus": false,
                "AppName": "demo-app"
            },
            {
                "Tags": {
                    "Value": "value",
                    "Key": "key"
                }
            }
        ],
        "CurrentPage": 1,
        "TotalSize": 2
    },
    "Code": 200,
    "Success": true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

