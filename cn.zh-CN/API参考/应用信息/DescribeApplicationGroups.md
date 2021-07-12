# DescribeApplicationGroups

调用DescribeApplicationGroups接口获取应用实例分组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationGroups&type=ROA&version=2019-05-06)

## 请求头

该接口使用公共请求头，无特殊请求头。更多信息，请参见[公共请求和返回头](~~126964~~)。

## 请求语法

```
GET /pop/v1/sam/app/describeApplicationGroups HTTP/1.1
```

## 请求参数

|名称|类型|位置|是否必选|示例值|描述|
|--|--|--|----|---|--|
|AppId|String|Query|是|d700e680-aa4d-4ec1-afc2-6566b5ff\*\*\*\*|应用ID。 |
|CurrentPage|Integer|Query|否|1|页码。 |
|PageSize|Integer|Query|否|10|页面大小。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|91F93257-7A4A-4BD3-9A7E-2F6EAE6D\*\*\*\*|请求ID。 |
|Message|String|success|调用结果的附加信息。 |
|TraceId|String|0a98a02315955564772843261e\*\*\*\*|调用链ID，用于精确查询调用信息。 |
|Data|Array of ApplicationGroup| |应用分组信息。 |
|Jdk|String|Open JDK 8|部署时设置的JDK。 |
|ImageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时设置的ImageUrl。 |
|PackageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时设置的WAR或JAR包地址。 |
|PackageType|String|Image|部署类型。 |
|PackageVersion|String|1.0.0|部署时设置的软件版本。若为**ImageUrl**部署，则自动生成。 |
|GroupName|String|\_DEFAULT\_GROUP|分组名称。 |
|GroupId|String|b2a8a925-477a-eswa-b823-d5e22500\*\*\*\*|分组ID。 |
|WebContainer|String|Apache Tomcat 7|部署时设置的WebContainer。 |
|Replicas|Integer|10|所有实例数。 |
|EdasContainerVersion|String|3.5.3|部署时所使用的EdasContainer版本。 |
|RunningInstances|Integer|1|运行中的实例数。 |
|GroupType|Integer|0|分组类型。 |
|ErrorCode|String|success|错误码。 |
|Code|String|200|接口状态或POP错误码。取值说明如下：

 -   **2xx**：成功。
-   **3xx**：重定向。
-   **4xx**：请求错误。
-   **5xx**：服务器错误。 |
|Success|Boolean|true|获取应用实例分组是否成功。取值说明如下：

 -   **true**：表示获取成功。
-   **false**：表示获取失败。 |

## 示例

请求示例

```
GET /pop/v1/sam/app/describeApplicationGroups?AppId=d700e680-aa4d-4ec1-afc2-6566b5ff****&CurrentPage=1&PageSize=10 HTTP/1.1
Host:sae.aliyuncs.com
Content-Type:application/json

公共请求参数
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeApplicationGroupsResponse>
    <RequestId>91F93257-7A4A-4BD3-9A7E-2F6EAE6D****</RequestId>
    <Message>success</Message>
    <TraceId>0a98a02315955564772843261e****</TraceId>
    <Data>
        <Jdk>Open JDK 8</Jdk>
        <ImageUrl>registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest</ImageUrl>
        <PackageUrl>registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest</PackageUrl>
        <PackageType>Image</PackageType>
        <PackageVersion>1.0.0</PackageVersion>
        <GroupName>_DEFAULT_GROUP</GroupName>
        <GroupId>b2a8a925-477a-eswa-b823-d5e22500****</GroupId>
        <WebContainer>Apache Tomcat 7</WebContainer>
        <Replicas>10</Replicas>
        <EdasContainerVersion>3.5.3</EdasContainerVersion>
        <RunningInstances>1</RunningInstances>
        <GroupType>0</GroupType>
    </Data>
    <ErrorCode>success</ErrorCode>
    <Code>200</Code>
    <Success>true</Success>
</DescribeApplicationGroupsResponse>
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
    "Jdk" : "Open JDK 8",
    "ImageUrl" : "registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest",
    "PackageUrl" : "registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest",
    "PackageType" : "Image",
    "PackageVersion" : "1.0.0",
    "GroupName" : "_DEFAULT_GROUP",
    "GroupId" : "b2a8a925-477a-eswa-b823-d5e22500****",
    "WebContainer" : "Apache Tomcat 7",
    "Replicas" : 10,
    "EdasContainerVersion" : "3.5.3",
    "RunningInstances" : 1,
    "GroupType" : 0
  } ],
  "ErrorCode" : "success",
  "Code" : "200",
  "Success" : true
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

