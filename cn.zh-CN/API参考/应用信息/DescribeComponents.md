# DescribeComponents

调用DescribeComponents接口获取应用创建部署时所需的组件版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeComponents&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/resource/components HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|否|d700e680-aa4d-4ec1-afc2-6566b5ff\*\*\*\*|应用ID。 |
|Type|String|Query|是|TOMCAT|支持的组件类型。取值说明如下：

 -   **Tomcat**
-   **JDK** |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID。 |
|Data|Array of Data| |支持的应用组件信息。 |
|Type|String|JDK|组件类型。 |
|ComponentKey|String|Open JDK 8|组件ID。 |
|ComponentDescription|String|Open JDK 8|组件描述。 |
|Expired|Boolean|false|组件是否过期。取值说明如下：

 -   **true**：表示组件已过期。
-   **false**：表示组件未过期。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2XX**：成功。
-   **3XX**：重定向。
-   **4XX**：请求错误。
-   **5XX**：服务器错误。 |
|Success|Boolean|true|获取组件版本是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/resource/components?AppId=d700e680-aa4d-4ec1-afc2-6566b5ff****&Type=TOMCAT HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeComponentsResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <Type>JDK</Type>
        <ComponentKey>Open JDK 8</ComponentKey>
        <ComponentDescription>Open JDK 8</ComponentDescription>
        <Expired>false</Expired>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeComponentsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "91F93257-7A4A-4BD3-9A7E-2F6EAE6D****",
  "Message" : "success",
  "TraceId" : "0a98a02315955564772843261e****",
  "Data" : [ {
    "Type" : "JDK",
    "ComponentKey" : "Open JDK 8",
    "ComponentDescription" : "Open JDK 8",
    "Expired" : false
  } ],
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidComponentType.NotFound|The specified Type does not exist.|指定的Type不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

