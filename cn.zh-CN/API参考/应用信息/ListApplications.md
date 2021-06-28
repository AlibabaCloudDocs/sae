# ListApplications

调用ListApplications接口获取应用列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListApplications&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/listApplications HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|CurrentPage|Integer|Query|否|1|当前页数。取值从0开始。 |
|PageSize|Integer|Query|否|20|页面大小。取值范围为\[0,200\]。 |
|AppName|String|Query|否|demo-app|应用名称。 |
|NamespaceId|String|Query|否|cn-beijing:demo|命名空间ID。 |
|Tags|String|Query|否|\[\{"key":"key","value":"value"\}\]|标签列表，JSON字符串。 |
|OrderBy|String|Query|否|running|对应用进行排序。取值说明如下：

 -   **running**：表示按照当前实例数进行排序。
-   **instances**：表示按照目标实例数进行排序。 |
|Reverse|Boolean|Query|否|true|对应用进行升降序排序。取值说明如下：

 -   **true**：表示应用按升序排序。
-   **false**：表示应用按降序排序。 |
|FieldType|String|Query|否|appName|设置筛选应用的维度。取值说明如下：

 -   **appName**：应用名称。
-   **appIds**：应用ID。
-   **slbIps**：SLB IP地址。
-   **instanceIps**：实例IP地址。 |
|FieldValue|String|Query|否|demo-app|输入目标应用的应用名称、应用ID、SLB IP地址或实例IP地址。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Message|String|success|调用结果的附加信息。 |
|RequestId|String|B4D805CA-926D-41B1-8E63-7AD0C1ED\*\*\*\*|请求ID。 |
|Data|Object| |应用列表。 |
|CurrentPage|Integer|1|当前页数。 |
|TotalSize|Integer|2|应用总个数。 |
|PageSize|Integer|20|页面大小。 |
|Applications|Array of Application| |应用列表。 |
|AppName|String|demo-app|应用名称。 |
|NamespaceId|String|cn-beijing:demo|命名空间ID。 |
|AppDeletingStatus|Boolean|false|是否正在删除应用。取值说明如下：

 -   **true**：表示应用正在被删除。
-   **false**：表示应用没有被删除。 |
|AppId|String|f7730764-d88f-4b9a-8d8e-cd8efbfe\*\*\*\*|应用ID。 |
|Tags|Array of Tags| |应用标签。 |
|Key|String|key|标签键。 |
|Value|String|value|标签值。 |
|RunningInstances|Integer|2|运行中的实例个数。 |
|Instances|Integer|2|应用实例个数。 |
|RegionId|String|cn-beijing|地域ID。 |
|AppDescription|String|description|应用描述信息。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。 |
|Success|Boolean|true|获取应用列表。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/listApplications?CurrentPage=1&PageSize=20&AppName=demo-app&NamespaceId=cn-beijing:demo&Tags=[{"key":"key","value":"value"}]&OrderBy=running&Reverse=true&FieldType=appName&FieldValue=demo-app HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<ListApplicationsResponse>
    <Message>success</Message>
    <RequestId>B4D805CA-926D-41B1-8E63-7AD0C1ED****</RequestId>
    <Data>
        <CurrentPage>1</CurrentPage>
        <TotalSize>2</TotalSize>
        <PageSize>20</PageSize>
        <Applications>
            <AppName>demo-app</AppName>
            <NamespaceId>cn-beijing:demo</NamespaceId>
            <AppDeletingStatus>false</AppDeletingStatus>
            <AppId>f7730764-d88f-4b9a-8d8e-cd8efbfe****</AppId>
            <Tags>
                <Key>key</Key>
                <Value>value</Value>
            </Tags>
            <RunningInstances>2</RunningInstances>
            <Instances>2</Instances>
            <RegionId>cn-beijing</RegionId>
            <AppDescription>description</AppDescription>
        </Applications>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</ListApplicationsResponse>
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
    "TotalSize" : 2,
    "PageSize" : 20,
    "Applications" : [ {
      "AppName" : "demo-app",
      "NamespaceId" : "cn-beijing:demo",
      "AppDeletingStatus" : false,
      "AppId" : "f7730764-d88f-4b9a-8d8e-cd8efbfe****",
      "Tags" : [ {
        "Key" : "key",
        "Value" : "value"
      } ],
      "RunningInstances" : 2,
      "Instances" : 2,
      "RegionId" : "cn-beijing",
      "AppDescription" : "description"
    } ]
  },
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

